# Methods

Goには、クラス( class )のしくみはありませんが、型にメソッド( method )を定義できます。<br>
メソッドは、特別なレシーバ( receiver )引数を関数に取ります。<br>
レシーバは、 func キーワードとメソッド名の間に自身の引数リストで表現します。<br>
この例では、 Abs メソッドは v という名前の Vertex 型のレシーバを持つことを意味しています。<br>

```go
package main //パッケージを宣言

import (　//fmtパッケージをインポート
	"fmt"
)

// 構造体Human(人)を定義
type Human struct {
	Name string // 名前
	Age  int    // 年齢
}

// Human構造体から挨拶文を作成します。
func (h Human) Hello() string {　
	return fmt.Sprintf("こんにちは！%sは%d歳です", h.Name, h.Age)
}

func main() {
	taro := Human{　//　変数taroにHuman{　Name: "Taro",Age:  20,}が入る
		Name: "Taro",
		Age:  20,
	}

	fmt.Println(taro.Hello()) // こんにちは！Taroは20歳です
}
```
