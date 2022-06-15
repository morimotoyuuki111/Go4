# Methods

Goには、クラス( class )のしくみはありませんが、型にメソッド( method )を定義できます。<br>
メソッドは、特別なレシーバ( receiver )引数を関数に取ります。<br>
レシーバは、 func キーワードとメソッド名の間に自身の引数リストで表現します。<br>
この例では、 Abs メソッドは v という名前の Vertex 型のレシーバを持つことを意味しています。<br>

```go
package main　//パッケージを宣言

import (　//fmtパッケージ　mathパッケージを宣言
  "fmt"
  "math"
)

type Vertex struct { //type Vertex（構造体の名前） struct
    X,Y float64 //各変数　　float64は小数点を入れる変数
}

func (v Vertex) abs() float64 {　
  return math.Sqrt(v.X*v.X + v.Y*v.Y)
}

func main() {
    v := Venrtex{3. 4}
    fmt.Println(v.abs())
}
```
