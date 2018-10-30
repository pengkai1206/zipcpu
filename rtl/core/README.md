## ZipCPU的核心

以下是ZipCPU的核心文件。在这里，您不仅可以找到主要的ZipCPU核心，还可以找到：

- 几个预取例程

  o [prefetch.v](./prefetch.v)  较旧的预取模块，一次只获取一条指令，因此阻止了流水线操作。

  o [pipefetch.v](./pipefetch.v), 我第一次尝试使用缓存构建预取。它采用了一种相当独特的缓存方法，将其作为内存中的滚动窗口实现。 这个文件因历史原因而存在，但不多。

  o [dblfetch.v](./dbgfetch.v), 一次取两个指令（在后续时钟上）。这是为了通过利用许多内存访问在第二次访问时更快的事实来提高CPU不流水线时的速度。

  o [pfcache.v](./pfcache.v), 这是CPU的当前/最佳指令缓存。


- [idecode.v](./idecode.v), 指令解码器

- 几个内存访问例程

  o [memops.v](./memops.v), 典型/传统的一个存储器操作一次访问存储器。这是我的第一个内存方法，当CPU没有以其pipelind模式运行时，仍然采用适当的方法。

  o [pipemem.v](./pipemem.v), 一种更快的内存访问方法，它将连续的内存访问组合成一个流水线总线访问。到目前为止，该例程补偿了ZipCPU（尚未）具有集成数据高速缓存的事实。

  o [dcache.v](./dcache.v), 是我尝试构建数据缓存。这从未与CPU集成，并且在MMU也集成之前可能无法集成。

- [div.v](./div.v), the divide unit

- [cpuops.v](./cpuops.v), the ALU unit

The defines within [cpudefs.v](../cpudefs.v) will determine which of these modules gets linked into your CPU.

