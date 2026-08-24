---
title: Browsers
excerpt: Control D can be configured directly in most modern browsers.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
> 🚧 Usage Warning
>
> Configuring Control D directly in the browser, will only change your DNS resolver... in the browser. The rest of the operating system will keep using your existing DNS resolvers.
>
> You may need to do these steps even if you configured Secure DNS directly in your OS, as some browsers use DNS-over-HTTPS, which will disregard your OS DNS resolver.

# Quick Start (All)

Every modern browser *except Safari* supports DNS-over-HTTPS. Configuration is pretty similar in all of them.

1. Open browser **Settings** menu
2. Search for "DNS"
3. Open whichever menu is returned in your search
4. Select **Use Secure DNS** or **Enable DNS over HTTPS** and choose **Custom**
5. Paste your Device's unique DNS-over-HTTPS resolver into the box 

# Special Considerations

The above steps will work in every browser. Some browsers require additional steps, or have their own quirks, which are listed below. 

## Firefox

To find this setting on Firefox, under the "Enable DNS over HTTPS" section, choose "Max Protection" and then select "Custom" from the "Choose provider" dropdown.

## Edge

If you encounter the following error, temporarily disable the Default Rule -> Redirect (or remove redirection from the Google Service). This will make this error go away, and then you can change the settings back to what they were. 

![](https://files.readme.io/8b531d8-edge_error.JPG "edge_error.JPG")

This happens because when you enable DNS-over-HTTPS in MS Edge, it makes a request to google.com, which if spoofed, will be treated as a "failure condition" and show this incorrect error. 

## Chrome

You can view the [full tutorial on our blog](https://blog.controld.com/how-to-set-up-control-d-on-google-chrome/). 

## Brave

1. Open browser **Settings** menu.
2. Navigate to **Privacy and Security**.
3. Select **Security**.
4. Enable the **Use secure DNS** option.
5. Select **Add a custom DNS service** from the drop down menu.
6. Paste your Device's unique DNS-over-HTTPS resolver into the box.
