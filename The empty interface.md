# The empty interface

ゼロ個のメソッドを指定されたインターフェース型は、 空のインターフェース と呼ばれます:<br>

```go
interface{}
```

空のインターフェースは、任意の型の値を保持できます。 (全ての型は、少なくともゼロ個のメソッドを実装しています。

空のインターフェースは、未知の型の値を扱うコードで使用されます。 例えば、 fmt.Print は interface{} 型の任意の数の引数を受け取ります。<br>

```go
package main　//パッケージを宣言

import "fmt"　//fmtパッケージをインポート

func main() {
    var i interface{}　　　// iが変数　空のインターフェースを定義　　　宣言した変数にはどんな型の値でも代入可能
    describe(i)//変数 iが空なのでnil?　　
    
    i = 42
    describe(i) 　　//iに４２を代入されていて型がint型

　　　　　　　　i = "hello"　　
	　　　　describe(i)　//iに"hello"文字列なので　型がstring型
}

func describe(i interface{}) {
	fmt.Printf("(%v, %T)\n", i, i)//%vはその変数（型）の詳細情報、%Tはその型名が出力される
}

出力結果
(<nil>, <nil>)
(42, int)
(hello, string)
```
