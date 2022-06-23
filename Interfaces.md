# Interfaces

interface(インタフェース)型は、メソッドのシグニチャの集まりで定義します。

そのメソッドの集まりを実装した値を、<br>interface型の変数へ持たせることができます。<br>

- # インターフェース<br>
Interface(インターフェース) とはメソッドの型だけを定義した型のことです。
interface(インターフェース) を利用することで、オブジェクト指向言語でいうところのポリモーフィズムと同様の機能を実現できます。<br>


- # インターフェースの定義<br>
インターフェースの定義は以下のように記述します<br>
（メソッドは複数記述することができます）<br>
インターフェースの定義の内容は、単なるメソッドリストです。<br>
メソッドを並べていく<br>

```go
type 型名 interface {
    メソッド名1(引数の型, ...) (返り値の型, ...)
      .....
    メソッド名N(引数の型, ...) (返り値の型, ...)
}
```


- # 空インターフェース
Go言語には、全ての型と互換性を持っている interface{}型（空インターフェース） というものが存在しています。<br>

interface{}（空インターフェース） は文字通りゼロ個のメソッドを指定されたインターフェース型のことなので、以下の様に定義する事ができます。<br>

```go
interface{}
```

以下の例の様に interface{}（空インターフェース） で宣言した変数にはどんな型の値でも代入可能です。<br>

```go
var obj interface{}

obj = 0123                                                            // int
obj = "String"                                                       // string
obj = []string{"Python", "Golang", "Ruby"}                          // slice
obj = func greetings(_ string) string { return "Hello World" }     // function
```

- # 型アサーション
全ての型と互換性を持っている interface{} ですが、interface{}型 の引数で受け渡された値は、元の型の情報が欠落しています。<br>
そこで、 型アサーションは、<br>
インターフェースの値の基になる具体的な値を利用する手段を提供します。<br>
型のアサーションには以下の構文を使用します。<br>

```go
value := <変数>.(<型>)
```

この文は、インターフェースの値 <変数> が具体的な型 <型> を保持し、基になる <型> の値を変数 value に代入することを主張します。<br>
また、以下の様にする事で、1番目の変数には型アサーション成功時に実際の値が格納され、2番目の変数には型アサーションの成功の有無（true/false）が格納されます。<br>

```go
value, ok := <変数>.(<型>)
```

実際に以上の方法で型のアサーションが出来る事を確認します。<br>

```go
func main() {
    var intface interface{} = "hello"

    variable := intface.(string)
    fmt.Println(variable) //=> hello

    variable, ok := intface.(string)
    fmt.Println(variable, ok) //=> hello true

    float, ok := intface.(float64) 
    fmt.Println(float, ok) //=> 0 false
    //格納失敗が、成功したかの有無を確かめるokが存在するのでエラーにはならない。

    float = intface.(float64) 
    fmt.Println(float) //=> panic: interface conversion: interface {} is string, not float64
    //成功したかの有無を確かめるokが存在しないのでエラーが発生する。
}
```
上記の例ではインターフェースは string として型付けされているので、それと異なる float64 等を <型> 部分に書くとエラーが発生します。
（成功したかの有無を確かめるok（左辺に２番目の変数）が存在するのでエラーにはならない。）<br>


- # 型switch
データの型判定は switch 文でも行うことができます。Go 言語では、これを 型 switch といいます。
以下の様に 型switch を書く事ができます。<br>

```go
switch v := x.(type) {
case 型1: ...  // v は型1 の値になる
case 型2: ...  // v は型2 の値になる
    ...
default: ... 
}
```
型switch では上記の様に switch の後ろに型アサーション v := x.(type) を書き、case に型を指定します。<br>

実際の使用例を確認<br>
```go
func do(i interface{}) {
    switch variable := i.(type) {
    case int:
        fmt.Println(variable)
    case string:
        fmt.Println(variable)
    default:
        fmt.Println("Default")
    }
}

func main() {
    do(23) //=> 23
    do("hello") //=> hello
    do(true) //=> Default
}
```

- #  構造体にインターフェースの実装


構造体にインターフェースを実装する事ができる<br>
```go
func (引数 構造体名) 関数名(){
     関数の中身
}
```

インターフェースを実装できることを確認<br>
```go
type People interface {
    intro()
}

type Person struct {
    name string
}

//構造体PersonがインターフェースPeopleを実装した事を意味します。
func (arg Person) intro(){
    fmt.Println(arg.name)
}

func main() {
    bob := Person{"Bob"}
    bob.intro() //=> Bob
}
```

- # Interface(インターフェース)実例

Interface(インターフェース) とは何か、より具体的に捉えます。
以下の例では Person と Person2という構造体があり、各構造体に intro() メソッドが定義されており、各構造体が intro() を実行するための IntroForPerson() IntroForPerson2()が存在しています。<br>

```go
type Person struct {} //Person構造体
type Person2 struct {} //Person2構造体

//Person構造体のメソッドintro()
func (p Person) intro() string{ 
    return "Hello World"
}

//Person2構造体のメソッドintro()
func (p Person2) intro() string{
     return "Hello World"
}

//Person構造体のメソッドintro()を実行するメソッド
func IntroForPerson(arg *Person){
    fmt.Println(arg.intro())
}

//Person2構造体のメソッドintro()を実行するメソッド
func IntroForPerson2(arg *Person2){
    fmt.Println(arg.intro())
}

func main(){
  bob := new(Person)
  mike := new(Person2) 

  IntroForPerson(bob) //=> Hello World
  IntroForPerson2(mike) //=> Hello World
}
```

様の動きをするIntroForPersonとIntroForPerson2メソッドが存在しており冗長<br>
```go
type Person struct {} //Person構造体
type Person2 struct {} //Person2構造体

type People interface{
    intro()
}

func IntroForPerson(arg People) {
     arg.intro();
}

//Person構造体のメソッドintro()
func (p *Person) intro() { 
    fmt.Println("Hello World")
}

//Person2構造体のメソッドintro()
func (p *Person2) intro() {
     fmt.Println("Hello World")
}

func main(){
  bob := new(Person)
  mike := new(Person2) 

  IntroForPerson(bob) //=> Hello World
  IntroForPerson(mike) //=> Hello World
}
```
