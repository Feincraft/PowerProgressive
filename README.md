# Power Progressive
Usually, you have two options on how to run Power Apps: You can opne them in a browser or in the player.    
On mobile the situation is a bit better with the Wrap feature, allowing you to package your app and the player in a single native app for iOS or Android.
On the desktop, we seemingly don't have that option. But in fact, we do.     

Before we go into how, let's talk about Progressive Web Apps, also known as **PWAs**.    

## 1️⃣ Progressive Web Apps (PWA)
A relatively recent addition to web standards, PWA is a way to present web apps as if they were native desktop (or mobile apps).     
They can handle files, access hardware, show notifications and generally look and feel native.    
Spotify, BMW, Starbucks, Microsoft and other companies make either PWA versions of their apps or outright make it the only option.    

Both **Microsoft Store** and **Google Play** accept PWAs to their ecosystems as first class citizens.    
This is not yet the case with Apple, however you can install PWAs from Safari on your iPhone/iPad.    

And that last point is important: you don't have to publish your PWA on any app store.     
Just send a link to anyone and they will see a prmopt to install your app right in their browser.    

![image](https://user-images.githubusercontent.com/32096531/194196168-8c9b1ad0-dfe9-4779-b40d-576128d52d0c.png)

**Want to learn more?**     
https://learn.microsoft.com/en-us/microsoft-edge/progressive-web-apps-chromium/ux

So, PWAs are on the way to take over traditional native apps but what does it have to do with Power Apps?    

## 2️⃣ The Power Apps Connection
At their core, Power Apps are also built on web technologies, with a little Microsoft Cloud magic mixed in.
This of course is obvious if you ever run a Power App in a browser.   

Creating a PWA requires building a web app in a very specific way. 
It's not complicated but it needs to have some components that Power Apps don't currently offer, like a manifest file and Java Script code to handle special events. 

We can't modify the Power App but we can seemlessly integrate it into an existing PWA using every web developer's worst nightmare: an **IFrame**. 
This essentially means that we wrap the app in a PWA shell, which behaves like a native desktop app.

Take a look:

![PowerApps PWA O60](https://user-images.githubusercontent.com/32096531/194200558-925094e8-3804-463b-af21-2cd1808717a3.gif)

You have full control over how your app will look like with 95% of that done directly in Power Apps Studio.
There's however some work that you need to do to set it up.

## 3️⃣ Configuring your app
Get the solution and template from the GitHub repository.    
Unpack the [template archive](https://github.com/Feincraft/PowerProgressive/blob/main/PowerProgressive%20Template.zip) and open the following files in your favorite code editor: **index.html** and **manifest.json**.

### Configure Manifest
Let's start with the Manifest file, this is where the metadata about the app is located.    
Fill in the name, short name and description on the app.    
Short name is used in some cases, like for the app shortcut on mobile devices.

```json
"name": "Feincraft Logistics",
"short_name": "FeincraftLogs",
"description": "The Feincraft Logistics app",
```

Set theme color and background colors to the key color you're using in the app.   
It will be used as the titlebar color on desktop and the default background color.

```json
"theme_color": "#0078D5",
"background_color": "#0078D5",
```

The screenshots section is needed only if you're going to publish to app stores, to show how your app looks like.

```json
"screenshots": [
  {
    "src": "screenshot.png",
    "sizes": "1718x1024",
    "type": "image/png",
    "description": "The Feincraft Logistics app, dekstop version"
  }
] 
```

The last section is a long array of icons, in fact the same icon of different sizes.    
This is to represent the app on different platforms.    
You don't have to create so many icons for the app, just one with 512x512 dimentions.    
It can be useful to create seperate icons of smaller resolutions to make sure they are readable.

```json
"icons": [
  {
    "src": "/icons/512x512-icon.png",
    "type": "image/png",
    "sizes": "512x512",
    "purpose": "any"
  }
]
```

Another option is to use the PWA Studio extension in VSCode to generate icons automatically.     
While having the Manifest file open, go to the extension and click the Generate Icons button.

![Open Generate Icons](https://user-images.githubusercontent.com/32096531/194398517-de4c528f-7fc8-4d89-ba83-bd72dceff531.png)

Select a 512x512 icon from the dialog and click "Generate".    
The extension will create a set of icons for every size and will automatically populate

![Generate Icons](https://user-images.githubusercontent.com/32096531/194398638-5457f087-45d5-4217-9c13-e0f33a18eb1c.png)

Now we're done with the Manifest, let's move on to the template.

### Configure Template

The template is an HTML file containing the IFrame that will host your Power App.   
First thing are the icons, make sure to supply your own favicon, this will be the desktop shortcut icon too.    
Apple Touch icons are needed only for iPads and iPhones.
```html
<link rel="apple-touch-icon" href="/icons/180x180-icon.png">
<link rel="icon" href="favicon.ico" type="image/png" />
```

The following section describes the style of the titlebar.    
You can change anything you want but the only important thing is the location and size of the titlebar.    

```css
/* Titlebar text style */
font-size: 16px;
font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
color:white;
font-weight:bold;

/* Location of titlebar */
left: 910px;
top: 0px;
width: 100%;
height: 33px;

/* Color of titlebar */
background-color: transparent;
```

In the supplied example, the title bar does not take the entire top of the window, leaving space for buttons and a search bar.    
The draggable portion (highlighted in yellow below), is offset by 910px, the space required by the toolbar.

![Toolbar](https://user-images.githubusercontent.com/32096531/194404013-c8421318-a0d4-49dd-bc08-ee4b8644dbab.png)

Next, change the following line to adjust the text that will be displayed on the titlebar.

```html
<!-- Power App titlebar text -->
<div id="titlebar-drag">Feincraft Logistics</div>
```

And the last thing to do is to point the template to the right place.    
Change the **src** attribute of the IFrame to the URL of your app.    
Add **&hidenavbar=true** at the end so it looks like the example provided below.

```html
<iframe src="https://apps.powerapps.com/play/e/default-79f8134f-8056-4569-b5de-5bd62a6e0008/a/f79060fa-f84f-4bf9-ad93-25c141038d9e?tenantId=79f8134f-8056-4569-b5de-5bd62a6e0008&source=portal&skipAppMetadata=true&hidenavbar=true" 
```
You can use your own Power App or the one supplied with **Power Progressive**    
The sample app (Feincraft Logistics) can be found here:     
https://github.com/Feincraft/PowerProgressive/blob/main/PowerProgressive_1_0_0_1_managed.zip 

That's it! Your Power App is now an installable app.    
Don't believe me? Let's test it!

## 4️⃣ Test your app
You will need the app to be served by a web server.    
It can be in Azure with Static Web Apps, another web hosting or locally.    
Unless you already have a web development environment set up on your machine, the easiest way to test is with SWA CLI.    
A simple tool to test web apps locally.   

```powershell
npm install -g @azure/static-web-apps-cli
```

Now open the terminal in the folder where the app is located and type:

```powershell
swa start
```

SWA will serve the content of the folder (your app) at the spcified address.    
It would be something like http://localhost:4280    
You can Ctrl+Click directly in the terminal window to open the app.

![SWA Running](https://user-images.githubusercontent.com/32096531/194411165-9fb1307d-109b-4586-8fe5-fd609faa5eb4.png)

The app will initially open in the browser.    
Look at the right side of the address bar to find the app installation icon.

![Install PWA](https://user-images.githubusercontent.com/32096531/194412693-939d2d67-a713-4c54-b085-6ad98fd0f734.png)

Click Install and the app will turn into a desktop application with a native feel.    
You'll be presented with additional options on placing shortcuts and auto starting the app.

![Configure PWA](https://user-images.githubusercontent.com/32096531/194413274-46b47bbc-91f4-4577-91e0-412cabc36fad.png)

When you start the app for the first time, the app will be shown with a regular full length titlebar.    
You can collapse this titlebar to leave the compact titlebar we defined in the template.    
This needs to be done only once.

![Collapse Titlebar](https://user-images.githubusercontent.com/32096531/194413780-18d1c645-7f68-47f5-b7bc-6453a4735168.png)

Congratulations on deploying your first **Power Progressive** app!

### Further Reading

Want to know more about SWA CLI?    
https://azure.github.io/static-web-apps-cli/docs/intro

If you got this far I'd assume you already have **npm** installed, but just in case:    
https://nodejs.org/en/download/

## 5️⃣ Roadmap
There's a few things that will be added in future versions:
### Badges
![image](https://user-images.githubusercontent.com/32096531/194416911-a1bc8d77-5f8c-46f9-b8ba-991fb08daa17.png)

Let users know how many messages, tasks, or orders they have.

### Desktop Notifications 
![image](https://user-images.githubusercontent.com/32096531/194417015-b8111297-ce53-41a1-bbb8-239499924b65.png)

Notify of in-app events using the native notifications mechanism of your OS.   
Even notifications with interactive buttons are possible (Yes/No, Ok/Cancel, etc).

### Tasks
![msedge_2BkLSDfrnU](https://user-images.githubusercontent.com/32096531/194416737-81d3c1fb-aa49-41f8-ba28-1c1a0bb783bd.png)

Right-click to open the app at a certain screen (deeplinking) or perform an action.    

## 6️⃣ Feedback
Tag me in posts with your feedback, follow for updates.    
**LinkedIn:** https://www.linkedin.com/in/ifainb/    
**Twitter:** https://twitter.com/IFainberg (@IFainberg)    

Like this solution? ⭐

![Star It](https://user-images.githubusercontent.com/32096531/194415789-2ee4f5df-14f4-4b4e-a683-32d74f7f2a03.gif)
