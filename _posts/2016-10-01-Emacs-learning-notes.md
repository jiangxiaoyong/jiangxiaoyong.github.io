---
title: "Emacs learning notes"
excerpt: "Emacs config and leaning notes"
tags: 
  - Emacs
  - Clojure 
---

Here are the notes for Emacs editor

### Emacs key bindings for File/buffer/window commands 

```
C-x C-f     Find file or create new file
C-x C-s     Save buffer
C-x s       Save file (like save-as)
C-x b       Switch buffer
C-x k       Kill buffer
C-x o       Switch cursor to another window
C-x 1       Delete other windows
C-x 0       Delete current window
C-x 2       Split window horizontally
C-x 3       Split window vertically
```

### Emacs key bindings for Movement commands

```
C-a         Beginning of line
C-e         End of line
ESC-<       go to the beginning of the file
ESC->       go to the end of the file
M-m         Move to first non-whitespace character on the line
M-a         Move to beginning of function
C-n         Next line (down)
C-p         Previous line (up)
C-b         Back (left) one character
C-f         Forward (right) one character
M-f         Forward a word
M-b         Back a word
C-v         Forward a page
M-v         Back a page
C-s         Regex search forwards for text in current buffer and move to it. Press C-s again to move to next match
C-r         Regex search backwards
M-g g       Go to line
```

### Emacs key bindings for Edit commands

```
C-d         Kill character
C-k         kill line
M-d         Kill word forwards
M-delete    Kill word backwards
C-w         Kill region
M-w         Copy region to kill ring
M-y         Cycle through kill ring after yanking
C-y         Yank (paste)
```

### Emacs key bindings for Misc commands

```
M-x fn-name run commands by name
M-x package-refresh-contents  to get the latest list
M-x package-list-packages     to show package
M-x package-install           to install package
M-%         Query replace
C-spc       select region
M-x replace-string to replace string
```

### Clojure Buffer Key Bindings

```
C-c M-n       Switch to namespace of current buffer
C-c C-k       Compile current buffer
M-. and M-,   Navigate to source code for symbol under point and return to your original buffer
C-↑, C-↓      Cycle through REPL history
C-x C-e       sends the s-exp to the running REPLm, Evaluate expression immediately preceding point 
q             close stack trace
C-c M-o       clear REPL
```

### Paredit
```
M-(   parenthesis-wrap-round
C-→   To slurp, move closing parenthesis to the right to include next expression
C-←   to Barf, move closing parenthesis to the left to exclude last expression
C-M-f, C-M-b Move to the opening/closing parenthesis
C-(   move backward opening parenthesis
C-{   move forward opening parenthesis
C-)   move backward closing parenthesis
C-}   move forward closing parenthesis
```