# 第 1 章 - 基礎

最初の章では、関数、変数、プリミティブ型などの基本的なことを探っていきます。皆さんのご参加をお待ちしております。

また、あなたに話し掛けているこの愛らしいカニが誰なのか気になるかもしれません。私は
Rust プログラミング言語の非公式マスコット **Ferris**
です。はじめまして。

## こんにちは、!

*Rust ツアー*へようこそ。 これはプログラミング言語 Rust
の機能を段階的にガイドすることを目的としています。 Rust
は学習曲線が急な言語だと見なされることが多いですが、
複雑な事項に進む前に探ることがたくさんあると納得していただければと思います。

このガイドは以下の言語で見ることができます。

-   Deutsch
-   English
-   Español
-   Français
-   Interlingue
-   Magyar
-   Polski
-   Português Brasileiro
-   Русский
-   简体中文
-   繁體中文
-   日本語
-   한국어
-   Türkçe
-   Українська
-   ภาษาไทย

コンテンツへの提案や翻訳に貢献したい場合、 Rust ツアーの github リポジトリをチェックしてください。

この古典的な例では、Rust が Unicode 文字列をサポートしていることを示します。

## Rust Playground

このツアーでは、Rust Playground のインタラクティブなコーディングツールを使用します。

Rust で遊んで、あなたの創造性と挑戦を他の人に見せるのに最適な方法です。

```
fn main() {
    println!("Playground へようこそ。ここでコードを修正できます。");
}
```

## 変数

変数は **let** キーワードを使用して宣言します。

値を割り当てる際、Rust は 99%
のケースで変数の型を推論できます。それができない場合、変数宣言に型を追加できます。

同じ変数名に複数回割り当てできることに注目してください。
これは変数のシャドウイングと呼ばれるもので、型を変更して後でその名前で参照できます。

変数名にはスネークケース `snake_case` を使用します。

```
fn main() {
    // x の型を推論
    let x = 13;
    println!("{}", x);

    // x の型を指定
    let x: f64 = 3.14159;
    println!("{}", x);

    // 宣言の後で初期化（あまり使われません）
    let x;
    x = 0;
    println!("{}", x);
}
```

## 変数の変更

Rustは変数の変更についてとても配慮しています。値は 2
種類に分類されます。

-   **可変** - コンパイラは変数の書き込みと読み込みを許可します。
-   **不変** - コンパイラは変数の読み込みだけを許可します。

可変値は **mut** キーワードで表します。

この概念については後で詳しく説明しますが、今のところはこのキーワードに注意してください。

```
fn main() {
    let mut x = 42;
    println!("{}", x);
    x = 13;
    println!("{}", x);
}
```
## 基本的な型

Rustにはよく知られた様々な型があります。

-   ブール型 - `bool` は true または false を表します
-   符号なし整数型 - `u8` `u32` `u64` `u128` は正の整数を表します
-   符号付き整数型 - `i8` `i32` `i64` `i128` は正と負の整数を表します
-   ポインタサイズ整数型 - `usize` `isize`
    はメモリ内のインデックスとサイズを表します
-   浮動小数点数型 - `f32` `f64`
-   タプル型 - `(value, value, ...)`
    スタック上の固定された値の組を渡すために使用されます
-   配列型 - コンパイル時に長さが決まる同じ要素のコレクション
-   スライス型 - 実行時に長さが決まる同じ要素のコレクション
-   `str`(string slice) - 実行時に長さが決まるテキスト

Rust
はシステムプログラミング言語であるため、他の言語よりも複雑かもしれません。あまり意識しなかったようなメモリの問題を扱います。
これについては後ほど詳しく説明します。

数値型は、数値の最後に型を付加することで明示的に指定できます。（例:
`13u32`, `2u8`）

```
fn main() {
    let x = 12; // デフォルトでは i32
    let a = 12u8;
    let b = 4.3; // デフォルトでは f64
    let c = 4.3f32;
    let bv = true;
    let t = (13, false);
    let sentence = "hello world!";
    println!(
        "{} {} {} {} {} {} {} {}",
        x, a, b, c, bv, t.0, t.1, sentence
    );
}
```
## 基本型の変換

Rust で数値型を扱う際、型を明示する必要があります。`u8` と `u32`
を混ぜるとエラーになります。

幸い、Rust は **as** キーワードで数値型を簡単に変換できます。

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
## 定数

定数を使用すると、コード全体で何度も使用される共通の値を効率的に指定できます。
定数は、変数のように値が使われる場所でコピーするのではなく、コンパイル時に値が使われる場所の識別子を直接置き換えます。

変数とは異なり、定数は明示的な型指定が必要です。

定数名には大文字のスネークケース `SCREAMING_SNAKE_CASE` を使用します。

```
const PI: f32 = 3.14159;

fn main() {
    println!(
        "ゼロからアップル {} を作るには、まず宇宙を創造する必要があります。",
        PI
    );
}
```
## 配列

*配列*は、データ要素がすべて同じ型の固定長コレクションです。

*配列*のデータ型は `[T;N]` であり、T は要素の型、N
はコンパイル時に決まる固定長です。

個々の要素は `[x]` 演算子によって取得できます。ここで *x*
は取り出そうとする要素の *usize* 型のインデックス（0 始まり）です。

```
fn main() {
    let nums: [i32; 3] = [1, 2, 3];
    println!("{:?}", nums);
    println!("{}", nums[1]);
}
```

## 関数

関数には 0 個以上の引数があります。

この例では、add は `i32` 型（32 ビット長の整数）の引数を 2 つ取ります。

関数名にはスネークケース `snake_case` を使用します。

```
fn add(x: i32, y: i32) -> i32 {
    return x + y;
}

fn main() {
    println!("{}", add(42, 13));
}
```

## 複数の戻り値

関数は、値を**タプル**で返すことによって、複数の値を返せます。

タプルの要素はインデックス番号で参照できます。

Rust
はデータ構造の一部を抽出する機能を提供します。これについては後ほど他の方法も見ていきます。

```
fn swap(x: i32, y: i32) -> (i32, i32) {
    return (y, x);
}

fn main() {
    // 戻り値をタプルで返す
    let result = swap(123, 321);
    println!("{} {}", result.0, result.1);

    // タプルを2つの変数に分解
    let (a, b) = swap(result.0, result.1);
    println!("{} {}", a, b);
}
```
## 空の戻り値

