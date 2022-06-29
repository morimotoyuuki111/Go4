# Channels
チャネル( Channel )型は、チャネルオペレータの <-を用いて<br>値の送受信ができる通り道です。<br>

```go
ch <- v    // v をチャネル ch へ送信する
v := <-ch  // ch から受信した変数を v へ割り当てる
```

(データは、矢印の方向に流れます)

マップとスライスのように、チャネルは使う前に以下のように生成します:<br>

```go
ch := make(chan int)
```

通常、片方が準備できるまで送受信はブロックされます。これにより、明確なロックや条件変数がなくても、goroutineの同期を可能にします。

サンプルコードは、スライス内の数値を合算し、2つのgoroutine間で作業を分配します。 両方のgoroutineで計算が完了すると、最終結果が計算されます。<br>


```go
package mian //パッケージを宣言

import "fmt"　//fmtパッケージをインポート

//messages <- "Hello"が送信　msg := <-messagesが受信?
func main() {
  messages := make(chan string)　 //make(chan string)　新しいチャネル
  go func() { messages <- "Hello" }() //fnce()無関数
  
  msg := <-messages
  fmt.Println(msg)
}

出力結果
Hello

```
