---
layout: post
title: Most Useful Mac Terminal Knowledge
excerpt: "A personal mac terminal cheatsheet"
categories: Mac Terminal
comments: true
---

## Keyboard Shortcuts

I use mac terminal almost daily, but for some reason, these keyboard shortcuts had evaded me
all these years...

- Go to beginning of a line: ``` cmd + a ```
- Go to end of a line: ``` cmd + e ```
- Move left word-by-word: ``` alt + <- ```
- Move right word-by-word: ``` alt + -> ```

## Useful Unix Commands

1. Change ownership of a directory:
```
sudo chown -Rv <owner> <directory>
```
2. Make soft link
```
cd <where you want to create the link>
ln -s <file installed location> <name of the link>
```

3. Edit $Path variable
```
 PATH=$PATH\:/dir/path ; export PATH
```

4. Look for the port that is in use
```
lsof -i :<port number>
```

5. Running a background server processing
```
sudo node app.js >> ~/node.log &
```

## Terminal Style

After using my personal terminal style for so long, it has become a necessity.
To be filled in later...

1. color scheme + window transparency
2. prompt format
3. directory highlight
4. fortune + cowsay
5. shortcuts + aliases
