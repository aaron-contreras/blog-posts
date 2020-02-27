# To, and From vscode

Code editors are the tools of the developer. One can use a plain-text editor to write code but it lacks a lot of the nice featuers of a modern code editor; syntax highlighting, realtime linting, and auto-complete, to name a few. Modern code editors are important to a new developer as well, they can make errors easier to spot, help enforce good spacing (or tabbing, if you're into that), and make it easy to edit and write code.

## Code editors vs IDEs

An IDE (or Integrated Development Environment) allows one to *integrate* with their development environment. The IDE can show you the code where your test failed, or can compile your code for you at the click of a button instead of typing a command. Code editors are simply a nice place for you to write code and, well, edit it. Some code editors do blur the lines between editor and IDEs, and we will talk about them later. IDEs usually do come with a lot more overhead; they can have a lot more menus and commands you may have to learn and they usually take up more computing power as well. A code editor is streamlined to edit text and usually does not take a lot of computing power to run. (this can change in large files though, but an IDE will suffer from the same limitations). 

## IDEs

I won't be spending too much time on IDEs but I would like to talk about them a bit. IDEs are usually used in specific language environments. Microsoft's Visual Studio is an example of such, it is used in Windows environments to program in C type languages. Another example is Eclipse, which is an IDE for Java. 

## Types of code editors

I put code editors in two categories. Basic, and Advanced. They are not categoried by their needed level of compitence, but by their feature set. A basic code editor does not have much in the way of customization, or plugins, where an advanced one will. Basic code editors don't do a lot to help you write code, but leave you to find the mistakes the old-fashioned way. An advanced code editor can help you with linting, syntax, spacing and more. These categories do not have solid boundaries, and there is some overlap as well.

### Basic Code Editors

This is not an all inclusive list, but some common ones i've run into. 

#### nano

Nano comes with a lot of linux distrubutions, and is the go-to basic code editor for quick changes in config files to people new to linux. It has some nice features, such as syntax-highliting, but lacks auto-complete and some other nice features. It is very good at being quick, and easy to use. I would only reccomend this to people writing small scripts, or editing configuration files.

#### notepad

Notepad ships with windows, it is a very, very basic editor without syntax highlighting or auto-complete. It does nothing for you except show you the plain-text. Only use this when you do not have another text-editor available.

#### gedit

This is one of those text-editors that blur the lines between basic and advanced. I place it under basic becuause of it's limited plugins and popularity. It is a nice editor with syntax-highlighting, plugins, auto-tabbing/spacing, bracket-matching, and more. This editor is super lightweight and easy to use. This is a good code-editor for someone writing/editing scripts but doesn't need to add language specific features. This would be handy for system administrators. It also has a GUI, so it works well for people that want to use the mouse.

#### vi

The bane of all sys-admins and developers everywhere, nobody knows how to close it, let alone use it (you close it by pressing `ESC, :q!, ENTER`, by the way). This is another editor that blurs the lines between basic and advanced. Vi comes with every linux environment so is very useful on streamlined linux servers and remote operations where nano is not available. This editor is not intuitive and beginner friendly, but has some very nice features. Once one understands how to use it, one can edit a document very quickly and can move around the code very effeciently. Watching a master run vi, is nothing short of amazing. That being said, I wouldn't reccomend this to developers. There is a better alternative, vim, which I talk about below.

### Advanced Code Editors

Again, this is not an all inclusive list, but some that I have used or have been exposed to.

#### vim

Vim is very simillar to vi in many ways, but vim allows plugins. There is a substantial vim community and people have been writing plugins for a while. Vim has everything one would need. Syntax highlighting, it's very fast, bracket-matching, and more. Vim is very good at staying out of the developers way and allowing the dev to rapidly traverse the document. At it's core, it tries to keep you from removing your hands off the home row, it is a favorite of keyboard warriors. You can try vim by typing `vimtutor`, it walks you through the basic usage. Give it a shot, you might find you really like the keyboard commands.

#### Sublime Text

This is the first editor in the list that anybody could use right off the hop. It works very closely to any standard word processor without the overhead. Sublime seems to be somewhat popular. And it does have some nice features. The biggest drawback to this editor is it's cost. It's the only editor that is not free to use in this list. For that reason, I would suggest an alternative.

#### Atom

Written by the github team, Atom is an editor with a lot of plugins and addons. Some people that have used it say it feels 'heavy', but it's intellisense is very good.

#### vscode

This editor was written by Microsoft, but is totally free and open source. It has an integrated addon library where you can download addons that other people have written. It is very customizeable and fast. This editor is great for a developer that does not need/want an IDE and is the editor I have the most time with to-date. This editor is good for anyone. It's git-integration is very good and makes git a breeze to use, even for people new to version control. For these reasons, I reccomend vscode to pretty much everyone but the people that want to keep their hands on the home-row.

#### emacs/spacemacs

A very old editor that has stood the test of time. Emacs is an editor that has it all. Addons, keyboard control, the ability to click with the mouse, endless configuration, speed, etc. This is the editor I currently use. This editor was created to solve the problems developers had with code editors, and it solves it well. It has shortcuts for almost anything you'd want to do, and if it doesn't you can add your own. Configuration can be a bit confusing at first, as it uses a special programming language called *lisp* to configure. Emacs doesn't just attempt to be a code-editor, but is the closest to an IDE one can get without it being specifically an IDE. Emacs allows you to do almost anything you'd want without leaving the editor. Using spacemacs (a pre-configured emacs) with evil-mode is a great way to get started. I reccomend this to people who want more out of their editor and find themselves getting annoyed by reaching for the mouse.

## My Experience

When I started learning web-development, I started with sublime for a bit, when I found it was not free, I moved to atom for a short time. After spending a week or two with it I moved to vscode after a suggestion from a gitter chat-room. Vscode was my favorite editor for a long time and I would suggest it to anyone. It was very easy to use, and has a lot of neat features, but spending some time with it showed me it's flaws. Even with a decent computer, I ran into some peformance issues with larget projects, path completion was worthless in react development due to the time it took to regester. Some stuff got in the way, like the intellisense popups designed to help you code, but they would cover parts of the text you may have been looking at requiring you to press `ESC` or click close with your mouse. Eventually I disabled it. I noticed some people talking about emacs in the same gitter chatroom and decided to give it a shot. I started using `vimtutor` to get comfortable with the evil-mode bindings and found it very easy to move about a document. After a week, I uninstalled vscode to force myself to use only spacemacs. It took me about a week to get used to the different workflow, but I find it nice that the editor stays out of your way for the most part. It can be confusing to add packages/addons at first, but they seem to just work.

emacs with evil-mode will probably be the editor I stick with for a long time. I am by no means an expert with it and I learn new ways to do stuff every day. It's worth giving a shot for a while, there's a good chance you may never look back.
