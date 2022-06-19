# Pointers and functions

Golangのポインタは、別の変数のメモリアドレスを格納するために使用される変数です。変数のように関数へのポインタを渡すこともできます<br>

以下のプログラムでは、ポインター型引数のみを受け入れるように関数に指示する整数型ポインターパラメーターを持つ関数ptfを使用しています。基本的に、この関数は変数xの値を変更しました。開始時のxには値100が含まれています。ただし、関数呼び出しの後、出力に示されているように、値は748に変更されました。<br>



```go


package main //パッケージを宣言

import "fmt"　//インポートを宣言

// taking a function with integer
// type pointer as an parameter

func ptf(a *int) {　//ptf関数　。　　 (a *int) aが変数　*intがint型　。


    // dereferencing　
    *a = 748　　// 間接的参照で*intから変数aに間接的に*aに指し示す？　
    
}

func main() {

    var x = 100 //varは定義　変数xを定義

       fmt.Printf("The value of x before function call is: %d\n",x)
    
    // taking a pointer variable *int
    // and assigning the address 
     var pa *int = &x　 //

     ptf(pa)

     fmt.Printf("The value of x before function call is: %d\n",x)
}

出力結果
The value of x before function call is: 100
The value of x after function call is: 748
```
