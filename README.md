# asciidoctor-chunker

Splits asciidoc book's single HTML file generated by Asciidoctor into chunks by chapters.

## News

- 2018/7/11  Locally linked files with `link` and `script` tags with relative paths are copied to the destination directory keeping the structure of the relative path.  So the custom CSS and script files should be properly copied by `asciidoctor-chunker`.

## What it Dose

Asciidoctor-Chunker generates chunked HTML from a single HTML generated by Asciidoctor.

1. Splits part preambles and chapters into separate files.
1. Places footnotes into the file where they are defined.
1. Re-writes the relative links to point the chunked files.
1. Copies the local images and linked files (with `link` and `script` tags) whose path is relative, to the directory relative to the chunked html output.  Files are only copied if they are new or modified.

Asciidoctor-Chunker does not add any contents nor change the structure of the source HTML.

Here is [the sample output](http://www.seinan-gu.ac.jp/~shito/asciidoctor/html_chunk/index.html) created from the [Asciidoctor User Manual](https://asciidoctor.org/docs/user-manual/).  The footer on the sample page is added by setting the asciidoctor attribute and is not added by asciidoctor-chunker.


## How to Install

Asciidoctor-Chunker is written in Common Lisp.  The easiest way to install Lisp environment is to use [Roswell](https://github.com/roswell/roswell).

1. Follow [the instruction here](https://github.com/roswell/roswell/wiki/Installation) to install Roswell.
1. Invoke `ros setup` after installation.  This will install Lisp compiler automatically and sets things up.
1. Install the dependent packages as follows.
    ```
    $ ros install alexandria
    $ ros install lquery
    $ ros install cl-fad
    ```
1. Place `asciidoctor-chunker` folder under `~/common-lisp` directory.
1. Run the script `~/common-lisp/asciidoctor-chunker/roswell/asciidoctor-chunker.ros` as follows.
    ```
    $ asciidoctor-chunker.ros [single-html-file] -o [output-directory]
    ```

`[single-html-file]` is the single HTML file generated by [Asciidoctor](https://asciidoctor.org) from the book doctype.  If the output directory is not specified, the default is `output` under the current directory.

## Example

The project contains the `test` directory where you can generate the chunked html for the [Asciidoctor User Manual](https://asciidoctor.org/docs/user-manual/) by invoking `make`.  Simply go into the `test` directory and invoke `make`.  This will clone the asciidoctor project from the github for the first time, then the chunked html will be generated under `test/output-chunk/html_chunk/` directory.  The `index.html` is the first page.

```
$ cd test
$ make
```
