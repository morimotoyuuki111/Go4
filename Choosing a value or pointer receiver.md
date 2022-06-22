# Choosing a value or pointer receiver

ポインタレシーバを使う2つの理由があります。

ひとつは、メソッドがレシーバが指す先の変数を変更するためです。

ふたつに、メソッドの呼び出し毎に変数のコピーを避けるためです。 例えば、レシーバが大きな構造体である場合に効率的です。

例では、 Abs メソッドはレシーバ自身を変更する必要はありませんが、 Scale と Abs は両方とも *Vertex 型のレシーバです。

一般的には、値レシーバ、または、ポインタレシーバのどちらかですべてのメソッドを与え、混在させるべきではありません。<br>

```go
package main //パッケージを宣言

import (　//fmtパッケージをインポート
	"fmt"
)

type Number struct {　　Numberは構造体の名前　　struct構造体　
	X, Y float64　//変数　float64　は小数点を入れる変数　
}

//メソッドの書き方
func (n *Number) Scale(f float64) {　　//*Numberが渡されてる　Scaleメソッドを定義
	n.X = n.X * f
	n.Y = n.Y * f
}

//メソッドの書き方　
func (n *Number) Sum() float64 {　　
	return n.X + n.Y　 
}

//%v それぞれの型の既定の書式で表示
func main() {
	n := &Number{3, 4}　//3+４になっているため７　　&Numberは変数nのアドレスを取得
	fmt.Printf("Before scaling: %+v, Sum: %v\n", n, n.Sum())　
	n.Scale(5)　　//
	fmt.Printf("After scaling: %+v, Sum: %v\n", n, n.Sum())　　
}

出力結果
Before scaling: &{X:3 Y:4}, Sum: 7
After scaling: &{X:15 Y:20}, Sum: 35
