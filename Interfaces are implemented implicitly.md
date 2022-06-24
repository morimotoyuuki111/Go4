# Interfaces are implemented implicitly
型にメソッドを実装していくことによって、インタフェースを実装(満た)します。 インタフェースを実装することを明示的に宣言する必要はありません( "implements" キーワードは必要ありません)。

暗黙のインターフェースは、インターフェースの定義をその実装から切り離します。 インターフェースの実装は、事前の取り決めなしにパッケージに現れることがあります。<br>

```go
package main //パッケージを宣言

import "fmt"　//fmtパッケージをインポート
　　
type I interface {　　//インターフェースを定義　Iが型名
    M()　//メソッドM？
}

type T struct { //Tが構造体の名前　structが構造体
    S string　//Sがフィールド　string型
}

// This method means type T implements the interface I,
// but we don't need to explicitly declare that it does so.
// declare that it does so.
func (t T) M() {
     fmt.Println(t.S)
}

func main() {
     var i I = T{"hello"} 
     i.M()
}

出力結果
hello
```
