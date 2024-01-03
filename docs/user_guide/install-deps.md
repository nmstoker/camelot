---
title: Installing Dependencies
---
<script src="../../js/asciinema-player.min.js"></script>
<link rel="stylesheet" type="text/css" href="../../css/asciinema-player.css" />

The dependencies [Ghostscript](https://www.ghostscript.com) and [Tkinter](https://wiki.python.org/moin/TkInter) can be installed using your system's package manager or by running their installer.

## OS-specific instructions

=== "Linux / MacOS"
	=== "Arch Linux"

		``` bash
		# pacman -S ghostscript tk
		```

		_Screencast below illustrates installation for ghostscript only (tkinter was already present)_

		<div id="player1"></div>
		<script>
		AsciinemaPlayer.create(
		'../../casts/archlinux_install_ghostscript.cast',
		document.getElementById('player1'),
		{ poster: "npt:0:0" }
		);
		</script>

	=== "Ubuntu"
		``` bash
		$ apt install ghostscript python3-tk
		```


	=== "MacOS"
		``` bash
		$ brew install ghostscript tcl-tk
		```

=== "Windows"

	**For Ghostscript**: you can get the installer at their [downloads page](https://www.ghostscript.com/download/gsdnld.html).

    <div id="player2"></div>
    <script>
      AsciinemaPlayer.create(
        '../../casts/windows11_install_ghostscript.cast',
        document.getElementById('player2'),
        { poster: "npt:0:1" }
      );
    </script>

	**For Tkinter**: if you installed Python with the standard [Python.org installer](https://www.python.org/downloads/windows/) TCL/Tkinter will typically be installed by default (unless you deselected it).

	If it is not installed with the standard Python.org installer then the easiest option is to try re-installing Python again, making sure to select it in the options, or you can download the [ActiveTcl Community Edition](https://www.activestate.com/activetcl/downloads) from ActiveState.  If you are using Conda then you can install it into your virtual environment with: `conda install -c conda-forge tk`.

## Checks to see if dependencies are installed correctly

You can run the following checks to see if the dependencies were installed correctly.

### For Ghostscript

Open the Python REPL and run the following:

=== "Linux / MacOS"

	``` python
	>>> from ctypes.util import find_library
	>>> find_library("gs")
	"libgs.so.10"
	```

	**Check:** The output of the ``find_library`` function should not be empty.

	If the output is empty, then it's possible that the Ghostscript library is not available one of the `LD_LIBRARY_PATH`/`DYLD_LIBRARY_PATH` variables depending on your operating system (Linux / MacOS). In this case, you may have to modify one of those path variables to include it.

	=== "Arch Linux"

		<div id="player3"></div>
		<script>
		AsciinemaPlayer.create(
		'../../casts/archlinux_check_ghostscript.cast',
		document.getElementById('player3'),
		{ poster: "npt:0:0" }
		);
		</script>

	=== "Ubuntu"
		_Screencast for Ubuntu coming soon!_

=== "Windows"

	``` python
	>>> import ctypes
	>>> from ctypes.util import find_library
	>>> find_library("".join(("gsdll", str(ctypes.sizeof(ctypes.c_voidp) * 8), ".dll")))
	<name-of-ghostscript-library-on-windows>
	```

	**Check:** The output of the `find_library` function should not be empty.

	If the output is empty, then it's possible that the Ghostscript library is not available in the `PATH` variable on your system. In this case, you may have to modify it to include it.

    <div id="player4"></div>
    <script>
      AsciinemaPlayer.create(
        '../../casts/windows11_check_ghostscript.cast',
        document.getElementById('player4'),
        { poster: "npt:0:1" }
      );
    </script>

### For Tkinter

Launch Python and then import Tkinter::

``` python
>>> import tkinter
```

**Check:** Importing ``tkinter`` should not raise an import error.
