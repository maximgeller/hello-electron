# Build a desktop app with HTML, CSS and JS 
You're probably going like, "Say what now?", but yes, it's possible. All thanks to [Electron.js](https://electronjs.org). Electron is a package developed by [GitHub](https://github.com/electron/electron) that allows you to make native apps with web technologies like HTML, CSS and JS.
For this to work, you're going to have to have [Node.js](https://nodejs.org/en/download/). To check if you have all the required dependencies, run ```node -v``` and ```npm -v``` in your terminal. If either of them come up looking like this: ```'node' is not recognized as an internal or external command,
operable program or batch file.```, then download Node.js using the link above. Then, in command prompt, run ```npm install --save-dev electron``` to install Electron.

## Setup
The structure of our app is going to look a bit different to most Enlight tutorial apps.
Make a folder named `electron-app`, and open command prompt. Open the folder by typing `cd` and then the directory of the folder. It should look something like this: `cd C:\Users\me\Desktop\electron-app`. Once you are inside the folder, run the command `npm init`. It will ask you for the name of the app. By default this is the name of the folder. You can leave everything blank, except for `main`, which you need to change to `main.js`, and `test`, which you need to change to `electron  .` The `electron` is telling Node to run the command `electron` and the `.` is telling Node to do that right here for all the files in this folder. Once you are finished, open the folder in your favorite editor, such as [VSCode](https://code.visualstudio.com) or [Atom](https://atom.io).

## Making the app
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
# Now what?
You have just built a desktop application using Electron! That's great and all, but what can you do with it? One idea is to integrate one of any of the other projects on Enlight into this app. In my case, I would love to have my to-do list as a desktop app. Let's pull the source code from the [to-do list tutorial](https://enlight.nyc/projects/to-do) and put it in our markup, style, and script! Let's create two new files, `app.js` and `style.css` for the style and script of the to-do list. We'll add the necessary HTML to the already existing `index.html` file! Have a look at the source code and write your files in a similar way, like this:
```javascript
// app.js
function  newItem() {
	var  item  =  document.getElementById('input').value;
	var  ul  =  document.getElementById("list");
	var  li  =  document.createElement('li');

	li.appendChild(document.createTextNode("- "+item));
	ul.appendChild(li);
	document.getElementById('input').value="";
	li.onclick  =  removeItem;
}

document.body.onkeyup  =  function(e){
	if(e.keyCode  ==  13){
	newItem();
	}
}

function  removeItem(e) {
	e.target.parentElement.removeChild(e.target);
}
```
Next, we do the style.
```css


<!--stackedit_data:
eyJoaXN0b3J5IjpbOTU5MjYyMDcxLC0zMDM5NzE3MTUsLTIwMz
UzMTkxMTJdfQ==
-->