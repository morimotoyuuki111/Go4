# Pointer receivers

ポインタレシーバでメソッドを宣言できます。

これはレシーバの型が、ある型 T への構文 *T があることを意味します。 （なお、 T は *int のようなポインタ自身を取ることはできません）

例では *Vertex に Scale メソッドが定義されています。

ポインタレシーバを持つメソッド(ここでは Scale )は、レシーバが指す変数を変更できます。 レシーバ自身を更新することが多いため、変数レシーバよりもポインタレシーバの方が一般的です。

Scale の宣言(line 16)から * を消し、プログラムの振る舞いがどう変わるのかを確認してみましょう。

変数レシーバでは、 Scale メソッドの操作は元の Vertex 変数のコピーを操作します。 （これは関数の引数としての振るまいと同じです）。 つまり main 関数で宣言した Vertex 変数を変更するためには、Scale メソッドはポインタレシーバにする必要があるのです。<br>

```go
package main //パッケージを宣言

import "fmt"　//fmtパッケージをインポート

type person struct {　//type 構造体の名前 struct
	name string  //フィールド　データ型１　　
	age  int　    //フィールド　データ型２　
}

func (p person) hello() { 　//pを使って構造体のフィールドを使うことができる (p person)がレシーバ　(変数　型)　hello()が関数
	fmt.Printf("%s (%d)\n", p.name, p.age)
}

func (p *person) increment() {　//(p *person)がポインタで渡されている　アドレスを格納するための変数が用意されてるのがポインタ
	p.age++
}

func main() { //
	p := person{
		name: "John",
		age:  30,
	}
	p.hello() // John (30) //hello関数を呼び出している
	p.increment()　　//increment関数を呼び出している
	p.hello() // John (31)　//increment関数を呼び出した後もう一度hello関数を呼び出しているためageが一つ増えて３１になる
}
```

- 関数の引数に参照渡しと値渡しがあるのと同様に、レシーバにも参照渡しと値渡しがあります。<br>参照渡しのレシーバを特に ポインタレシーバ (pointer receiver)、値渡しのレシーバーをバリューレシーバ(value receiver) といいます。<br>

- インクリメント（英：increment）とは<br>
　今の数字に1を足すこと<br>
 
関数はどこからでも呼び出せる
