---
title: "Develop code in Visual Studio without projects or solutions | Microsoft Docs"
ms.custom: ""
ms.date: "02/17/2017"
ms.reviewer: ""
ms.suite: ""
ms.technology:
  - "vs-ide-general"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords:
  - "vs.texteditor"
dev_langs:
  - "JScript"
  - "VB"
  - "CSharp"
helpviewer_keywords:
  - "code, editing"
  - "code editor, syntax coloring"
  - "code editor [Visual Studio]"
  - "brace matching"
  - "code editor, line numbers"
  - "code editor, brace matching"
  - "line numbers"
  - "syntax coloring"
  - "code editor"
  - "code files"
  - "code"
ms.assetid: cb53bb9b-5b76-4759-b9b8-7bf32298bcbb
caps.latest.revision: 44
author: "kempb"
ms.author: "kempb"
manager: "ghogen"
translation.priority.ht:
  - "de-de"
  - "es-es"
  - "fr-fr"
  - "it-it"
  - "ja-jp"
  - "ko-kr"
  - "ru-ru"
  - "zh-cn"
  - "zh-tw"
translation.priority.mt:
  - "cs-cz"
  - "pl-pl"
  - "pt-br"
  - "tr-tr"
---
# Develop code in Visual Studio without projects or solutions

In Visual Studio 2017, you can open code from nearly any type of directory-based project into Visual Studio without the need for a solution or project file. This means you can, for example, find a code project on Git, clone it, and then open it directly into Visual Studio and begin developing without having to create a solution or projects.

Not only can you edit the code and build it in Visual Studio, you can also navigate through your code (such as by using the Navigate To command). Code will appear with syntax colorization and, in many cases, include basic statement completion and debugging, complete with breakpoints. Some languages will include even more functionality. See [Create portable, custom editor settings](create-portable-custom-editor-options.md) for more information.

## Open code anywhere
You can open code into Visual Studio in the following ways.
- On the Visual Studio menu bar, choose **File**, **Open**, **Folder**, then browse to the code location.
- On the context (right-click) menu of a folder containing code, choose the **Open in Visual Studio** command.
- Open code cloned from a GitHub repo.

