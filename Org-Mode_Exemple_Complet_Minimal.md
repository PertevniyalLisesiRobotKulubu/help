Never compile this.

```emacs-lisp
;; -*- no-byte-compile: t; -*-
```


# Org-Mode Exemple Complet Minimal

    ID: org_gcr_2017-05-12_mara:1035FF79-3703-49A6-8522-618B38A48F6C

Configure EMACS to easily provide ECMs.

Sysop is likely to use this often.

Start EMACS with this command:

    emacs --debug-init --no-init-file --no-splash --background-color white --foreground-color black  --vertical-scroll-bars --eval '(switch-to-buffer "*Messages*")' --name ECM-TEST --title ECM-TEST --load ~/src/help/.org-mode-ecm.emacs.el &


## Principle of Least Astonishment (POLA)

    ID: org_gcr_2017-05-12_mara:626B5DD1-97D8-4B85-96BC-B9A96F18AF1E


### Load Behavior

    ID: org_gcr_2017-05-12_mara:75985F03-F3B9-4DA3-8F6E-393E4C2F06E7

EMACS can load 3 different representations of a Emacs-Lisp source file code OOTB. The name of source code file is the value before the file extension. When you pass `load` a name it searches for an acceptable representation. Representation types are indicated by their extension name. `.el` is a human readable and uncompiled. `.elc` is not human readable and compiled. `.gz` is Gzip compressed and contains `.el` or `.elc` files.

The variable `load-suffixes` determines the order for which text and byte-code representations are first searched by extension-name. The variable `load-file-rep-suffixes` determines the order for all other extension types.

OOTB, EMACS combines the productivity of REPL style of development with the speed of compiled code by `load`&rsquo;ing byte-code first, text second, and compressed third. This workflow gives you the fastest code at run-time and lets you experiment with new features stored in text. When you are ready to use them every time, you compile them. There is only one downside of this approach: when you forget that it works this way it can be confusing.

When you forget about that style of system you end up with surprising behavior. The surprise comes when you forget to compile code and then write new code that depends on the now old version of that code. After the next build, your system can break in surprising ways. This violates the Principle of Least Astonishment.

This system values predictability so it does the simplest thing possible: `load` searches for the newest representation of a file and uses that one. It assumes that Sysop has total and complete control over the management of file representations.

This is the **first** thing that *ought* to happen in the initialization of **any** tangled system.

```emacs-lisp
(setq load-prefer-newer t)
```


## Org-Mode Exemple Complet Minimal

    ID: org_gcr_2017-05-12_mara:572E2309-5DCA-4AE1-AAC4-36B7E07AD46D

Every new EMACS releases comes with the latest stable Org-Mode release. To get hot-fixes, cutting edge features, and easy patch creation though, you need to use the version from Git.

These detailed and clear [directions](http://orgmode.org/manual/Installation.html) explain how ot run Org-Mode from Git. The only thing worth mentioning again is that in order to use **any** version of Org-Mode other than the one that comes OOTB you **must** load Org-Mode **before** anything else in your initialization file. It is easy to do! When you get unexpected Org-Mode behavior be sure to stop and investigate `org-version` and decide whether or not it is what you expect and prepare an ECM if necessary.

Add the Org-Mode core distribution the load path.

```emacs-lisp
(add-to-list 'load-path "~/src/org-mode/lisp")
```

Add the Org-Mode-Contributions distribution to the load path. The contributions are essential.

```emacs-lisp
(add-to-list 'load-path "~/src/org-mode/contrib/lisp")
```

Allow single-character alphabetical bullet lists. This configuration must occur before loading Org-Mode. **Never** remove this from a submitted ECM.

```emacs-lisp
(setq org-list-allow-alphabetical t)
```

Unchecked boxes prevent marking the parent as done. This configuration must occur before loading Org-Mode. **Never** remove this from a submitted ECM.

```emacs-lisp
(setq org-enforce-todo-checkbox-dependencies t)
```

Found a copy <span class="underline">Literate Programming</span> so use `GUILLEMET` delimeters.

```emacs-lisp
(setq org-babel-noweb-wrap-start "«")
(setq org-babel-noweb-wrap-end "»")
```

Load Org-Mode.

```emacs-lisp
(require 'org)
```

Display system info.

```emacs-lisp
(message "ECM Information As Of: %s\nOrg-Version: %s\nOrg-Git-Version:
         %s\nEmacs-Version: %s\nNoweb wrap start and stop delimeters: '%s' and '%s'\nnorg-babel-default-header-args:\n"
         (let* ((timestamp (format-time-string "%Y-%m-%dT%T"))
                (safe (replace-regexp-in-string ":" "-" timestamp)))
           safe)
         (org-version)
         (org-git-version)
         (emacs-version)
         org-babel-noweb-wrap-start
         org-babel-noweb-wrap-end)
(princ org-babel-default-header-args)
```
