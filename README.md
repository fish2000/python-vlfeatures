Summary
=======

A _self-contained_ python wrapper for [vlfeat](http://www.vlfeat.org/).
It is based on libvl 0.9.9 (and should be adapted to run along 
with the current vlfeat by some kind person :-) ).

Requirements
------------

* [numpy](numpy.scipy.org)
* [Boost.Python](http://www.boost.org/doc/libs/1_49_0/libs/python/doc/)
* [matplotlib](http://matplotlib.sourceforge.net/)

OSX
---

[Homebrew](http://mxcl.github.com/homebrew/) gives you boost via ```brew install boost```.
```setup.py``` should work for both a homebrew based an
macports based system. I need to run
    ARCHFLAGS="-arch x86_64" python setup.py install
for a successful build.
