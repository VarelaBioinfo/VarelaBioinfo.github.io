---
title: "VIM is your friend, you just need to get to know him."
categories:
    - Post Formats
tags:
    - Post Formats
    - readability
    - standard
---
![vim is your friend](/assets/images/vim-is-your-close-friend.png)

So there I was, with a completely black screen on my terminal trying to type something but every key I pressed was only making everything worse. Never have I thought typing a letter would be such a pain. 
Suddenly, my technique on typing every letter in my keyboard was rewarded with an `f` . "So my keyboard was not borken", I thought.

After typing my example.txt and ignoring why VIM did everything but following my orders, I was ready to save my file and exit this nightmare. Surprise baby! theres is not an easy way out `"type :quit<Enter> to quit VIM"`. 

## The beauty of VIM is not in the asthetics

VIM stands for Vi IMproved. Vi was an early attempt to a visual text editor. Vi stands for Visual. [Differences between Vi and Vim](https://www.shell-tips.com/linux/vi-vs-vim/). When you type the comand `vi file_name.txt` you will start the vim command and open the text editor. Until here VIM doesn't look anything like a visual text editor. But don't be confused. The beauty of VIM is not in the asthetics but in its powerful command combinations that let you navigate and edit text files in a
matter of seconds or better yet in a few keystrockes. As a highly valuable tool for developers, VIM style text editing shortcuts can be implemented in almost every systems as plugin, extension or package. [Vimium, a google chrome plugin](https://chrome.google.com/webstore/detail/vimium/dbepggeogbaibhgnhhndojpepiihcmeb), [jupyterlab VIM extension](https://pypi.org/project/jupyterlab-vim/), [Vintage mode for Sublime Text](https://www.sublimetext.com/docs/3/vintage.html), [VIM mode in
Rstudio](https://blog.rstudio.com/2015/02/23/rstudio-0-99-preview-vim-mode-improvements/). You can even have [Vim mode in your command line](https://blog.sanctum.geek.nz/vi-mode-in-bash/).  If you learn VIM you will be able to smoothly edit, write, and move around without touching the mouse or the arrow keys. **You' ll become lightning fast!**


## Learning VIM is like learning a new language 

VIM can be challenging at first because you don't know in which mode of the program you are on. There are 3 main modes. **Normal mode**, **Insert mode** and **Visual mode**.  Once you know this everything begins to make sense because evey mode is intended for one task.

### Normal mode 

Normal mode is the default mode you enter every time you run `vi textfile.txt`. This mode is intended to move around the text but not for editing the text.  It is just lets say the navigation mode. 
In normal mode you can move your cursor in multiple directions in order to get to the word you want to edit. 

```
# Pressing the key:
k moves your cursor one line up 
j moves your cursor one line down 
l moves your cursor one character right 
h moves your cursor one character left
```

So if you have this text and you are on normal mode

```
I want to move
freely in vim 
```
and you want to move from the `I` to the end of `freely`  you need to press one time `j` so you can go to the line below and then press 6 times `l` key to move six times to the right. 

This can seem a little bit slow at the begining but trust the process and bulid some muscle memory upon moving yourself around. 

**With the purpose of not making you fell asleep while you are trying to get to your desired word here are two easy moves you can apply on normal mode.** 

```
# Pressing the key:
0 (zero) moves your cursor to the beggining of the line
$ (shift + number key with the $) moves your cursor to the end of the line 
```
In the example above by pressing `$` you will move directly to the end of `move` in just one key press. 


## Insert mode 

So enough with moving around. I want to start writing please! Sure, as easy as pressing `i` key which stands for insert, as in insert mode. Isn't this easy? Now you are **starting to speak VIM!** By pressing `i` key you tell VIM you want to enter insert mode and VIM shows you the mode you are on at the bottom of the screen.
![VIM shows you the mode](/assets/images/vim-shows-the-mode.png)


So let all your inspiration flow and write that amazing piece of code, a productive commit on git or a beautiful Markdown file. You are free to erase as you normally do and when you need to return to navigation mode just press the `espcape key`. 
Normal mode as opposed to insert mode shows nothing in the bottom bar. Seeing nothing here is like seeing -- NAVIGATION--. **Now you know**. 


## Visual mode 

Maybe this mode is a litte more advanced but it is important to know its functionality. You will mainly use it for text selection, copy and paste.  As you imagine you **enter this mode** by pressing `v` while you are on normal mode. Here you will notice a selection starts to cover your text if you move to any direction as you do with the Normal mode commands `(j,k,l,h)`. 

```
# Pressing the key:
y (as for yank, to pull wiht a jerk) will copy the selected text 
x (imagine open scissors will cut the selected text
p (as for paste) will paste the previously cutted or yanked text 
```
![VIM visual mode](/assets/images/vim-visual-mode.png)

## How to save your work 

Finished your creation and want to save or just exit. Go to the normal mode with `escape` key. Now type `:` colon (which is the way to tell VIM I want to write a command)  and write the action you want to execute followed by `enter`. 

**Tip**: If you are writing huge documents save often otherwise you'll need to recover your file using vim [recovery mode](https://vim.fandom.com/wiki/Recovering_files).  

```
# Typing
:w just save the changes you have done 
:wq save the changes and quit 
:q exit vim 
:q! just to quit without saving any changes 
:x save the changes and exits vim 
```



## Now you are ready to start controlling VIM 

Do not feel overwhelmed with the robustness of this text editor. Practice makes perfect! Soon you'll realise you are ready for more challenging moves and actions. **Complexity builds upon this moves you now know.**  



### **Enjoy your FIKA!**





