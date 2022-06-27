# Errors
Goのプログラムは、エラーの状態を error 値で表現します。

error 型は fmt.Stringer に似た組み込みのインタフェースです:<br>

```go
type error interface {
    Error() string
}
```

( fmt.Stringer と同様に、 fmt パッケージは、変数を文字列で出力する際に error インタフェースを確認します。 )

よく、関数は error 変数を返します。そして、呼び出し元はエラーが nil かどうかを確認することでエラーをハンドル(取り扱い)します。


```go
i, err := strconv.Atoi("42")
if err != nil {
    fmt.Printf("couldn't convert number: %v\n", err)
    return
}
fmt.Println("Converted integer:", i)
```
nil の error は成功したことを示し、 nilではない error は失敗したことを示します。<br>

```go
package main

import (
	"fmt"
	"time"
)

type MyError struct {
	When time.Time
	What string
}

func (e *MyError) Error() string {
	return fmt.Sprintf("at %v, %s",
		e.When, e.What)
}

func run() error {
	return &MyError{
		time.Now(),
		"it didn't work",
	}
}

func main() {
	if err := run(); err != nil {
		fmt.Println(err)
	}
}

出力結果
at 2009-11-10 23:00:00 +0000 UTC m=+0.000000001, it didn't work
```                                                       
