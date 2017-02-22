##Caffe for Dilation Network

This is a fork of Caffe that support the training of dilation network
described in [this ICLR conference
paper](http://arxiv.org/abs/1511.07122). It is updated with the master
branch of [BVLC/caffe](https://github.com/BVLC/caffe) at commit
[f28f5a](https://github.com/BVLC/caffe/commit/f28f5ae2f2453f42b5824723efc326a04dd16d85)
(June 27, 2016). The original README of Caffe is at
[README_caffe.md](https://github.com/fyu/caffe-dilation/blob/master/README_caffe.md).

### Build

This fork perserves the compatibililty with vanilla Caffe. For help of
compiling this code, please turn to Caffe installation guide.

Makefile in this fork is changed slightly so that it is easier to
build caffe from different git branches at the same time. There are
some changes in the resulting build dir:

- git branch name is appended
after `${BUILD_DIR}`. So the actual build dir is
`${BUILD_DIR}_${GIT_BRANCH}`, such as `./build_master`.
- `${BUILD_DIR}_${GIT_BRANCH}/python` should be added to PYTHONPATH
instead of the python dir in the caffe source code.


### Usage

Please check [fyu/dilation](https://github.com/fyu/dilation/) for how
to use this code. The built caffe binary is used directly by
[dilation/train.py](https://github.com/fyu/dilation/blob/master/train.py).





# Updates Required

```
make all - j
make pycaffe -j 
mate test -j 
make runtest -j
```
## In MakeFile
```
LIBRARIES += glog gflags protobuf leveldb snappy \
  lmdb boost_system boost_filesystem  hdf5_hl hdf5 m \
  opencv_core opencv_highgui opencv_imgproc opencv_imgcodecs
```

## In MakeFile.config
```
  CUDA_ARCH := -gencode arch=compute_60,code=sm_60 \
#		-gencode arch=compute_20,code=sm_21 \
#		-gencode arch=compute_30,code=sm_30 \
#		-gencode arch=compute_35,code=sm_35 \
#		-gencode arch=compute_50,code=sm_50 \
#		-gencode arch=compute_52,code=sm_52 \
		-gencode arch=compute_61,code=sm_61 \
		-gencode arch=compute_61,code=compute_61
```

## For Python `caffe_pb2`

```
cp python/caffe/proto/caffe_pb2.py build_master/python/caffe/proto/caffe_pb2.py
``` 

## bashrc

```
export LD_LIBRARY_PATH="$LD_LIBRARY_PATH:/home/ankit/caffe-dilation/build_master/lib"
export PYTHONPATH="${PYTHONPATH}:/home/ankit/caffe-dilation/build_master/python"

```

