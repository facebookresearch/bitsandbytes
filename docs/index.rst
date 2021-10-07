.. bitsandbytes documentation master file, created by
   sphinx-quickstart on Wed Oct  6 11:17:23 2021.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Module tree:
===========================================

.. toctree::

   tree/bitsandbytes.rst


Module tree overview
--------------------

- **bitsandbytes.functional**: Contains quantization functions and stateless 8-bit optimizer update functions.
- **bitsandbytes.nn.modules**: Contains stable embedding layer with automatic 32-bit optimizer overrides (important for NLP stability)
- **bitsandbytes.optim**: Contains 8-bit optimizers.

TL;DR
-----

**Installation**:

1. Note down version: ``conda list | grep cudatoolkit``
2. Replace 111 with the version that you see: ``pip install bitsandbytes-cuda111``

**Usage**:

1. Comment out optimizer: ``#torch.optim.Adam(....)``
2. Add 8-bit optimizer of your choice ``bnb.optim.Adam8bit(....)`` (arguments stay the same)
3. Replace embedding layer if necessary: ``torch.nn.Embedding(..) -> bnb.nn.Embedding(..)``

**Problems/Errors**:
1. RuntimeError: CUDA error: no kernel image is available for execution on the device.

Solutions:
1a. This problem arises with the cuda version loaded by bitsandbytes is not supported by your GPU, or if you pytorch CUDA version mismatches. So solve this problem you need to debug ``$LD_LIBRARY_PATH``, ``$CUDA_HOME``, ``$PATH``. You can print these via ``echo $PATH``. You should look for multiple paths to different CUDA versions. This can include versions in your anaconda path, for example ``$HOME/anaconda3/lib``. You can check those versions via ``ls -l $HOME/anaconda3/lib/*cuda*`` or equivalent paths. Look at the CUDA versions of files in these paths. Does it match with ``nvidia-smi``?
1b. Another solution can be to compile the library from source. This can be still problematic if your PATH variables have multiple cuda versions.



