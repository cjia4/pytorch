1. aten: A Tensor Library的缩写。与Tensor相关的内容都放在这个目录下。如Tensor的定义、存储、Tensor间的操作（即算子/OP）等；

可以看到在aten/src/Aten目录下，算子实现都在native/目录中。其中有CPU的算子实现，以及CUDA的算子实现（cuda/）等。

2. torch: 即PyTorch的前端代码。我们用户在import torch时实际引入的是这个目录。

其中包括前端的Python文件，也包括高性能的c++底层实现（csrc/）。为实现Python和c++模块的打通，这里使用了pybind作为胶水。在python中使用torch._C.[name]实际调用的就是libtorch.so中的c++实现，而PyTorch在前端将其进一步封装为python函数供用户调用。

3. c10、caffe2：移植caffe后端，c10指的是caffe tensor library，相当于caffe的aten。

PyTorch1.0完整移植了caffe2的源码，将两个项目进行了合并。引入caffe的原因是Pytorch本身拥有良好的前端，caffe2拥有良好的后端，二者在开发过程中拥有大量共享代码和库。例如在PyTorch中，c10::Device和at::Device是等价的。

4. tools：用于代码自动生成（codegen），例如autograd根据配置文件实现反向求导OP的映射。

5. scripts：一些脚本，用于不同平台项目构建或其他功能性脚本；