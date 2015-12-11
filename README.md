# angular2-electron-quickstrat
Simple Angular2-Electron project quickstart guide

First, do [angular2-quickstart](https://github.com/nallwhy/angular2-quickstart).

## Setting

### npm
```sh
npm install electron-prebuilt -g
npm install electron-packager -g
```

### ./package.json
```javascript
{
  ...
  "scripts": {
    ...
    "start": "electron main.js",
    "package": "electron-packager ./ <appname> --platform=<platform:linux, win32, darwin, all> --arch=<arch:ia32, x64, all> --version=<Electron version> --out=<path> --overwrite"
    ...
  }
}
```
--out=<path> argument
  - Absolute path starts with '/'
  - Relative path
  - A path starts with '~/' concerned as *relative* path.

If you want to see more options of electron-packager, please visit [electron-packager](https://github.com/maxogden/electron-packager).

### ./main.js
```javascript
const electron = require('electron');
const app = electron.app;  // Module to control application life.
const BrowserWindow = electron.BrowserWindow;  // Module to create native browser window.

// Report crashes to our server.
electron.crashReporter.start();

// Keep a global reference of the window object, if you don't, the window will
// be closed automatically when the JavaScript object is garbage collected.
var mainWindow = null;

// Quit when all windows are closed.
app.on('window-all-closed', function() {
  // On OS X it is common for applications and their menu bar
  // to stay active until the user quits explicitly with Cmd + Q
  if (process.platform != 'darwin') {
    app.quit();
  }
});

// This method will be called when Electron has finished
// initialization and is ready to create browser windows.
app.on('ready', function() {
  // Create the browser window.
  mainWindow = new BrowserWindow({width: 800, height: 600});

  // and load the index.html of the app.
  mainWindow.loadURL('file://' + __dirname + '/src/index.html');

  // Open the DevTools.
  mainWindow.webContents.openDevTools();

  // Emitted when the window is closed.
  mainWindow.on('closed', function() {
    // Dereference the window object, usually you would store windows
    // in an array if your app supports multi windows, this is the time
    // when you should delete the corresponding element.
    mainWindow = null;
  });
});
```

## Run
```sh
npm run tsc
npm start
```

## Distribute
```sh
npm run package -- <other args>
```
