---
title: "1,2,3... Everybody say Commit!"
image:
  path: /assets/images/posts/git-it-out-loud/hack-capital-git-logo-640x426.png
  thumbnail: /assets/images/posts/git-it-out-loud/hack-capital-git-logo-640x426.png
categories:
- Version control 
tags:
- Git 
- Github 
- basic
author: alfredo
---
Probably, I was not the only person in the world saving every little change I made to my code. Fear is one of the most common feelings in nature, it keeps you alert and alive, yet it can paralize yourself and stop you from creating marvelous things. Sometimes coding can be challenging. While you can spend two hours writing a few lines it can take less than a second to loose everything. All that hard work must be adequately stored and accessible and for that there must be an efficient way.

# So Version Control ha!

[Git](https://git-scm.com/about) is equal to freedom. Git is a Version Control system, this means that you don't have to give the same file three different bizarre names like: `perfect-file.txt, perfect-file-final.txt, perfect-file-the-one.txt`. So you can still have all the changes you wanted to test.  

You can access a specific version of the file or files you decided to track using Git. You can test new implementations to a project without loosing the actual functional version you previously created. Besides, if you integrate Git with its better half [Github](https://github.com/about), you will be able to share with the whole world your code, collaborate and back up your work. 


# How to start tracking my project 

After you [installed git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git) you just have to go to the main directoy of your project and use the command to **initialize** your repository (fancy name for the directory that git creates to function properly). 

```bash
# Create your project
mkdir project-to-track
# Go to your project
cd project-to-track
# Initialize tracking
git init 
```

Git will create for you a **branch** that will be named by default `master`. This will be your main line of work. In technical terms `master` will always point to the last snapshot you took (your last commit). 

# Taking photos of the current state of your project 

## `git add`

All that Git does to store the changes in your project is taking a snapshot whenever you tell so. Then, it saves that polaroid so you can access and recover that particular moment of your work with a unique ticket. This ticket is composed of 40 letters and digits. **Photo is called by Git a commit and of course you can write a quote in the back of that photo to remember why you decided to make that edit.** 

In order to take the snapshot (commit) you must first tell Git which of the files you want to **add** to that commit. You can do this basically in 3 ways. 

```bash
# This will add all modified files to the commit 
git add .
# This will add only the file you specified 
git add file1.txt 
# This will add all the files that you specified  
git add file1.txt file2.txt file3.txt
```

> If you want to see which files were modified and yet not added for creating a commit use `git status`. This will also tell you on which branch you are. 
```bash
git status 
```

## `git commit`

**1,2,3... Everybody say Commit!** Yes. Now it's time to capture the changes and remembrer it for a long time by also writing a message. 

```bash
# Tells git to create the structure to track your changes and write a message telling why you made this
git commit -m "Add my first commit"
```

> To see all the commits, the tickets, author, date and message just do `git log` 
```bash
git log
```

# By creating other branches you can experiment without messing with your main files 

You can create other pointers (branches) that will follow other paths of your project without loosing your main work that will be always secure and pointed by `master`. In this way, you can **create branches with the name you desire** and whenever those modifications are stable, you can incorporate (`merge`) them to your `master` branch.

```bash
# Create, name and select the new branch where you will experiment without altering your master branch 
git checkout -b branch-with-name-you-want
# Edit the file 
vi test.txt
# Add the file you modified while in non-master branch 
git add test.txt
# Create the structure to track your changes and write a message telling why you made this change 
git commit -m"50 or less character message, be short but accurate and focus on the why not the how"
# Return to you master branch 
git checkout master 
# Add the modifications to your master branch
git merge branch-with-name-you-want
# Delete branch to keep things clean
git branch -d branch-with-name-you-want
```

> You can create a larger commit by just writing `git commit`. This will oppen your default text editor which will probably be VIM and if you don't know how to exit. Don't worrry. I got your back with this [basic VIM tutorial](https://fikandata.github.io/data%20science/2021/03/13/vim-is-your-friend.html). 

## You are the photographer now!

Git is a tool widely used by developers because of it's power, ease of teamwork and open-source development. Keep practicing the workflow and commands will become second nature to you. It's worth it! 

### Extracting insights

Photo by <a href="https://unsplash.com/@hackcapital?utm_content=creditCopyText&utm_medium=referral&utm_source=unsplash">Hack Capital</a> on <a href="https://unsplash.com/photos/black-flat-screen-computer-monitors-uv5_bsypFUM?utm_content=creditCopyText&utm_medium=referral&utm_source=unsplash">Unsplash</a>
