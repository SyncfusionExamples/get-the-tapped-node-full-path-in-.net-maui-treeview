# get-the-tapped-node-full-path-in-.net-maui-treeview

This repository demonstrates how to retrieve the full hierarchical path of a tapped node in the .NET MAUI TreeView (SfTreeView) control. It provides a sample implementation using the TapCommand property to capture user interaction and display the complete path from the root to the selected node.

## Sample

To retrieve the full path of a TreeViewNode in a .NET MAUI TreeView when a node is tapped, you can utilize the TapCommand property. This allows you to execute a command that can access and process the node’s information upon user interaction.

### XAML
```xaml
<syncfusion:SfTreeView x:Name="treeView"
                       TapCommand="{Binding TappedCommand}"
                       ChildPropertyName="SubFiles"
                       ItemsSource="{Binding ImageNodeInfo}">
   
</syncfusion:SfTreeView>
```

### ViewModel
```csharp
private Command<object>? tappedCommand;

public Command<object>? TappedCommand
{
    get { return tappedCommand; }
    set { tappedCommand = value; }
}

public FileManagerViewModel()
{
    TappedCommand = new Command<object>(ExecuteTapCommand);
}

// If a user taps on a node in the TreeView, this method gets triggered,
// retrieves the full path of the node, and displays it in an alert.
private void ExecuteTapCommand(object obj)
{
    var tappedNode = obj as Syncfusion.TreeView.Engine.TreeViewNode;
    string nodepath = GetNodePath(tappedNode);
    
    // Show the full path of the tapped node in display alert.
    App.Current!.MainPage!.DisplayAlert("Path ", nodepath, "Ok");
}

// Method to retrieve the full hierarchical path of the tapped node.
private string GetNodePath(TreeViewNode? node)
{
    string fullpath = "";
    string path = "";

    while (node != null)
    {
        // extracts the node's name.
        path = @"\" + (node.Content as FileManager)!.ItemName;

        // If the node has a parent, node is set to its parent(node.ParentNode).
        // If there is no parent, node is set to null, terminating the loop.
        if (node.ParentNode != null)
        {
            node = node.ParentNode;
        }
        else
        {
            node = null;
        }
        fullpath = path + fullpath;
    }
    return fullpath;
}
```

## Requirements to run the demo

To run the demo, refer to [System Requirements for .NET MAUI](https://help.syncfusion.com/maui/system-requirements).

## Troubleshooting:
### Path too long exception

If you are facing path too long exception when building this example project, close Visual Studio and rename the repository to short and build the project.

## License

Syncfusion® has no liability for any damage or consequence that may arise from using or viewing the samples. The samples are for demonstrative purposes. If you choose to use or access the samples, you agree to not hold Syncfusion® liable, in any form, for any damage related to use, for accessing, or viewing the samples. By accessing, viewing, or seeing the samples, you acknowledge and agree Syncfusion®'s samples will not allow you seek injunctive relief in any form for any claim related to the sample. If you do not agree to this, do not view, access, utilize, or otherwise do anything with Syncfusion®'s samples.