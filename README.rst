==================
jtratner's dotvim
==================

These are my dotvim files. I separated them out from `my dotfiles`_ because I
wanted to be able to offer them individually (and, more specifically, to share
them with my *Machine Learning* class on Coursera :) ). Octave is baked right
in. It defaults to using Matlab for syntax highlighting, but you can look
below for instructions on how to set the default to Octave. If you need help
or want to get in touch with me, you can `email me`_.

.. _my dotfiles : https://github.com/jtratner/dotfiles
.. _email me : mailto:dotvim@jeffreytratner.com

Using these vim files
=====================

Super-quick Install
-------------------

Get a working set of files by entering the following on a command line.

::

    git clone https://github.com/jtratner/dotfiles.git dotvim
    cd dotvim
    ./install.sh

(note: install.sh will back up your files and update submodules automatically)

Installing on Windows
---------------------

If you are using Windows, you can use the vim files by copying into your home
folder (where ``$HOME`` is your directory, where you have folders for My
Documents, etc). You can get my either via git clone or by downloading them as
a zip file on github.

* ``vimrc.symlink`` should be copied to ``$HOME/_vimrc`` (note the '_' !)
* ``vim.symlink`` should be copied to ``$HOME/vimfiles``

Getting fonts for Powerline
---------------------------

You can get patched fonts to use with Powerline online, for example, you can
get them `in the fonts folder of my dotfiles`_

.. _in the fonts folder of my dotfiles : https://github.com/jtratner/dotfiles/tree/master/fonts/fonts.symlink/ubuntu-mono-powerline


.. contents:: What's In This Readme
    :depth: 2



Learning vim
============

The most important commands
---------------------------

.. todo: fix up this table so it wraps, etc

The basics: you open your file, type ``i`` to start editing, and then
``<Esc>`` to type commands, followed by ``i`` again to go back to editing.
Vim does take some time to learn, but once you do, you will be *way* more
productive.

