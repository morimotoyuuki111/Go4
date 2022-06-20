＃　　Methods and pointer indirection

下の2つの呼び出しを比べると、ポインタを引数に取る ScaleFunc 関数は、ポインタを渡す必要があることに気がつくでしょう:<br>

```go
var v Vertex
ScaleFunc(v, 5)  // Compile error!
ScaleFunc(&v, 5) // OK
```

メソッドがポインタレシーバである場合、呼び出し時に、変数、または、ポインタのいずれかのレシーバとして取ることができます:<br>

```go
var v Vertex
v.Scale(5)  // OK
p := &v
p.Scale(10) // OK
```
v.Scale(5) のステートメントでは、 v は変数であり、ポインタではありません。 メソッドでポインタレシーバが自動的に呼びだされます。 Scale メソッドはポインタレシーバを持つ場合、Goは利便性のため、 v.Scale(5) のステートメントを (&v).Scale(5) として解釈します。<br>


```go
package main //パッケージメイン

import "fmt"　//fmtパッケージをインポート

type Vertex struct {　構造体　 Vertexは構造体の名前
	X, Y float64　//変数　　float64　は小数点を入れる変数
}

func (v *Vertex) Scale(f float64) {　//*Vertexに対してメソッドを定義する　*Vertexが渡されてる
	v.X = v.X * f　
	v.Y = v.Y * f
}

func ScaleFunc(v *Vertex, f float64) {　 //　メソッドをScaleFunc関数に書き直してる　
	v.X = v.X * f
	v.Y = v.Y * f
}

func main() {
	v := Vertex{3, 4}　
	v.Scale(2)//２をかける
	ScaleFunc(&v, 10)　　//&vはv := Vertex{3, 4}　に入って３０＊２　４０＊２ため{60 80}となる

	p := &Vertex{4, 3}　//4*8 4*3
	p.Scale(3)//をかける
	ScaleFunc(p, 8)//pに&Vertex{4, 3}が入っている　 32*3 24*3のため&{96 72}となる

	fmt.Println(v, p)
}

出力結果
{60 80} &{96 72}
```
