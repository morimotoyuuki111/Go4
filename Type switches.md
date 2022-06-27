# Type switches

型switch はいくつかの型アサーションを直列に使用できる構造です。

型switchは通常のswitch文と似ていますが、型switchのcaseは型(値ではない)を指定し、それらの値は指定されたインターフェースの値が保持する値の型と比較されます。<br>

```go
switch v := i.(type) {
case T:
    // here v has type T
case S:
    // here v has type S
default:
    // no match; here v has the same type as i
}
```

型switchの宣言は、型アサーション i.(T) と同じ構文を持ちますが、特定の型 T はキーワード type に置き換えられます。

このswitch文は、インターフェースの値 i が 型 T または S の値を保持するかどうかをテストします。 T および S の各caseにおいて、変数 v はそれぞれ 型 T または S であり、 i によって保持される値を保持します。 defaultの場合(一致するものがない場合)、変数 v は同じインターフェース型で値は i となります。<br>

```go
package main　//パッケージを宣言

import "fmt"　//fmtパッケージをインポート

func do(i interface{}) {　　//do関数　の中にinterfaceを定義　iは変数
    switch v := i.(type) {　//vが条件の値？　　typeは型に名前をつけるのでint型
    cage int:　//intが値　iがintの値になる　
        fmt.Printlf("Twice %v is %v\n",v, v*2) //％vがそれぞれの型の既定の書式で表示なのでTwice ２１is 42(v*2なので２１*２)
    case string:　//string型　
        fmt.Printf("%q is %v bytes long\n", v, len(v))//%q=("..."付き文字列) 書いてあることはわかるが５はどこからきた？
    default:　// どのcaseにも当てはまらない場合に実行される処理
         fmt.Printf("I don't know about type %T!\n", v) //%Tは変数の型を文字列で表示　bool型
	}
}

func main() {
    do(21)
    do("hello")
    do(true)
}

出力結果
Twice 21 is 42
"hello" is 5 bytes long
I don't know about type bool!
```
