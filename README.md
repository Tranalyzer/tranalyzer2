# Tranalyzer2 Installation Procedure
Tranalyzer can be downloaded from one of the following page:

* http://tranalyzer.sf.net
* http://tranalyzer.com

## Dependencies
* **Ubuntu/Kali:**
    * sudo apt-get install automake libpcap-dev libtool zlib1g-dev
* **Arch:**
    * sudo pacman -S automake libpcap libtool zlib
* **Gentoo:**
    * sudo emerge automake libpcap libtool zlib
* **OpenSUSE:**
    * sudo zypper install automake gcc libpcap-devel libtool zlib-devel
* **Red Hat/Fedora:**
    * sudo yum install automake libpcap-devel libtool zlib-devel
* **Mac OS X:**
    * brew install autoconf automake libpcap libtool zlib

## Compilation
To build Tranalyzer2 and the plugins, run one of the following command:

* Tranalyzer2 and a default set of plugins: (e.g. T2HOME: ~/tranalyzer2/trunk)
> `cd "$T2HOME"; ./autogen.sh`
* Tranalyzer2 and all the plugins in `T2HOME`
> `cd "$T2HOME"; ./autogen.sh -a`
* Tranalyzer2 and a custom set of plugins (listed in plugins.build)
> `cd "$T2HOME"; ./autogen.sh -b`

where `T2HOME` points to the root folder of Tranalyzer, i.e., where this file is located.

For finer control of which plugins to build, either run `./autogen.sh` from every folder you want to build, use `./autogen.sh -b` with a file listing one plugin name per line or use the `t2conf` script or `t2build` alias defined in `$T2HOME/scripts/t2_aliases`.

Run `t2conf -h` or `t2build -h` for the full list of options accepted by the scripts.

## Installation
The `-i` option of the autogen script installs Tranalyzer2 in /usr/local/bin and the man page in /usr/local/man/man1. Note that root rights are required for the installation.

Alternatively, add the following alias to your `~/.bash_aliases`:

> `alias tranalyzer="$T2HOME/tranalyzer2/src/tranalyzer"`

## Utilities
The file `$T2HOME/scripts/t2_aliases` provides a set of aliases and functions which facilitate working with Tranalyzer. To access them, append the following lines to `~/.bashrc` or `~/.bash_aliases`
```
if [ -f "$T2HOME/scripts/t2_aliases" ]; then
    . "$T2HOME/scripts/t2_aliases"             # Note the leading '.'
fi
```
For a full description of the file, refer to scripts/doc/scripts.pdf.

## Documentation
Tranalyzer2 core and every plugin come with their own documentation found in the doc/ subfolder. The full documentation of Tranalyzer2 and all the locally available plugins can be built by running `make` in `$T2HOME/doc`. The following function, added to `~/.bash_aliases` can be quite handy to access the different parts of the documentation. Replace `evince` with your preferred PDF viewer. Note that if `t2_aliases` was installed, then this function is automatically available.

```
function t2doc() {
    if [ -z "$1" ]; then
        if [ -f "$T2HOME/doc/documentation.pdf" ]; then
            evince "$T2HOME/doc/documentation.pdf" &
        fi
    elif [ ! -d "$T2HOME/$1" ]; then
        echo "Plugin '$1' not found"
    elif [ ! -f "$T2HOME/$1/doc/$1.pdf" ]; then
        echo "Documentation for plugin '$1' could not be found"
    else
        evince "$T2HOME/$1/doc/$1.pdf" &
    fi
}
```

## Copyright
Copyright (c) 2008-2018 by Tranalyzer Development Team
