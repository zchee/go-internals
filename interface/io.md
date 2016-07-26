io
==========

package `io` interface.

`io.Reader`
-----------

```go
type Reader interface {
	Read(p []byte) (n int, err error)
}
```

`io.Writer`
-----------

```go
type Writer interface {
	Write(p []byte) (n int, err error)
}
```

`io.Seeker`
-----------

```go
type Seeker interface {
	Seek(offset int64, whence int) (int64, error)
}
```

`io.ReadWriter`
---------------

```go
type ReadWriter interface {
	Reader
	Writer
}
```

`io.WriteCloser`
----------------

```go
type WriteCloser interface {
	Writer
	Closer
}
```

`io.ByteReader`
---------------

```go
type ByteReader interface {
	ReadByte() (c byte, err error)
}
```

`io.ReadWriteCloser`
--------------------

`io.ReadSeeker`
---------------

`io.WriteSeeker`
----------------

`io.ReadWriteSeeker`
--------------------

`io.ByteScanner`
----------------

`io.ByteWriter`
---------------

`io.RuneReader`
---------------

`io.RuneScanner`
---------------
