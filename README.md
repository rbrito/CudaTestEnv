CudaTestEnv
===========

Basic, incomplete, host-based CUDA API implementation use for testing my
programming assignments for the Coursera "Heterogeneous Parallel
Programming" class. It does not use an nVidia GPU but instead simulates the
threading and thread local variables, shared memory and barriers.  It only
supports 1 and 2 dimensional array because that is all that is needed so far
to complete my assignments.

Note, since this is using only using the standard `g++` compiler, there is
no error checking for using non-CUDA functions and constructs with in the
device functions. In fact, the `__global__` is just a no-op.

You will also need to call the device function using standard C-compliant
syntax and also pass the function to `setupCudaSim`. Here is an example:

    #ifndef CUDA_EMU
        vecAdd<<<dimGrid, dimBlock>>>(deviceInput1, deviceInput2, deviceOutput, inputLength);
    #else
        setupCudaSim (dimGrid, dimBlock, boost::bind(vecAdd, deviceInput1,
                      deviceInput2, deviceOutput, inputLength));
    #endif

I developed this on Cygwin in Windows 7. You will need `g++` (I used version
4.5) and Boost's `thread` and `system`.

To build and run my example, simply execute:

    cmake .
    make run1

then the `mp1` binary is created and uses the file `foo` as the first and
second argument:

    ./mp1 foo foo

make run1

this creates the mp1 GenDataMP1 binary, generates a vector test set of 90
elements and then run mp1 binary with the generated data

Contributors 
============

Myself, as well. I also used some code from the coursera git repo, and their contributors can be found at the following: 
[View list of contributors](https://github.com/ashwin/coursera-heterogeneous/contributors)
We welcome improvements to this code. Fork it, make your change and give me a pull request. Please follow the coding conventions already in use in the source files.


License
=======

All the files in this project are shared under the
[MIT License](http://opensource.org/licenses/mit-license.php).

Copyright (C) 2012
[Contributors](https://github.com/ashwin/coursera-heterogeneous/contributors)

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to
deal in the Software without restriction, including without limitation the
rights to use, copy, modify, merge, publish, distribute, sublicense, and/or
sell copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
=======

To use your own input, create text files for input1 and input2. Each integer
must be space separated and each row is terminated by a newline.
