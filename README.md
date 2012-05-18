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

```setup.py``` should work for both a homebrew based and a
[macports](http://www.macports.org/) based system. I need to run

    ARCHFLAGS="-arch x86_64" python setup.py install

for a successful build.

Linux
-----

Depending on your system, you may need to change

    LinkArgs.append('-lboost_python-mt-py26')

in ```setup.py```. Install boost.python on Ubuntu
systems via ```aptitude install libboost-python-dev```.

SIFT
----
Only the vl_sift (and ```__init__.py```) module was changed a bit. Assuming you
have ```box.pgm``` in your working directory, then

```python
import numpy, Image, vlfeat
box = Image.open("box.pgm")
box_array = numpy.array(box)
[f, d] = vlfeat.vl_sift(box_array.T, first_octave=-1, verbose=True)
```

produces nearly identical descriptors (in ```d```) to ```bin/sift``` from vlfeat. Note
that
* you don't need to specify ```dtype=np.float32``` when providing the ```box_array``` to vl_sift,
* you need to use ```box_array.T```
* the first octave is by default 0 (in ```bin/sift``` this is set to ```-1```).
* the ```x``` and ```y``` positions in ```f``` are swapped (compared to the binary),
  the first number refers to row in ```box_array``` and the second one to column.

The produced descriptors match those from the binary nearly perfectly (in particular,
the sequence of numbers is the same), sometimes some values are off by 1. I don't
know why that is (```vl_sift_calc_keypoint_descriptor``` produces two different
descriptors on seemingly identical input). If some has an idea (or, more probable,
I'm doing something stupid here), please let me know.

