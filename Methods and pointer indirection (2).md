# Methods and pointer indirection (2)

```go

packagae main

import (
        "fmt
)

type Human struct { //構造体　 Human(人間)は構造体の名前
        Name string　 //Name　変数　string型
}

[メソッドで書く方法]
func (h Human) HelloName() string {　//hを使って構造体のフィールドを使うことができる　(h Human)(メソッド)hが変数　Humanが型　HelloName()が関数　
        return fmt.Sprintf("Hello,%s, h.Name)　//関数の処理結果を返す
}

[関数で書く方法]
func HelloName(h Human) string {　　
         return fmt.Sprintf("Hello,%s, h.Name)
}

func main() 
        h := Human{"Bob"} //変数hにHuman{"Bob"}が代入される
        fmt.Println(h,HelloName())
        fmt.Println(HelloName(h))
        
        hh := &Human{"Bob"}　//&Humanは変数hhからポインタを抽出している?
        fmt.Println(hh.HelloName())
        fmt.Println(HelloName(*hh)) //ポインタ型を宣言している_
}
