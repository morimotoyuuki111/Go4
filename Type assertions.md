# Type assertions

型アサーション は、インターフェースの値の基になる具体的な値を利用する手段を提供します。<br>

```go
t := i.(T)
```
この文は、インターフェースの値 i が具体的な型 T を保持し、基になる T の値を変数 t に代入することを主張します。

i が T を保持していない場合、この文は panic を引き起こします。

インターフェースの値が特定の型を保持しているかどうかを テスト するために、型アサーションは2つの値(基になる値とアサーションが成功したかどうかを報告するブール値)を返すことができます。<br>

```go
t, ok := i.(T)
```

i が T を保持していれば、 t は基になる値になり、 ok は真(true)になります。

そうでなければ、 ok は偽(false)になり、 t は型 T のゼロ値になり panic は起きません。

この構文と map から読み取る構文との類似点に注意してください<br>

```go
package main　//パッケージを宣言

import "fmt"　//fmtパッケージをインポート

func main() {
    var i interface{} = "hello"　　//インターフェースを定義　iが変数　　iに"hello"が入る
    
    s := i.(string)　 //変数sにi.(string)　が入る
	fmt.Println(s)　//hello

	s, ok := i.(string)  //s, okにi.(string)が入る 
	fmt.Println(s, ok)　　//helloが文字列のため true

	f, ok := i.(float64) //f, okにi.(float64)が入る
	fmt.Println(f, ok)　//float64を保持してないためfalseになる?　文字列ではないため?

	f = i.(float64) // panic
	fmt.Println(f)///成功したかの有無を確かめるokが存在しないのでエラーが発生する。
}

出力結果
hello
hello true
0 false
panic: interface conversion: interface {} is string, not float64

goroutine 1 [running]:
main.main()
	/tmp/sandbox2575105939/prog.go:17 +0x165
```

- 例<br>
```go
　value, ok := <変数>.(<型>)
 ```
 
 インターフェースの値 <変数> が具体的な型 <型> を保持し、基になる <型> の値を変数 value に代入することを主張します。
また、以下の様にする事で、1番目の変数には型アサーション成功時に実際の値が格納され、2番目の変数には型アサーションの成功の有無（true/false）が格納されます。<br>
