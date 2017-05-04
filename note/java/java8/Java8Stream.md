# java8 streams #

## stream 作用 ##
> Stream represents a sequence of objects from a source, which supports aggregate operations.

## Stream特性 ##
1. Sequence of elements—— *A stream provides a set of elements of specific type in a sequential manner. A stream gets/computes elements on demand. It never stores the elements*  **元素序列，处理过程中不对计算结果进行存储**
2. Source—— *Stream takes Collections, Arrays, or I/O resources as input source.*  **stream将集合，数组或者I/O资源等作为输入源**
3. aggregate operation—— *Stream supports aggregate operations like filter, map, limit, reduce, find, match and so on.* **stream支持聚合操作：例如filter, map, limit, reduce, find等**
4. pipelining——*Most of the stream operations return stream itself so that their result can be pipelined. These operations are called intermediate operations and their function is to take input, process them, and return output to the target. collect() method is a terminal operation which is normally present at the end of the pipelining operation to mark the end of the stream*  **管道**
5. automatic iterations——*Stream operations do the iterations internally over the source elements provided, in contrast to Collections where explicit iteration is required.*  **支持隐式的迭代**