関数に戻り値の型が指定されていない場合、*unit*
と呼ばれる空のタプルを返します。

空のタプルは `()` と表記します。

`()`
はあまり使われませんが、時々出てくるので意味は知っておく必要があります。

```
fn make_nothing() -> () {
    return ();
}

// 戻り値は () と推論
fn make_nothing2() {
    // この関数は戻り値が指定されないため () を返す
}

fn main() {
    let a = make_nothing();
    let b = make_nothing2();

    // 空を表示するのは難しいので、
    // a と b のデバッグ文字列を表示
    println!("a の値: {:?}", a);
    println!("b の値: {:?}", b);
}
```
## 第 1 章 - まとめ

ここまでお疲れ様でした。Rust の基本はそれほど難しくなかったですよね？
Rust のコンパイラがどのように考えているのかを覗いてみました。
システムプログラミング言語として、メモリ内の値のサイズ、変更が可能かどうか、計算を確実にすることを重視しています。
次はお馴染みの `if` と `for` ループについて見ていきます。

その他の資料:

-   [Youtube: Rust Cast - A deeper dive on Rust\'s primitive number types](https://www.youtube.com/watch?v=n5TRBkbystY)
-   [Website: Rust Book 2018 - A deeper description on basic data types](https://doc.rust-lang.org/1.30.0/book/2018-edition/ch03-02-data-types.html)
-   [Website: Rust Cheat Sheet - Data Types](https://cheats.rs/#basic-types)

# 第 2 章 - 基本制御フロー

この章では、Rustの基本的な制御フローについて説明します。 C
系の言語に慣れていればすぐに馴染めますし、ちょっとした驚きがあるかもしれません。

## if/else if/else

Rust でのコード分岐はそれほど目新しくはありません。

条件には括弧がありませんが、本当に必要だったでしょうか？これでコードはすっきりします。

いつもの論理演算子が使えます: `==`, `!=`, `<`, `>`, `<=`, `>=`, `!`,
`||`, `&&`

```
fn main() {
    let x = 42;
    if x < 42 {
        println!("42 より小さい");
    } else if x == 42 {
        println!("42 に等しい");
    } else {
        println!("42 より大きい");
    }
}
```

## loop

無限ループが必要ですか？

Rust では簡単です。

`break` によってループから脱出できます。

後で見ますが `loop` には秘密があります。

```
fn main() {
    let mut x = 0;
    loop {
        x += 1;
        if x == 42 {
            break;
        }
    }
    println!("{}", x);
}
```

## while

`while` を使えば、ループに条件を簡単に追加できます。

条件が `false` と評価された場合、ループは終了します。

```
fn main() {
    let mut x = 0;
    while x != 42 {
        x += 1;
    }
}
```

## for

Rust の `for` ループは強力に改良されています。
イテレータとして評価される式を反復処理します。
イテレータとは何でしょうか？
イテレータとは、項目がなくなるまで「次の項目は何ですか？」と質問することができるオブジェクトです。

それについては後の章で詳しく説明します。とりあえず、Rust
では整数のシーケンスを生成するイテレータを、簡単に作成できることを知っておいてください。

`..`
演算子は、開始番号から終了番号の手前までの数値を生成するイテレータを作成します。

`..=`
演算子は、開始番号から終了番号までの数値を生成するイテレータを作成します。

```
fn main() {
    for x in 0..5 {
        println!("{}", x);
    }

    for x in 0..=5 {
        println!("{}", x);
    }
}
```

## match

switch 文が足りない？ Rust
には、値が取り得るすべての条件にマッチさせて、マッチが真であればコードパスを実行するための、とても便利なキーワードがあります。
これが数値に対してどのように機能するか見てみましょう。
より複雑なデータのパターンマッチングについては、後の章で詳しく説明します。
待つだけの価値があることをお約束します。

`match` は網羅的なので、すべてのケースを処理しなければなりません。

マッチングと分解を組み合わせたパターンは、Rust
の中で最も一般的なパターンの一つです。

```
fn main() {
    let x = 42;

    match x {
        0 => {
            println!("found zero");
        }
        // 複数の値にマッチ
        1 | 2 => {
            println!("found 1 or 2!");
        }
        // 範囲にマッチ
        3..=9 => {
            println!("found a number 3 to 9 inclusively");
        }
        // マッチした数字を変数に束縛
        matched_num @ 10..=100 => {
            println!("found {} number between 10 to 100!", matched_num);
        }
        // どのパターンにもマッチしない場合のデフォルトマッチが必須
        _ => {
            println!("found something else!");
        }
    }
}
```

## loop から値を返す

`loop` は `break` で抜けて値を返すことができます。

```
fn main() {
    let mut x = 0;
    let v = loop {
        x += 1;
        if x == 13 {
            break "13 を発見";
        }
    };
    println!("loop の戻り値: {}", v);
}
```
## ブロック式から値を返す

`if`、`match`、関数、ブロックは、単一の方法で値を返すことができます。

`if`、`match`、関数、ブロックの最後が `;`
のない式であれば、戻り値として使用されます。
これは値を返すための簡潔なロジックを作成するのに最適な方法で、その値は新しい変数に入れることができます。

また、`if` 文を三項演算子のように使用できることにも注目してください。

```
fn example() -> i32 {
    let x = 42;
    // Rust の三項式
    let v = if x < 42 { -1 } else { 1 };
    println!("if より: {}", v);

    let food = "ハンバーガー";
    let result = match food {
        "ホットドッグ" => "ホットドッグです",
        // 単一の式で値を返す場合、中括弧は省略可能
        _ => "ホットドッグではありません",
    };
    println!("食品の識別: {}", result);

    let v = {
        // ブロックのスコープは関数のスコープから分離されている
        let a = 1;
        let b = 2;
        a + b
    };
    println!("ブロックより: {}", v);

    // Rust で関数の最後から値を返す慣用的な方法
    v + 4
}

fn main() {
    println!("関数より: {}", example());
}
```
## 第 2 章 - まとめ

基本的な言語機能においても、Rust の力を垣間見ることができたでしょうか。
今後は `for` と `match`
について、その能力を活用できるように知識を深めながら、進めていきます。
次回は Rust の基礎となるデータ構造に入ります。

# 第 3 章 - 基本的なデータ構造体

基本的な型をより深く学ぶ時がきました！この章では、 Rust
の中で最もプリミティブなデータ構造を見て、
それらがメモリ上でどう表現されるかについて詳しく見ていきます。あなたは
Rust が物事の動作原理をあまり隠していないことを楽しむでしょう。

## 構造体

一つの `struct` はフィールドの集合です。

*フィールド*
とはデータ構造とキーワードを紐付ける値です。その値はプリミティブ型かデータ構造を指定可能です。

その定義はメモリ上で隣合うデータの配置をコンパイラに伝える設計図の様なものです。

```
struct SeaCreature {
    // String は構造体である。
    animal_type: String,
    name: String,
    arms: i32,
    legs: i32,
    weapon: String,
}
```
## メソッドの定義

関数(function)と違って、メソッド(method)は特定のデータ型と紐づく関数のことです。

**スタティックメソッド** - ある型そのものに紐付き、演算子 `::`
で呼び出せます。

**インスタンスメソッド** - ある型のインスタンスに紐付き、演算子 `.`
で呼び出せます。

以降の章でまたメソッドの作り方について話します。

```
fn main() {
    // スタティックメソッドでStringインスタンスを作成する。
    let s = String::from("Hello world!");
    // インスタンスを使ってメソッド呼び出す。
    println!("{} is {} characters long.", s, s.len());
}
```

## メモリ

Rust
のプログラムでは、データを保持するために次の3種類のメモリ空間を持っています。

-   **データメモリ** - 固定長もしくは **スタティック** (例: プログラムのライフサイクルで常に存在するもの)なデータ。 プログラム内の文字列(例: 'Hello World'), この文字列のキャラクタは読み取りにしか使えないため、この領域に入ります。 コンパイラはこういったデータに対してチューニングをしており、メモリ上の位置はすでに知られていてかつ固定であるため、非常に速く使うことができます。
-   **スタックメモリ** - 関数内で宣言された変数。 関数が呼び出されている間は、メモリ上の位置は変更されることがないため、コンパイラからするとチューニングができるので、スタックメモリも非常に速くデータにアクセスできます。
-   **ヒープメモリ** - プログラムの実行時に作られるデータ。 このメモリにあるデータは追加、移動、削除、サイズの調節などの操作が許されています。動的であるため、遅いと思われがちですが、 これによりメモリの使い方に柔軟性を生み出すことができます。データをヒープメモリに入れることをアロケーション(allocation)といい、データをヒープメモリから削除することはディアロケーション(deallocation)と言います。

## メモリの中でデータを作成する

コードの中で **構造体** を **インスタンス化**
する際に、プログラムはフィールドデータをメモリ上で隣り合うように作成します。

全てのフィールドの値を指定してインスタンス化をする際：

`構造体名 {...}`.

構造体のフィールドは演算子 `.` で取り出すことができます。

例に示したコードのメモリ状況について：

-   ダブルクオートに囲まれたテキスト(例:
    \"Ferris\")は読み取り専用データであるため、 **データメモリ**
    に入ります。
-   関数の呼び出し `String::from` では構造体 `String`
    を作成し、この構造体と SeaCreature のフィールドを隣り合う形で
    *スタック* に入れられます。
    　フィールドの値は変更可能であり、メモリ上では以下の様に変更されます。

1.  *ヒープ* に変更可能なメモリを作り、テキストを入れます。
2.  1.で作成した参照アドレスを *ヒープ* に保存し、それを `String`
    に保存します(後の章でまた詳しく紹介します。)。

-   最後に、我々の友である *Ferris* と *Sarah*
    はプログラムの中では固定な位置であるため、*スタック* に入ります。

```
struct SeaCreature {
    animal_type: String,
    name: String,
    arms: i32,
    legs: i32,
    weapon: String,
}

fn main() {
    // SeaCreatureのデータはスタックに入ります。
    let ferris = SeaCreature {
        // String構造体もスタックに入りますが、
        // ヒープに入るデータの参照アドレスが一つ入ります。
        animal_type: String::from("crab"),
        name: String::from("Ferris"),
        arms: 2,
        legs: 4,
        weapon: String::from("claw"),
    };

    let sarah = SeaCreature {
        animal_type: String::from("octopus"),
        name: String::from("Sarah"),
        arms: 8,
        legs: 0,
        weapon: String::from("none"),
    };

    println!(
        "{} is a {}. They have {} arms, {} legs, and a {} weapon",
        ferris.name, ferris.animal_type, ferris.arms, ferris.legs, ferris.weapon
    );
    println!(
        "{} is a {}. They have {} arms, and {} legs. They have no weapon..",
        sarah.name, sarah.animal_type, sarah.arms, sarah.legs
    );
}
```

## タプルライクな構造体

Rust ではタプルの様な構造体を利用できます。

```
struct Location(i32, i32);

fn main() {
    // これもスタックに入れられる構造体です。
    let loc = Location(42, 32);
    println!("{}, {}", loc.0, loc.1);
}
```
## ユニットライクな構造体

Rust ではフィールドを持たない構造体を宣言できます。

第一章で述べた様に、*unit* は空ユニット `()`
の別名称です。こういった構造体が `ユニットライク`
と言われる理由でもあります。

この構造体はあまり使われません。

```
struct Marker;

fn main() {
    let _m = Marker;
}
```

## 列挙型

列挙型はキーワード `enum`
で新しい型を生成することができ、この型はいくつかのタグ付された値を持つことができます。

`match`
は保有する全ての列挙値を処理する手助けすることができ、コードの品質を維持することもできます。

```
#![allow(dead_code)] // この行でコンパイラのwaringsメッセージを止めます。

enum Species {
    Crab,
    Octopus,
    Fish,
    Clam
}

struct SeaCreature {
    species: Species,
    name: String,
    arms: i32,
    legs: i32,
    weapon: String,
}

fn main() {
    let ferris = SeaCreature {
        species: Species::Crab,
        name: String::from("Ferris"),
        arms: 2,
        legs: 4,
        weapon: String::from("claw"),
    };

    match ferris.species {
        Species::Crab => println!("{} is a crab",ferris.name),
        Species::Octopus => println!("{} is a octopus",ferris.name),
        Species::Fish => println!("{} is a fish",ferris.name),
        Species::Clam => println!("{} is a clam",ferris.name),
    }
}
```

## データを持つ列挙型

`enum` は一個もしくは複数な型のデータを持つことができ、C言語の `union`
の様な表現ができます。

`match`
を用いて列挙値に対するパターンマッチングを行う際、各データを変数名に束縛することができます。

`列挙` のメモリ事情:

-   列挙型のメモリサイズはそれが持つ最大要素のサイズと等しい。これにより全ての代入可能な値が同じサイズのメモリ空間を利用することを可能にします。
-   要素の型以外に、各要素には数字値がついており、どのタグであるかについて示しています。

その他の事情:

-   Rust の `列挙` は *tagged-union* とも言われています。
-   複数の型を組み合わせて新しい型を作ることができます。 これが Rust
    には *algebraic types* を持つと言われる理由です。

```
#![allow(dead_code)] // この行でコンパイラのwaringsメッセージを止めます。

enum Species { Crab, Octopus, Fish, Clam }
enum PoisonType { Acidic, Painful, Lethal }
enum Size { Big, Small }
enum Weapon {
    Claw(i32, Size),
    Poison(PoisonType),
    None
}

struct SeaCreature {
    species: Species,
    name: String,
    arms: i32,
    legs: i32,
    weapon: Weapon,
}

fn main() {
    // SeaCreatureのデータはスタックに入ります。
    let ferris = SeaCreature {
        // String構造体もスタックに入りますが、
        // ヒープに入るデータの参照アドレスが一つ入ります。
        species: Species::Crab,
        name: String::from("Ferris"),
        arms: 2,
        legs: 4,
        weapon: Weapon::Claw(2, Size::Small),
    };

    match ferris.species {
        Species::Crab => {
            match ferris.weapon {
                Weapon::Claw(num_claws,size) => {
                    let size_description = match size {
                        Size::Big => "big",
                        Size::Small => "small"
                    };
                    println!("ferris is a crab with {} {} claws", num_claws, size_description)
                },
                _ => println!("ferris is a crab with some other weapon")
            }
        },
        _ => println!("ferris is some other animal"),
    }
}
```
## 第三章 - まとめ

興奮するでしょう！これで我々は基本的なツールを手に入れ、コードで我々の思考を表現することができます。
次の章では Generics について説明します。

# 第 4 章 - ジェネリック型

ジェネリック型は Rust において非常に重要です。 これらの型は null
許容な値（つまりまだ値を持たない変数）の表現、エラー処理、コレクションなどに使用されます。
このセクションでは、あなたがいつも使用するであろう基本的なジェネリック型について学習します。

## ジェネリック型とは？

ジェネリック型は `struct` や `enum`
を部分的に定義することを可能にします。
コンパイル時にコードでの使用状況に基づいて完全に定義されたバージョンが生成されます。

Rust は通常、インスタンスを生成するコードから最終的な型を推論できます。
しかし補助が必要な場合は、`::<T>` 演算子を使って明示的に指定できます。
この演算子は `turbofish`
という名前でも知られています（彼とは仲良しです！）。

```
// 部分的に定義された構造体型
struct BagOfHolding<T> {
    item: T,
}

fn main() {
    // 注意: ジェネリック型を使用すると、型はコンパイル時に作成される。
    // ::<> (turbofish) で明示的に型を指定
    let i32_bag = BagOfHolding::<i32> { item: 42 };
    let bool_bag = BagOfHolding::<bool> { item: true };

    // ジェネリック型でも型推論可能
    let float_bag = BagOfHolding { item: 3.14 };

    // 注意: 実生活では手提げ袋を手提げ袋に入れないように
    let bag_in_bag = BagOfHolding {
        item: BagOfHolding { item: "boom!" },
    };

    println!(
        "{} {} {} {}",
        i32_bag.item, bool_bag.item, float_bag.item, bag_in_bag.item.item
    );
}
```

## 値がないことの表現

他の言語では、値が存在しないことを表すためにキーワード `null`
が用いられます。
これは変数やフィールドの操作に失敗する可能性があることを意味するため、プログラミング言語に困難をもたらします。

Rust には `null`
はありませんが、値がないことを表現することの重要性を無視しているわけではありません。
既に知っているツールを使った素朴な表現を考えてみましょう。

1つ以上の値を `None` によって代替するパターンは、`null` がない Rust
ではとても一般的です。
ジェネリック型はこの問題を解決するのに役立ちます。

```
enum Item {
    Inventory(String),
    // None は項目がないことを表す
    None,
}

struct BagOfHolding {
    item: Item,
}
```
## Option

Rustには `Option`
と呼ばれるジェネリックな列挙型が組み込まれており、`null` を使わずに null
許容な値を表現できます。

    enum Option<T> {
        None,
        Some(T),
    }

この列挙型はとても一般的なもので、`Some` と `None`
を使えばどこでもインスタンスを生成できます。

```
// 部分的に定義された構造体型
struct BagOfHolding<T> {
    // パラメータ T を渡すことが可能
    item: Option<T>,
}

fn main() {
    // 注意: i32 が入るバッグに、何も入っていません！
    // None からは型が決められないため、型を指定する必要があります。
    let i32_bag = BagOfHolding::<i32> { item: None };

    if i32_bag.item.is_none() {
        println!("バッグには何もない！")
    } else {
        println!("バッグには何かある！")
    }

    let i32_bag = BagOfHolding::<i32> { item: Some(42) };

    if i32_bag.item.is_some() {
        println!("バッグには何かある！")
    } else {
        println!("バッグには何もない！")
    }

    // match は Option をエレガントに分解して、
    // すべてのケースが処理されることを保証できます！
    match i32_bag.item {
        Some(v) => println!("バッグに {} を発見！", v),
        None => println!("何も見付からなかった"),
    }
}
```
## Result

Rustには `Result`
と呼ばれるジェネリックな列挙型が組み込まれており、失敗する可能性のある値を返せます。
これは言語がエラーを処理する際の慣用的な方法です。

    enum Result<T, E> {
        Ok(T),
        Err(E),
    }

このジェネリック型はカンマで区切られた複数の*パラメータ化された型*を持つことに注意してください。

この列挙型はとても一般的なもので、`Ok` と `Err`
を使えばどこでもインスタンスを生成できます。

```
fn do_something_that_might_fail(i:i32) -> Result<f32,String> {
    if i == 42 {
        Ok(13.0)
    } else {
        Err(String::from("正しい値ではありません"))
    }
}

fn main() {
    let result = do_something_that_might_fail(12);

    // match は Result をエレガントに分解して、
    // すべてのケースが処理されることを保証できます！
    match result {
        Ok(v) => println!("発見 {}", v),
        Err(e) => println!("Error: {}",e),
    }
}
```

## 失敗するかもしれない main

`main` は `Result` を返すことができます。

```
fn do_something_that_might_fail(i: i32) -> Result<f32, String> {
    if i == 42 {
        Ok(13.0)
    } else {
        Err(String::from("正しい値ではありません"))
    }
}

// main は値を返しませんが、エラーを返すことがあります！
fn main() -> Result<(), String> {
    let result = do_something_that_might_fail(12);

    match result {
        Ok(v) => println!("発見 {}", v),
        Err(_e) => {
            // エラーをうまく処理

            // 何が起きたのかを説明する新しい Err を main から返します！
            return Err(String::from("main で何か問題が起きました！"));
        }
    }

    // Result の Ok の中にある unit 値によって、
    // すべてが正常であることを表現していることに注意してください。
    Ok(())
}
```
## 簡潔なエラー処理

`Result` はとてもよく使うので、Rust にはそれを扱うための強力な演算子 `?`
が用意されています。 以下の2つのコードは等価です。

    do_something_that_might_fail()?

    match do_something_that_might_fail() {
        Ok(v) => v,
        Err(e) => return Err(e),
    }

```
fn do_something_that_might_fail(i: i32) -> Result<f32, String> {
    if i == 42 {
        Ok(13.0)
    } else {
        Err(String::from("正しい値ではありません"))
    }
}

fn main() -> Result<(), String> {
    // コードが簡潔なのに注目！
    let v = do_something_that_might_fail(42)?;
    println!("発見 {}", v);
    Ok(())
}
```
## やっつけな Option/Result 処理

`Option`/`Result`
を使って作業するのは、ちょっとしたコードを書くのには厄介です。 `Option`
と `Result` の両方には `unwrap`
と呼ばれる関数があり、手っ取り早く値を取得するのには便利です。 `unwrap`
は以下のことを行います。

1.  `Option`/`Result` 内の値を取得します。
2.  列挙型が `None`/`Err` の場合、`panic!` します。

以下の2つのコードは等価です。

    my_option.unwrap()

    match my_option {
        Some(v) => v,
        None => panic!("Rust によって生成されたエラーメッセージ！"),
    }

同様に:

    my_result.unwrap()

    match my_result {
        Ok(v) => v,
        Err(e) => panic!("Rust によって生成されたエラーメッセージ！"),
    }

良い Rust 使い（Rustacean）であるためには、可能な限り適切に `match`
を使用してください。

```
fn do_something_that_might_fail(i: i32) -> Result<f32, String> {
    if i == 42 {
        Ok(13.0)
    } else {
        Err(String::from("正しい値ではありません"))
    }
}

fn main() -> Result<(), String> {
    // 簡潔ですが、値が存在することを仮定しており、
    // すぐにダメになる可能性があります。
    let v = do_something_that_might_fail(42).unwrap();
    println!("発見 {}", v);

    // パニックするでしょう！
    let v = do_something_that_might_fail(1).unwrap();
    println!("発見 {}", v);

    Ok(())
}
```
## ベクタ型

最も有用なジェネリック型のいくつかはコレクション型です。 ベクタは構造体
`Vec` で表される可変サイズのリストです。

マクロ `vec!` を使えば、手動で構築するよりも簡単にベクタを生成できます。

`Vec` にはメソッド `iter()` があります。
これによってベクタからイテレータを生成すれば、ベクタを簡単に `for`
ループに入れることができます。

メモリに関する詳細：

-   `Vec`
    は構造体ですが、内部的にはヒープ上の固定リストへの参照を含んでいます。
-   ベクタはデフォルトの容量で始まります。
    容量よりも多くの項目が追加された場合、ヒープ上により大きな容量の固定リストを生成して、データを再割り当てします。

```
fn main() {
    // 型を明示的に指定
    let mut i32_vec = Vec::<i32>::new(); // turbofish <3
    i32_vec.push(1);
    i32_vec.push(2);
    i32_vec.push(3);

    // もっと賢く、型を自動的に推論
    let mut float_vec = Vec::new();
    float_vec.push(1.3);
    float_vec.push(2.3);
    float_vec.push(3.4);

    // きれいなマクロ！
    let string_vec = vec![String::from("Hello"), String::from("World")];

    for word in string_vec.iter() {
        println!("{}", word);
    }
}
```

## 第 4 章 - まとめ

この章でジェネリック型がどれだけの力を発揮するのかがわかりました。
すべて使いこなせなくても心配しないでください。
今は、コードの中で何度も目にするであろう主要なアイデアを意識するだけで良いと思います。
私たちの関数はかなり長くなっています。 次の章では、Rust
の重要な概念であるデータの所有権について説明します。

# 第 5 章 - データの所有権と借用

Rust
には他のプログラミング言語に比べて、メモリを管理するための独特な枠組みがあります。
ここでは圧倒されないように、コンパイラの動作と検証を一つずつ見ていきます。
突き詰めると、ここで紹介するルールはあなたを苦しめるためのものではなく、
コードをエラーになりにくいものにするためのものだと覚えておくことが重要です。

## 所有権

型のインスタンスを作成して変数に**束縛**するとメモリリソースが作成され、そのすべての**ライフタイム**に渡って
Rust コンパイラが検証します。
束縛された変数はリソースの**所有者**と呼ばれます。

```
struct Foo {
    x: i32,
}

fn main() {
    // 構造体をインスタンス化し、変数に束縛してメモリリソースを作成
    let foo = Foo { x: 42 };
    // foo は所有者
}
```

## スコープベースのリソース管理

Rust
では、スコープの終わりをリソースのデストラクトと解放の場所として使用します。

このデストラクトと解放のことを**ドロップ** (drop) と呼びます。

メモリの詳細:

-   Rust にはガベージコレクションがありません。
-   C++ では Resource Acquisition Is Initialization (RAII)「リソース取得は初期化である」とも呼ばれています。

```
struct Foo {
    x: i32,
}

fn main() {
    let foo_a = Foo { x: 42 };
    let foo_b = Foo { x: 13 };

    println!("{}", foo_a.x);

    println!("{}", foo_b.x);
    // foo_b はここでドロップ
    // foo_a はここでドロップ
}
```
## ドロップは階層的

構造体がドロップされると、まず構造体自体がドロップされ、次にその子要素が個別に削除されます。

メモリの詳細:

-   メモリを自動的に解放することで、メモリリークを軽減できます。
-   メモリリソースのドロップは一度しかできません。

```
struct Bar {
    x: i32,
}

struct Foo {
    bar: Bar,
}

fn main() {
    let foo = Foo { bar: Bar { x: 42 } };
    println!("{}", foo.bar.x);
    // foo が最初にドロップ
    // 次に foo.bar がドロップ
}
```

## 所有権の移動

所有者が関数の実引数として渡されると、所有権は関数の仮引数に移動 (move)
します。

**移動**後は、元の関数内の変数は使用できなくなります。

メモリの詳細:

-   **移動**している間、所有者の値のスタックメモリは、関数呼び出しパラメータのスタックメモリにコピーされます。

```
struct Foo {
    x: i32,
}

fn do_something(f: Foo) {
    println!("{}", f.x);
    // f はここでドロップ
}

fn main() {
    let foo = Foo { x: 42 };
    // foo の所有権は do_something に移動
    do_something(foo);
    // foo は使えなくなる
}
```

## 所有権を返す

所有権を関数から返すこともできます。

```
struct Foo {
    x: i32,
}

fn do_something() -> Foo {
    Foo { x: 42 }
    // 所有権は外に移動
}

fn main() {
    let foo = do_something();
    // foo は所有者になる
    // 関数のスコープの終端により、foo はドロップ
}
```
## 参照による所有権の借用

参照は、`&`
演算子を使ってリソースへのアクセスを借用できるようにしてくれます。

参照も他のリソースと同様にドロップされます。

```
struct Foo {
    x: i32,
}

fn main() {
    let foo = Foo { x: 42 };
    let f = &foo;
    println!("{}", f.x);
    // f はここでドロップ
    // foo はここでドロップ
}
```

## 参照による所有権の可変な借用

`&mut`
演算子を使えば、リソースへの変更可能なアクセスを借用することもできます。

リソースの所有者は、可変な借用の間は移動や変更ができません。

メモリの詳細:

-   データ競合を防止するため、Rust では同時に 2つの変数から値を変更することはできません。

```
struct Foo {
    x: i32,
}

fn do_something(f: Foo) {
    println!("{}", f.x);
    // f はここでドロップ
}

fn main() {
    let mut foo = Foo { x: 42 };
    let f = &mut foo;

    // 失敗: do_something(foo) はここでエラー
    // foo は可変に借用されており移動できないため

    // 失敗: foo.x = 13; はここでエラー
    // foo は可変に借用されている間は変更できないため

    f.x = 13;
    // f はここから先では使用されないため、ここでドロップ

    println!("{}", foo.x);

    // 可変な借用はドロップされているため変更可能
    foo.x = 7;

    // foo の所有権を関数に移動
    do_something(foo);
}
```
## 参照外し

`&mut` による参照では、`*` 演算子によって参照を外す (dereference)
ことで、所有者の値を設定できます。

`*`
演算子によって所有者の値のコピーを取得することもできます（コピー可能な型については後の章で説明します）。

```
fn main() {
    let mut foo = 42;
    let f = &mut foo;
    let bar = *f; // 所有者の値を取得
    *f = 13;      // 参照の所有者の値を設定
    println!("{}", bar);
    println!("{}", foo);
}
```

## 借用したデータの受け渡し

Rust の参照に関するルールは、以下のようにまとめられます。

-   Rust では、可変な参照が 1つだけか、不変な参照が複数かの**どちらか**が許可されます。**両方を同時には使用できません**。
-   参照は所有者よりも**長く存在**してはなりません。

これは関数へ参照を渡す際に問題となることはありません。

メモリの詳細:

-   参照の最初のルールはデータ競合を防ぎます。データ競合とは？ データを読み込む際、データへの書き込みが同時に行われると、同期が取れなくなる可能性があります。 これはマルチスレッドプログラミングでよく起こります。
-   参照の 2 番目のルールは、存在しないデータへの参照（C 言語ではダングリングポインタと呼ばれる）による誤動作を防ぐためのものです。

```
struct Foo {
    x: i32,
}

fn do_something(f: &mut Foo) {
    f.x += 1;
    // f への可変な参照はここでドロップ
}

fn main() {
    let mut foo = Foo { x: 42 };
    do_something(&mut foo);
    // 関数 do_something で可変な参照はドロップされるため、
    // 別の参照を作ることが可能
    do_something(&mut foo);
    // foo はここでドロップ
}
```
## 参照の参照

参照の一部を参照することができます。

```
struct Foo {
    x: i32,
}

fn do_something(a: &Foo) -> &i32 {
    return &a.x;
}

fn main() {
    let mut foo = Foo { x: 42 };
    let x = &mut foo.x;
    *x = 13;
    // x はここでドロップされるため、不変な参照が作成可能
    let y = do_something(&foo);
    println!("{}", y);
    // y はここでドロップ
    // foo はここでドロップ
}
```
## 明示的なライフタイム

Rust
では、常にコードに表れるわけではありませんが、コンパイラはすべての変数のライフタイムを管理しており、参照がその所有者よりも長く存在しないことを検証しようとします。

関数は、どの引数と戻り値とがライフタイムを共有しているかを、識別のための指定子で明示的に指定できます。

ライフタイム指定子は常に `'` で始まります（例: `'a`, `'b`, `'c`）。

```
struct Foo {
    x: i32,
}

// 引数 foo と戻り値はライフタイムを共有
fn do_something<'a>(foo: &'a Foo) -> &'a i32 {
    return &foo.x;
}

fn main() {
    let mut foo = Foo { x: 42 };
    let x = &mut foo.x;
    *x = 13;
    // x はここでドロップされるため、不変な参照が作成可能
    let y = do_something(&foo);
    println!("{}", y);
    // y はここでドロップ
    // foo はここでドロップ
}
```

## 複数のライフタイム

ライフタイム指定子は、関数の引数や戻り値のライフタイムをコンパイラが解決できない場合に、明示的に指定することができます。

```
struct Foo {
    x: i32,
}

// foo_b と戻り値はライフタイムを共有
// foo_a のライフタイムは別
fn do_something<'a, 'b>(foo_a: &'a Foo, foo_b: &'b Foo) -> &'b i32 {
    println!("{}", foo_a.x);
    println!("{}", foo_b.x);
    return &foo_b.x;
}

fn main() {
    let foo_a = Foo { x: 42 };
    let foo_b = Foo { x: 12 };
    let x = do_something(&foo_a, &foo_b);
    // ここから先は foo_b のライフタイムしか存在しないため、
    // foo_a はここでドロップ
    println!("{}", x);
    // x はここでドロップ
    // foo_b はここでドロップ
}
```
## スタティックライフタイム

**スタティック**変数は、コンパイル時に作成され、プログラムの開始から終了まで存在するメモリリソースです。
これらの変数の型は明示的に指定しなければなりません。

**スタティックライフタイム**は、プログラムの終了まで無期限に持続するメモリリソースです。
この定義では、スタティックライフタイムを持つリソースは実行時にも作成できることに注意してください。

スタティックライフタイムを持つリソースには、特別なライフタイム指定子
`'static` があります。

`'static` リソースは決して**ドロップ**することはありません。

スタティックライフタイムを持つリソースが参照を含む場合、それらはすべて
`'static`
でなければなりません（そうでなければ、参照はプログラムの終了前にドロップする可能性があります）。

メモリの詳細:

-   スタティック変数を変更することは本質的に危険です。なぜならスタティック変数は誰でもグローバルにアクセスして読み取ることができるからです。 グローバルデータの課題については後ほど説明します。
-   Rust ではコンパイラがメモリを保証できない操作を実行するために、`unsafe { ... }` ブロックを使用することができます。 R̸͉̟͈͔̄͛̾̇͜U̶͓͖͋̅Ṡ̴͉͇̃̉̀T̵̻̻͔̟͉́͆Ơ̷̥̟̳̓͝N̶̨̼̹̲͛Ö̵̝͉̖̏̾̔M̶̡̠̺̠̐͜Î̷̛͓̣̃̐̏C̸̥̤̭̏͛̎͜O̶̧͚͖͔̊͗̇͠N̸͇̰̏̏̽̃ について気軽に話してはいけません。

```
static PI: f64 = 3.1415;

fn main() {
    // スタティック変数は関数スコープでも定義可能
    static mut SECRET: &'static str = "swordfish";

    // 文字列リテラルは 'static ライフタイム
    let msg: &'static str = "Hello World!";
    let p: &'static f64 = &PI;
    println!("{} {}", msg, p);

    // ルールを破ることはできますが、それを明示する必要があります。
    unsafe {
        // 文字列リテラルは 'static なので SECRET に代入可能
        SECRET = "abracadabra";
        println!("{}", SECRET);
    }
}
```
## データ型のライフタイム

関数と同様に、データ型はメンバのライフタイムを指定できます。

Rust
は、参照を含む構造体が、その参照が指す所有者よりも長く存在しないことを検証します。

構造体には、何もないところを指している参照を含めることはできません。

```
struct Foo<'a> {
    i:&'a i32
}

fn main() {
    let x = 42;
    let foo = Foo {
        i: &x
    };
    println!("{}",foo.i);
}
```
## 第 5 章 - まとめ

ここまでお疲れ様でした。
所有権を受け入れるのは大変だと思いますが、あなたは Rustacean
への道を歩んでいます。 言語としての Rust
が、システムプログラミングに共通する課題の多くを解決しようとしているのが、はっきりしたのではないでしょうか。

-   リソースの意図しない変更
-   リソースの解放漏れ
-   リソースを誤って複数回解放
-   解放されたリソースの利用
-   他でリソースを読み込んでいる最中にリソースへの書き込みが行われた場合に発生するデータ競合
-   コンパイラが保証できない部分の明確化

次の章では、所有権を応用して、Rust
がどのようにテキストを扱うかを見ていきます。

# 第 6 章 - テキスト

さて、Rustにおけるメモリの考え方について少し理解できたので、テキストについて深堀りするための準備が整いました。
Rustでは、他の言語ではあまり馴染みのない国際的なテキストやバイトレベルの問題が考慮されています。
それでも、Rustにはこれらの問題を管理するための優れたツールが多くあります。

## 文字列リテラル

文字列リテラルは常にUnicodeです。
文字列リテラルの型は`&'static str`です。:

-   `&` はメモリ中の場所を参照していることを意味しており、 `&mut` を欠いているのは、 コンパイラがそれを修正することを認めていないということです。
-   `'static` は文字列データがプログラムの終了まで有効であるということを意味しています。（文字列データは決して消えません。）
-   `str` は常に有効な**utf-8**であるバイト列を指していることを意味しています。

メモリに関する詳細：

-   Rustのコンパイラは文字列をプログラムメモリのデータセグメントに入れるでしょう。

```
fn main() {
    let a: &'static str = "こんにちは 🦀";
    println!("{} {}", a, a.len());
}
```

## utf-8とは

様々な言語がコンピュター上で使われるようになるに連れて,
ASCIIで許可されている以上のテキスト文字を表現する必要が出てきました。（ASCIIで許可されているのは1バイト、つまり256文字です）

**utf-8**
は1～4バイトの可変バイト長で導入され、それによって表現可能な文字の範囲が大幅に広がりました。

可変サイズ文字の利点として挙げられるのは、テキストが非常に一般的なASCIIのための不要なバイトを持たなかったことです。（**utf-8**
で必要とされるのはたった1バイトです）

可変サイズの文字の欠点として挙げられるのは、簡単なインデキシング（例：4番目の文字を取得するために
`my_text[3]` を使用すること）における文字の検索が（**O(1)**
定数時間で）素早くできなくなることです。すぐ前にある文字が可変幅を持つことで、4番目の文字がバイト列のどこから実際に始まるのかが変わってしまう可能性があります。

その代わり、Unicode文字が実際にどこから始まるのかを知るために **utf-8**
バイトのシーケンスを繰り返さなければなりません。（計算量は線形時間
**O(n)**）

Ferris「水中にいるお友達の絵文字を表現するのに **utf-8**
があると嬉しいね！」

🐠🐙🐟🐬🐋


## エスケープ文字

特定の文字を視覚的に表現するのは難しいので、**エスケープ コード**
を使用することでその場所に記号を挿入することができます。

RustではC言語の共通エスケープコードがサポートされています。:

-   `\n` - 改行
-   `\r` - キャリッジ・リターン
-   `\t` - タブ
-   `\\` - バックスラッシュ
-   `\0` - null
-   `\'` - シングルクォート

エスケープ文字の一覧はここにあります。

```
fn main() {
    let a: &'static str = "Ferrisは言う:\t\"こんにちは\"";
    println!("{}",a);
}
```
## 複数行の文字列リテラル

Rustにおける文字列はデフォルトで複数行に対応しています。

改行したくない場合は、行の最後に `\` を挿入しましょう。

```
fn main() {
    let haiku: &'static str = "
        書いてみたり
        けしたり果ては
        けしの花
        - 立花北枝";
    println!("{}", haiku);


    println!("こんにちは \
    世界") // 世界の前にある間隔は無視されます
}
```
## 生文字列リテラル

生文字列では、`r#"`で始まり`"#`で終わる文字列を逐語的に書くことができます。
これによって、通常の文字列との区別がつかない可能性のある文字をリテラルとして挿入することができます。(二重引用符やバックスラッシュなど)

```
fn main() {
    let a: &'static str = r#"
        <div class="advice">
            生文字列は様々な場面で役に立ちます。
        </div>
        "#;
    println!("{}", a);
}
```
## ファイルから文字列リテラルを読み込む

非常に大きなテキストがある場合は, `include_str!` というマクロを使って
ローカルファイルのテキストをプログラムの中でインクルードしてみてください。：

```
let hello_html = include_str!("hello.html");
```

## 文字列スライス

文字列スライスは、常に有効な utf-8
でなければならないメモリ内のバイト列への参照です。

文字列のスライス(サブスライス)である `str` のスライスも有効な utf-8
でなければなりません。

`&str` の一般的なメソッド：

-   `len` は文字列リテラルの長さをバイト単位で取得します。（文字数ではない）
-   基本的なテストのための `starts_with`/`ends_with`
-   `is_empty` は長さがゼロの時にtrueを返します。
-   `find` はテキストの最初の位置の `Option<usize>` を返します。

```
fn main() {
    let a = "hi 🦀";
    println!("{}", a.len());
    let first_word = &a[0..2];
    let second_word = &a[3..7];
    // let half_crab = &a[3..5]; は失敗します。
    // Rust は無効な unicode 文字のスライスを受け付けません。
    println!("{} {}", first_word, second_word);
}
```
## Chars

Unicodeでの作業が非常に困難なため、Rustではutf-8バイトのシーケンスを
`char` 型の文字のベクトルとして取得する方法が提供されています。

char\` は常に 4
バイトの長さです。(これによって個々の文字を効率的に検索できるようになっています)

```
fn main() {
    // 文字をcharのベクトルとして集める
    let chars = "hi 🦀".chars().collect::<Vec<char>>();
    println!("{}", chars.len()); // should be 4
    // chars は 4 バイトなので、u32 に変換することができる
    println!("{}", chars[3] as u32);
}
```
## String

A **String** はヒープにutf-8バイト列をもつ構造体です。

そのメモリはヒープ上にあるため、文字列リテラルでは出来ないような、拡張や修正などが可能です。

共通のメソッド:

-   `push_str` 文字列の最後にutf-8バイトを追加します。
-   `replace` utf-8バイト列を他のutf-8バイト列で置換します。
-   `to_lowercase`/`to_uppercase` 大文字や小文字に変えます。
-   `trim` 空白を切り取ります。

Stringがドロップされると、そのヒープ内のメモリもドロップされます。

`String` には `&str`で文字列を拡張し、自分自身を返す `+`
演算子がありますが、 期待しているほど使い勝手は良くないかもしれません。

```
fn main() {
    let mut helloworld = String::from("hello");
    helloworld.push_str(" world");
    helloworld = helloworld + "!";
    println!("{}", helloworld);
}
```
## 関数パラメータとしてのテキスト

文字列リテラルや文字列は、一般的に文字列スライスとして関数に渡されます。
これによって、実際には所有権を渡す必要がないほとんど場合において柔軟性が増します。

```
fn say_it_loud(msg:&str){
    println!("{}!!!",msg.to_string().to_uppercase());
}

fn main() {
    // say_it_loudは&'static strを&strとして借用することができます
    say_it_loud("hello");
    // say_it_loudはStringを&strとして借用することもできます
    say_it_loud(&String::from("goodbye"));
}
```

## 文字列の構築

`concat` と `join`
は、文字列を構築するためのシンプルだが強力な方法です。

```
fn main() {
    let helloworld = ["hello", " ", "world", "!"].concat();
    let abc = ["a", "b", "c"].join(",");
    println!("{}", helloworld);
    println!("{}",abc);
}
```
## 文字列のフォーマット

`format!`マクロを使うと、パラメータ化された文字列を定義して文字列を作成することができ、
値をどこにどのように配置すべきかはプレースホルダ（例：`{}`）で指定します。

`format!` は `println!` と同じパラメータ付きの文字列を使用します。

この関数の機能は、*Tour of Rust* では説明しきれません。 ドキュメント をチェックしてください。

```
fn main() {
    let a = 42;
    let f = format!("secret to life: {}",a);
    println!("{}",f);
}
```
## 文字列変換

多くの型は `to_string` を用いて文字列に変換することができます。

ジェネリック関数 `parse`
を用いることで文字列や文字列リテラルを型付きの値に変換できます。この関数は失敗する可能性があるので、`Result`を返します。

```
fn main() -> Result<(), std::num::ParseIntError> {
    let a = 42;
    let a_string = a.to_string();
    let b = a_string.parse::<i32>()?;
    println!("{} {}", a, b);
    Ok(())
}
```

## 第 6 章 - まとめ

これで、テキストの基本が分かりましたね！これまで見てきたようにUnicodeによってテキストの操作は少し厄介になりますが、標準ライブラリにはその管理を簡単にするための多くの機能があります。

これまでほとんどの場合、手続き的なパラダイム（つまり、関数とデータだけ）からRustを見てきましたが、今回はRustのオブジェクト指向パラダイムによって開放されるtraitsと能力について話します。

