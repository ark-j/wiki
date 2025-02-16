---
hide:
    - navigation
    - toc
---

# mkdocs syntax guide

This page contains examples of how to proceed with notetaking and knowledge base with mkdocs syntax

## Admonitions
- adds different card laout for notes and warning etc
- this are proceed with `!!!` and space and then name of perticular thing
!!! note
!!! abstract
!!! info
!!! tip
!!! success
!!! question
!!! warning
!!! failure
!!! danger
!!! bug
!!! example
!!! quote
- if you want to name the field differently then do this
```md
!!! note  "custom name"
    this is custom note
```
!!! note "custom name"
    this is custom note
- remove the title
```md
!!! note  ""
    this is custom note
```
!!! note  ""
    this is custom note
- collapsible admonitions
```md
??? note

    Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla et euismod
    nulla. Curabitur feugiat, tortor non consequat finibus, justo purus auctor
    massa, nec semper lorem quam in massa.
```
??? note

    Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla et euismod
    nulla. Curabitur feugiat, tortor non consequat finibus, justo purus auctor
    massa, nec semper lorem quam in massa.

## Code Blocks
- sample code block
``` py
import tensorflow as tf
```
- code block with title
``` py title="bubble_sort.py"
def bubble_sort(items):
    for i in range(len(items)):
        for j in range(len(items) - 1 - i):
            if items[j] > items[j + 1]:
                items[j], items[j + 1] = items[j + 1], items[j]
```
- code block with line numbers
``` py linenums="1"
def bubble_sort(items):
    for i in range(len(items)):
        for j in range(len(items) - 1 - i):
            if items[j] > items[j + 1]:
                items[j], items[j + 1] = items[j + 1], items[j]
```
- code with line highlight
``` py linenums="1" hl_lines="2 3"
def bubble_sort(items):
    for i in range(len(items)):
        for j in range(len(items) - 1 - i):
            if items[j] > items[j + 1]:
                items[j], items[j + 1] = items[j + 1], items[j]
```

- emmbedding code from source file
```py linenums="1" title="example.py"
--8<-- "example.py"
```

- content tab
=== "C"

    ``` c
    #include <stdio.h>

    int main(void) {
      printf("Hello world!\n");
      return 0;
    }
    ```

=== "C++"

    ``` c++
    #include <iostream>

    int main(void) {
      std::cout << "Hello world!" << std::endl;
      return 0;
    }
    ```

## tables
| Method      | Description                          |
| ----------- | ------------------------------------ |
| `GET`       | :material-check:     Fetch resource  |
| `PUT`       | :material-check-all: Update resource |
| `DELETE`    | :material-close:     Delete resource |

## formatting
```title="text with highlight"
- ==This was marked==
- ^^This was inserted^^
- ~~This was deleted~~
```

- ==This was marked==
- ^^This was inserted^^
- ~~This was deleted~~

```title="Text with sub- and superscripts"
- H~2~O
- A^T^A
```

- H~2~O
- A^T^A

```title="Keyboard keys"
++ctrl+alt+del++
```
++ctrl+alt+del++

## adding animations
<div class="termy">

```console
$ ls -ltr /
drwxr-xr-x root root 4.0 KB Thu Jan  1 05:30:00 1970  boot
lrwxrwxrwx root root   7 B  Thu Nov 21 14:26:21 2024  sbin ⇒ usr/bin
drwxr-xr-x root root 4.0 KB Thu Nov 21 14:26:21 2024  mnt
lrwxrwxrwx root root   7 B  Thu Nov 21 14:26:21 2024  lib64 ⇒ usr/lib
lrwxrwxrwx root root   7 B  Thu Nov 21 14:26:21 2024  lib ⇒ usr/lib
lrwxrwxrwx root root   7 B  Thu Nov 21 14:26:21 2024  bin ⇒ usr/bin
drwx------ root root  16 KB Sun Dec 22 21:28:38 2024  lost+found
drwxr-xr-x root root 4.0 KB Sun Dec 22 21:30:07 2024  srv
drwxr-xr-x root root 4.0 KB Sun Dec 22 21:31:40 2024  home
drwxr-xr-x root root 4.0 KB Mon Dec 23 01:35:05 2024  opt
drwx------ root root 4.0 KB Mon Jan  6 01:28:23 2025 󰉐 root
drwxr-xr-x root root 4.0 KB Wed Jan 29 17:20:23 2025  usr
dr-xr-xr-x root root   0 B  Thu Jan 30 23:53:50 2025  sys
dr-xr-xr-x root root   0 B  Thu Jan 30 23:53:50 2025  proc
drwxr-xr-x root root 4.0 KB Thu Jan 30 23:53:57 2025  var
drwxr-xr-x root root 4.1 KB Thu Jan 30 23:53:57 2025  dev
drwxr-xr-x root root 4.0 KB Thu Jan 30 23:54:09 2025  etc
drwxr-xr-x root root 800 B  Thu Jan 30 23:55:34 2025  run
drwxrwxrwt root root 560 B  Fri Jan 31 00:31:09 2025  tmp
```

</div>
