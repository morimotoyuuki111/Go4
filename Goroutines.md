# Goroutines

goroutine (ゴルーチン)は、Goのランタイムに管理される軽量なスレッドです。<br>

```go
go f(x, y, z)
```
と書けば、新しいgoroutineが実行されます。

```go
f(x, y, z)
```
f , x , y , z の評価は、実行元(current)のgoroutineで実行され、 f の実行は、新しいgoroutineで実行されます。

goroutineは、同じアドレス空間で実行されるため、共有メモリへのアクセスは必ず同期する必要があります。 sync パッケージは同期する際に役に立つ方法を提供していますが、別の方法がある<br>

```go
package main　//パッケージを宣言

import (　//fmtパッケージをインポート　timeパッケージをインポート
    "fmt"
    "time"
)

func say(s string) {　//say関数　s　変数　string型
	for i := 0; i < 5; i++ {　//i := 0;　変数の初期化　　i < 5;　繰り返しの条件　i++変数の更新
		time.Sleep(100 * time.Millisecond)//time.Sleep()で関数を呼び出しています 100ミリ秒停止させる?
		fmt.Println(s)
	}
}

func main() { 
	go say("world")　//goステートメントで関数を指定することで、並行実行される?
	say("hello")
}

出力結果
hello
world
world
hello
hello
world
world
hello
```
