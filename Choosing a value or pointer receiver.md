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
```

- スライス型
```go
var a []string
var b []string // aとbの型は同一
```

- マップ型
```go
var a map[int]bool
// aとbの型は同一
var b map[int]bool
// キーの型が異なるため、aとcの型は異なる
var c map[int32]bool
// 要素の型が異なるため、aとdの型は異なる
var d map[int]string

```

- ポインタ
Go では変数に & を付けることで、その変数のメモリ上のアドレスを取得可能
変数のアドレスを取り出す & はアドレス演算子
Go ではアドレスを格納するための変数が用意されています。これを ポインターといいます。

```go
var x int32 = 10
fmt.Println(" x = ", x)  //  x =  10
fmt.Println("&x = ", &x) // &x =  0xc000118000
var p *int32
p = &x
fmt.Println(" p = ", p)  //  p =  0xc000118000
```
ポインターの初期値は nil です。nil はどのアドレス情報も保持していない状態です
```go
var p *int32
fmt.Println(" p = ", p) // p =  <nil>
```
nil を fmt.Println で表示すると <nil> と表示されます。
	
-Go のポインター変数に * を付けると、そのポインター変数が保持しているアドレスに書き込まれている値を意味します。<br>
	
行目で変数 x のアドレスを、ポインター変数 p に代入。そして、 8行目でポインター p が指し示す内容 (つまり変数 x の値) を書き換えています。9行目では x の値が書き換えられていることが確認
```go
var x int32 = 10
fmt.Println(" x = ", x)  //  x =  10
fmt.Println("&x = ", &x) // &x =  0xc00001407c

var p *int32
p = &x
fmt.Println(" p = ", p) //   p =  0xc00001407c
*p = 20
fmt.Println(" x = ", x) //   x =  20
```
- ポインターのまとめ
普通の変数のアドレスは & で取り出せる (& は「アドレス演算子」)<br>
ポインター変数はアドレスを保持する<br>
ポインター変数が保持するアドレスに書き込まれた値は * を付けて参照できる (* は「間接演算子」。間接演算子でアドレスの参照する値を参照することは「デリファレンス」)<br>
Go のポインターは算術演算はない<br>
	
- 構造体<br>
<a href="https://github.com/morimotoyuuki111/Go3/blob/main/Structs.md">過去の勉強</a><br>

- 配列<br>
<a href="https://web-camp.io/magazine/archives/62260">参考サイト</a><br>
<a href="https://wa3.i-3-i.info/word11924.html">参考サイト</a><br>

- bool型<br>
<a href="https://golang.keicode.com/basics/go-data-types.php#3">参考サイト</a><br>

- 素数<br>
<a href="https://ja.wikipedia.org/wiki/%E7%B4%A0%E6%95%B0">参考サイト</a><br>

- int型<br>
<a href="https://wa3.i-3-i.info/word14966.html">参考サイト</a><br>

- string型<br>
<a href="https://wa3.i-3-i.info/word14965.html">参考サイト</a><br>

- パッケージ<br>
 Goには予め用意されている標準パッケージがあり、標準パッケージを利用する事で、プログラミングを効率良く行うための便利な機能<br>
 ※fmtパッケージはコンソールを出力するパッケージ※<br>
  
- インポート　<br>
取り込む、持ち込む、などの意味<br>

- func main<br>
 メイン関数という意味<br>
    
- 関数<br>
関数とは複数の処理をまとめておくこと<br>

- 変数の定義<br>
```go
  func main(){ //プログラムをコンパイルして実行すると、まず main パッケージの中にある main()関数が実行される
  i := 2
  fmt.Println(i)  // 2が出力される
}
```
<a href="https://y-hiroyuki.xyz/go/variable/what-is-variable">参考サイト</a>

- 関数の定義
```go
func 関数名(){
 //処理内容
}
```

- func　関数名で関数の宣言を行う<br>
- ()内には引数を指定しますが今回の内容では、引数は使用しないので、()の中は空のままにしておく<br>
- 2行目の関数の処理内容は関数を呼び出しを行った際に実行される<br>

- main関数<br>
プログラムの最初に呼び出される関数<br>
<a href="https://zenn.dev/kubo_programmer/articles/990891ff3a43c5">参考サイト</a>

- 引数<br>
引数とは、関数に渡す値<br>
引数を使用する場合は「func 関数名(引数名 型)」と記述する事で、引数を呼び出し先の値<br>
