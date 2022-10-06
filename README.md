# Power Progressive
Usually, you have two options on how to run Power Apps: You can opne them in a browser or in the player.    
On mobile the situation is a bit better with the Wrap feature, allowing you to package your app and the player in a single native app for iOS or Android.
On the desktop, we seemingly don't have that option. But in fact, we do.     

Before we go into how, let's talk about Progressive Web Apps, also known as **PWAs**.    

## Progressive Web Apps (PWA)
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

## The Power Apps Connection
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

## Configuring your app
Get the solution and template from the GitHub repository.    
Unpack the template archive and open the following files in your favorite code editor: index.html and 

[WORK IN PROGRESS]

## Pros and Cons
