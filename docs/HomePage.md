# HomePage

For full documentation visit [mkdocs.org](https://www.mkdocs.org).

## Commands

* `mkdocs new [dir-name]` - Create a new project.
* `mkdocs serve` - Start the live-reloading docs server.
* `mkdocs build` - Build the documentation site.
* `mkdocs -h` - Print help message and exit.

## Project layout

    mkdocs.yml    # The configuration file.
    docs/
        index.md  # The documentation homepage.
        ...       # Other markdown pages, images and other files.

## Code Annotation Examples

### Codeblocks

Some `code` goes here.

###Plain codeblock

A plain codeblock： 

```
Some code here
def my_func():
    # This is for test.
    print("Hello, Leo.")
```

#### Code for a specific language

Some more code with the `py` at the start:

```py
def my_func():
    # This is for test.
    print("Hello, Leo.")
```

With a title:

```py title="test.py"
import pandas as pd
def my_func():
    # This is for test.
    print("Hello, Leo.")
```

With a line number:

```py linenums="1" title="test.py"
import pandas as pd
def my_func():
    # This is for test.
    print("Hello, Leo.")
```

## Icons and Emojs

:smile:

:fontawesome-regular-face-laugh-wink:

:octicons-heart-fill-24:{ .heart }

For more details about emojs, visit <a \
href="https://squidfunk.github.io/mkdocs-material/reference/icons-emojis/#mkdocsyml_1" \
target="_blank" rel="noopener">the official document</a>.
