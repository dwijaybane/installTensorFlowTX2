# installTensorFlowTX2
April 4, 2018
JetsonHacks

Install TensorFlow v1.6 on NVIDIA Jetson TX2 Development Kit

Jetson TX2 is flashed with JetPack 3.2 which installs:
* L4T 28.2 an Ubuntu 16.04 64-bit variant (aarch64)
* CUDA 9.0
* cuDNN 7.0.5

### Pre-built installation

If you are only interested in installing Tensorflow on the TX2, not building from source, pre-built wheel files are available here: https://github.com/dwijaybane/installTensorFlowTX2/releases

You can also use prebuilt bazel 0.11.1 by downloading bazel-11.1 and rename it and move to system:
mv bazel-11.1 bazel
sudo cp bazel /usr/local/bin/

If you are interested in building from source, read on.
### Preparation
Before installing TensorFlow, a swap file should be created (minimum of 8GB recommended). The Jetson TX2 does not have enough physical memory to compile TensorFlow. The swap file may be located on the internal eMMC, and may be removed after the build.

There is a convenience script for building a swap file. To build a 8GB swapfile on the eMMC in the home directory:

$ ./createSwapfile.sh -d ~/ -s 8

After TensorFlow has finished building, the swap file is no longer needed and may be removed.


These scripts support either Python 2.7 or Python 3.5.
TensorFlow should be built in the following order:

## For Python 2.7

#### installPrerequisites.sh
Installs Java and other dependencies needed. Also builds Bazel version 0.11.1.

#### cloneTensorFlow.sh
Git clones v1.6.0 from the TensorFlow repository and patches the source code for aarch64

#### setTensorFlowEV.sh
Sets up the TensorFlow environment variables. This script will ask for the default python library path. There are many settings to chose from, the script picks the usual suspects. Uses python 2.7.

## For Python 3.5

#### installPrerequisitesPy3.sh
Installs Java and other dependencies needed. Also builds Bazel version 0.11.1.

#### cloneTensorFlow.sh
Git clones v1.6.0 from the TensorFlow repository and patches the source code for aarch64

#### setTensorFlowEVPy3.sh
Sets up the TensorFlow environment variables. This script will ask for the default python library path. There are many settings to chose from, the script picks the usual suspects. Uses python 3.5.

## Build TensorFlow
Once the prerequisites have been installed and the environment configured, it is time to build TensorFlow itself.

#### buildTensorFlow.sh
Builds TensorFlow.

#### packageTensorFlow.sh
Once TensorFlow has finished building, this script may be used to create a 'wheel' file, a package for installing with Python. The wheel file will be in the $HOME directory.

#### Install wheel file
For Python 2.X

$ pip install $HOME/<em>wheel file</em>

For Python 3.X

$ pip3 install $HOME/<em>wheel file</em> 


### Notes
This TensorFlow installation procedure was derived from these discussion threads: 

<ul>
<li>https://github.com/tensorflow/tensorflow/issues/851</li>
<li>http://stackoverflow.com/questions/39783919/tensorflow-on-nvidia-tx1/</li>
<li>https://devtalk.nvidia.com/default/topic/1000717/tensorflow-on-jetson-tx2/</li>
<li>https://github.com/tensorflow/tensorflow/issues/9697</li>
</ul>

### Release Notes
April 4, 2018
* L4T 28.2 (JetPack 3.2)
* TensorFlow 1.6
* Without TensorRT support

September 13, 2017
* L4T 28.1 (JetPack 3.1)
* TensorFlow 1.3
* Github changed some sha256 checksums, patches added to workspace.bzl as workaround

September 2017
* L4T 28.1 (JetPack 3.1)
* TensorFlow 1.3

April 2017
* Initial Release
* L4T 27.1 (JetPack 3.0)
* TensorFlow 1.0



## License
MIT License

Copyright (c) 2017 Jetsonhacks

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
