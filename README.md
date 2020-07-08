# Build a desktop app with HTML, CSS and JS 
You're probably going like, "Say what now?", but yes, it's possible. All thanks to [Electron.js](https://electronjs.org). Electron is a package developed by [GitHub](https://github.com/electron/electron) that allows you to make native apps with web technologies like HTML, CSS and JS.
For this to work, you're going to have to have [Node.js](https://nodejs.org/en/download/). To check if you have all the required dependencies, run ```node -v``` and ```npm -v``` in your terminal. If either of them come up looking like this: ```'node' is not recognized as an internal or external command,
operable program or batch file.```, then download Node.js using the link above. Then, in command prompt, run ```npm install --save-dev electron``` to install Electron.

## Setup
The structure of our app is going to look a bit different to most Enlight tutorial apps.
Make a folder named `electron-app`, and open command prompt. Open the folder by typing `cd` and then the directory of the folder. It should look something like this: `cd C:\Users\me\Desktop\electron-app`. Once you are inside the folder, run the command `npm init`. It will ask you for the name of the app. By default this is the name of the folder. You can leave everything blank, except for `main`, which you need to change to `main.js`, and `test`, which you need to change to `electron  .` The `electron` is telling Node to run the command `electron` and the `.` is telling Node to do that right here for all the files in this folder. Once you are finished, open the folder in your favorite editor, such as [VSCode](https://code.visualstudio.com) or [Atom](https://atom.io).

## Now, we actually make the app.
Create a file called `main.js`, and put the following code in:

```javascript

const { app, BrowserWindow } = require('electron')

function createWindow () {
    // Create the browser window.
    const win = new BrowserWindow({
        width: 800,
        height: 600,
        webPreferences: {
            nodeIntegration: true
        }
    })

    // and load the index.html of the app.
    win.loadFile('index.html')

    // Open the DevTools.
    win.webContents.openDevTools()
}

// This method will be called when Electron has finished
// initialization and is ready to create browser windows.
// Some APIs can only be used after this event occurs.
app.whenReady().then(createWindow)

// Quit when all windows are closed, except on macOS. There, it's common
// for applications and their menu bar to stay active until the user quits
// explicitly with Cmd + Q.
app.on('window-all-closed', () => {
    if (process.platform !== 'darwin') {
        app.quit()
    }
})

app.on('activate', () => {
    // On macOS it's common to re-create a window in the app when the
    // dock icon is clicked and there are no other windows open.
    if (BrowserWindow.getAllWindows().length === 0) {
        createWindow()
    }
})
```

Now we can add our HTML into ```index.html```:
```html
<!doctype html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport"
          content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>electron-app</title>
</head>
<body>
    <h1>This app is built with HTML!</h1>
    <h3>And it's not witchcraft! It's Electron!</h3>
</body>
</html>
```
Finally, open command prompt in the project folder, and run `npm test`. You should see a window on your desktop like this: ![electron app](https://cdn.discordapp.com/attachments/659135546060439592/730402981668847646/unknown.png)

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTkxNTYwNjQ1MV19
-->