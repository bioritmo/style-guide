# General guidelines #

These general guidelines are advised regardless of the kind of source code you are working on - from Ruby to HTML and Objective-C source code or Markdown files, these basic practices should be followed. The best way to follow these guidelines is by configuring your editor to do all the hard work for you.

* Do not leave trailing whitespaces or line endings on your files:
    * On Vim you can add something like ```autocmd BufWritePre * :%s/\s\+$//e``` to your ```~/.vimrc```.
    * On Sublime Text you can just set the ```trim_trailing_white_space_on_save``` option to ```true```.
    * On TextMate, you can install the [uber-glory](https://github.com/glennr/uber-glory-tmbundle) bundle.

* Tab size and indentation: Use 2 spaces instead of hard tabs for indentation.
    * On Vim: edit your ```~/.vimrc``` and add ```set sw=2```, ```set sts=2```, ```set expandtab``` and ```set autoindent```.
    * On Sublime Text: edit user preferences (⌘ + ,) and set ```tab_size``` to ```2```, ```translate_tabs_to_spaces``` to ```true``` and ```use_tab_stops``` to ```true```.
    * On TextMate: everything is pretty much pre-configured with these good defaults (2 spaces, no tabs).

* Avoid the usage of very large lines, regardless of the line wrap that your editor does, to keep your code succinct and readable.
