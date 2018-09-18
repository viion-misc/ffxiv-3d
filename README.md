# ffxiv-3d

Concept of a web based 3D Model Viewer for FFXIV

## How to use

You need https://textools.dualwield.net/
- https://bitbucket.org/liinko/ffxiv-textools/issues?status=new&status=open

Extract some models, and then modify the code to the correct paths. Currently set to show Fenrir mount, armor works fine. As FFXIV TexTools is open source I took it and modified it to automatically go through all items/mounts/companions and extract each one, it was very slow taking hours and hours to finish. Impractical really!

Doubt there will be any production on this, so feel free to use as you want! No questions asked. All the logic is in `index.html` as I was lazy :D maybe one day I will clean this up.

Clone it and run it on a web server of sorts, i just used https://www.npmjs.com/package/live-server

## Live example:

http://xivapi.com/_3d/index.html

![Example](https://i.imgur.com/JFNreqG.jpg)


## TexTools mod

I added a button with this logic, it basically goes through the list, selects an item which prompts TexTools to load information about it and then call the export command on the selected item. Repeat over n over. Often would crash but could work a lot better if I spent more time learning about TexTools or asking for support from the Maintainer.

- (1.8.5) My modified code: https://github.com/viion-misc/FFXIV_TexTools2/commit/3a8c2ee893f044b88762c5c47bab6727f3cd1a44
- (1.9.8) Official by liinko https://github.com/liinko/FFXIV_TexTools2

```csharp
private void Button_Click(object sender, RoutedEventArgs e)
{
    //
    // GEAR
    //
    CategoryViewModel Gear = (CategoryViewModel)textureTreeView.Items.GetItemAt(0);
    Gear.IsSelected = true;

    foreach (CategoryViewModel category in Gear.Children)
    {
        category.IsExpanded = true;
        category.IsSelected = true;

        string time = string.Format("{0:HH:mm:ss tt}", DateTime.Now);
        string logfilename = "E:\\xivdb\\FFXIV_TextTools2_Output\\log.txt";
  
        File.AppendAllText(logfilename, time + " - Category: " + category.Name.ToString() + " - Items: " + category.Children.Count.ToString() + Environment.NewLine);

        foreach (CategoryViewModel item in category.Children)
        {
            item.IsExpanded = true;
            item.IsSelected = true;
            actionSelectedItemChanged(item);

            SaveModel.Save(
                mViewModel.getMvm().getModelName(),
                mViewModel.getMvm().getSelectedMeshId(),
                mViewModel.getMvm().getMeshData(),
                mViewModel.getMvm().getMeshList()
            );

            File.AppendAllText(logfilename, time + " - Saved: " + item.Name.ToString() + " -- " + mViewModel.getMvm().getModelName() + Environment.NewLine);
        }
    }

    //
    // COMPANIONS
    //
    CategoryViewModel Companions = (CategoryViewModel)textureTreeView.Items.GetItemAt(2);
    Companions.IsSelected = true;

    foreach (CategoryViewModel category in Companions.Children)
    {
        category.IsExpanded = true;
        category.IsSelected = true;

        string time = string.Format("{0:HH:mm:ss tt}", DateTime.Now);
        string logfilename = "E:\\xivdb\\FFXIV_TextTools2_Output\\log.txt";

        File.AppendAllText(logfilename, time + " - Category: " + category.Name.ToString() + " - Items: " + category.Children.Count.ToString() + Environment.NewLine);

        foreach (CategoryViewModel item in category.Children)
        {
            item.IsExpanded = true;
            item.IsSelected = true;
            actionSelectedItemChanged(item);

            SaveModel.Save(
                mViewModel.getMvm().getModelName(),
                mViewModel.getMvm().getSelectedMeshId(),
                mViewModel.getMvm().getMeshData(),
                mViewModel.getMvm().getMeshList()
            );

            File.AppendAllText(logfilename, time + " - Saved: " + item.Name.ToString() + " -- " + mViewModel.getMvm().getModelName() + Environment.NewLine);
        }
    }

}
```
