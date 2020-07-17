# electron-default-menu

A simple module that returns a default Electron menu template, similar to the one you'll get if you don't use `Menu.setApplicationMenu()` at all.  You can modify the returned template before creating the application menu.

Based on the sample code supplied in the [Electron menu documentation](https://github.com/atom/electron/blob/master/docs/api/menu.md)

Like the sample code, it checks the environment, and returns appropriate additional menus for Mac OS X, and sets the `role` for each menu accordingly.

Must be used from the Electron environment.

## Install

**Install using npm**

```shell
npm install --save electron-default-menu
```

**Install using yarn**

```shell
yarn add electron-default-menu
```

## Example usage:

```javascript
import { Menu, app, dialog, shell } from 'electron';
import defaultMenu from 'electron-default-menu';

app.on('ready', () => {
  // Get default menu template
  const menu = defaultMenu(app, shell);

  // Add custom menu
  menu.splice(4, 0, {
    label: 'Custom',
    submenu: [
      {
        label: 'Do something',
        click: (item, focusedWindow) => {
          dialog.showMessageBox({message: 'Do something', buttons: ['OK'] });
        }
      }
    ]
  });

  // Set application menu
  Menu.setApplicationMenu(Menu.buildFromTemplate(menu));
});
```
