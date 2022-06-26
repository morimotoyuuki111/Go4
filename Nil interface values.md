# Nil interface values

nil インターフェースの値は、値も具体的な型も保持しません。

呼び出す 具体的な メソッドを示す型がインターフェースのタプル内に存在しないため、 nil インターフェースのメソッドを呼び出すと、ランタイムエラーになります。<br>

```go
pacakage main //パッケージを宣言

import "fmt"　//fmtパッケージをインポート

type I interface {　インターフェースを定義　
    M()　//Mメソッド
}

func main() {
    var i I　//i Iを定義
    describe(i)　
    i.M()
}

func describe(i I) {
	fmt.Printf("(%v, %T)\n", i, i)
}

出力結果
(<nil>, <nil>)
panic: runtime error: invalid memory address or nil pointer dereference
[signal SIGSEGV: segmentation violation code=0x1 addr=0x0 pc=0x47f2e1]

goroutine 1 [running]:
main.main()
	/tmp/sandbox293555346/prog.go:12 +0x61
  ```
