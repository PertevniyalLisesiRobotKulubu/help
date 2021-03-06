Never compile this.

```emacs-lisp
;; -*- no-byte-compile: t; -*-
```


# Org2blog

    ID: org_gcr_2017-05-12_mara:B6246A7A-5514-4478-BC3D-7768B05B08B8

```emacs-lisp
;; -*- no-byte-compile: t; -*-
```

Sysop is likely to use this periodically.

Start EMACS with this command:

    emacs --debug-init --no-init-file --no-splash --background-color white --foreground-color black --vertical-scroll-bars --eval '(switch-to-buffer "*Messages*")' --name O2B-TEST --title O2B-TEST --load ~/src/help/.org-mode-contribute.emacs.el

```emacs-lisp
(load-file "~/src/help/.org-mode-package-management.emacs.el")
```


# Org2blog

    ID: org_gcr_2017-05-12_mara:B6246A7A-5514-4478-BC3D-7768B05B08B8

Configure Org2blog for use, development, and support.

> An elisp implementation of clientside XML-RPC

```emacs-lisp
(add-to-list 'load-path "~/src/xml-rpc-el")
(require 'xml-rpc)

```

> Weblog maintenance via XML-RPC APIs

```emacs-lisp
(add-to-list 'load-path "~/src/metaweblog")
(require 'metaweblog)
```

> Blog from Org mode to wordpress

```emacs-lisp
(add-to-list 'load-path "~/src/org2blog")
(require 'org2blog)
(add-hook 'org-mode-hook #'org2blog/wp-org-mode-hook-fn)
```

Org2Blog depends on Org-Mode. This system loads Org-Mode from Git. Enter the `ELPA` cache directory and delete it.

This system works with WisdomAndWonder. It keeps its posts separate giving focus to each Web.

```emacs-lisp
(setq org2blog/wp-track-posts nil)
```

Configure Org2Blog.

```emacs-lisp
(setq org2blog/wp-blog-alist
      '(("wisdomandwonder"
         :url "https://www.wisdomandwonder.com/xmlrpc.php"
         :username "admin"
         :default-categories ("Article" "Link")
         :confirm t
         :show 'show)))
```


# Pretty Mode

    ID: org_gcr_2017-05-15_mara:CB452410-955E-4A91-A811-10755A35A142

Visualize ASCII values as their most likely Unicode representation.

```emacs-lisp
(add-to-list 'load-path "~/src/pretty-mode")
(require 'pretty-mode)
(global-pretty-mode t)
```
