---
title: Installing Camelot
---

This part of the documentation covers the steps to install Camelot.

After [installing the dependencies](install-deps.md), which include [Ghostscript](https://www.ghostscript.com) and [Tkinter](https://wiki.python.org/moin/TkInter), you can use one of the following methods to install Camelot:

!!! warning

    The ``lattice`` flavor will fail to run if Ghostscript is not installed. You may run into errors as shown in [issue #193](https://github.com/camelot-dev/camelot/issues/193).

## pip

To install Camelot from PyPI using ``pip``, please include the extra ``cv`` requirement as shown::

``` bash
$ pip install "camelot-py[base]"
```

## conda

`conda`_ is a package manager and environment management system for the [Anaconda](https://anaconda.org) / [Miniconda](https://docs.conda.io/projects/miniconda/en/latest/) distributions. It can be used to install Camelot from the ``conda-forge`` channel:

``` bash
$ conda install -c conda-forge camelot-py
```

## From the source code

After [installing the dependencies](install-deps.md), you can install Camelot from source by:

1. Cloning the GitHub repository.

    ``` bash
    $ git clone https://www.github.com/camelot-dev/camelot
    ```

2. And then simply using pip again.

    ``` bash
    $ cd camelot
    $ pip install ".[base]"
    ```
