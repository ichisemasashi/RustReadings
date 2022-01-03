# Rust入門


プログラミング言語Rust入門です．なるべくわかりやすいように解説しました．公式ドキュメントを読んでみたけど，あまりよくわからなかったという人に向いているかもしれません．



# はじめに

## 📌 はじめに

Rust はマルチパラダイムプログラミング言語です．Rust
は静的型付け（statically-typed），式ベース（expression-based）であり，手続き型・関数型プログラミングの両方を実装することが出来ます．また，オブジェクト指向を言語としてサポートしている訳ではありませんが，オブジェクト指向プログラミングも制限付きで実装することが出来ます．Rust
はパフォーマンス，信頼性，生産性に重点を置き，システムプログラミング言語として適した言語を目指しています．

個人的に Rust は関数型プログラミング言語である Haskell
に大きく影響を受けており，ほとんどの部分が Haskell
から引き継いでいるように思えます．ただし，純粋関数型でもなく，モナドというものもありません．そこにポインタや参照といった別の言語の概念を取り入れ，さらに所有権といった独自の機能を組み込んだものです．これは，用語や機能が既存のプログラミング言語の概念に似てはいますが，必ずしも一致していないため，混乱しやすいところです．なので，最初は
Rust を全く新しい言語として扱ったほうがいいかもしれません．

Rust には公式ドキュメント The Rust Programming Language
Book
があります．これはかなり丁寧で豊富な内容が含まれているわけですが，説明が冗長であり，量も多いので読むのに時間がかかります．そのため，手っ取り早く
Rust を始める場合は Tour of Rust
を利用した方がいいです．手軽にコードを動かしながら進められるのでとても解りやすいです．順番としては
Tour of Rust
をやり終えてから公式ドキュメントまたは他の参考サイトを参照するのが良いと思います．

これから Rust
について解説していきます．注意として，わかり易さ・明確さを重視しているため，公式ドキュメントで使用している用語，およびその意味とは異なるところがいくつかあります．また，読者対象には何かしらのプログラミング言語を学んでいる人を想定しています．\
Rust
は簡単な言語ではありません．プログラミング初心者の場合は，まず別の言語から覚えることをオススメします．




# 基本

## 📌 Hello World!!

以下は，おなじみの Hello World
プログラムです．非常に単純で直感的に書けます．Rust
Playground というサイトでは Rust
プログラムを手軽に試すことができます．試しに下の内容を実行してみても構いません．サイトを開いたら最初から似たようなプログラムが入力されているかもしれません．


``` 
fn main() {
    print!("hello world!")
}
```


## 📌 コメント

Rust のコメントには，一行コメント ( `//` )と，ブロックコメント（ `/*`
）（`*/`）があります． `/*` ブロックコメントは `/*` このようにネストして
`*/` 書くことができます．`*/`

## 📌 式と文

Rust は式ベースの言語です．ほとんどが **式**
（expression）で表されます．ここで式は返り値を評価するものです．簡単に言うと，式は何かしらの値を返します．それに対して，
**文** （statement）は処理を実行しますが値を返しません．

## 📌 ブロック

式の１つに **ブロック** があります．これは `{` と `}`
で囲んだものです．例えば `{0}` というのは `0`
を返す式です．ブロックが返す値は省略することができます．その場合は `()`
を返します．この `()` を **ユニット** と言います．つまり，`{}`
というのは `{()}` ということになります．\
ブロックには２つの機能があります．１つはスコープを作成します．もう１つは，文をいくつも記述できることです．


``` 
{ statement; statement; statement; ...; (expression) }
```


ここでセミコロン (`;`) は式を文に変化させるものです．

## 📌 オブジェクト

数値や関数や参照など，型の実体はすべて **オブジェクト**
です．つまり，式が返す値もまたオブジェクトになります．例えば， `1`
という値も数値オブジェクトであり，`1 == {1}` という関係にあります．

## 📌 所有権

オブジェクトには **所有権** (Ownership)
が付いています．この所有権には２つの属性があります．

