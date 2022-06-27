# Stringers

もっともよく使われているinterfaceの一つに fmt パッケージ に定義されている Stringer があります:<br>

```go
type Stringer interface {
    String() string
}
```

Stringer インタフェースは、stringとして表現することができる型です。 fmt パッケージ(と、多くのパッケージ)では、変数を文字列で出力するためにこのインタフェースがあることを確認します。<br>

```go
package main　//パッケージを宣言

import "fmt"　//fmtパッケージをインポート

type Person struct {　//構造体　Person構造体の名前
    Name string　//typeは新しい方を定義する　string型
	  Age  int　//int型
}

func (p Person) String() string {　//Person構造体のString()関数をメソッドで使用する
    return fmt.Sprintf("%v (%v years)", p.Name, p.Age)　//String()関数を終了
}

func main() {
	a := Person{"Arthur Dent", 42} //変数aにPerson{"Arthur Dent", 42}が代入
	z := Person{"Zaphod Beeblebrox", 9001}　//変数ZにPerson{"Zaphod Beeblebrox", 9001}が代入
	fmt.Println(a, z)
}

出力結果
Arthur Dent (42 years) Zaphod Beeblebrox (9001 years)
```
