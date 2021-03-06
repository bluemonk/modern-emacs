Purpose of this document is to provide a reference for most of the
configuration changes that can improve the Emacs experience by making
the environment more aligned to modern alternatives. This goes from
simple look'n'feel changes to installing essential packages to basic
key rebinding.

The typical target would be a new user looking to improve the defaults
and get a fully functional Emacs environment without relying on the
otherwise excellent pre-packaged distributions like Prelude or
Smartemacs, but also seasoned users who might want a reference for new
installations.

The document is divided in sections that have little to none
dependency with each other, thus keeping the configuration modular and
allowing cherry picking of the interested features only. Accidentally,
the documents also provides some suggestions on the best choice
between two or more similar packages: this reflects the author's
preference and it's not necessarily the community consensus, although
a lot of efforts have been spent in the selection process.

# Configuration file

All the configuration snippets shown in this document should be written in the Emacs
initialization file. There are normally three choices:

* `~/.emacs` -> This is an hidden file (because it starts with a dot) in
the user's home directory (normally indicated by a ~). Best choice for
quick installations, but it rapidly becomes cluttered and difficult to
manage. Ideal choice for beginners.
* `~/.emacs.d/init.el` -> Keeping all the configuration inside the
hidden .emacs.d directory is generally considered the best practice.

Every time you change the configuration, you can either quit Emacs and
start again, or more efficiently issue the following command:

```
M-x eval-buffer
```

This will reload the configuration and you will see the effects
immediately.

# Add the Melpa package repository

Emacs 24.4 comes pre-configured to use the official Elpa
repository. Most developers use the Melpa archives, so chances are
that the latest packages are found there.

```elisp
;; Add the melpa package repository
;; Remember to always use HTTPS
;;
(require 'package) ;; You might already have this line
(add-to-list 'package-archives
             '("melpa" . "https://melpa.org/packages/"))
```

# Initialize the packages

Emacs initialize packages after loading the init file. This is
normally OK, but a few packages might require some configuration or
some settings after being loaded, and if we write that configuration
in the init file Emacs will generate an error.

Workarounds exists, but to make thing easy just write this on the very
top of your init file (to make sure it's loaded first):

```elist
;; Initialize packages
;;
(package-initialize)
```

# Remove ugly defaults

Emacs desktop version comes pre-configured with some defaults that
many deem quite ulgy. If you don't like them, you can get rid of
them with the following configuration:

### Remove the splash screen ###

```elisp
;; Remove the splash screen
;; 
(setq inhibit-splash-screen t)
```

### Remove the menu bar ###

```elisp
;; Remove the menu bar
;;
(customize-set-variable 'menu-bar-mode nil)
```
### Remove the tool bar ###

```elisp
;; Remove the tool bar
;;
(customize-set-variable 'tool-bar-mode nil)
```

### Remove scroll bar ###

```elisp
;; Remove the scroll bar
;;
(customize-set-variable 'scroll-bar-mode nil)
```

# Use a better theme

This is largely a matter of preference. Browse
[this gallery](https://emacsthemes.com/) and choose one that you like.
I like the zenburn theme; you can install it with the following command:

<kbd>M-x package-install [RET] zenburn-theme [RET]</kbd>

Then enable it in the init file:

```elisp
;; Load the zeburn theme
;;
(load-theme 'zenburn t)
```

# Better font

Also a matter of preference. You can checkout
[this great repository](https://github.com/hbin/top-programming-fonts)
for some excellent programming fonts.
I'm in love with the beautiful Menlo
font. Install it and then enable it:

```elisp
;; Use Menlo as default font
(set-default-font "Menlo 10")
```

You can adjust the font size by changing the number after the font
name.

# Hurt yourserf with guru mode

Bozhidar Batsov is one of the best emacs hackers out there. He's the author
of guru-mode, which aims to teach you the emacs-way by disabling navigation
keys like the arrow keys, page up and page down, and forcing you to use
C-n, C-p, C-f, C-b and so on. Annoying at first, it will quickly get under
your skin so that it will feels so wrong to move your hands from the keyboard
again. Highly recommended.

Install it

<kbd>M-x package-install [RET] guru-mode [RET]</kbd>

and enable it on programming modes using the following configuration

```elisp
;; Guru mode - hooked to prog modes
(add-hook 'prog-mode-hook 'guru-mode)
(add-hook 'html-mode-hook 'guru-mode)
```

Alternatively, you can just enable it globally:

```elisp
(guru-global-mode +1)
```