The following example shows how to clone a GitHub repo and then open its code in Visual Studio. To follow this procedure, you must have a GitHub account and Git for Windows installed on your system. See [Signing up for a new GitHub account](https://help.github.com/articles/signing-up-for-a-new-github-account/) and [Git for Windows](https://git-for-windows.github.io/) for more information.

### To open code from a cloned GitHub repo

1. Go to the GitHub repo that has the code you want to work on. To do this, you need to have a GitHub account.
1. Go to the repo you want to clone.
1. On the repo's GitHub page, choose the **Clone or Download** button and then choose the **Copy to Clipboard** button in the dropdown menu to copy the secure URL for the GitHub site.

  ![GitHub clone button](../VS 2017 RTW Topics/media/VSIDE_Code_Clone.png)

    > [!NOTE]
    >  While you also have the option to open the project on your desktop or download a .zip file of the project, this example demonstrates how to clone the repo using the secure URL method.

1. In Visual Studio, choose the **Team Explorer** tab to open Team Explorer.
1. In Team Explorer, under the **Local Git Repositories** section, choose the **Clone** command and then paste the URL of the GitHub page into the text box.

  ![Clone the project](../VS 2017 RTW Topics/media/VSIDE_Code_Clone2.png)

1. Choose the **Clone** button to clone the project's files to a local Git repository. Depending on the size of the repo, this process could take several minutes.
1. After the repo has been cloned to your system, in Team Explorer, choose the **Open** command on the context (right-click) menu of the newly cloned project.

  ![Cloned project](../VS 2017 RTW Topics/media/VSIDE_Code_Clone3.png)

1. Choose the **Show Folder View** command to view the files in Solution Explorer

  ![Show folder view](../VS 2017 RTW Topics/media/VSIDE_Code_Clone3_show.png)

  You can now browse folders and files in the cloned project and view and search the code in the Visual Studio code editor, complete with syntax colorization and other features.

    ![Searching cloned project code](../VS 2017 RTW Topics/media/VSIDE_Code_Clone4.png)


## Debug your code
You can debug your code in Visual Studio. To debug some languages, though, you may need to specify a "startup file" in the code project. Valid startup files include scripts, executables, and projects. Visual Studio runs this specified code first when you debug your code.

Visual Studio currently supports debugging for the following languages:
- Node.js
- Python
- MSBuild-based projects (C#, VB, C++)
- Any executable with PDB (Python Debugger) files.

### To debug Node.js and Python:
1. Install Node.js or Python Tools or Visual Studio 2017 and the Node.js runtime.
1. On the context menu of any JavaScript file in Solution Explorer, choose the **Set as Startup Item** command.
1. Choose the F5 key to begin debugging.

### To debug MSBuild projects
1. On the Visual Studio menu, choose **Debug**. On the dropdown menu, choose the project or select the project or file that you want to display as the startup item in Solution Explorer.
1. Choose the F5 key to begin debugging.

### To debug executable files
1. On the Visual Studio menu, choose **Debug**. On the dropdown menu, choose the project or select the project or file that you want to display as the startup item in Solution Explorer.
1. Choose the F5 key to begin debugging.


## Enable custom build tools
If you try to run your code and Visual Studio doesn't know how to run it, an info bar prompts you to choose an item in your codebase in Solution Explorer to be the startup item. However, if the codebase uses custom build tools that Visual Studio doesn't recognize, then you will probably not be able to immediately run and debug the code in Visual Studio (such as by choosing the F5 key) until you specify the custom parameters and arguments required by the language. To enable this, Visual Studio provides *build tasks*. Build tasks are files you can create to specify any items a language needs to build and run your code.

#### To create a build task

1. Choose the folder of the project in Solution explorer, and on its context (right-click) menu, choose **Configure Tasks**.

  ![Configure tasks](../VS 2017 RTW Topics/media/VSIDE_Code_Config_Task.png)

  Choosing **Configure Tasks** opens a file called tasks.vs.json. If this file doesn't exist, it is created. This file contains the build tasks for the selected folder.

  ![Tasks.vs.json file](../VS 2017 RTW Topics/media/VSIDE_Code_Tasks_JSON.png)

1. Add to tasks.vs.json the build tasks needed to run your codebase. You can add clean and rebuild taskTypes. Visual Studio supports the VSCode `$variable` substitution, in addition to any environment variables (such as `$env.var`) or keys in the root of tasks.json.

1. Once the build task file is filled in correctly, save it and then choose it in Solution Explorer and set it as the startup item.

  Now, you can choose F5 to run your codebase. You can now edit and debug your codebase in Visual Studio even though Visual Studio doesn't recognize the build tools of the codebase. Output from the build task appears in the **Output** window, and build errors appear in the **Error List**. The tasks.vs.json build task file couples the Visual Studio inner development loop to the custom build tools used by your codebase.


## Add a custom task to a file
Custom build tasks can be added to individual files, or to all files of a specific type. For instance, NuGet package files can be configured to have a "Restore Packages" task, or all source files can be configured to have a static analysis task, such as a linter for all .js files.

The following example shows how to add a custom task called "Make Documentation" for a codebase.

### To add a custom task

1. Choose a file or folder in Solution Explorer and choose the **Task Settings** command on the context menu.

  ![Task 1](../VS 2017 RTW Topics/media/VSIDE_Code_Tasks_Custom1.png)

1. Add the task to the tasks.json file.

  ![Task 2](../VS 2017 RTW Topics/media/VSIDE_Code_Tasks_Custom2.png)

1. On the context menu of the item, choose the new **Make Documentation** command.