![rust-onwership01](https://storage.googleapis.com/zenn-user-upload/ym0o15tj4kbs3tyrqqow30n9bp3h)

## 📌 束縛

`let` 文を使うことでオブジェクトと変数を **束縛**
します．変数はそのスコープから外れたときに束縛していた所有権を放棄します．また，最初に束縛したオブジェクトの所有権は基本的に原本となり，原本および仮の所有権がすべて放棄された時にオブジェクトは破棄されます．

![onwership02](https://storage.googleapis.com/zenn-user-upload/eraje1uvwj8c0q3uz9z804am1lir)

## 📌 参照

Rust
では所有権を使ってオブジェクトを受け渡します．通常は所有権を渡してしまうと束縛が解除されて，受け取った側がそれを束縛します．そこで，仮の所有権を作成して相手に渡すことで，渡す側は束縛を解除されず，仮の所有権を受け取った側はその所有権を使ってオブジェクトを操作することが出来ます．そして，受け取った側の変数がスコープを外れた時に束縛していた仮の所有権が破棄されます．この時，原本または他の仮の所有権があればオブジェクトは破棄されません．仮の所有権を作成する方法の１つが
**参照** （reference）です．これは `&` 演算子を使います．

## 📌 可変性

Rust は標準でオブジェクトを **不変** （immutable）で束縛します．そこで，
`let` ではなく `let mut` を使うことで，オブジェクトを **可変**
（mutable）で束縛することが出来ます．\
今までのことをまとめると次のようになります．

![rust-ownership03](https://storage.googleapis.com/zenn-user-upload/2p2nk7hbow4x1l6d90325kzswhck)

原本の所有権から仮の所有権を作成することが出来ます．また，仮の所有権を複製することも出来ますし，仮の所有権からさらに仮の所有権を作れます．ただし，仮の所有権から原本の所有権は作れません．

![rust-onwership04](https://storage.googleapis.com/zenn-user-upload/sdla0v4i1kedb3rcg1t9bahuvr9k)

## 📌 借用チェック

同一オブジェクトに対する参照と可変について，いくつか制限があります．

-   不変参照 (`&`) は何個でも同時に存在することが出来る
-   不変参照 (`&`) と可変参照 (`&mut`) は同時に存在することが出来ない
-   可変参照 (`&mut`) は同時に１つしか存在することが出来ない

ここで大事なことは，上記の制限は **関数呼び出し時**
（かつコンパイル時）にチェックされるということです（これを
**借用チェック**
と呼びます）．このチェックが行われる直前の可変参照（必ず１つ）もしくは不変参照（複数可）がその時に存在していることになります．少なくとも可変参照を作成した時には，それまでの不変参照または可変参照がすべて無効となり，存在しないことになります．もちろん，あくまで同一オブジェクトに対する参照に対してです．\
以下は複数の不変参照が存在しても問題のないコードです．


``` 
fn main() {
    let a = 10;               // immutable object
    let aref1 = &a;           // reference
    let aref2 = &a;           // reference
    println!("{}, {}, {}", a, aref1, aref2); // borrow check!! - OK
}
```


次は，可変参照をしているところが複数ありますが，借用チェック時に制約を満たしているのでこれも問題ありません．


``` 
fn main() {
    let mut a = 10;           // mutable object
    let a_ref1 = &a;          // reference
    let a_mut_ref1 = &mut a;  // mutable reference
    let a_mut_ref2 = &mut a;  // mutable refernece
    *a_mut_ref2 = 20;         // assign
    println!("{}", a);        // borrow check!! - OK
}
```


次は，可変参照を複数存在してしまうことになるのでコンパイルエラーになります．


``` 
fn main() {
    let mut a = 10;           // mutable object
    let a_ref1 = &a;          // reference
    let a_mut_ref1 = &mut a;  // mutable reference
    let a_mut_ref2 = &mut a;  // この時点で a_ref1, a_mut_ref1 は存在しない
    *a_mut_ref1 = 20;         // assign (error)
    println!("{}", a);        // borrow check!! - Error!
}
```


次は，可変参照と不変参照が同時に存在してしまうことになるのでコンパイルエラーになります．


``` 
fn main() {
    let mut a = 10;           // mutable object
    let a_ref1 = &a;          // reference
    let a_mut_ref1 = &mut a;  // mutable reference
    let a_mut_ref2 = &mut a;  // この時点で a_ref1, a_mut_ref1 は存在しない
    println!("{}", a_ref1);   // borrow check!! - Error!
}
```


不変参照や可変参照を複数束縛しているコードでも借用チェック時に制約を満たしていればコンパイルは通ります．


``` 
fn main() {
    let mut a = 10;           // mutable object
    let a_ref1 = &a;          // reference
    let a_mut_ref1 = &mut a;  // mutable reference
    let a_mut_ref2 = &mut a;  // この時点で a_ref1, a_mut_ref1 は存在しない
    let a_ref2 = &a;          // この時点で a_mut_ref2 は存在しない
    //println!("{}", a_mut_ref2);        // borrow check!! - Error!
    //println!("{} {}", a_ref1, a_ref2); // borrow check!! - Error!
    println!("{}", a_ref2);   // borrow check!! - OK
}
```


このように関数呼び出しによる借用チェックによって，スコープから抜けていない変数であっても，それが参照なら存在していないことになりうるということです（ここで存在していないと言っていますが，実際には存在できないようにコンパイル時にエラーが出るということ）．参照を束縛した変数をなるべく作らないことが大切です．

## 📌 参照外し

参照（仮の所有権）を使ってオブジェクトの操作をする場合は
**参照外し**（dereference）が必要です．これは `*` 演算子を使います．


``` 
fn main() {
    let mut a = 10;            // mutable object
    let a_mut_ref = &mut a;    // mutable reference
    *a_mut_ref = 20;           // dereference and assign
    println!("{}", a_mut_ref); // auto dereference
}
```


参照外しは関数に渡した時や， `.`
演算子によるフィールド操作・メソッド呼び出し時などにおいて自動で行われる場合があります．




# コピートレイト

## 📌 コピートレイト

Rust には **トレイト**
（trait）というデータ型を分類する概念があります．例えば，数値全般を表す
`Num`
というトレイトがあったとき，それを実装しているデータ型はすべて数値型として分類することができる，というものです．トレイトには特有のメソッドを実装することが出来ます．また，ジェネリクスにおいて，あるトレイトを実装した型であるという制約をかけることが出来ます．これを
**トレイト境界** （trait bound）と呼びます．

トレイトは標準でいくつか実装されているものがあり，その１つが
**コピートレイト** （Copy
Trait）です．束縛したオブジェクトがコピートレイトを実装したデータ型の変数から別の変数に束縛するときは，所有権は移動せず，値をコピーして新しいオブジェクト（そして所有権）を作成します．Rust
のプリミティブ型はコピートレイトを実装しています．


``` 
fn main() {
    let a = 10;            // immutable object
    let b = a;             // copy
    print!("{} {}", a, b); // borrow check!! - OK
}
```


不変参照 (`&`) もコピートレイトを実装しています．


``` 
fn main() {
    let a = 10;                  // immutable object
    let a_ref = &a;              // reference
    let a_ref_copy = a_ref;      // copy reference
    print!("{} {} {}", a, a_ref, a_ref_copy); // borrow check!! - OK
}
```


注意なのが，可変参照 (`&mut`)
はコピートレイトを実装していません．なぜなら，可変参照は１つしか存在してはいけないからです．


``` 
fn main() {
    let mut a = 10;                 // mutable object
    let a_mut_ref = &mut a;         // mutable reference
    let a_mut_ref_move = a_mut_ref; // move mutable reference
    print!("{}", a_mut_ref);        // borrow check!! - Error!
}
```


次のように可変参照の場合は移動します．


``` 
fn main() {
    let mut a = 10;                 // mutable object
    let a_mut_ref = &mut a;         // mutable reference
    let a_mut_ref_move = a_mut_ref; // move mutable reference
    print!("{}", a_mut_ref_move);   // borrow check!! - OK
}
```


データ型がコピートレイトを実装しているかどうかはドキュメントに記載されています．調べたい型のドキュメントにある
`Trait Implementations` の中に `Copy`
があるかどうか確認してみてください．

![rust-copytrait-implementation](https://storage.googleapis.com/zenn-user-upload/ryxhp3bdp07212iu158s1wj7bcnz)

また，下記に示す関数 `copy_trait_check`
では，トレイト境界を使って引数の型がコピートレイトを実装していることを制約します．実装されていなかったらコンパイルエラーになります．エラーから分かるように，
`String` 型はコピートレイトを実装していません．


``` 
fn copy_trait_check<T: Copy>(_: T) {} // trait bound

fn main() {
    let s = String::from("hello");    // String
    copy_trait_check(s);
                    // ^ the trait `Copy` is not implemented for `String`
                    // error[E0277]: the trait bound `String: Copy` is not satisfied
    let a = 10;          // i32
    copy_trait_check(a); // OK
}
```


不変束縛の変数から可変束縛の変数に変えることができます．

![rust-ownership05](https://storage.googleapis.com/zenn-user-upload/09t17cvqsj3r7eifr14mh9xohu0q)

変数 `a` から変数 `b` に所有権が移動し，可変に変わります．そして，変数
`a`
の束縛は解除されます．もし，オブジェクトがコピートレイトを実装していたらコピーが作成され，変数
`a` はオブジェクトを束縛したままで，変数 `b`
には新しい可変のオブジェクトが束縛されます．




# データ型

## 📌 基本データ型

Rust の標準にある基本的なデータ型は次のとおりです：

-   整数型: `i8`, `u8`, `i16`, `u16`, `i32`, `u32`, `i64`, `u64`,
    `isize`, `usize`
-   浮動小数点型: `f32`, `f64`
-   ブーリアン型: `bool`
-   文字列型: `char`
-   タプル（複合）型: `(500, 6.4, true)`, `()` はユニット．
-   配列型: `[1,2,3,4,5]`, `[3;5] = [3,3,3,3,3]`

数値型のリテラルには次のものが使えます：

-   `98_222` (10進数)
-   `0xff` (16進数)
-   `0o77` (8進数)
-   `0b1111_0000` (2進数)
-   `b'A'` (バイト)
-   `0.` (浮動小数点数)

基本的なデータ型はコピートレイトを実装しています．また，複合・配列型については，含まれている要素がすべてコピートレイトを実装していれば，全体もコピートレイトを実装したことになります．\
参照も型の１つで，不変参照はコピートレイトを実装していますし，可変参照は実装していません．また，参照のまた参照ということも可能です．


``` 
fn main() {
    let a = 42;
    let ref_ref_ref_a = &&&a;
    let ref_a = **ref_ref_ref_a;
    let b = *ref_a;
    print!("{} {}", a, b);
}
```


比較するときは基本的に同じ型でなくてはならないので，参照もまた型であるということが以下でわかります．


``` 
fn main() {
    let a         = 10;     // immutable object
    let a_ref     = &a;     // reference
    let a_ref_ref = &a_ref; // reference to reference
    println!("{}", a == a_ref);
    // error[E0277]: can't compare `{integer}` with `&{integer}`
    println!("{}", a_ref_ref == a_ref);
    // error[E0277]: can't compare `&{integer}` with `{integer}`
}
```


Rust
は強い型推論を持っていますが，意図的にデータ型を指定したい場合があります．その場合は変数名の後ろに
`:` を付けてデータ型を指定します．


``` 
fn main() {
    let a: i32 = 10;
    let b: u32 = 20;
    let c: f32 = 0.;
    let d: &i32 = &50;
    print!("{} {} {} {}", a, b, c, d);
}
```


変数は **パターン** を使って，要素を分解して束縛することが出来ます．


``` 
fn main() {
    let (x,y,z) = (1,2,3);
    let [a,b,c] = [4,5,6];
    let (i,_,_) = (7,8,9);
    println!("xyz= {} {} {}", x, y, z);
    println!("abc= {} {} {}", a, b, c);
    println!("  i= {}", i);
}
```


`_` は **ワイルドカード**
と呼ばれるもので，オブジェクトを無視するときに使います．\
Rust では同じスコープ内で，変数名を使い回すことができます．


``` 
fn main() {
    let str_len = String::from("hello world!");
    let str_len = str_len.len();
    println!("{}", str_len);
}
```


あるスコープのさらにローカルなスコープにおいても外側にある変数名と同じ名前で新しく束縛できます．このとき，外側の変数はローカルから隠れます．これを
**シャドーイング** と言います．


``` 
fn main() {
    let a = 10;
    
    { // local scope
        let mut a = 20;
        a += 30;
        println!("{}", a); // 50
    }
    
    println!("{}", a); // 10
}
```


明示的に数値オブジェクトを型変換して使いたい場合があります．その場合は
`as` を使います．


``` 
fn main() {
    let a = 13u8;
    let b = 7u32;
    let c = a as u32 + b;
    println!("{}", c);

    let t = true;
    println!("{}", t as u8);
}
```


## 📌 スライス

**スライス**
は参照の１つで，別のオブジェクト内の連続した要素を指し示すものです．スライスを取得するには，オブジェクトに対して
**数列指定**
（`[m..n]`）します．参照なので，スライスの型は例えば配列だと `&[T]`
となります． `T` は任意の型です．


``` 
fn main() {
    let a = [1,2,3,4,5];
    let a_slice = &a[1..3];
    dbg!(a_slice); // [2,3]
}
```


### 数列

数列は `Range` 型と呼ばれるもので `m..n` の形で指定します． `m` と `n`
はそれぞれ開始値と終了値で， `m` から `n-1` までの連番を表します．
`m..=n` とすることで， `m` から `n` までの連番を表します．数列は `for`
式で利用することができます．


``` 
fn main() {
    let mut sum=0;
    for i in 1..100 {
        sum += i;
    }
    println!("sum={}", sum);
}
```


Rust はインデックスが `0`
から始まります．数列指定では開始インデックスと終了インデックスを `..`
を使って指定します．例えば `m..n` なら `[m, m+1, m+2, …, n-1]`
となります． `m..=n` の場合は `[m, m+1, m+2, …, n]`
となります．開始インデックスと終了インデックスは省略することが出来ます．


``` 
let s = String::from("hello");
let slice = &s[0..2];
let slice = &s[0..=2];
let slice = &s[..2];
let slice = &s[3..s.len()];
let slice = &s[3..];
let slice = &s[..];
```


### 文字列リテラル

文字列のスライスの型は `&str`
です．そして，文字列リテラルは不変の文字列スライス (`&str`) です．


``` 
let s = "Hello, world!";
```





# 関数

## 📌 関数

関数を定義するには `fn` を使い，本体は `{}`
で囲みます．引数の型は必ず明記しなければなりません． `fn` は文で， `{}`
は式です．式は返り値を持つものでしたよね．返り値の型は `->`
で指定します．\
また， `return` で処理を中断して値を返すことが出来ます．


``` 
fn add(a: i32, b: i32) -> i32 {
    a+b
}

fn main() {
    print!("{}", add(10,20));
}
```


関数の引数に対してパターンによる分解束縛をすることが出来ます．


``` 
fn print_coordinates(&(x, y): &(i32, i32)) {
    println!("location: ({},{})", x, y);
}

fn main() {
    let point = (3, 5);
    print_coordinates(&point);
}
```





# 制御構文

## 📌 if 式

`if` は条件によって処理を分岐するものです． `if`, `else`, `else if`
が使えます．それぞれに続くものは式 `{}` です．


``` 
fn main() {
    let number = 6;
    if number % 4 == 0 {
        println!("number is divisible by 4");
    } else if number % 2 == 0 {
        println!("number is divisible by 2");
    } else {
        println!("number is not divisible by 4 or 2");
    }
}
```


`if`
は式なので，値を返せます．ただし，その場合は返す値が同じ型でなければなりません．


``` 
fn main() {
    let condition = true;
    let number = if condition { 5 } else { 6 };
    // let number = if condition { 5 } else { "six" }; Error!
    println!("The value of number is: {}", number);
}
```


## 📌 loop 式

無限ループするには `loop` を使います．ループから抜ける場合は `break`
を使います． `loop` もまた式なので， `break`
に返り値を指定することが出来ます．


``` 
fn main() {
    let mut counter = 0;
    let result = loop {
        counter += 1;
        if counter == 10 {
            break counter * 2;
        }
    };
    
    println!("The result is {}", result);
}
```


## 📌 while 式

条件を満たしている間だけループさせる場合は `while` 式を使います．
`while` 式は常に `()` を返します． `break`
は使えますが，値を返すことは出来ません．


``` 
fn main() {
    let mut number = 3;
    while number != 0 {
        println!("{}", number);
        number -= 1;
    };
    
    println!("LIFTOFF!!!");
}
```


## 📌 for 式

イテレータを使って，各要素に対して処理を行いたい場合は `for`
を使います． `for` 式は常に `()`
を返します．（イテレータとは，連続する一連のデータへのアクセスを提供するオブジェクトのことです）


``` 
fn main() {
    let a = [10, 20, 30, 40, 50];
    
    for element in a.iter() {
        println!("the value is: {}", element);
    }
}
```





# 構造体

## 📌 構造体

**構造体** はデータ型の要素を集めたものです．１つ１つの要素を
**フィールド** と呼びます．構造体の定義は `struct`
を使い，フィールドは名前と型を指定します．


``` 
struct User {
    username: String,
    email: String,
    sign_in_count: u64,
    active: bool,
}
```


構造体のオブジェクトを作成する場合は，各フィールドを `key:value`
という形で束縛します．


``` 
let user1 = User {
    email: String::from("someone@example.com"),
    username: String::from("someusername123"),
    active: true,
    sign_in_count: 1,
};
```



ここでは「 **オブジェクト** 」と「 **インスタンス**
」について説明します．一般的に構造体や列挙型など（オブジェクト指向でのクラス）の実体は「インスタンス」と呼ばれています．しかし，本書ではそれらを「オブジェクト」に統一します．そして，「インスタンス」は，関数型プログラミング言語
Haskell に従って， **データ型**
を表します．例えば，コピートレイトを実装した構造体 `Hoge`
があるとします．このとき， `Hoge` はコピートレイトの **インスタンス**
（**データ型**
）です．そして，トレイト境界でコピートレイトを指定した場合，コピートレイトのインスタンスである
`Hoge` は制約を満たしていることになります．


可変のオブジェクトを作成するとすべてのフィールドが可変になります．オブジェクトのフィールドは
`.` 演算子を使って指定します．


``` 
let mut user1 = User {
    email: String::from("someone@example.com"),
    username: String::from("someusername123"),
    active: true,
    sign_in_count: 1,
};

user1.email = String::from("anotheremail@example.com");
```


オブジェクト作成時に指定する変数名と構造体のフィールド名が一致している場合，フィールド名を省略することが出来ます．


``` 
fn build_user(email: String, username: String) -> User {
    User {
        email,
        username,
        active: true,
        sign_in_count: 1,
    }
}
```


あるオブジェクトのフィールドに束縛したものを使って，新しいオブジェクトを作成するときに便利な構文があります．オブジェクト作成時に，明示的にフィールドを指定しなかったものは
`..`
の後に渡したオブジェクトのフィールドを束縛します．ただし，コピートレイトを実装している型なら複製され，そうでないなら所有権が移動することに注意が必要です．


``` 
let user2 = User {
    email: String::from("another@example.com"),
    username: String::from("anotherusername567"),
    ..user1
};
```


## 📌 タプル構造体

指定した要素で構成されたタプルに名前をつけることが出来ます．このようなタプルを
**タプル構造体**
といいます．この場合，フィールド名はありません．タプル構造体は同じ構成をしていても別の型として区別されます．タプルは
`.0` というように要素のインデックスを指定するか，要素の分解を使います．


``` 
struct Color(i32, i32, i32);
struct Point(i32, i32, i32);

fn main() {
    let black = Color(0, 0, 0);
    let Point (x,y,z) = Point(0, 0, 0);
    
    println!("{} {} {}", black.0, black.1, black.2);
    println!("{} {} {}", x, y, z);
}
```


Rust
は静的型付け言語です．この特性を利用して既存の型から新しい型を作成することで意図的な意味を付加させて，制約することが出来ます．また，既存の型を利用するので薄いラッパー型と考えることも出来ます．これは
**Newtype**
パターンと呼ばれるもので，タプル構造体を利用する例の１つです．\
例えば， `String` 型から `Password` 型を作成し， `{}`
で出力したときに伏せ字にする場合は次のようになります．


``` 
use std::fmt;

struct Password(String);

impl fmt::Display for Password {
    fn fmt(&self, f: &mut fmt::Formatter<'_>) -> fmt::Result {
        write!(f, "{}", self.0.chars().map(|_| '*').collect::<String>())
    }
}

fn main() {
    let a = String::from("123456789");
    println!("{}", a); // 123456789
    
    let a = Password(String::from("123456789"));
    println!("{}", a); // *********
}
```


## 📌 ユニット構造体

`()`
のことをユニットと言いました．このようなフィールドを何も持たない構造体のことを
**ユニット構造体** （Unit-like
Structs）と言います．（日本語ドキュメントだとユニット様構造体と翻訳されていますが，ユニット構造体の方が言いやすいし意味も伝わるでしょう）．ユニット構造体はフィールドを持たず，トレイトだけ実装するといった時に使われるようです．

## 📌 メソッド

**メソッド** は関数に似ていますが，構造体と関連していて， `self`
を使うことで，そのメソッドを呼び出したオブジェクトを操作することが出来ます．メソッドの第一引数は必ず
`self` になります．また，基本的に不変参照 (`&self`) か可変参照
(`&mut self`)
になります．もちろん，可変参照のメソッドは，呼び出し元が可変の所有権を使って呼び出さなければなりません．メソッドは
`impl` ブロックの中で，関数と同じく `fn` を使って定義します．


``` 
struct Rectangle {
    width: u32,
    height: u32,
}

impl Rectangle {
    fn area(&self) -> u32 {
        self.width * self.height
    }
}

fn main() {
    let rect1 = Rectangle { width: 30, height: 50, };

    println!("The area of the rectangle is {} square pixels.", rect1.area());
}
```


`impl`
ブロックは複数定義することが出来ます．トレイトごとに実装を分けたりすることが出来ます．


``` 
impl Rectangle {
    fn area(&self) -> u32 {
        self.width * self.height
    }
}

impl Rectangle {
    fn can_hold(&self, other: &Rectangle) -> bool {
        self.width > other.width && self.height > other.height
    }
}
```



メソッドの第一引数が参照ではなく `self`
の場合があります．これは呼び出し元のオブジェクトの所有権をメソッドが受け取ります．つまり，このメソッドを呼び出したとき，呼び出し元のオブジェクトが束縛されていたら，それは解除され使用できなくなるということです．これはメソッド呼び出しによってオブジェクトが別のものに変換するといったときに使われるようです．例えば，後に出てくる
`Option` や `Result` の `unwrap` というメソッドは `unwrap(self)` です．


## 📌 関連関数

`impl` ブロックの中で関数を定義することが出来ます．それは `self`
を引数に取りません．このような関数を **関連関数**
と呼びます．これは構造体に関連しているにも関わらず，そのオブジェクトが無くても呼び出すことが出来ます．関連関数は主にその構造体のオブジェクトを生成する関数の定義に使い，そのような関連関数には
`new` という名前が使われます．関連関数は構造体の名前に `::`
を使って呼び出します．


``` 
struct Point {
    x: f64,
    y: f64,
}

impl Point {
    fn new(x: f64, y: f64) -> Self { // Self は実装している型の型エイリアス
        Self { x, y }
    }
}

fn main() {
    let a = Point::new(3., 5.);

    print!("x={}, y={}", a.x, a.y);
}
```





# 列挙型

## 📌 列挙型

**列挙型**
は取りうる様々な値を列挙しておき，そのうちのどれか１つだけ値を取るデータ型です．列挙した値のことを
**列挙子** （variant）と呼びます．構造体がフィールドの集合に対して `AND`
の関係であると考えれば，列挙型は `OR` の関係にあると言えます．列挙型は
`enum` を使って定義し，列挙子は `::` で指定します．


``` 
enum IpAddrKind {
    V4,
    V6,
}
let four = IpAddrKind::V4;
let six = IpAddrKind::V6;
```


列挙子はそれぞれ別々の型にすることが出来ます．


``` 
enum IpAddr {
    V4(u8, u8, u8, u8),
    V6(String),
}

let home = IpAddr::V4(127, 0, 0, 1);
let loopback = IpAddr::V6(String::from("::1"));
```


列挙型は，構造体のようにメソッドを定義することも出来ますし，トレイトのインスタンスにもなることが出来ます．




# ジェネリクス

## 📌 ジェネリクス

Rust
では，例えば数値演算をするときに，左値と右値の型が同じである必要があります．ここで，加算を行う
`add`
という関数を考えてみます．数値型には整数型や浮動小数点型などあります．型の数だけ
`add`
関数を定義してしまうと同じコードが大量に出来てしまいます．そこで，引数の型が変わっても関数本体のコードが変わらない場合は，任意の型を受け取れる関数を定義することでコードの重複を避けることが出来ます．このような仕組みを
**ジェネリクス** と言い，任意の型のことを **ジェネリック型**
と言います．

関数，構造体，列挙型でジェネリック型を使うには，それぞれの名前の後ろに
`<>` でジェネリック型の名前を指定します．名前には慣例的に `T`
をよく使います．また，複数であれば， `,` で列挙します．


``` 
fn add<T: std::ops::Add<Output=T> >(a: T, b: T) -> T {
    a+b
}

struct Point<T> { x: T, y: T }

enum Result<T,E> {
    Ok(T),
    Err(E),
}
```


メソッドの定義では次のように記述します．


``` 
struct Point<T> { x: T, y: T }

impl<T> Point<T> {
    fn xy(self) -> (T, T) {
        (self.x, self.y)
    }
}
```


`impl` の後ろに `<T>` を宣言しています．こうすることで `Point<T>` の `T`
がジェネリック型であることを明示しています．もし， `impl<T>`
でなければ， `Point<T>` の `T` はジェネリック型ではなく `T`
という名前の型を指定することになってしまいます．これとは逆に，ジェネリック型に明示的な型を指定するやり方があります．


``` 
impl Point<f64> {
    fn distance(&self) -> f64 {
        (self.x.powi(2) + self.y.powi(2)).sqrt()
    }
}
```


ジェネリック型は任意の型を受け取りますが，静的型付け言語では，コンパイル時に型がわかるので，型に特化したコードが生成されます．このような仕組みを
**単相化** （monomorphzation）と言います．

Rust
は強い型推論があるので，ジェネリック型に対して適切な型を自動で推論してくれます．しかし，明示的に指定したい場合もあります．この場合は
`::<...>`
演算子を使います．この演算子は魚が速く泳いでいるように見えることから
**turbofish** と呼ばれています．


``` 
let point = Point::<f64>{x: 3., y: 5.};
```





# Option

## 📌 Option

Rust には無効な値を取ることができる便利な列挙型として `Option`
があります． `T` はジェネリック型です．


``` 
enum Option<T> {
    Some(T),
    None,
}
```


`Option` 型に有効な値を束縛するときは `Some`
を使います．また，無効な値を束縛するときは `None` を使います．


``` 
let some_number = Some(5);
let some_string = Some("a string");
let absent_number: Option<i32> = None;
```


`Option`
型のオブジェクトから値を取り出すには，この後に説明するパターンマッチングか，
`unwrap` などのメソッドを使います．




# パターンマッチング

## 📌 match 式

**パターンマッチング**
は，式の値がパターンに一致するかしないかを判定する仕組みです． `match`
式は，パターンマッチングによって評価する式を変えるときに使います．


``` 
enum Coin {
    Penny,
    Nickel,
    Dime,
    Quarter,
}

fn value_in_cents(coin: Coin) -> u8 {
    match coin {
        Coin::Penny => 1,
        Coin::Nickel => 5,
        Coin::Dime => 10,
        Coin::Quarter => 25,
    }
}
```


`match` 式はパターンと式を `=>` で結合したものを並べたものです．この
`パターン => 式` のことを **アーム** （arm）と言います． `match`
式はアームのパターンを順番に処理していき，最初にパターンに一致した式を評価してその結果を返します．そして，パターンに一致したアーム以降は処理されません．このような仕組みを短絡評価またはショートサーキットと呼びます


``` 
fn plus_one(x: Option<i32>) -> Option<i32> {
    match x {
        None => None,
        Some(i) => Some(i + 1),
    }
}

let five = Some(5);
let six = plus_one(five);
let none = plus_one(None);
```


`match`
式はマッチング対象のオブジェクトが取りうる値をすべて網羅しなければなりません．そのため，記述したアーム以外に一致する
**ワイルドカード** （`_`）を使うことができます．


``` 
let some_u8_value = 0u8;
match some_u8_value {
    1 => println!("one"),
    3 => println!("three"),
    5 => println!("five"),
    7 => println!("seven"),
    _ => (),
}
```


`Option` 型が束縛しているオブジェクトを `match`
式で取り出すことが出来ます．ここで注意なのが， `match`
式でパターンが一致したときに，束縛しているオブジェクトを受け取りますが，そのとき所有権も移動しているということです．


``` 
fn main() {
    let a: Option<String> = Some(String::from("hello"));
    match a {
        Some(x) => println!("{}", x), // move ownership
        None => ()
    }
    println!("{:?}", a);
    //               ^ value borrowed here after partial move
    // error[E0382]: borrow of partially moved value: `a`
}
```


これは何が起きているかと言うと，変数 `a` が束縛している `Option`
型のオブジェクトが，内部で束縛しているオブジェクトの所有権をアームのパターンによって取り出され所有権が渡されています．これにより，変数
`a`
は束縛したままですが，その内部では何も束縛していないことになります．なので，部分移動（partial
move）が発生していることになりエラーとなります．この部分移動に対応する方法として次の２つがあります．

１つはアームのパターンでオブジェクトを参照で受け取る方法です．注意なのが，パターンで参照を取得するときは
`ref` を使います．可変参照なら `ref mut` です．


``` 
fn main() {
    let a: Option<String> = Some(String::from("hello"));
    match a {
        Some(ref x) => println!("{}", x), // reference
        None => ()
    }
    println!("{:?}", a); // borrow check!! - OK
}
```


もう１つは，返り値としてオブジェクトを返すことです．


``` 
fn main() {
    let a: Option<String> = Some(String::from("hello"));
    let a = match a {
        Some(x) => { println!("{}", x); Some(x) }
        None => None,
    };
    println!("{:?}", a); // borrow check!! - OK
}
```


## 📌 パターンによる変数束縛

変数に束縛するときにパターンを使って分解出来ることを覚えていますか？\
この分解束縛のパターンでも参照を使うことが出来ます．


``` 
struct Account { name: String, pass: String }

fn main() {
    let a = Account { name: String::from("name"), pass: String::from("pass") };
    let Account { name, pass } = a;    // move ownership
    println!("{} {}", name, pass);     // borrow check!! - OK
    println!("{} {}", a.name, a.pass); // borrow check!! - Error
}
```


上記のコードはパターンによる分解束縛時に所有権も移動してしまい，借用チェックでコンパイルエラーになります．その場合は，パターンに
`ref` を使って不変参照で受け取ることで借用チェックに通ることになります．


``` 
struct Account { name: String, pass: String }

fn main() {
    let a = Account { name: String::from("name"), pass: String::from("pass") };
    let Account { ref name, ref pass } = a; // reference
    println!("{} {}", name, pass);     // borrow check!! - OK
    println!("{} {}", a.name, a.pass); // borrow check!! - OK
}
```


## 📌 if let 式

match 式のアーム（ワイルドカード以外）が１つのときは `if let`
式を使うと短く記述することが出来ます．例えば次のコードを見てください．


``` 
let some_u8_value = Some(0u8);
match some_u8_value {
    Some(3) => println!("three"),
    _ => (),
}
```


`if let` 式を使うと次のように短く記述することが出来ます．


``` 
if let Some(3) = some_u8_value {
    println!("three");
}
```


`if let` と同様に `while let` も使うことが出来ます．

## 📌 マッチガード

**マッチガード** は `match` 式のアームのパターンに，さらに `if`
条件を加えることができるものです．これにより，より複雑なパターンを扱えます：


``` 
let num = Some(4);

match num {
    Some(x) if x < 5 => println!("less than five: {}", x),
    Some(x) => println!("{}", x),
    None => (),
}
```





# エラー処理

## 📌 panic!

基本的に復帰不能なエラーが発生したら，どうしようも出来ません．メッセージを表示してプログラムを終了する手っ取り早い方法が
`panic!` です


``` 
fn main() {
    panic!("crash");
}
```


## 📌 Result 型

どこかでエラーが発生したとしても，すぐにプログラムを終了させるわけにはなかなかいきません．ある関数の内部でエラーが発生したら，それを呼び出し元に知らせる必要があります．そこで
`Result` 型が使われます．


``` 
enum Result<T, E> {
    Ok(T),
    Err(E),
}
```


ここではファイル処理を考えてみます．既存のファイルを開いて処理をしたいとします．もし，ファイルが無ければ作成します．その場合，最初にファイルを開こうとしたときにエラーが発生し，そのエラーがファイルが無かったことを表していればファイルを新規に作成するようにします．ファイルを開く処理
`File::open` は `std::io::Result` 型を返します．これは
`Result<T, Error>` 型の別名です．


``` 
use std::{fs::File, io::ErrorKind};

fn main() {
    let f = File::open("hello.txt");
    let f = match f {
        Ok(file) => file,
        Err(ref error) if error.kind() == ErrorKind::NotFound => {
            match File::create("hello.txt") {
                Ok(fc) => fc,
                Err(e) => panic!("Tried to create file but there was a problem: {:?}", e),
            }
        },
        Err(error) => {
            panic!("There was a problem opening the file: {:?}", error)
        },
    };
}
```


## 📌 unwrap, expect

`Option` 型， `Result` 型ともに，値を取り出す `unwrap`
という関数があります．これは，もし値が `None`， `Err` のときに，
`panic!` を呼び出します．


``` 
pub fn unwrap(self) -> T
```


`unwrap` が `panic!`
を呼び出すと，標準のエラーメッセージが表示されますが， `unwrap`
の代わりに `expect`
を呼ぶと，エラーメッセージに情報を追加することが出来ます．


``` 
pub fn expect(self, msg: &str) -> T
```


`Option` 型と `Result` 型の `unwrap` は以下のように `match`
式を短くしたものです．


``` 
option.unwrap()
//
// ↓
//
match option {
    Some(v) => v,
    None => panic!(...),
}
```



``` 
result.unwrap()
//
// ↓
//
match result {
    Ok(v) => v,
    Err(e) => panic!(...),
}
```


## 📌 エラー伝搬

`Option` 型， `Result` 型を返す関数の中で，値が `None` または `Err`
のときに，処理を中断して呼び出し元に値を返す仕組みが用意されています．それは
`?` 演算子を使います．


``` 
fn hoge() -> Option<i32> {
    let a = Some(10);
    let b = a?;
    Some(b)
}
```



``` 
fn hoge() -> Option<i32> {
    let a = None;
    let b = a?; // return Option<i32>::None
    Some(b)
}
```


## 📌 コンビネータ

`Option` 型， `Result` 型も **コンビネータ**
です．このコンビネータがエラー処理のコードを大幅に削減してくれます．手続き型であれば，１つ１つの関数呼出しの結果がエラーか無効な値かを確認していきます．これだと，確認コードが大量に出来てしまいます．そこで，まずはエラー伝搬です．関数が
`Option` か `Result` を返せば， `?`
演算子を使ってチェーン方式で処理を記述することが出来ます．途中でエラーが発生すれば，処理を打ち切ってエラー伝搬されます．


``` 
let ret = open()?.read()?.replace()?.write()?.close()?;
```


コンビネータとは簡単に言うと， **高階関数**
のことで，高階関数とは関数を引数に取る関数のことです．例えば，関数 f(x)
と g(x)，これらの合成関数が (f\\circ g)(x) = f(g(x))
とします．この場合，この \\circ
がコンビネータで，２つの関数を取っています．先程の
`open.read.replace.write.close` で考えてみると
`close(write(replace(read(open()))))` の関係に見えないでしょうか．ここで
`.` 演算子がコンビネータであり，その役を担っているのが `Option` 型と
`Result` 型と考えることが出来ます．

`Option` 型， `Result`
型にはコンビネータとしての便利なメソッドが多く用意されています．基本的なものとして，
`map` は値に関数を適用して，その結果をコンビネータに変換します．


``` 
pub fn map<U, F: FnOnce(T) -> U>(self, f: F) -> Option<U>     // Option
pub fn map<U, F: FnOnce(T) -> U>(self, op: F) -> Result<U, E> // Result
```


`and_then` は関数を適用して，その結果をそのまま返します．つまり，
`and_then` に渡す関数はコンビネータを返します．


``` 
pub fn and_then<U, F: FnOnce(T) -> Option<U>>(self, f: F) -> Option<U>        // Option
pub fn and_then<U, F: FnOnce(T) -> Result<U, E>>(self, op: F) -> Result<U, E> // Result
```


コンビネータは型を合わせる必要があります． `Option`
のメソッドに渡す関数は．単純に `T` 型を返す関数や `Option`
を返す関数ならよいのですが， `Result`
を返す場合にはそのままでは利用できません．そこで， `Option` と `Result`
には相互に変換するメソッドがいくつかあります．例えば， `ok_or` は
`Option` から `Result` に， `ok` は `Result` から `Option`
に変換します．これにより `Option` や `Result`
を返す関数を１つのメソッドチェーン内に利用することが出来ます．

コンビネータは `?` 演算子を使っていなければ，途中の処理で `None`
になったり， `Err`
になった場合，チェーンの最後の型で返ってきます．これによりエラー処理を書く場所が少なくなります．

構造体のメソッドのところでも少し触れましたが，コンビネータのメソッドの引数は
`self` が多いです．これは，メソッド呼び出しで， `Option<u32>` が
`Option<f32>` になったり， `Option<T>` が `Result<T,E>`
になったり型の変換を行っているからです．




# トレイト

## 📌 トレイトとは

すでにトレイト，コピートレイト，トレイト境界について触れていますが，ここでさらに詳しく解説します．まずは，おさらいです．
**トレイト**
（trait）はデータ型を分類する仕組みのことです．また，ジェネリック型に
**トレイト境界** を指定することで，その型が特定のトレイトの
**インスタンス**
であることを制約します．さらに，トレイトには特有のメソッドを実装することが出来，型に対して共通の振る舞いを定義することが出来ます．つまり，あるトレイトのメソッドは，そのインスタンスであれば呼び出せることになります．また，インスタンスによってその振る舞いの実装を変えることも出来ます．

トレイトを定義するには `trait`
を使います．トレイト名を指定して，ブロック内に共通のメソッドを定義します．このメソッドはインスタンス側で実装しなければなりませんが，トレイト側で実装することも出来ます．この場合は，インスタンス側はトレイト側の実装をそのまま使うことも出来ますし，その振る舞いを上書き（
**オーバーライド** ）することも出来ます．


``` 
pub trait Geometry {
    fn area(&self) -> f64;
    fn name(&self) -> &str { return "Geometry" }
}
```


トレイトの実装は `impl A for B` で指定します．ここで `A`
にはトレイト名を， `B` には実装する型を指定します．


``` 
impl Geometry for Rectangle {
    fn area(&self) -> f64 {
        self.width as f64 * self.height as f64
    }
    fn name(&self) -> &str { return "Rectangle" }
}
```


`Geometry` トレイトを定義して， `Rectangle`, `Triangle`
というインスタンスを定義する場合は次のようになります．


``` 
pub trait Geometry {
    fn area(&self) -> f64;
    fn name(&self) -> &str { return "Geometry" }
}

struct Rectangle { width: u32, height: u32 }

impl Geometry for Rectangle {
    fn area(&self) -> f64 {
        self.width as f64 * self.height as f64
    }
    fn name(&self) -> &str { return "Rectangle" }
}

struct Triangle { bottom: u32, height: u32 }

impl Geometry for Triangle {
    fn area(&self) -> f64 {
        self.bottom as f64 * self.height as f64 * 0.5
    }
    fn name(&self) -> &str { return "Triangle" }
}

fn main() {
    let a = Rectangle { width: 10, height: 20 };
    let b = Triangle  { bottom: 20, height: 5 };
    println!("{} area={}", a.name(), a.area());
    println!("{} area={}", b.name(), b.area());
}
```


## 📌 トレイト継承

トレイトは別のトレイトのインスタンスになることが出来ます．これを
**継承** と呼ぶこともあります． `trait 継承先 : 継承元`
という形で指定します．継承したインスタンスは継承元のトレイトも実装する必要があります．


``` 
pub trait Geometry {
    ...
}

pub trait Drawable: Geometry {
    ...
}

impl Geometry for Rectangle {
    ...
}

impl Drawable for Rectangle {
    ...
}
```


トレイトのインスタンスを表すには `impl A` のようにします． `A`
はトレイト名です．次の関数の引数 `geometry` は `Geometry`
のインスタンスでなければなりません．これがトレイト境界です．


``` 
fn draw(geometry: &impl Geometry) {
    ...
}
```


トレイト境界の指定はより便利な方法があります：


``` 
fn draw<T: Geometry>(geom1: &T, geom2: &T) {
    ...
}
```


また，トレイトは `+` を使って複数指定することが出来ます：


``` 
fn draw(geometry: &(impl Geometry + Display))
fn draw<T: Geometry + Display>(geometry: &T)
```


他にも `where` を使って次のように書くことも出来ます：


``` 
fn draw<T>(geometry: &T)
    where T: Summary + Display
```


ジェネリック型にもトレイト境界を指定することが出来ます．次のコードでは，
`Display` と `PartialOrd` のインスタンスの場合なら， `cmd_display`
メソッドが実装されます．


``` 
use std::fmt::Display;

struct Pair<T> { x: T, y: T }

impl<T> Pair<T> {
    fn new(x: T, y: T) -> Self {
        Self { x, y }
    }
}

impl<T: Display + PartialOrd> Pair<T> {
    fn cmp_display(&self) {
        if self.x >= self.y {
            println!("The largest member is x = {}", self.x);
        } else {
            println!("The largest member is y = {}", self.y);
        }
    }
}
```


## 📌 derive属性

これまでいくつかのトレイトを見てきました．実際には多くのトレイトがあり，そして，型は多くのトレイトのインスタンスになっています．トレイトのインスタンスにするには
`impl`
で実装しなければならず，とても面倒です．そこで，規定の実装をしてくれる機能が用意されています．それが
`derive` 属性です．実装したいトレイトを型の定義時に
`#[derive(trait, …)]` という形で指定します．


``` 
#[derive(Debug, Copy, Clone)]
pub struct Vec3 {
```


以下は `derive` 属性でよく使われるものです：

  |属性     |         説明|
  |:-- |:--|
  |Copy |             所有権の移動をせずに，複製を作成するマーカートレイト|
  |Clone |            オブジェクトの複製（ディープコピー）を作成できる|
  |Debug  |           `{:?}` で出力できる|
  |PartialEq, Eq|     `==`, `!=` が使える．Eq はマーカートレイト．|
  |PartialOrd, Ord |  `<`, `>`, `<=`, `>=` が使える．Ord は順序付けができる．|

## 📌 From トレイト

ある型から別の型に変換するときに，便利な `From`
トレイトというのがあります． `from`
メソッドを対応した型ごとに実装することで，その型から `into`
メソッドで変換することが出来ます．


``` 
#[derive(Debug)]
struct Point { x: f64, y: f64 }

impl From<f64> for Point {
    fn from(input: f64) -> Self {
        Point { x: input, y: input }
    }
}

fn main() {
    let p1 = Point::from(1.0);
    let p2: Point = (1.0).into();
    println!("{:?} {:?}", p1, p2);
}
```





# RAII

## 📌 RAIIとは

**RAII** (Resource Acquisition Is Initialization)
とはリソースの確保をオブジェクトの初期化時に行い，リソースの開放をオブジェクトの破棄と同時に行う手法です．これから解説する内容は公式だとスマートポインタと呼ばれていますが，安易にポインタという用語を使うべきでないと思っているし，RAII
はポインタに限った話でもないので本書では使いません．

## 📌 Deref トレイト

実は，Rust の **参照** は RAII
の最も代表となる１つです．参照は仮の所有権を保持し，スコープから外れると仮の所有権を破棄します．参照の機能は大きく２つあります．参照先のオブジェクトを操作できること，参照先のオブジェクトの仮の所有権を破棄することです．このうち，参照先のオブジェクトを操作するには
**参照外し** が必要です．これを実現しているのが `Deref`
トレイトです．参照外しは参照に対して `*`
演算子を使います．このように，RAII
におけるリソースに対して操作をするには `Deref` トレイトを実装し `*`
演算子を使うことです．また，可変参照に対しては `DerefMut`
トレイトを実装します．

## 📌 Drop トレイト

参照のもう１つの機能が仮の所有権の破棄です．これは `Drop`
トレイトで実装します． `Drop`
トレイトのインスタンスのオブジェクトは，それが破棄されるときに `drop`
メソッドが呼ばれます．このメソッドでリソースの開放処理を行います．
`drop` メソッドは可変参照を引数に取ります．


``` 
impl Drop for Resource {
    fn drop(&mut self) {
        ...
    }
}
```


`drop`
メソッドは基本的にオブジェクトが破棄されるときに自動で呼び出されますが，明示的に呼びたい場合があるかもしれません．その場合は，
`std::mem::drop`
関数で強制的に呼び出してオブジェクトを破棄することが出来ます．ただし，あまり使うべきではありません．

## 📌 メモリ

Rust では次の３つのメモリ領域があります．１つ目は **データメモリ**
で，静的データが格納されています．静的データはプログラム実行中に存在するデータのことです．２つ目は
**スタックメモリ**
です．これは変数や関数呼び出し時の引数など一時的な格納場所で，コンパイラが最適化しやすく高速にデータ操作が出来ます．３つ目は
**ヒープメモリ**
です．ここにはプログラム実行中に利用できるメモリで，スタックメモリよりも大きなサイズを利用することが出来ます．ただし，利用するにはオーバーヘッドがかかります．また，スタックメモリのサイズはヒープメモリに比べてかなり限られているので，ヒープメモリを積極的に利用することになります．

## 📌 Box

これまで，メモリを意識してきませんでした．基本的に作成したオブジェクトはスタックメモリに置かれます．また，`static`
に指定したオブジェクトや文字列リテラルなどはデータメモリに置かれます．では，ヒープメモリに置くにはどうすればよいでしょうか．それが
`Box<T>` です．使い方は簡単で， `Box::new` または `Box::<T>::new`
にオブジェクトを渡すだけです．


``` 
let a = Box::new(10);        // type inference
let a = Box::<i32>::new(20); // explicit type
let a = 30;                  // immutable object
let b = Box::new(a);         // move object from stack memory to heap memory
let c = *b;                  // dereference
```


この図，覚えてますか？

![rust-onwership01](https://storage.googleapis.com/zenn-user-upload/ym0o15tj4kbs3tyrqqow30n9bp3h)

`Box` を表すと...

![rust-box](https://storage.googleapis.com/zenn-user-upload/e4k4iftu64ii5e3phhey858mnjnn)

## 📌 Rc

**Rc** (Reference Count) とは **参照カウンタ**
のことです．原本の所有権を束縛できるのは１つだけです．参照を使えば，仮の所有権を作成することができます．しかし，参照は制約が強いです．同じオブジェクトを複数から束縛することは出来ないのでしょうか．それを可能にするのが参照カウンタで，
`Rc<T>` です． `Rc`
は原本または仮の所有権を保持することが出来ます．基本的な機能としては参照と変わらず，仮の所有権を作成します．ただし，
`&` 演算子ではなく `clone` というメソッドです．


``` 
use std::rc::Rc;

let a = Rc::new(10);
let b = a.clone();
```


この `clone` メソッドはディープコピーの `clone`
と勘違いしやすいため，関連関数の `clone` を使うほうが良いらしいです．


``` 
use std::rc::Rc;

let a = Rc::new(10);
let b = Rc::clone(&a);
```


通常は，原本の所有権を束縛した変数が破棄されるときは，仮の所有権を持った変数は存在してはいけません．しかし，
`Rc` の場合は，原本の所有権を束縛した変数が破棄されたときに， `clone`
で作成した仮の所有権を束縛した変数が存在することができます．このとき，オブジェクトは破棄されず，すべての仮の所有権を束縛した変数が破棄されたときにオブジェクトが破棄されます．

また，この図が出てきました．

![rust-onwership01](https://storage.googleapis.com/zenn-user-upload/ym0o15tj4kbs3tyrqqow30n9bp3h)

`Rc` を表すと...

![rust-rc01](https://storage.googleapis.com/zenn-user-upload/732u6h6cky7nwrstwqmfe2bums9w)

`Rc` はオブジェクトをヒープメモリに置きます．なので， `Box`
の代わりに使うことができます．


``` 
use std::rc::Rc;

fn main() {
    let a = Rc::new(10);
    let b = Rc::clone(&a);
    println!("{} {}", a, b);
}
```





# 内部可変性

## 📌 内部可変性

Rust
には制限付きで，不変オブジェクトを安全に可変にする方法が用意されています．この実装は内部可変性パターン（Interior
mutability）と呼ばれるものが使われています．ここでは，詳しく説明しませんが，内部的には
`unsafe` で実装されています．この機能を使うには `Cell`, `RefCell`
を使います．まずは， `Rc` について考えながら `Cell`, `RefCell`
の使い方を見ていきます．

`Rc`
は内部で参照している数を保持することで所有権を共有しています．その数は
`Rc::strong_count` で取得することができます．


``` 
use std::rc::Rc;

fn main() {
    let a = Rc::new(10);        // shared reference to immutable object
    dbg!(Rc::strong_count(&a)); // Rc::strong_count(&a) = 1

    let b = Rc::clone(&a);      // cloned shared reference
    dbg!(Rc::strong_count(&a)); // Rc::strong_count(&a) = 2
    dbg!(Rc::strong_count(&b)); // Rc::strong_count(&b) = 2
}
```


`Rc::clone`
を呼び出すことで，参照カウンタの値が増えていることがわかります．ここで，変数
`a`
は不変にもかかわらず，内部で保持している参照カウンタの値が変わっていることになります．通常は不変束縛の変数から可変参照を作ることができません．
`Rc::clone`
は不変参照を引数に取っているので，内部の参照カウンタを変更することが出来ないはずです．


``` 
pub fn clone(&self) -> Self
```


そこで，内部可変性です．不変・可変の検査はコンパイル時に行われますが，内部可変性を使うと実行時（ランタイム時）に行われるようになり，制約が緩くなります．とはいえ，好き勝手に値を変えられては困るので，
`Cell` や `RefCell`
型にその機能をまとめて正当性を保つようになっています．ちなみに内部的には
`UnsafeCell` というものを使って実装されています．\
`Cell` の使い方は `Cell::new` で作成し， `get`, `set` で操作します．


``` 
use std::cell::Cell;

fn main() {
    let a = Cell::new(10); // immutable object with interior mutability
    dbg!(a.get()); // a.get() = 10
    a.set(20);
    dbg!(a.get()); // a.get() = 20
}
```


`replace` は値を置き換えて，以前の値を返します． `into_inner`
は内部の値を取り出します．（ `T` 型に型変換します）


``` 
fn main() {
    let a = Cell::new(10); // immutable object with interior mutability
    let b = a.replace(20);
    dbg!(a.get()); // a.get() = 20
    dbg!(b);       // b = 10
    
    let c = a.into_inner(); // turn Cell<T> into T
    dbg!(c);       // c = 20
    dbg!(a);       // borrow check - Error
}
```


例えば， `Rc` が内部で保持している参照カウンタを `RefCount` とした場合，
`Rc<T> = &(Cell<RefCount>, T)` と考えることができます．また， `Rc`
で共有しているオブジェクトを可変にしたい場合，次のようなコードは出来ません．


``` 
fn main() {
    let mut a = Rc::new(10); // shared reference to immutable object
    *a = 20; // Error
}
```


この場合は `Cell` を使います．


``` 
fn main() {
    let a = Rc::new(Cell::new(10));
    a.set(20);
    dbg!(a.get()); // a.get() = 20

    let b = Rc::clone(&a);
    b.set(30);
    dbg!(a.get()); // a.get() = 30
}
```


`Cell<T>` の大きな制約として， `T` は `Copy`
トレイト境界があることです．このため，参照版である `RefCell<T>`
があります． `RefCell` には不変参照を返す `borrow`, 可変参照を返す
`borrow_mut` メソッドがあり，それぞれ不変参照である `Ref`
型，可変参照である `RefMut` 型を返します．


``` 
pub fn borrow(&self) -> Ref<'_, T>;
pub fn borrow_mut(&self) -> RefMut<'_, T>;
```


`Ref`, `RefMut` には，通常の不変参照( `&` )，可変参照( `&mut`
)と同じ制約があります．ただし，この場合の借用チェックは実行時に行われ，その時に制約を満たしていなければ
`panic!` が呼ばれます．


``` 
use std::{rc::Rc, cell::RefCell};

fn main() {
    let a = Rc::new(RefCell::new(String::from("hoge")));
    dbg!(a.borrow()); // a.borrow() = "hoge"
    
    *(a.borrow_mut()) = String::from("foo");
    dbg!(a.borrow()); // a.borrow() = "foo"
    
    let b = Rc::clone(&a);
    *(b.borrow_mut()) = String::from("bar");
    dbg!(a.borrow()); // a.borrow() = "bar"
    
    let c = a.borrow_mut();
    let d = a.borrow_mut(); // panic!
}
```


`Ref`， `RefMut`
はRAIIの実装になっていて，複数の可変参照や不変と可変参照が同時に存在することが出来ないように検査しています．

ここまで，所有権を共有する `Rc` ，内部可変性を持つ `Cell` と `RefCell`
を見てきました．\
またまた，この図です．

![rust-onwership01](https://storage.googleapis.com/zenn-user-upload/ym0o15tj4kbs3tyrqqow30n9bp3h)

`Rc`, `Cell`, `RefCell` を表すと...

![rust-cell](https://storage.googleapis.com/zenn-user-upload/0j9x7co5ll9cs0xl1eztl55dq4qs)




# クロージャ

## 📌 クロージャとは

**クロージャ**
とは，簡単に言うと，変数に束縛できたり，関数の引数として渡すことのできる名前のない関数（無名関数）のことです．クロージャはその呼び出し元のスコープにある変数を
**キャプチャ**
することも出来ます．厳密に言うと，無名関数の中で束縛していない変数のことを自由変数と言い，自由変数をまとめた環境を無名関数のスコープ内に閉じこめたものをクロージャと呼びます．

クロージャは `||` で定義します．引数があれば `|param1, param2|` のように
`||` の間に入れます．その後に `{}`
で本体を記述します．本体が式１つだけなら `{}`
を省略することが出来ます．次のコードは関数とそれと同じ振る舞いをするクロージャの例です．


``` 
fn  add_one_v1   (x: u32) -> u32 { x + 1 }
let add_one_v2 = |x: u32| -> u32 { x + 1 };
let add_one_v3 = |x|             { x + 1 };
let add_one_v4 = |x|               x + 1  ;
```


クロージャはそれぞれ独自（unique）の型を持っています．クロージャは `Fn`,
`FnMut`, `FnOnce` トレイトのどれかのインスタンスです．それぞれ `&self`,
`&mut self`, `self`
を内部的に引数として受け取っているかどうかの違いがあります．また， `Fn`
は `FnMut` を， `FnMut` は `FnOnce` を継承しています．

自由変数をまとめた環境をどのように扱うかで，どのトレイトのインスタンスになるかが決まります．まず，すべてのクロージャは必ず
`FnOnce`
のインスタンスになります．そして，無名関数の中で環境から所有権を移動することがなければ（可変参照は出来る），
`FnMut`
のインスタンスになります．さらに，環境を変更しないのであれば，不変参照となるので
`Fn` のインスタンスになります．

自由変数が環境にまとめられるとき，自由変数が束縛しているオブジェクトがコピートレイトのインスタンスであれば，コピーが作成されます．もし，自由変数をクロージャの中だけで使用するということが分かっているならば，環境にまとめられるときに，コピーではなく所有権を移動することが出来ます．それを行うには，クロージャの前に
`move` を指定します．

## 📌 Fn と fn

`Fn` トレイトと `fn` というキーワードは別ものです． `fn`
は関数定義で使いますが， `fn` は型でもあります．そして， `fn` のことを
**関数ポインタ** と言います． `fn` は `Fn` のインスタンスなので，
`FnMut`, `FnOnce` のインスタンスでもあります．

## 📌 Sized トレイト

Rust
は静的型付け言語です．静的型の特徴の１つとして，型のサイズがコンパイル時に分かることです．しかし，コンパイル時にサイズがわからないこともあります．Rust
は型のサイズが分かっているとき，自動でその型を `Sized`
トレイトのインスタンスにします．Rust は型が `Sized`
トレイトのインスタンスであることを仮定し，それを制約します．つまり，関数の引数などは
`Sized`
トレイトのインスタンスでなければなりません．ジェネリック型も同じです．それに対して，例えば，
`str` 型は実行時にサイズが決まるので，そのような型のことを
**動的サイズ型** （Dynamically sized types: DST）といいます．

トレイトは `Sized`
トレイトの対象になりません．トレイトはデータ型の分類の仕組みであり，サイズは考慮していないからです．ここで，クロージャに話を戻します．クロージャはトレイトで実装されているので，コンパイル時にサイズがわからないのです．例えば，次のようにクロージャを返す関数はエラーになります．


``` 
fn returns_closure() -> Fn(i32) -> i32 {
    |x| x + 1
}
// error[E0277]: the trait bound `std::ops::Fn(i32) -> i32 + 'static:
// std::marker::Sized` is not satisfied
```


このような動的サイズ型をどうすれば `Sized`
トレイトのインスタンスにすることができるかということですが，参照（ `&`
）にするか， `Box` にするかです．例えば， `Box`
を使えばクロージャを次のように返すことが出来ます．


``` 
fn returns_closure() -> Box<Fn(i32) -> i32> {
    Box::new(|x| x + 1)
}
```


既に述べたように Rust は引数の型が `Sized`
であることを制約します．例えば次のようなコードがあります．


``` 
fn put<T: std::fmt::Debug>(a: &T) {
    println!("{:?}", a);
}

fn main() {
    put("hoge");
}
```


この `T` は文字列スライスである `str` で，関数 `put`
の引数は参照で受け取っています． `str`
は動的サイズ型なので参照を付けていますが，これはエラーになってしまいます．これは暗黙的に
`T: Sized` となっているためで，引数側に参照を付けても `T` が `Sized`
でなければなりません．しかし，引数側で参照を付けているので，コードとしては動的サイズ型を指定しても問題ありません．そこで，
`T` が動的サイズ型を受け入れられるように `?Sized`
を指定するこができます．


``` 
fn put<T: std::fmt::Debug + ?Sized>(a: &T) {
    println!("{:?}", a);
}

fn main() {
    put("hoge");
}
```


これでコンパイルが通ります．

## 📌 参照を返す関数

`str` 型は動的サイズ型です．このままでは `Sized`
にならないので，文字列スライスは `&str`
型です．クロージャを返すところでは参照を使わずに `Box`
を使いました．参照を使っても返すことができるのですが，関数から参照を返すときには
**ライフタイム**
（lifetime）というものを考慮しなければなりません．個人的にこのライフタイムは余程の理由がない限り扱うべきでないものと思っているので，本書では詳しく扱いません．なので，関数から参照を返すのは可能なかぎり避けましょう．また，構造体にも参照のフィールドを持つことも出来ますが，こちらもライフタイムが必要になってしまいます．

## 📌 静的と動的

Rust
は静的型付け言語にもかかわらず，動的サイズ型もサポートしているのが強みでもあります．これにより静的ディスパッチおよび動的ディスパッチの両方を実現することが出来ます．動的サイズ型は参照や
`Box`
を使うことで扱えることがわかりました．クロージャはトレイトであり，動的サイズ型であり，参照や
`Box`
を使うことでオブジェクトとして扱えるようになります．このようなオブジェクトを
**トレイトオブジェクト** といいます．

トレイトオブジェクトは，トレイトのメソッドのみ呼び出せることになります．トレイトオブジェクトは，そのトレイトのインスタンスであればどの型のオブジェクトでも置き換えることができます．このように，トレイトオブジェクトを扱う側は実際のオブジェクトの型を知らなくても，そのメソッドを呼び出せるということ，そしてオブジェクトの型によってメソッドの動作を変えることが出来ることになります．これらの仕組みを
**動的ディスパッチ** といいます．

ジェネリック型や `impl Trait`
で指定した型はコンパイル時に型が決まりますので静的です．この `Trait`
には任意のトレイト名を指定します．トレイトの型は `Sized`
ではないので，参照や `Box` で指定する必要があるのですが，静的である
`impl Trait` と区別しやすいように，動的であることを明示する `dyn`
が導入され， `dyn Trait` という型を使います．よって， `&dyn Trait` や
`&mut dyn Trait`, `Box<dyn Trait>` という形で利用します．

ここでクロージャを返す関数を振り返ってみます．動的と静的を区別するために
`dyn`
を指定するのですが，これは後から導入されたものなので，省略してもコンパイルは通ります．ただし，警告で付けるように促されるので，実際は次のようになります：


``` 
fn returns_closure() -> Box<dyn Fn(i32) -> i32> {
    Box::new(|x| x + 1)
}
```


実は `impl` を使うと簡単に静的として扱えます：


``` 
fn returns_closure() -> impl Fn(i32) -> i32 {
    |x| x + 1
}
```





# ライフタイム

## 📌 ライフタイム

**ライフタイム**
というのは参照が有効になるスコープのことです．参照は原本の所有権が存在している限り有効なもので，借用チェックによって厳密にチェックされます．元々，関数に渡すために参照で仮の所有権を渡して破棄してもらう仕組みなのに，それを関数の返り値として返すとはおかしな話です．Rust
はパフォーマンスを最優先しているので，仕方ないとは思います．返せたほうが便利なときもあるでしょう．Rust
の初期版では参照を使っているところは明示的にすべてライフタイムを指定する必要があったようですが，今はかなり緩和されました．

ライフタイムは `&` 演算子の後ろに指定します．慣例的に `a,b,c,…`
と指定します．


``` 
&i32        // a reference
&'a i32     // a reference with an explicit lifetime
&'a mut i32 // a mutable reference with an explicit lifetime
```


特別なライフタイムの１つに `‘static`
があります．これはプログラム実行中にずっと存在するライフタイムです．ライフタイムが
`‘static`
なオブジェクトはデータメモリに置かれます．例えば，文字列リテラルは
`‘static` なライフタイムを持っています．

ライフタイムを指定したコードは本当に見づらいので，なるべくライフタイムを指定するようなコードは書かないほうがいいとは思います．


``` 
impl<'i, 't, 'a, R, P, E: 'i> RuleListParser<'i, 't, 'a, P>
where
    P: QualifiedRuleParser<'i, QualifiedRule = R, Error = E>
        + AtRuleParser<'i, AtRule = R, Error = E>,
{
    pub fn new_for_stylesheet(input: &'a mut Parser<'i, 't>, parser: P) -> Self {
        // ...
    }
}
```





# 並列処理

## 📌 スレッド

最も基本的な並列処理はスレッドを作成することです．スレッドを作成するには
`thread::spawn` を使います．引数にはクロージャを指定します．


``` 
use std::thread;
thread::spawn(|| {
    // thread code
});
```


`thread::spawn` は `JoinHandle` 型を返します． `join()`
メソッドを呼び出すことで終了を待ちます． `join()` は `Result`
型を返します．


``` 
let handle = thread::spawn(|| {
    // thread code
});
handle.join().unwrap();
```


クロージャの環境をスレッド間で共有することは通常の方法では出来ません．コピーを作成できるなら，環境にコピーされますが，そうでないなら所有権を移動しなければなりません．その場合は
`move` を使います．


``` 
use std::thread;

fn main() {
    let v = vec![1, 2, 3];

    let handle = thread::spawn(move || {
        println!("Here's a vector: {:?}", v);
    });

    handle.join().unwrap();
}
```


複数のスレッド間で状態を共有するには **排他制御**
が必要です．これを行うために `Mutex` があります． `lock`
メソッドでリソースをロックします． `lock` メソッドは `LockResult`
型を返します．また， `LockResult` 型は RAII である `MutexGuard`
オブジェクトを束縛しているので，自動でロックを解除します．


``` 
use std::sync::Mutex;

fn main() {
    let m = Mutex::new(5);

    {
        let mut num = m.lock().unwrap();
        *num = 6;
    }

    println!("m = {:?}", m);
}
```


排他制御を行う `Mutex`
は出来ましたが，このオブジェクトをスレッド間で共有しなければなりません．所有権の共有は
`Rc` で出来ますが，これのマルチスレッド版である `Arc` を使います．


``` 
use std::sync::Arc;

fn main() {
    let counter = Arc::new(Mutex::new(0));

    for _ in 0..10 {
        let counter = Arc::clone(&counter);
        let handle = thread::spawn(move || {
            let mut num = counter.lock().unwrap();
            *num += 1;
        });
        ...
```


おや，またこの図が出てきました．

![rust-onwership01](https://storage.googleapis.com/zenn-user-upload/ym0o15tj4kbs3tyrqqow30n9bp3h)

マルチスレッド版の `Rc` である `Arc`，排他制御を行う `Mutex`
の関係を表すと...

![rust-arc](https://storage.googleapis.com/zenn-user-upload/qwzx4e8of0842gq6ul8drqegepmn)

## 📌 Send + Sync

マルチスレッドではオブジェクトの所有権の操作を考慮する必要があります．オブジェクトの所有権がスレッド間で移動できる場合は，
`Send` マーカートレイトのインスタンスになります． **マーカートレイト**
とは，メソッドを持たないトレイトのことで，トレイト境界に使うためのものです．
`Sized`
トレイトもマーカートレイトの１つです．次に，複数のスレッドから安全に参照できる場合は
`Sync` マーカートレイトのインスタンスになります．これは参照 `&T` が
`Send` ならば， `T` 型は `Sync`
であり，参照が別のスレッドに送ることができるという意味になります．

ほとんどのプリミティブ型は `Send+Sync` です．また， `Sync`
であるデータ型で構成された型は，それもまた `Sync`
です．これは自動的にそれぞれのインスタンスになります．これらを手動で実装するのは安全ではありません．マルチスレッドに対応していない
`Rc` は `Send` でもなく， `Sync` でもありません（かわりに `!Send` や
`!Sync` の非実装マーカートレイトがつきます）．それに対して， `Arc` は
`Send+Sync` です．また， `Arc` が束縛する型もまた `Send+Sync`
である必要があります．もし， `Send+Sync` でないなら， `Mutex`
を利用します．

次の図は `Rc` と `Arc`
のドキュメントからの抜粋です．`Trait Implementations`
にありますが，新規に定義したデータ型などは基本的に `Send` と `Sync`
は自動的につくので `Auto Trait Implementations`
で確認することが出来ます．

![rust-send+sync-rc](https://storage.googleapis.com/zenn-user-upload/c3nzdj059wh9b5nwz0rwb8ww5z85)

![rust-send+sync-arc](https://storage.googleapis.com/zenn-user-upload/s9b3xgu8sf6a9wu48ojlmu2wm3pb)

## 📌 RwLock

排他制御を行うのは `Mutex` 以外に `RwLock` があります． `Mutex`
は常に１つのスレッドがリソースの操作をすることが出来ますが， `RwLock`
の場合は，不変参照だけなら複数のスレッドが同時にリソースをロックすることができ，可変参照のときだけ，１つのスレッドに制限するものです．他にアトミック変数というのもあります．これはプリミティブ型のみしか扱えませんが，
`Mutex` よりは高速に動作します．処理速度に問題がなければ基本的に `Mutex`
を使うのがいいでしょう． `RwLock`
やアトミック変数の詳細は公式リファレンスなどを参照してください．




# 所有権のまとめ

## 📌 所有権のまとめ

さて，この図に戻ってきました．

![rust-onwership01](https://storage.googleapis.com/zenn-user-upload/ym0o15tj4kbs3tyrqqow30n9bp3h)

といっても，今回が最後です．ここまで長かったですね．これまでの内容をまとめてみましょう．

![rust-ownership-final](https://storage.googleapis.com/zenn-user-upload/byn0wuekmq60gsibs3b1pne4u47w)




# マクロ

## 📌 マクロ

**マクロ**
はメタプログラミングの１つで，コードを展開してくれるものです．特に関数の可変長引数に対応していて，多用します．関数マクロは，関数の最後に
`!` 演算子が付いたものです．\
`print!`, `println!` は標準出力に文字列を出力するマクロです． `eprint!`,
`eprintln!` は標準エラーに文字列を出力します． `dbg!`
は式を評価してデバッグ表示してくれます． `unimplemented!`
は未実装を表し， `panic!` を起こします． `todo!`
も同じですが，ニュアンスが異なり，「まだ未実装」という意味です．\
マクロの機能は多いので，詳しくは公式ドキュメントなどを参照してください．




# イテレータ

## 📌 イテレータ

**イテレータ**
は連続したオブジェクトを順番に取り扱うための機能を提供するオブジェクトです．配列やスライス，後で解説する
**コレクション** でよく使います．イテレータは `Iterator`
トレイトのインスタンスです：


``` 
pub trait Iterator {
    type Item;
    fn next(&mut self) -> Option<Self::Item>;
    
    // methods with default implementations elided
}
```


ここで， `type Item` は **関連型** と呼ばれるもので，インスタンスはこの
`Item` 型を定義しなければなりません．

イテレータには多くの便利なメソッドが定義されています．いくつか紹介します．まずは
`zip`
です．これは別のイテレータを受け取って合成し，新しいイテレータを返します．要素はタプルになります．このようなイテレータから別のイテレータを作るメソッドは
**アダプタ** と呼ばれています．


``` 
let a1 = [1, 2, 3];
let a2 = [4, 5, 6];
let mut iter = a1.iter().zip(a2.iter());
```


`map` は各要素に関数を適用します：


``` 
let a = [1, 2, 3];
let mut iter = a.iter().map(|x| 2 * x);
```


`filter` は各要素に対して関数を適用し， `true`
を返した要素だけを取り出します：


``` 
let a = [0i32, 1, 2];
let mut iter = a.iter().filter(|x| x.is_positive());
```


`fold`
は状態を持ち，各要素に対して関数を適用して状態を更新し，その状態を返します：


``` 
let a = [1, 2, 3];
// the sum of all of the elements of the array
let sum = a.iter().fold(0, |acc, x| acc + x);
```


`collect` はイテレータの全要素をコレクションに変換します：


``` 
let a = [1, 2, 3];
let doubled: Vec<i32> = a.iter()
                         .map(|&x| x * 2)
                         .collect();
```


`enumerate` はインデックスと各要素のペアをタプルにします：


``` 
let a = ['a', 'b', 'c'];
let mut iter = a.iter().enumerate();
// (0, &'a'), (1, &'b'), (2, &'c')
```


`for_each`
は要素に関数を適用しますが，その関数は戻り値を返しません．また，
`for_each` メソッドはイテレータを返しません．それに対して， `inspect`
はイテレータを返します． `map` では `println!`
といったIO出力などの副作用が使えないので代わりに `inspect` を使います：


``` 
let a = [1, 4, 2, 3];
let sum = a.iter()
    .cloned()
    .inspect(|x| println!("about to filter: {}", x))
    .fold(0, |sum, i| sum + i);
println!("{}", sum);
```


コレクションなどイテレータを返すメソッドには `iter()`, `iter_mut()`,
`into_iter()` があります．それぞれ，引数に `&self`, `&mut self`, `self`
を受け取ります．




# コレクション

## 📌 コレクションとは

Rust
の標準ライブラリには便利な複数のオブジェクトを管理するデータ構造が用意されています．これらを
**コレクション**
と呼びます．コレクションはヒープメモリに置かれます．ここでは代表的なコレクションを解説します．

## 📌 Vec

ベクタ `Vec<T>` は伸縮可能な配列です．空のベクタを作成するには
`Vec::new` を使います：


``` 
let v: Vec<i32> = Vec::new();
```


初期値を指定してベクタを作成する場合は `vec!` マクロを使います：


``` 
let v = vec![1, 2, 3];
```


各要素を取り出して処理する一般的な方法は `for` 式を使います：


``` 
let v = vec![100, 32, 57];
for i in &v {
    println!("{}", i);
}
```


`Vec<T>` のメソッドの一部です：


``` 
insert(&mut self, index: usize, element: T)
remove(&mut self, index: usize) -> T
push(&mut self, value: T)
pop(&mut self) -> Option<T>
append(&mut self, other: &mut Vec<T>)
clear(&mut self)
len(&self) -> usize
is_empty(&self) -> bool
first(&self) -> Option<&T>
first_mut(&mut self) -> Option<&mut T>
last(&self) -> Option<&T>
last_mut(&mut self) -> Option<&mut T>
```


## 📌 String

**文字列** を表す `String` もコレクションです．内部では **UTF-8**
でエンコードされたデータです．文字列型には `OsString`, `OsStr`,
`CString`, `CStr`, `String`, `str`
などがあります．それぞれ，エンコード方式が違います． `String` と `str`
のようにペアになっており， `str` はスライスです．

文字列の生成は `String::new` です：


``` 
let mut s = String::new();
```


文字列以外の型から，文字列に変換するには `to_string`
メソッドが便利です．これは `Display`
トレイトのインスタンスなら自動で実装してくれます．


``` 
let i = 5;
let five = i.to_string();
```


文字列リテラルからの作成は `String::from` を使います：


``` 
let five = String::from("5");
```


文字列から数値型に変換するには `parse` を使います．これは `Result`
型を返します：


``` 
let a_string = String::from("5");
let b = a_string.parse::<i32>()?;
```


書式付きで文字列を作成するには `format!` マクロを使います：


``` 
let s1 = String::from("tic");
let s2 = String::from("tac");
let s3 = String::from("toe");
let s = format!("{}-{}-{}", s1, s2, s3);
```


`String` のメソッドの一部です：


``` 
push_str(&mut self, string: &str)
push(&mut self, ch: char)
pop(&mut self) -> Option<char>
as_bytes(&self) -> &[u8]
truncate(&mut self, new_len: usize)
insert(&mut self, idx: usize, ch: char)
insert_str(&mut self, idx: usize, string: &str)
remove(&mut self, idx: usize) -> char
len(&self) -> usize
is_empty(&self) -> bool
clar(&mut self)
chars(&self) -> Chars<'_>
bytes(&self) -> Bytes<'_>
starts_with<'a,P>(&'a self, pat: P) -> bool
ends_with<'a,P>(&'a self, pat: P) -> bool
find<'a, P>(&'a self, pat: P) -> Option<usize>
rfind<'a, P>(&'a self, pat: P) -> Option<usize>
trim(&self) -> &str
```


## 📌 HashMap

`HashMap<K,V>` は **連想配列**
です．オブジェクトにキーを結びつけて管理します．空の連想配列を作成するには
`HashMap::new` を使い，新しい要素を挿入する場合は `insert` を使います：


``` 
use std::collections::HashMap;

let mut scores = HashMap::new();

scores.insert(String::from("Blue"), 10);
scores.insert(String::from("Yellow"), 50);
```


キーに対応した要素を取得するには \`get を使います：


``` 
use std::collections::HashMap;

let mut scores = HashMap::new();
scores.insert(String::from("Blue"), 10);
scores.insert(String::from("Yellow"), 50);

let team_name = String::from("Blue");
let score = scores.get(&team_name);
```


各要素を取り出す場合は `for` 式で，キーとオブジェクトを分解束縛します：


``` 
use std::collections::HashMap;

let mut scores = HashMap::new();
scores.insert(String::from("Blue"), 10);
scores.insert(String::from("Yellow"), 50);

for (key, value) in &scores {
    println!("{}: {}", key, value);
}
```


キーがまだ存在していないときに挿入する場合は `entry` と `or_insert`
を使います：


``` 
use std::collections::HashMap;

let mut scores = HashMap::new();
scores.insert(String::from("Blue"), 10);
scores.entry(String::from("Yellow")).or_insert(50);
scores.entry(String::from("Blue")).or_insert(50);
println!("{:?}", scores);
```


２つのベクタから連想配列を作成するにはイテレータを使って， `zip`,
`collect` を使う方法があります：


``` 
use std::collections::HashMap;

let teams = vec![String::from("Blue"), String::from("Yellow")];
let initial_scores = vec![10, 50];

let mut scores: HashMap<_, _> =
    teams.into_iter().zip(initial_scores.into_iter()).collect();
```


`HashMap<K,V>` のメソッドの一部です：


``` 
keys(&self) -> Keys<'_, K, V>
values(&self) -> Values<'_, K, V>
values_mut(&mut self) -> ValuesMut<'_, K, V>
iter(&self) -> Iter<'_, K, V>
iter_mut(&mut self) -> IterMut<'_, K, V>
len(&self) -> usize
clear(&mut self)
entry(&mut self, key: K) -> Entry<'_, K, V>
contains_key<Q: ?Sized>(&self, k: &Q) -> bool
insert(&mut self, k: K, v: V) -> Option<V>
remove<Q: ?Sized>(&mut self, k: &Q) -> Option<V>
```





# Cargo

## 📌 Cargo

**Cargo** はパッケージ管理ツールです． **パッケージ**
とは１つ以上のクレートを含んだもののことです．そして， **クレート** とは
Rust
プログラムをビルドしたもので，バイナリクレート（実行可能ファイル）とライブラリクレートの２つがあります．パッケージは複数のバイナリクレートを含めることができますが，ライブラリクレートは１つまでしか含めることが出来ません．
**モジュール**
はクレートの中でグループ化されたコードのことで，読みやすさと再利用性を高めるためのものです．また，
**プライバシー**
を設定することができ，内部の実装を利用できなくすることも出来ます．

`init`
コマンドを使うと，実行したフォルダ内に，単一のバイナリクレートを含んだパッケージの作成環境が作られます．


    cargo init


実行すると次のような構成になります．


    (workspace)
    ├─ src
    │   └── main.rs
    ├── cargo.toml
    └── .gitignore 


`cargo.toml` は構成ファイルです． `src/main.rs` が **クレートルート**
です．このファイルがモジュール構造の起点となります．\
`build` コマンドを実行するとビルドが始まります．Cargo
は必要な外部パッケージなどを自動でダウンロードしてビルドします．依存する外部パッケージは
`cargo.toml` に記述し，実際にダウンロードしたパッケージのバージョンを
`cargo.lock` ファイルに書き込みます．


    cargo build


`run`
コマンドを実行すると，作成した実行可能ファイルを起動します．ビルドが必要な場合は自動的にビルドしてくれます．


    cargo run


`build`, `run`
コマンドは標準でデバッグ情報付き実行可能ファイルを作成します．オプション
`--release`
をつけることで，リリース用の実行可能ファイルを作成することができます．また，Rust
にはプロファイルというものがあり，`dev` と `release` があります．
`--release` オプションは `release`
プロファイルを使用することを明示するものです．このプロファイルをカスタマイズすることができます．例えば，最適化オプションなどです．詳しくはドキュメントを参照してください．


    cargo build
        Finished dev [unoptimized + debuginfo] target(s) in 0.0 secs
    cargo build --release
        Finished release [optimized] target(s) in 0.0 secs


`check` コマンドはコンパイルチェックをします． `build`
コマンドとは違ってリンクを行わないので，コンパイルが通るかのチェックはこちらのほうが早いです．


    cargo check


外部パッケージを使用したい場合は， `Cargo.toml` の `dependencies`
セクションに使用したいパッケージを指定します．例えば `rand`
パッケージを使う場合は次のようにします：


    [dependencies]
    rand = "0.8.0"


現在のパッケージ構成を確認したい場合は以下のコマンドを使います：


    cargo tree


バイナリパッケージをインストールすることができます．その場合は `install`
コマンドを使います．


    cargo install <package>





# モジュール

## 📌 モジュールを定義

モジュールの定義は `mod` を使います．モジュールの本体は `{}`
で囲みます．モジュールの中にモジュールを定義することも出来ます．


``` 
mod M1 {
    mod M2 {
        mod M3 {
            fn hoge() {}
        }
    }
    
    mod M4 {
        fn foo() {}
        fn bar() {}
    }
}
```


モジュールは同じモジュール内に対してだけ公開された状態になります．そこで，外部のモジュールに対しても公開するには
`pub` を使います． `pub`
はモジュール，関数，構造体などに１つずつ設定することが出来ます．


``` 
pub mod M1 {
    pub mod M2 {
        pub mod M3 {
            pub fn hoge() {}
        }
    }
}
```


## 📌 パス

モジュールを利用するには **パス**
が必要です．モジュールの起点はクレートルートで，パスは `crate`
になります．前のコードが `src/main.rs`
に含まれていた場合，それぞれのパスは次のようになります．


    crate
    └─ M1
        ├─ M2
        │   └─ M3
        │       └── hoge
        └─ M4
            ├── foo
            └── bar


パスの指定には２種類あります．絶対パスと相対パスです．絶対パスはクレートルートを表す
`crate`，または外部パッケージおよび標準ライブラリの場合はパッケージ名から指定することが出来ます．相対パスの場合は
`self`, または `super` を使います． `self` は現在のモジュールから，
`super` は親のモジュールからの指定になります．パスの区切りは `::`
を使います．ちなみに `self::` は省略出来ます．


``` 
crate::M1::M2::M3::hoge
```


## 📌 モジュールの利用

モジュールを利用するには `use` を使ってパスを指定します：


``` 
use crate::M1::M2::M3::hoge;
use std::fmt::Result;
```


`use` で指定したパスに `as` で別名をつけることが出来ます：


``` 
use std::io::Result as IoResult;
```


`use`
で指定するパスにおいて，あるモジュールから別々のパスを指定する場合，それぞれのパスを
`use`
で指定すると必要な行が増えてしまいます．そこで，パスのリストを記述することが出来ます：


``` 
use crate::M1::{M2::M3, M4};
```


また，あるモジュール以下をすべて現在のスコープで利用する場合はグロブ（
`*` ）を指定することができます：


``` 
use crate::M1::*;
```


## 📌 モジュールツリー

クレートそのものがモジュールであり，クレートルートは `src/main.rs`
ファイルで，パスは `crate` でした．Rust
のモジュールシステムはクレートルート以下のフォルダとファイルもまたモジュールと見なします．これによって別々のファイルに実装を分けることが出来るわけです．このフォルダとファイルによるモジュールの作り方が２種類あります．先に一般的な方法を説明します．

`mod` では `{}`
で囲む他に，指定した名前と同じファイルを同じフォルダ内から検索して，その中身を挿入することが出来ます．例えば，
`src/hoge.rs` というファイルがあるとします． `src/main.rs` から
`mod hoge;` とすれば `src/hoge.rs` の中身を `src/main.rs`
ファイルに挿入します．ここで `src/hoge.rs`
の中身が次のようになっているとします．


``` 
pub fn hoge() {}
```


この場合， `src/main.rs` からは `crate::hoge::hoge()`
で呼び出すことが出来ます．

次に下図のようなフォルダ構成を考えます．このような構成にすると，
`src/main.rs` から `mod module1;` とすることで， `src/module1/mod.rs`
ファイルが読み込まれます．そのファイルの中身は `pub mod foo;`
とします．これで，`src/main.rs` から `src/module1/foo.rs`
のモジュールを利用することが出来ます．同じように `pub mod bar;` を
`mod.rs` に追加すれば `bar.rs`
モジュールも利用できるようになります．このようにモジュールの階層を作ってプログラムを構築していきます．これを
**モジュールツリー** といいます．


    (workspace)
    ├─ src
    │   ├── main.rs
    │   └─ module1
    │       ├── mod.rs
    │       ├── foo.rs
    │       └── bar.rs
    ├── cargo.toml
    └── .gitignore


![rust-moduletree01](https://storage.googleapis.com/zenn-user-upload/jit9csxjb4hx1rzu7g296quy17sb)

もう１つのモジュールツリーの作り方ですが，下図を見てください．今度は
`mod.rs` ファイルの代わりに，フォルダと同じファイル `module1.rs`
が存在しています．このファイルの中身は `mod.rs`
と同じになります．ファイルの構成が違いますが，モジュールツリーは同じなので，コードに変更はありません．


    (workspace)
    ├─ src
    │   ├── main.rs
    │   ├── module1.rs
    │   └─ module1
    │       ├── foo.rs
    │       └── bar.rs
    ├── cargo.toml
    └── .gitignore
            \end{code}
        \end{minipage}


![rust-moduletree02](https://storage.googleapis.com/zenn-user-upload/8wcro4sw1jawqqwf64rmty5o1m9x)

## 📌 モジュールの再公開

`pub use`
を使うことで，外部モジュールからでも，指定したパスで利用できるようになります．これを再公開といいます．


``` 
pub use crate::module1;
```





# ユニットテスト

## 📌 ユニットテスト

Rust
にはテストコードを記述する機能が用意されています．テストを実行するには以下のコマンドを実行します：


    cargo test


実行するユニットテストの関数には `test` 属性を付けます：


``` 
#[test]
fn it_works() {
    assert_eq!(2 + 2, 4);
}
```


テスト時のみ（`cargo test`）ビルドするモジュールを作ることが出来ます．それにはモジュールの前に
`cfg(test)` 属性を付けます．


``` 
#[cfg(test)]
mod tests {
    #[test]
    fn it_works() {
        assert_eq!(2 + 2, 4);
    }
}
```


テストに便利なマクロがいくつか用意されています． `assert!`
マクロは引数が `true` かどうかをテストします．また， `==` や `!=`
演算子を使う代わりに `assert_eq!`， `assert_ne!`
マクロが用意されています．


``` 
#[cfg(test)]
mod tests {
    #[test]
    fn it_works() {
        assert!(2 == 2);
        assert_eq!(2 + 2, 4);
        assert_ne!(2 + 2, 5);
    }
}
```


`assert!` マクロや， `unwrap` などは `panic!`
を呼び出す場合があります．場合によっては `panic!`
が呼び出されることを期待したテストコードを記述したい場合があります．しかし，テストは通常
`panic!` を起こすと失敗になります．そこで， `should_panic`
属性を付けることで， `panic!`
を起こすことがテストの目的であることを明示します：


```
#[test]
#[should_panic]
fn it_works() {
    panic!();
}
```





# Tips

## 📌 未使用の変数

プログラムの中に未使用の変数があればコンパイル時に警告が出ます．その場合は変数の前にアンダースコア（`_`）を付けることで，警告を抑制できます．

## 📌 分解束縛

分解束縛において，多くのフィールドがあるときに，必要なものだけ束縛して，残りは無視したいことがあるかもしれません．そのときは，
`..` を使用します：


``` 
struct Point {
    x: i32,
    y: i32,
    z: i32,
}

let origin = Point { x: 0, y: 0, z: 0 };

match origin {
    Point { x, .. } => println!("x is {}", x),
}
```


## 📌 ドキュメント

オフラインで Rust のドキュメントを参照するには次のコマンドを使います


    rustup doc


現在のワークスペースに関するドキュメントを参照するには次のコマンドを使います


    cargo doc [--open]


Rust には `rustdoc`
というソースコードからドキュメントを作成するツールが付属しています．
`cargo doc`
はワークスペースにあるソースコードおよび，外部パッケージからドキュメントを生成してくれます．コメントにドキュメントを入れるには
`///` や `//!` を使います． `///` は宣言に対して，`//!`
はコンテキストに対して，ドキュメントを作成します．詳しくは公式ドキュメントを参照してください．

## 📌 デバッグ時やテスト時のみ有効なコード

`cfg!`
を使うことで環境に合わせたコードを作成することが出来ます．例えばデバッグ時の場合は
`debug_assertions` を指定します．


``` 
if cfg!(debug_assertions) {
    ...
}
```


否定の時は `not` を使います．


``` 
if cfg!(not(debug_assertions)) {
    ...
}
```


他には，テスト( `cargo test` )時に有効になる `test` があります．


``` 
if cfg!(test) {
    ...
}
```


## 📌 属性

属性とは追加情報（メタデータ）のことで，宣言やコンテキストに対して付与することができます．よく使うのは，トレイトの規定実装を示す
`#[derive(...)]`，ユニットテストの `#[test]`, `#[should_panic]`,
`#[ignore]`，そして，コンパイラに伝える `#[allow(...)]` や `#[cfg(...)]`
です．コンテキストはそのモジュール内に全て適用されるので，例えばクレートルート(
`src/main.rs` など)の先頭に `#![allow(...)]`
を指定すると，すべてのモジュールに適用されます．

## 📌 演算子のオーバーロード

Rust
は新しい演算子の定義をすることができません．任意の演算子のオーバーロードは
`std::ops` にあるものだけ可能です．


``` 
use std::ops::Add;
#[derive(Debug, PartialEq)]
    struct Point {
    x: i32,
    y: i32,
}

impl Add for Point {
    type Output = Point;

    fn add(self, other: Point) -> Point {
        Point {
            x: self.x + other.x,
            y: self.y + other.y,
        }
    }
}
```


## 📌 型の別名

既存の型に別名を付けることができます．その場合は `type` を使います．


``` 
type Kilometers = i32;
```


## 📌 Prelude

`Prelude` とは標準で使用可能なモジュールのことです．ここには基本的な型や
`Box`, `Vec`
といった頻繁に使用するものが含まれています．例えば次のような単純な Hello
World!! コードがあります．


``` 
fn main() {
    println!("Hello world!");
}
```


これを，Rust Playground でコード展開してみると，次のようになります．


``` 
#![feature(prelude_import)]
#[prelude_import]
use std::prelude::v1::*;
#[macro_use]
extern crate std;
fn main() {
    {
        ::std::io::_print(
            ::core::fmt::Arguments::new_v1(
                &["Hello world!\n"],
                &match () {
                    () => [],
                }
            )
        );
    };
}
```


`use std::prelude::v1::*`
があるのがわかります．このように，パッケージ内のライブラリを利用するときに最低限必要なものをまとめたものを
`prelude` として用意されている場合があります．

## 📌 dbg!

`dbg!`
マクロは変数や式の結果を出力するのに便利です．次のように使います．


``` 
let a = 2;
let b = dbg!(a * 2) + 1;
// ^-- prints: [src/main.rs:2] a * 2 = 4
assert_eq!(b, 5);
```


## 📌 DisplayとDebugトレイト

`Display` と `Debug`
トレイトは文字列変換やデバッグ出力に便利なトレイトです． `Debug`
トレイトは `derive` 属性で規定実装が可能ですが， `Display`
はそれが出来ません．例えば， `Debug` トレイトを `derive`
で規定実装し，`Display` トレイトを実装する場合は次のようになります．


``` 
use std::fmt;

#[derive(Debug)]
struct Point {
    x: f64,
    y: f64,
}

impl fmt::Display for Point {
    fn fmt(&self, f: &mut fmt::Formatter<'_>) -> fmt::Result {
        write!(f, "{}, {}", self.x, self.y)
    }
}

fn main() {
    let p = Point { x: 1.0, y: 2.0 };
    println!("{}, {:?}", p, p);
}
```


## 📌 if let Some(x) をもっと短く

以下のコードを見てください．


``` 
fn main() {
    let a = Some(10);
    if let Some(x) = a {
        dbg!(x);
    }
}
```


これは次のように，さらに短く書くことができます．ただし，コードとして意図がわかりづらくなってしまうので注意です．


``` 
fn main() {
    let a = Some(10);
    for x in a {
        dbg!(x);
    }
}
```


## 📌 while 式

他の言語には `do...while(condition)`
といった一回実行して，２回目以降は条件を満たしているときに実行される構文が用意されていることがあります．これを
Rust で行う場合は，まず `loop` 式を使う方法が考えられます．


``` 
fn main() {
    let mut x = 0;
    loop {
        x += 1;
        if x >= 10 {
            break;
        }
    }
    dbg!(x); // x=10
}
```


これは，次のように `while` 式に書き換えることができます．


``` 
fn main() {
    let mut x = 0;
    while {
        x += 1;
        x < 10
    } {}
    dbg!(x); // x=10
}
```


`while`
式の条件には式が使えるので，ブロックも使えます．ブロックの最後に条件を入れることで短く書くことが出来ます．この場合は空ブロック(
`{}` )を忘れないようにしましょう．\
ただし，この条件式を使う方法では， `break`
などが使えません．この場合は， **ラベル** を使います．Rust
ではループに名前を付けることができます．このラベルを `break`
で指定することで条件式でも `break` を使うことができます．ラベルは
`while` などの前に `'label:` という形で指定します．


``` 
fn main() {
    let mut x = 0;
    'a: while {
        x += 1;
        if x > 5 { break 'a; }
        x < 10
    } {}
    dbg!(x); // x=6
}
```


このラベル機能は，例えばネストされたループで，内側のループから外側のループを一気に抜けることができます．


``` 
fn main() {
    let mut x = 0;
    'outer: loop {
        'inner: while {
            x += 1;
            if x > 5 { break 'outer; }
            x < 10
        } {}
    }
    dbg!(x); // x=6
}
```


もちろん，このラベルは条件式だけでなく，本体の中でも使用することができます．

## 📌 rustfmt

Rust にはコード整形ツールがついています．それが `rustfmt`
です．次のように使います．


    rustfmt <filename>


`cargo fmt` を使うとワークスペース内のファイルに対して実行します．


    cargo fmt


`--check` オプションを指定すると，整形を行わずに警告を表示してくれます．
`cargo fmt` にこのオプションをつけるときは， `cargo`
のオプションと区別するために `--` を前に付けます．


    rustfmt <filename> --check
    cargo fmt -- --check


## 📌 clippy

不適切なコードを指摘してくれる `clippy`
というツールがあります．次のように使います．


    cargo clippy


## 📌 APIガイドライン

Rust
の関数や変数の名前など，コーディングに関する規約がまとめられています．一読することをオススメします．

-   Rust API Guidelines




# さいごに

## 📌 さいごに

いかがだったでしょうか．思っていた以上に長くなってしまいましたが，これでも全部説明しきれていないのが本音です．ただ，一番解説したかった所有権のところはしっかり書いたつもりです．ここで，説明されていないところ，例えばドキュメントコメント，rustfmt,
clippy
などの詳細は公式ドキュメントなどを参照してください．とはいえ，正直あまり公式ドキュメントはオススメしません．そもそもこの入門を書いたのも，公式ドキュメントがとてもわかりづらいと思ったからです（あくまで私個人の意見です）．

私も Rust を本気で勉強してまだ２～３ヶ月ぐらいだと思います．Rust
入門みたいな本は一冊も購入していないし読んでもいません．基本的に公式ドキュメントや
Tour of
Rust，ネットで公開されている情報だけです．なので，大いに勘違いしているかもしれません．なにか間違っているところがあればご連絡していただけると嬉しいです．少しでも参考になれば幸いです．

本書は「
Rustではじめるレイトレーシング入門
」から Rust に関する解説を抜粋したものです． Rust
を使って実際にプログラミングしたい人は是非試してみてください．

また，最初に作った Rust の
スライド
もあるので参考になるかもしれません．

twitter: \@mebiusbox2

## 📌 参考文献

-   The Rust Programming Language
-   The Rust Programming Language
    日本語版
-   Tour of Rust
-   Rust by Example
-   Rust Playground
-   Rust for a Pythonista #2: Building a Rust crate for CSS
    inlining
-   Rustに影響を与えた言語たち
-   RustでOption値やResult値を上手に扱う
-   最速で知る！
    プログラミング言語Rustの基本機能とメモリ管理【第二言語としてのRust】
-   ウォークスルー Haskell




