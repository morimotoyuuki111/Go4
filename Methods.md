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
	Name string // 名前　//フィールドを定義
	Age  int    // 年齢　//フィールドを定義
}

// Human構造体から挨拶文を作成します。
func (h Human) Hello() string {　　//hを使って構造体のフィールドを使うことができる
	return fmt.Sprintf("こんにちは！%sは%d歳です", h.Name, h.Age)
}

func main() {
	taro := Human{　//　変数taroにHuman{　Name: "Taro",Age:  20,}が初期化されて入る
		Name: "Taro",
		Age:  20,
	}

	fmt.Println(taro.Hello()) // こんにちは！Taroは20歳です
}
```

- メソッド
構造体などの特定の型に関連づけられた関数

```go
func (h Human) Hello() string {　　//hを使って構造体のフィールドを使うことができる
	return fmt.Sprintf("こんにちは！%sは%d歳です", h.Name, h.Age)
```

(h Human)の使い方は変数名.フィールド名　サンプルコード
(h Human)はレシーバと呼ぶ
