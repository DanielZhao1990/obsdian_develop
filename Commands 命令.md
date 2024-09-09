

Commands are actions that the user can perform from the [Command Palette](https://help.obsidian.md/Plugins/Command+palette) or by using a hot key.  
命令是用户可以从[命令面板](https://help.obsidian.md/Plugins/Command+palette)或通过使用热键执行的操作。

![command.png](https://publish-01.obsidian.md/access/caa27d6312fe5c26ebc657cc609543be/Assets/command.png)

To register a new command for your plugin, call the [addCommand()](https://docs.obsidian.md/Reference/TypeScript+API/Plugin/addCommand) method inside the `onload()` method:  
要为您的插件注册一个新命令，请在`onload()`方法中调用[addCommand()](https://docs.obsidian.md/Reference/TypeScript+API/Plugin/addCommand)方法：

```ts
import { Plugin } from "obsidian";

export default class ExamplePlugin extends Plugin {
  async onload() {
    this.addCommand({
      id: "print-greeting-to-console",
      name: "Print greeting to console",
      callback: () => {
        console.log("Hey, you!");
      },
    });
  }
}
```

## 0.1 Conditional commands 条件命令

If your command is only able to run under certain conditions, then consider using [checkCallback()](https://docs.obsidian.md/Reference/TypeScript+API/Command/checkCallback) instead.  
如果您的命令只能在某些条件下运行，则考虑使用[checkCallback()](https://docs.obsidian.md/Reference/TypeScript+API/Command/checkCallback)。

The `checkCallback` runs twice. First, to perform a preliminary check to determine whether the command can run. Second, to perform the action.  
`checkCallback`运行两次。第一次进行初步检查以确定命令是否可以运行。第二次执行该操作。

Since time may pass between the two runs, you need to perform the check during both calls.  
由于在两次运行之间可能会经过一段时间，因此您需要在两次调用中都进行检查。

To determine whether the callback should perform a preliminary check or an action, a `checking` argument is passed to the callback.  
为了确定回调是否应该执行初步检查或操作，`checking`参数会传递给回调。

- If `checking` is set to `true`, perform a preliminary check.  
    如果`checking`设置为`true`，则执行初步检查。
- If `checking` is set to `false`, perform an action.  
    如果 `checking` 设置为 `false`，则执行一个操作。

The command in the following example depends on a required value. In both runs, the callback checks that the value is present but only performs the action if `checking` is `false`.  
以下示例中的命令依赖于一个必需的值。在两次运行中，回调检查该值是否存在，但仅在 `checking` 为 `false` 时执行操作。

```ts
this.addCommand({
  id: 'example-command',
  name: 'Example command',
  // highlight-next-line
  checkCallback: (checking: boolean) => {
    const value = getRequiredValue();

    if (value) {
      if (!checking) {
        doCommand(value);
      }

      return true
    }

    return false;
  },
});
```

## 0.2 Editor commands 编辑器命令

If your command needs access to the editor, you can also use the [editorCallback()](https://docs.obsidian.md/Reference/TypeScript+API/Command/editorCallback), which provides the active editor and its view as arguments.  
如果您的命令需要访问编辑器，您还可以使用 [editorCallback()](https://docs.obsidian.md/Reference/TypeScript+API/Command/editorCallback)，它提供活动编辑器及其视图作为参数。

```ts
this.addCommand({
  id: 'example-command',
  name: 'Example command',
  editorCallback: (editor: Editor, view: MarkdownView) => {
    const sel = editor.getSelection()

    console.log(`You have selected: ${sel}`);
  },
}
```

Note 注意

Editor commands only appear in the Command Palette when there's an active editor available.  
只有在有活动编辑器可用时，编辑器命令才会出现在命令面板中。

If the editor callback can only run given under certain conditions, consider using the [editorCheckCallback()](https://docs.obsidian.md/Reference/TypeScript+API/Command/editorCheckCallback) instead. For more information, refer to [Conditional commands](https://docs.obsidian.md/Plugins/User+interface/Commands#Conditional%20commands).  
如果编辑器回调只能在特定条件下运行，请考虑使用 [editorCheckCallback()](https://docs.obsidian.md/Reference/TypeScript+API/Command/editorCheckCallback)。有关更多信息，请参阅 [条件命令](https://docs.obsidian.md/Plugins/User+interface/Commands#Conditional%20commands)。

```ts
this.addCommand({
  id: 'example-command',
  name: 'Example command',
  editorCheckCallback: (checking: boolean, editor: Editor, view: MarkdownView) => {
    const value = getRequiredValue();

    if (value) {
      if (!checking) {
        doCommand(value);
      }

      return true
    }

    return false;
  },
});
```

## 0.3 Hot keys 热键

The user can run commands using a keyboard shortcut, or _hot key_. While they can configure this themselves, you can also provide a default hot key.  
用户可以使用键盘快捷键或 _热键_ 运行命令。虽然他们可以自己配置，但您也可以提供默认热键。

Warning 警告

Avoid setting default hot keys for plugins that you intend for others to use. Hot keys are highly likely to conflict with those defined by other plugins or by the user themselves.  
避免为您打算让其他人使用的插件设置默认热键。热键很可能与其他插件或用户自己定义的热键发生冲突。

In this example, the user can run the command by pressing and holding Ctrl (or Cmd on Mac) and Shift together, and then pressing the letter `a` on their keyboard.  
在这个例子中，用户可以通过同时按住 Ctrl（或在 Mac 上按 Cmd）和 Shift，然后按下键盘上的字母 `a` 来运行命令。

```ts
this.addCommand({
  id: 'example-command',
  name: 'Example command',
  hotkeys: [{ modifiers: ["Mod", "Shift"], key: "a" }],
  callback: () => {
    console.log('Hey, you!');
  },
});
```

Note 注意

The Mod key is a special modifier key that becomes Ctrl on Windows and Linux, and Cmd on macOS.  
Mod 键是一个特殊的修饰键，在 Windows 和 Linux 上变为 Ctrl，在 macOS 上变为 Cmd。