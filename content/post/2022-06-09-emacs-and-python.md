---
title: "Emacs_and_python"
date: 2022-06-09T14:15:56+12:00
Description: ""
Tags: []
Categories: []
DisableComments: false
tags: ["emacs", "org-mode", "elisp", "productivity"]
---

Emacs and python itegration is always hard to me. Especially, when I used Anaconda, it's terrfible. - The Anaconda will ask you that your console (cmd.exe) cannot load python library. I tried several tricks but it doesn't work for me. 

So let's get simple - just install vanilla python and setup the system path in your Windows machine. We have alot of thing to do integrate with Emacs. 

Once you installed python well, then you need to determine a Emacs python-mode and IDE packages. https://www.emacswiki.org/emacs/PythonProgrammingInEmacs

I choosed a Jedi language server as language server protocol and installed Jedi.el with `M-x package-install RET jedi RET` and installed the jedi server as `M-x jedi:install-serve`. I faced some issues about python path setup. I need to check my path including all python core and packages.
- http://tkf.github.io/emacs-jedi/latest/

Next,install virtualenv and you need to update your init.el 

```
(add-hook 'python-mode-hook 'jedi:setup)
(setq jedi:complete-on-dot t) 
```

Now you can use popup-style help and auto-complete when you open python extention, 'py'.


