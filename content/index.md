
# Table of Contents

1.  [Introduction](#org2a695dc)
    1.  [Using this page.](#orge33e6e2)
    2.  [Essentials](#org591ecc3)
        1.  [Enable Melpa](#org226adc0)
        2.  [use-package](#org5d0edf6)
    3.  [Recent files](#orge96d4bf)
    4.  [Writing text](#org9f76e57)
        1.  [Focused writing](#org301fdff)
        2.  [Visual-line-mode](#org99285a1)
        3.  [Spell check](#org465710f)
    5.  [Org mode](#org19af6c5)
        1.  [Asthetics](#org1d51990)
        2.  [Org agenda](#orgd7af2dd)
        3.  [Knowledge mangmet](#orgb2715ca)
    6.  [snippet](#org44a7bbb)


<a id="org2a695dc"></a>

# Introduction

In late 2023 two things happened that made me push this project forward. One, I declared config bankruptcy and started to rewrite my config from scratch and, two, the guilt of renewing this domain for another year kicked in.

This site is a extension of a [paper written in 2022](https://www.ingentaconnect.com/content/matthey/jmtr/2022/00000066/00000002/art00002;jsessionid=85415haetimmp.x-ic-live-03) which I hope will work as a minimal viable config for people wanting to start out using this tool within their workflows.

I have since moved way from the bench and am no longer a reserch scientist. My work has moved into helping scientists with their work using digital tools. Emacs is one such tool.


<a id="orge33e6e2"></a>

## Using this page.

This page is a single hosted file. It is written in org. If you download the file and run \`M-x org-babel-tangle-file\` and point it to  \`init.el\`, that will create a config of just the parts needed by emacs. Put this in you  \`~./emacs.d\` file and you are good to go.

Raw files for both the org, and tangled .el file can be found in the assosisated GitHub repo. Let's get going!


<a id="org591ecc3"></a>

## Essentials

This section covers basic functionality needed for either admin, quality of life, or for other programs to work.


<a id="org226adc0"></a>

### Enable Melpa

[Melpa](https://melpa.org/#/) is *the* emacs package repository. Most, if not all, packages in this config are grabbed from there. The below code enables this.

    (require 'package)
    (add-to-list 'package-archives '("melpa" . "https://melpa.org/packages/") t)
    ;; Comment/uncomment this line to enable MELPA Stable if desired.  See `package-archive-priorities`
    ;; and `package-pinned-packages`. Most users will not need or want to do this.
    ;;(add-to-list 'package-archives '("melpa-stable" . "https://stable.melpa.org/packages/") t)
    (package-initialize)
    (package-refresh-contents)


<a id="org5d0edf6"></a>

### use-package

    
    
    (require 'use-package)

1.  enable evil mode

    [evil mode](https://github.com/emacs-evil/evil) a quaility of life feature, it gives you access to vi behaviours. some workflows are better with it.
    
        
        
        ;; Download Evil
        (unless (package-installed-p 'evil)
          (package-install 'evil))
        
        ;; Enable Evil
        (require 'evil)
        (evil-mode 1)
    
    1.  Auto complete in m-x
    
            
            
                (require 'ivy)
                (ivy-mode 1)
            
            
              (setq ivy-on-del-error-function #'ignore)
            
            
            
                (require 'smex)
            
            
            
              (require 'ido)
            (ido-mode 1)
            
            (setq ido-enable-flex-matching t)


<a id="orge96d4bf"></a>

## Recent files

    
    
    
    (recentf-mode 1)
    (setq recentf-max-menu-items 25)

1.  Aesthetics

    1.  Hide tool bar and menu
    
            
            
            (menu-bar-mode -1)
            (tool-bar-mode -1)
    
    2.  Themes
    
        This is super subjective so choose something that works for you, a non-exhaustive list can be found [here](https://emacsthemes.com/).
        
            
            
              (require 'kanagawa-theme)
            (load-theme 'kanagawa t)

2.  Misc.

        (setq use-short-answers t)


<a id="org9f76e57"></a>

## Writing text


<a id="org301fdff"></a>

### Focused writing

I am a big fan of writeroom-mode, which centers the text and makes the buffer full screen. Focus mode is also super neat, only showing colour formatting on the text block you are writing. Both can be enabled with \`M-x\`.

    
    (require 'focus)
    (require 'writeroom-mode)


<a id="org99285a1"></a>

### Visual-line-mode

It's word wrap, it's needed.

    
    (visual-line-mode 1)


<a id="org465710f"></a>

### Spell check

    
    (flyspell-mode t)


<a id="org19af6c5"></a>

## Org mode


<a id="org1d51990"></a>

### Asthetics

    (require 'org-modern-mode)
    (with-eval-after-load 'org (global-org-modern-mode))


<a id="orgd7af2dd"></a>

### Org agenda

    
    (setq org-agenda-files
        (directory-files-recursively "~/Dropbox/org" "\\.org$"))

1.  Key bindings

        
        (global-set-key (kbd "<f12>") 'org-agenda)


<a id="orgb2715ca"></a>

### Knowledge mangmet

1.  Org Roam

        
        
        (use-package org-roam
          :ensure t
          :custom
          (org-roam-directory (file-truename "~/Dropbox/OrgRoam/"))
          :bind (("C-c n l" . org-roam-buffer-toggle)
        	 ("C-c n f" . org-roam-node-find)
        	 ("C-c n g" . org-roam-graph)
        	 ("C-c n i" . org-roam-node-insert)
        	 ("C-c n c" . org-roam-capture)
        	 ;; Dailies
        	 ("C-c n j" . org-roam-dailies-capture-today))
          :config
          ;; If you're using a vertical completion framework, you might want a more informative completion interface
          (setq org-roam-node-display-template (concat "${title:*} " (propertize "${tags:10}" 'face 'org-tag)))
          (org-roam-db-autosync-mode)
          ;; If using org-roam-protocol
          (require 'org-roam-roam))

2.  Denote

        
        
        (require 'denote)
        (setq denote-directory "~/Dropbox/Denote/")


<a id="org44a7bbb"></a>

## snippet

$ cd ~/.emacs.d/plugins
$ git clone &#x2013;recursive <https://github.com/joaotavora/yasnippet>

    
    
    (add-to-list 'load-path
    	      "~/.emacs.d/plugins/yasnippet")
    (require 'yasnippet)
    (yas-global-mode 1)