+--------------+---------------------------------------------------------------------------------------------------------------------------+
| Command      | What it does                                                                                                              |
+--------------+---------------------------------------------------------------------------------------------------------------------------+
| ``i``        | lets you edit the file (starts "insert mode") -- **Use <Esc>** to exit insert mode and be able to type the other commands |
+--------------+---------------------------------------------------------------------------------------------------------------------------+
| ``<Esc>``    | exits insert mode                                                                                                         |
+--------------+---------------------------------------------------------------------------------------------------------------------------+
| ``u``        | undos the last change                                                                                                     |
+--------------+---------------------------------------------------------------------------------------------------------------------------+
| ``:``        | puts you in command line mode (so you can do commands                                                                     |
+--------------+---------------------------------------------------------------------------------------------------------------------------+
| ``:w[rite]`` | save your file                                                                                                            |
+--------------+---------------------------------------------------------------------------------------------------------------------------+
| ``:q[uit]``  | quit vim                                                                                                                  |
+--------------+---------------------------------------------------------------------------------------------------------------------------+
| ``:wq``      | save current buffer and quit                                                                                              |
+--------------+---------------------------------------------------------------------------------------------------------------------------+
| ``y[ank]``   | with a motion (``:help motion``), copies the text under cursor                                                            |
+--------------+---------------------------------------------------------------------------------------------------------------------------+
| ``p[aste]``  | pastes yanked text                                                                                                        |
+--------------+---------------------------------------------------------------------------------------------------------------------------+
| ``dd``       | deletes and yanks current line                                                                                            |
+--------------+---------------------------------------------------------------------------------------------------------------------------+
| ``x``        | deletes a single character                                                                                                |
+--------------+---------------------------------------------------------------------------------------------------------------------------+
| ``h,j,k,l``  | move around the page (see main ``:help`` for more)                                                                        |
+--------------+---------------------------------------------------------------------------------------------------------------------------+
| ``v``        | lets you select text (use ``<Esc>`` or ``:`` to get out of selection mode)                                                |
+--------------+---------------------------------------------------------------------------------------------------------------------------+

For more on Vim, I suggest you check out `this Vim cheat sheet` and/or
run ``vimtutor`` (``:help vimtutor`` for more).

.. _this Vim cheat sheet : http://www.fsckin.com/wp-content/uploads/2007/10/vi-vim_cheat_sheet.gif

Using vim with Octave
---------------------

There are a few things you might like to do with Octave files. 

Use Octave highlighting
"""""""""""""""""""""""

Vim defaults to ``matlab`` filetype for ``.m`` files, which is fine, but
doesn't highlight everything correctly. Instead, you can set Octave syntax
highlighting for the current file with::

    :set ft=octave

If you want to set this permanently, add this to your ``vimrc``::

    autocmd BufNewFile, BufRead *.m setlocal ft=octave

Add ``;`` to a bunch of lines
"""""""""""""""""""""""""""""


To add a ``;`` to the end of every line that doesn't have one, you can
highlight the lines you want with ``v``, type ``:`` and then use this substitution::

    " the '<'>' part will already be there
    :'<,'>s/\([^;]\)\_$/\1;/


Comment and uncomment lines
"""""""""""""""""""""""""""

To comment out a set of lines, again highlight them with ``v``, type ``:`` and
use this simple subsituttion::

    :'<,'>s/^/%/

And to uncomment::

    :'<,'>s/^%//

Search for a term
"""""""""""""""""

You can find any particular line of text by typing ``/`` in "command mode"
(that's the default mode, press ``<Esc>`` while typing to get to it). For
example::

    /apple <Return>

Will highlight all instances of apple in the document. (you can type
``,<space>`` to turn off the highlighting (the actual comma


My dotvim
==========

The ``vimrc.symlink`` file is pretty well documented. I've laid out a few
things below. (again, `my dotfiles`_ have quite a bit more)


Included plugins
----------------

Check out `my dotfiles`_ for some highlights on the included plugins. But a
few that might be helpful.

* **Gundo** - lets you scroll through your undo history with ``,g``
* **Powerline** - sets the fancy status bar at the bottom of the screen. Try
  installing a patched font and using the fancy encoding for additional
  awesomeness.
* **Ctrl-P** - type ``<Ctrl-P>`` to pop up a list of files in the current
  directory (and be able to open them). You can also use ``<Ctrl-Up>`` and
  ``<Ctrl-Down>`` to view recently used files and currently opened buffers.

Vim shortcuts
-------------

Mappings
""""""""

===========  ==============  =============================
Mapping      Mnemonic        Settings
===========  ==============  =============================
<leader> en  'edit normal'   tw=78; fo+=t, colorcolumn+=0
<leader> ec  'edit comment'  tw=72; fo+=t, colorcolumn+=0
<leader> ed  'edit done'     restore defaults
                             (or tw=80,fo-=t, colorcolumn=0)
<leader> p   'paste'         paste from clipboard
<leader> y   'yank'          yank to clipboard
Q            'quick form'?   format the current paragraph (e.g. wrap lines)
===========  ==============  =============================

Commands
""""""""

===========  =============================
Command      Settings
===========  =============================
<F3>         toggle VoOM
:DiffSaved   Show diffs between current file and saved file
===========  =============================

reStructuredText/autounderline Functions
----------------------------------------

* ``:Underline <arg>`` and ``:Title <arg>`` where ``<arg>`` is a character or
  number. (title creates an under and overline)

::

    some vim text

    ":Un -

    some vim text
    -------------

Some (optional) plugins have dependencies
-----------------------------------------

I've tried to document dependencies below, but a quick list here for
reference. **NONE of these are necessary to use my dotfiles,** they just
enable additional features.

===========    ==============
Plugin         Dependencies
===========    ==============
Syntastic      Requires 'compilers' for whatever files you want to check (for example, to check ``.rst`` files you need docutils)
Hammer         Requires ``github/markup``, ``coderay``, and ``tilt``
Ack            Requires an installation of ``ack`` (well worth it!)
Vim-IPython    Requires ``ipython`` to be installed (see IPython section for more)
===========    ==============

Compiling Vim/Installing extra dependencies/IPython/etc
=======================================================

Go look at `my dotfiles`_ for a detailed guide. I wanted to leave this README
quick and simple.

Latest version
==============

I tweak this version a bit and I update it less frequently -- you can find the
bleeding edge version at `my dotfiles`_.
