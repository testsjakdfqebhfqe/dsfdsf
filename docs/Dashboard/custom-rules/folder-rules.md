---
title: Folders
excerpt: Group your rules into folders, and assign actions to them.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
  pages:
    - type: basic
      slug: magic-folders
      title: Magic Folders
---
Folders give you a way to organize your Custom Rules and can be used for multiple use cases. 

# Use Cases

## Structure

The simplest use case is to organize your Custom Rules into logical categories, so you can keep track of them all in one place. A normal folder can contain a mix of Custom Rules of all action types. 

## Action Folders

A folder can be optionally assigned an action, meaning any domain that exist in this folder will inherit the action type of the folder. With this, you can make your own "Allow" and "Deny" folders, or get more creative. For example, create a Redirect folder that spoofs to Brussles proxies. Any domain you add to it, will be automatically spoofed via proxies in Brussels. 

![](https://files.readme.io/a527cf5741ffc5e33fbbc57696325ccfa64f3306a119d3eb8573369c0c2ad528-image.png)

## Sharing

A folder can be exported as a json file. This file can be modified, or shared, and then re-imported back into another Profile. 

![](https://files.readme.io/eadeaae817594a5ab931cfee2a9600cc3f7ba1500f8656638878d361e43af7e6-image.png)

To import a folder, select Upload Folder from the **...** menu in the root Rules area (not inside a folder).

![](https://files.readme.io/8ba93f37291c47cc23529d72a7673ebd600d37ea89ddf90ed2fa5c943b67a2ac-image.png)

<br />

# Magic Folders

There are special folders that you can create that allow you to enforce advanced behaviors. See [Magic Folders](doc:magic-folders)
