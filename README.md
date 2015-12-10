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
(add-to-list 'package-archives
             '("melpa", "http://melpa.org/packages/") t)
```

# Initialize the packages

Emacs initialize packages after loading the init file. This is
normally OK, but a few packages might require some configuration or
some settings after being loaded, and if we write that configuration
in the init file Emacs will generate an error.

Workarounds exists, but to make thing easy just write this on the very
top of your init file (to make sure it's loaded first):

```elist
(package-initialize)
```

# Remove ugly defaults

Emacs desktop version comes pre-configured with some defaults that
many deem quite ulgy. Let's get rid of them:

## Remove splash screen

```elisp
(setq inhibit-splash-screen t)
```

## Remove menu bar

(customize-set-variable 'menu-bar-mode nil)

### Remove tool bar

(customize-set-variable 'tool-bar-mode nil)

## Remove scroll bar

(customize-set-variable 'scroll-bar-mode nil)

# Use a better theme

This is largely a matter of preference. I like the zenburn theme, to
install it like this:

```
M-x package-install zenburn
```

Then enable it in the init file:

```elisp
(load-theme 'zenburn t)
```

# Better font

Also a matter of preference. I'm in love with the beautiful Menlo
font. Install it and then enable it:

```elisp
(set-default-font "Menlo 10")
```

You can adjust the font size by changing the number after the font
name.


