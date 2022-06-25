# Interface values with nil underlying values

インターフェース自体の中にある具体的な値が nil の場合、メソッドは nil をレシーバーとして呼び出されます。

いくつかの言語ではこれは null ポインター例外を引き起こしますが、Go では nil をレシーバーとして呼び出されても適切に処理するメソッドを記述するのが一般的です(この例では M メソッドのように)。

具体的な値として nil を保持するインターフェイスの値それ自体は非 nil であることに注意してください。<br>

```go
package main　//パッケージを宣言

import "fmt"　//fmtパッケージを宣言

type I interface {　//インターフェースを定義
	M()　//Mはメソッド
}

type T struct {　//構造体　Tが構造体の名前
	S string　Sがフィールド　string型
}

func (t *T) M() {　　// T構造体（T型）のMメソッド
	if t == nil {　//タイプtがnilの時true そうじゃなければfalse
		fmt.Println("<nil>")
		return //<nil>を返してる？
	}
	fmt.Println(t.S) 
}

func main() {
	var i I //i Iを定義

	var t *T　　//t *Tを定義
	i = t //iにtを代入
	describe(i)//中身は<nil>,と＊T型の*main.T(予想)
	i.M()//メソッドM()で呼び出してるのでnil？

	i = &T{"hello"}
	describe(i)
	i.M()
}

func describe(i I) {
	fmt.Printf("(%v, %T)\n", i, i)
}

出力結果
(<nil>, *main.T)
<nil>
(&{hello}, *main.T)
hello
```
