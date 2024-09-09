

Plugins let you extend Obsidian with your own features to create a custom note-taking experience.  
插件让您可以通过自己的功能扩展 Obsidian，以创建自定义的笔记体验。

In this tutorial, you'll compile a sample plugin from source code and load it into Obsidian.  
在本教程中，您将从源代码编译一个示例插件并将其加载到 Obsidian 中。

## 0.1 What you'll learn 您将学到的内容

After you've completed this tutorial, you'll be able to:  
完成本教程后，您将能够：

- Configure an environment for developing Obsidian plugins.  
    配置开发 Obsidian 插件的环境。
- Compile a plugin from source code.  
    从源代码编译插件。
- Reload a plugin after making changes to it.  
    在对插件进行更改后重新加载插件。

## 0.2 Prerequisites 先决条件

To complete this tutorial, you'll need:  
要完成本教程，您需要：

- [Git](https://git-scm.com/) installed on your local machine.  
    在您的本地计算机上安装[Git](https://git-scm.com/)。
- A local development environment for [Node.js](https://node.js.org/en/about/).  
    一个用于[Node.js](https://node.js.org/en/about/)的本地开发环境。
- A code editor, such as [Visual Studio Code](https://code.visualstudio.com/).  
    一个代码编辑器，例如[Visual Studio Code](https://code.visualstudio.com/)。

## 0.3 Before you start 在您开始之前

When developing plugins, one mistake can lead to unintended changes to your vault. To prevent data loss, you should never develop plugins in your main vault. Always use a separate vault dedicated to plugin development.  
在开发插件时，一个错误可能会导致对您的库产生意外更改。为了防止数据丢失，您绝不应该在主库中开发插件。始终使用一个专门用于插件开发的单独库。

[Create an empty vault](https://help.obsidian.md/Getting+started/Create+a+vault#Create+empty+vault).  
[创建一个空库](https://help.obsidian.md/Getting+started/Create+a+vault#Create+empty+vault)。

## 0.4 Step 1: Download the sample plugin  
第一步：下载示例插件

In this step, you'll download a sample plugin to the `plugins` directory in your vault's [`.obsidian` directory](https://help.obsidian.md/Advanced+topics/How+Obsidian+stores+data#Per+vault+data) so that Obsidian can find it.  
在这一步中，您将下载一个示例插件到您的保险库的 `plugins` 目录中的 [`.obsidian` 目录](https://help.obsidian.md/Advanced+topics/How+Obsidian+stores+data#Per+vault+data)，以便 Obsidian 可以找到它。

The sample plugin you'll use in this tutorial is available in a [GitHub repository](https://github.com/obsidianmd/obsidian-sample-plugin).  
您将在本教程中使用的示例插件可以在 [GitHub 仓库](https://github.com/obsidianmd/obsidian-sample-plugin) 中找到。

1. Open a terminal window and change the project directory to the `plugins` directory.  
    打开终端窗口并将项目目录更改为 `plugins` 目录。
    
    ```bash
    cd path/to/vault
    mkdir .obsidian/plugins
    cd .obsidian/plugins
    ```
    
2. Clone the sample plugin using Git.  
    使用 Git 克隆示例插件。
    
    ```bash
    git clone https://github.com/obsidianmd/obsidian-sample-plugin.git
    ```
    

GitHub template repository  
GitHub 模板仓库

The repository for the sample plugin is a GitHub template repository, which means you can create your own repository from the sample plugin. To learn how, refer to [Creating a repository from a template](https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-repository-from-a-template#creating-a-repository-from-a-template).  
示例插件的仓库是一个 GitHub 模板仓库，这意味着您可以从示例插件创建自己的仓库。要了解如何操作，请参考 [从模板创建仓库](https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-repository-from-a-template#creating-a-repository-from-a-template)。

Remember to use the URL of your own repository when cloning the sample plugin.  
克隆示例插件时，请记得使用您自己仓库的 URL。

## 0.5 Step 2: Build the plugin  
第 2 步：构建插件

In this step, you'll compile the sample plugin so that Obsidian can load it.  
在这一步中，您将编译示例插件，以便 Obsidian 可以加载它。

1. Navigate to the plugin directory.  
    导航到插件目录。
    
    ```bash
    cd obsidian-sample-plugin
    ```
    
2. Install dependencies. 安装依赖项。
    
    ```bash
    npm install
    ```
    
3. Compile the source code. The following command keeps running in the terminal and rebuilds the plugin when you modify the source code.  
    编译源代码。以下命令在终端中持续运行，并在您修改源代码时重新构建插件。
    
    ```bash
    npm run dev
    ```
    

Notice that the plugin directory now has a `main.js` file that contains a compiled version of the plugin.  
请注意，插件目录现在有一个 `main.js` 文件，其中包含插件的编译版本。

## 0.6 Step 3: Enable the plugin  
第 3 步：启用插件

To load a plugin in Obsidian, you first need to enable it.  
要在 Obsidian 中加载插件，您首先需要启用它。

1. In Obsidian, open **Settings**.  
    在 Obsidian 中，打开 **设置**。
2. In the side menu, select **Community plugins**.  
    在侧边菜单中，选择 **社区插件**。
3. Select **Turn on community plugins**.  
    选择 **启用社区插件**。
4. Under **Installed plugins**, enable the **Sample Plugin** by selecting the toggle button next to it.  
    在 **已安装插件** 下，通过选择旁边的切换按钮来启用 **示例插件**。

You're now ready to use the plugin in Obsidian. Next, we'll make some changes to the plugin.  
你现在可以在 Obsidian 中使用该插件。接下来，我们将对插件进行一些更改。

## 0.7 Step 4: Update the plugin manifest  
第 4 步：更新插件清单

In this step, you'll rename the plugin by updating the plugin manifest, `manifest.json`. The manifest contains information about your plugin, such as its name and description.  
在此步骤中，您将通过更新插件清单 `manifest.json` 来重命名插件。清单包含有关您的插件的信息，例如名称和描述。

1. Open `manifest.json` in your code editor.  
    在代码编辑器中打开 `manifest.json`。
2. Change `id` to a unique identifier, such as `"hello-world"`.  
    将 `id` 更改为唯一标识符，例如 `"hello-world"`。
3. Change `name` to a human-friendly name, such as `"Hello world"`.  
    将 `name` 更改为人性化的名称，例如 `"Hello world"`。
4. Restart Obsidian to load the new changes to the plugin manifest.  
    重新启动 Obsidian 以加载插件清单的新更改。

Go back to **Installed plugins** and notice that the name of the plugin has been updated to reflect the changes you made.  
返回到 **已安装插件**，注意插件的名称已更新以反映您所做的更改。

Remember to restart Obsidian whenever you make changes to `manifest.json`.  
每当您对 `manifest.json` 进行更改时，请记得重启 Obsidian。

## 0.8 Step 5: Update the source code  
第 5 步：更新源代码

To let the user interact with your plugin, add a _ribbon icon_ that greets the user when they select it.  
为了让用户与您的插件互动，添加一个 _图标_，当用户选择它时向他们问好。

1. Open `main.ts` in your code editor.  
    在您的代码编辑器中打开 `main.ts`。
    
2. Rename the plugin class from `MyPlugin` to `HelloWorldPlugin`.  
    将插件类从 `MyPlugin` 重命名为 `HelloWorldPlugin`。
    
3. Import `Notice` from the `obsidian` package.  
    从 `obsidian` 包中导入 `Notice`。
    
    ```ts
    import { Notice, Plugin } from "obsidian";
    ```
    
4. In the `onload()` method, add the following code:  
    在 `onload()` 方法中，添加以下代码：
    
    ```ts
    this.addRibbonIcon('dice', 'Greet', () => {
      new Notice('Hello, world!');
    });
    ```
    
5. In the **Command palette**, select **Reload app without saving** to reload the plugin.  
    在**命令面板**中，选择**不保存重新加载应用**以重新加载插件。
    

You can now see a dice icon in the ribbon on the left side of the Obsidian window. Select it to display a message in the upper-right corner.  
您现在可以在 Obsidian 窗口左侧的功能区看到一个骰子图标。选择它以在右上角显示一条消息。

Remember, you need to **reload your plugin after changing the source code**, either by disabling it then enabling it again in the community plugins panel, or using the command palette as detailed in part 5 of this step.  
记住，您需要在更改源代码后**重新加载您的插件**，可以通过在社区插件面板中禁用然后重新启用它，或者使用命令面板，如本步骤第 5 部分所述。

Hot reloading 热重载

Install the [Hot-Reload](https://github.com/pjeby/hot-reload) plugin to automatically reload your plugin while developing.  
安装[热重载](https://github.com/pjeby/hot-reload)插件，以便在开发时自动重新加载您的插件。

## 0.9 Conclusion 结论

In this tutorial, you've built your first Obsidian plugin using the TypeScript API. You've modified the plugin and reloaded it to reflect the changes inside Obsidian.  
在本教程中，您使用 TypeScript API 构建了第一个 Obsidian 插件。您已修改插件并重新加载以反映 Obsidian 中的更改。