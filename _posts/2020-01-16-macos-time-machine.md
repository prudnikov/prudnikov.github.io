---
layout: page
title: Mastering Time Machine Bakups
description: Tips and Tricks on mastering macOS Time Machine backup
excerpt: Tips and Tricks on mastering macOS Time Machine backup. Decrease time machine backup size. Speeding up backup. Using time machine without external drive.
keywords: macos, time machine, tips&tricks
date:   2020-01-16 15:16
comments: true
tags:
- macos
homepage: false
permalink: /macos-time-machine
links:
- https://www.howtogeek.com/294600/save-space-on-your-time-machine-drive-by-excluding-these-folders-from-backups/
---

## Exclude unnecessary files
Time Machine excludes a lot of files and directories you don't need to be backed up by default. There is a file that contains all those locations:

```
/System/Library/CoreServices/backupd.bundle/Contents/Resources/StdExclusions.plist
```

Individual programs can also mark particular files to not be backed up. Typically, this includes caches and other temporary files. You can find a list of these exempt files by running the following command in the Terminal:

```sudo mdfind "com_apple_backup_excludeItem = 'com.apple.backupd'"```

However, you always have things that change frequently on your drive that you don't need to backup. Here is my list of exclusions. 

## What to exclude from backup?
* ~./npm
* ~/Downloads
* ~/Temp
* ~/Dropbox

