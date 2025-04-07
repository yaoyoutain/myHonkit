# IO

## 目录

- [io包](#io包)
  - [reader 接口](#reader-接口)
  - [writer 接口](#writer-接口)
  - [接口实现](#接口实现)
  - [ReaderAt 和 WriterAt 接口](#ReaderAt-和-WriterAt-接口)
    - [ReaderAt 接口](#ReaderAt-接口)
    - [WriterAt 接口](#WriterAt-接口)
  - [ReaderFrom 和 WriterTo 接口](#ReaderFrom-和-WriterTo-接口)
    - [ReadFrom 接口](#ReadFrom-接口)
    - [WriterTo接口](#WriterTo接口)
  - [seeker 接口](#seeker-接口)
    - [whence 的值 在io包中定义相应的常量](#whence-的值-在io包中定义相应的常量)
  - [Closer接口](#Closer接口)
    - [小提示](#小提示)
  - [Copy 和 CopyN 函数](#Copy-和-CopyN-函数)
    - [copy](#copy)
    - [CopyN](#CopyN)
  - [WriteString 函数](#WriteString-函数)

# io包

> 在 io 包中最重要的是两个接口：Reader 和 Writer 接口。本章所提到的各种 IO 包，都跟这两个接口有关，也就是说，只要满足这两个接口，它就可以使用 IO 包的功能。

1. Reader 接口

## reader 接口

> Read 将 len(p) 个字节读取到 p 中。它返回读取的字节数 n（0 <= n <= len(p)） 以及任何遇到的错误。即使 Read 返回的 n < len(p)，它也会在调用过程中占用 len(p) 个字节作为暂存空间。若可读取的数据不到 len(p) 个字节，Read 会返回可用数据，而不是等待更多数据。
>
> 当 Read 在成功读取 n > 0 个字节后遇到一个错误或 EOF (end-of-file)，它会返回读取的字节数。它可能会同时在本次的调用中返回一个non-nil错误,或在下一次的调用中返回这个错误（且 n 为 0）。 一般情况下, Reader会返回一个非0字节数n, 若 n = len(p) 个字节从输入源的结尾处由 Read 返回，Read可能返回 err == EOF 或者 err == nil。并且之后的 Read() 都应该返回 (n:0, err:EOF)。
>
> 调用者在考虑错误之前应当首先处理返回的数据。这样做可以正确地处理在读取一些字节后产生的 I/O 错误，同时允许EOF的出现。

```go 
type Reader interface {
    Read(p []byte) (n int, err error)
}
```


## writer 接口

> Write 将 len(p) 个字节从 p 中写入到基本数据流中。它返回从 p 中被写入的字节数 n（0 <= n <= len(p)）以及任何遇到的引起写入提前停止的错误。若 Write 返回的 n < len(p)，它就必须返回一个 非nil 的错误。

```go 
type Writer interface {
    Write(p []byte) (n int, err error)
}
```


## 接口实现

- os.File 同时实现了 io.Reader 和 io.Writer
- strings.Reader 实现了 io.Reader
- bufio.Reader/Writer 分别实现了 io.Reader 和 io.Writer
- bytes.Buffer 同时实现了 io.Reader 和 io.Writer
- bytes.Reader 实现了 io.Reader
- compress/gzip.Reader/Writer 分别实现了 io.Reader 和 io.Writer
- crypto/cipher.StreamReader/StreamWriter 分别实现了 io.Reader 和 io.Writer
- crypto/tls.Conn 同时实现了 io.Reader 和 io.Writer
- encoding/csv.Reader/Writer 分别实现了 io.Reader 和 io.Writer
- mime/multipart.Part 实现了 io.Reader
- net/conn 分别实现了 io.Reader 和 io.Writer(Conn接口定义了Read/Write)

## ReaderAt 和 WriterAt 接口

### **ReaderAt 接口**

> ReadAt 从基本输入源的偏移量 off 处开始，将 len(p) 个字节读取到 p 中。它返回读取的字节数 n（0 <= n <= len(p)）以及任何遇到的错误。
>
> 当 ReadAt 返回的 n < len(p) 时，它就会返回一个 非nil 的错误来解释 为什么没有返回更多的字节。在这一点上，ReadAt 比 Read 更严格。
>
> 即使 ReadAt 返回的 n < len(p)，它也会在调用过程中使用 p 的全部作为暂存空间。若可读取的数据不到 len(p) 字节，ReadAt 就会阻塞,直到所有数据都可用或一个错误发生。 在这一点上 ReadAt 不同于 Read。
>
> 若 n = len(p) 个字节从输入源的结尾处由 ReadAt 返回，Read可能返回 err == EOF 或者 err == nil
>
> 若 ReadAt 携带一个偏移量从输入源读取，ReadAt 应当既不影响偏移量也不被它所影响。
>
> 可对相同的输入源并行执行 ReadAt 调用。

```go 
type ReaderAt interface {
    ReadAt(p []byte, off int64) (n int, err error)
}
```


### **WriterAt 接口**

> WriteAt 从 p 中将 len(p) 个字节写入到偏移量 off 处的基本数据流中。它返回从 p 中被写入的字节数 n（0 <= n <= len(p)）以及任何遇到的引起写入提前停止的错误。若 WriteAt 返回的 n < len(p)，它就必须返回一个 非nil 的错误。
>
> 若 WriteAt 携带一个偏移量写入到目标中，WriteAt 应当既不影响偏移量也不被它所影响。
>
> 若被写区域没有重叠，可对相同的目标并行执行 WriteAt 调用。

```go 
type WriterAt interface {
    WriteAt(p []byte, off int64) (n int, err error)
}
```


> 📌注： 这里是左闭右开区间 ， 会覆盖掉原有数据

## ReaderFrom 和 WriterTo 接口

### ReadFrom 接口

> ReadFrom 从 r 中读取数据，直到 EOF 或发生错误。其返回值 n 为读取的字节数。除 io.EOF 之外，在读取过程中遇到的任何错误也将被返回。
> 如果 ReaderFrom 可用，Copy 函数就会使用它。

```go 
type ReaderFrom interface {
    ReadFrom(r Reader) (n int64, err error)
}
```


注意：ReadFrom 方法不会返回 err == EOF。

### **WriterTo**接口

> WriteTo 将数据写入 w 中，直到没有数据可写或发生错误。其返回值 n 为写入的字节数。 在写入过程中遇到的任何错误也将被返回。
>
> 如果 WriterTo 可用，Copy 函数就会使用它。

```go 
type WriterTo interface {
    WriteTo(w Writer) (n int64, err error)
}
```


## seeker 接口

> Seek 设置下一次 Read 或 Write 的偏移量为 offset，它的解释取决于 whence： 0 表示相对于文件的起始处，1 表示相对于当前的偏移，而 2 表示相对于其结尾处。 Seek 返回新的偏移量和一个错误，如果有的话。

```go 
type Seeker interface {
    Seek(offset int64, whence int) (ret int64, err error)
}
```


#### whence 的值 在io包中定义相应的常量

```go 
const (
  SeekStart   = 0 // seek relative to the origin of the file
  SeekCurrent = 1 // seek relative to the current offset
  SeekEnd     = 2 // seek relative to the end
)
```


## Closer接口

> 该接口比较简单，只有一个 Close() 方法，用于关闭数据流。
>
> 文件 (os.File)、归档（压缩包）、数据库连接、Socket 等需要手动关闭的资源都实现了 Closer 接口。
>
> 实际编程中，经常将 Close 方法的调用放在 defer 语句中。

```go 
type Closer interface {
    Close() error
}
```


### 小提示

1. file.Close() 应该在err检查后再调用&#x20;

```go 
file, err := os.Open("studygolang.txt")
defer file.Close()
if err != nil {
    ...
}
```


## Copy 和 CopyN 函数

### copy

> Copy 将 src 复制到 dst，直到在 src 上到达 EOF 或发生错误。它返回复制的字节数，如果有错误的话，还会返回在复制时遇到的第一个错误。
>
> 成功的 Copy 返回 err == nil，而非 err == EOF。由于 Copy 被定义为从 src 读取直到 EOF 为止，因此它不会将来自 Read 的 EOF 当做错误来报告。
>
> 若 dst 实现了 ReaderFrom 接口，其复制操作可通过调用 dst.ReadFrom(src) 实现。此外，若 src 实现了 WriterTo 接口，其复制操作可通过调用 src.WriteTo(dst) 实现。

```go 
func Copy(dst Writer, src Reader) (written int64, err error)
```


### **CopyN**

> CopyN 将 n 个字节(或到一个error)从 src 复制到 dst。 它返回复制的字节数以及在复制时遇到的最早的错误。当且仅当err == nil时,written == n 。
>
> 若 dst 实现了 ReaderFrom 接口，复制操作也就会使用它来实现。

```go 
func CopyN(dst Writer, src Reader, n int64) (written int64, err error)
```


## WriteString 函数

> WriteString 将s的内容写入w中，当 w 实现了 WriteString 方法时，会直接调用该方法，否则执行 w\.Write(\[]byte(s))。

```go 
func WriteString(w Writer, s string) (n int, err error)
```
