# Interface values

下記のように、インターフェースの値は、<br>
値と具体的な型のタプルのように考えることができます:<br>

```go
(value, type)
```
インターフェースの値は、特定の基底になる具体的な型の値を保持します。<br>

インターフェースの値のメソッドを呼び出すと、その基底型の同じ名前のメソッドが実行されます。<br>

```go
pacakage main //パッケージを宣言

import(　fmtパッケージをインポート、mathパッケージをインポート
     "fmt"
     "math"
)

type I interface {　　//インターフェースを定義　Iは型
    M()　//Mはメソッド
}

type T struct {　//構造体　Tは構造体の名前
    S string　 //Sがフィールド　　string型
}　

// This method means type T implements the interface I,
// but we don't need to explicitly declare that it does so.
// declare that it does so.
func (t *T) M() {　 
    fmt.Println(t.S)
}

type F float64  //構造体？　メソッド？

func (f F) M() {　
    fmt.Println(f)
}

func main() {
	var i I　 //i Iを定義

	i = &T{"Hello"} //iに&T{"Hello"}が代入される
	describe(i) //なぜ*main.T？
	i.M()　// (&{Hello} 

	i = F(math.Pi) //Piは円周率
	describe(i)　//なぜmain.F
	i.M() // 
}

func describe(i I) {
	fmt.Printf("(%v,%T)\n", i, i) //
}

出力結果
(&{Hello}, *main.T)
Hello
(3.141592653589793, cmain.F)
3.141592653589793

```
