# Chapter 1 イントロダクション

## 1.1 効率の必要性

- 操作の数： 100万（10^6）個の要素をもつWebアプリにおいて、毎回すべての要素を100万個の要素から探すと仮定すると、すべての要素を確認するのに最悪１兆（10^12）回データを読み出す必要がある。

- プロセッサの速度: 高速なデスクトップコンピュータでされ、毎秒10億回以上の操作は実行できないので、上記の操作を完了するには、$10^{12}/10^{9}=1000$秒、すなわち16.7分かかる。

- 大きなデータセット: Googleは85億ものWebページを対象に検索を行っているので、上記のメソッドで検索を行っているとすると、8.5秒も検索に時間がかかるが、実際Googleの検索エンジンはそんなに遅くない（コンマ数秒レベル）。

- 解決策: アルゴリズムによるデータの並び替え。参照するデータの数を減らしていく。

## 1.2 インターフェイス

### インターフェイスと実装

- インターフェイス: データ構造がサポートしている操作一式。インターフェイスからわかるのは、そのデータ構造がサポートしている操作の一覧と、それらの操作に対する引数及び返り値の特徴。

- 実装：データ構造の内部表現、と実際に操作を行うアルゴリズムの定義。

## 1.3 数学的背景

- 指数：$b^x$

- 対数：$log_{b}k$ とは、k を何回 b で 割ると 1 以下になるかを表す数。自然対数と二進対数は比較可能。

[![Image from Gyazo](https://i.gyazo.com/bfed0520d3d2398b81a20e7de9fa5f40.png)](https://gyazo.com/bfed0520d3d2398b81a20e7de9fa5f40)

- 階乗：n!の大きさはスターリングの近似を使って見積もることができる。

[![Image from Gyazo](https://i.gyazo.com/61ea80ae2206cd01681e8c5ab70668e4.png)](https://gyazo.com/61ea80ae2206cd01681e8c5ab70668e4)

[![Image from Gyazo](https://i.gyazo.com/da3ac7f08bd94d279d816613816e1508.png)](https://gyazo.com/da3ac7f08bd94d279d816613816e1508)

- 漸近記法（ビッグオー記法）：ある関数$f(n)$について、次のように定義される関数の集合$O(f (n))$。

[![Image from Gyazo](https://i.gyazo.com/345d16bb17924ed9332acaf68b26e2d4.png)](https://gyazo.com/345d16bb17924ed9332acaf68b26e2d4)

```
public static void snippet(int n) {
    for (int i = 0; i < n; i++) {
        a[i] = i;
    }
}
```
1. 代入1回 (int i = 0)
2. 比較n+1回 (i < n)
3. インクリメントn回 (i++)
4. 配列のオフセット計算n回 (a[i])
5. 間接代入n回 (a[i]=i)

$$T(n) = a+b(n+1)+cn+dn+en$$

$$T (n) = O(n)$$

- 期待実行時間: 乱択アルゴリズムを分析する際に用いる。

[![Image from Gyazo](https://i.gyazo.com/8ad908ba07055d1edd894e89d7972c02.png)](https://gyazo.com/8ad908ba07055d1edd894e89d7972c02)

## 1.4 計算モデル

- w ビットのワードRAM(word-RAM)モデル: ワード幅 w において、データ構造に格納されうる要素数がnであれば$w > logn$と仮定する。

## 1.5 正しさ、時間計算量、空間計算量

### 性能

- 正しさ: データ構造はそのインターフェースを正しく実装しなければならない。

- 時間計算量(time complexity): データ構造における操作の実行時間は短いほどよい。

- 空間計算量(space complexity): データ構造のメモリ使用量は小さいほどよい。

### 実行時間の議論

- 最悪実行時間(worst-case running time): 実行時間に対する保証の中で、最も強力なもの。

- 償却実行時間(amortized running time): 償却実行時間が $f(n)$であるとは、典型的な操作にかかるコストが $f(n)$超えないことを意味する。より正確には、$m$ 個の操作にかかる実行時間を合計しても、 $mf(n)$を超えないことを意味する

- 期待実行時間(expected running time): 実行時間が確率変数であり、 その確率変数の期待値が$f(n)$であることを意味する。

# Chapter 2 配列を使ったリスト

# Chapter 3 連結リスト

# Chapter 4 スキップリスト

# Chapter 5 ハッシュテーブル

ハッシュテーブル: 「ハッシュ値」を使うことによって、要素の挿入・削除・検索を非常に高速に行うことができるインターフェイス。

## 5.1 ChainedHashTable: チェイン法を使ったハッシュテーブル

ChainedHashTableというデータ構造では、チェイン法を使ってデータをリストの配列tに保存する。また、リスト全体に格納されている要素数の合計を整数 n とする。

[![Image from Gyazo](https://i.gyazo.com/90fda4ddea2fe5e8df02b5eb35a9222b.png)](https://gyazo.com/90fda4ddea2fe5e8df02b5eb35a9222b)

```java
List<T>[] T;
int n;
```
データ x のハッシュ値を $hash(x)$ と書く。$hash(x)$ は {$0,...,t.length − 1$} の範囲にある値である。ハッシュ値が $i$ であるようなデータは、すべてリスト $t[i]$ に格納する。

$n ≤ t.length$ という不変条件を保持することで、リストの平均要素数は常に1 以下になる($n/t.length ≤ 1$)。


ハッシュテーブルに要素xを追加するには、配列tの大きさを増やす必要があるかどうかを確認し、配列の拡張が必要な場合は、tの大きさを2倍にする（元のテーブルに入っていた要素をすべて新しい要素に入れ直す（償却実行時間：$O(1)$））。その後、 x を ChainedHashTable に追加する（$O(1)$）。

```java
boolean add(T x) {
    if (find(x) != null) {
        return false;
    }
    if (n+1 > t.length) {
        resize();
    }
    t[hash(x)].add(x);
    n++;
    return true;
}
```

要素 x をハッシュテーブルから削除するには、x が見つかるまでリスト
t[hash(x)] を辿ればよい。$O(n_{hash(x)})$

```java
T remove(T x) {
    Iterator<T> it = t[hash(x)].iterator();
    while(it.hasNext()) {
        T y = it.next();
        if (y.equals(x)) {
            it.remove();
            n--;
            return y;
        }
    }
    return null;
}
```

ハッシュテーブルからｘを見つける操作も同様に、t[hash(x)] を辿ればよい。$O(n_{hash(x)})$

```java
T find(Object x) {
    for (T y : t[hash(x)]) {
        if (y.equals(x)) {
            return y;
        }
    }
    return null;
}
```

ハッシュテーブルの性能はハッシュ関数の選択に大きく左右される。良いハッシュ関数は、要素を t.length 個のリストに均等に分散する関数であり、このときの各リストの長さの期待値は $O(n/t.length) = O(1)$ となる。

一方、最悪のハッシュ関数は、すべての要素を同じリストに追加してしまう。すなわち、リスト t[hash(x)] の長さを n にしてしまう。

### 乗算ハッシュ法

剰余算術と整数の割り算からハッシュ値を効率的に計算する方法。

乗算ハッシュ法では、ある整数 $d$ について、大きさ $2^d$ であるハッシュテーブルを使う。整数 $d$ は次数(dimension)と呼ばれる。整数 $x ∈ \{0,...,2
w −1\}$のハッシュ値は次のように計算する。

$hash(x) = ((z · x) mod 2^w)div 2^{w−d}$

ここで、z は奇数の集合 $\{1,3,5,...,2w − 1\}$ からランダムに選択する。整数のビット数を w とするとき、整数の演算の結果は $2^w$ を法として合同になる。

[![Image from Gyazo](https://i.gyazo.com/f0383b0fe4e5fc6e3e47de4860aaad7a.png)](https://gyazo.com/f0383b0fe4e5fc6e3e47de4860aaad7a)

```java
int hash(Object x) {
    return ((unsigned) (z * x % Math.pow(2, w))) >> (w-d);
}
```

例:
```java
int hash (int x) {
    int x = 42;
    int w = 32;
    int d = 8;
    long z = 4102541685l;
    return (long) (z * x % Math.pow(2, 32)) >> (w-d);
}
```

### 要約

ChainedHashTable は、USet インターフェースを実装する。grow() のコストを無視すると、ChainedHashTable における add(x)、remove(x)、find(x) の期待実行時間は O(1) である。さらに、空の ChainedHashTable に対して m 個の add(x)、remove(x) からなる任意の操作列を順に実行するとき、grow() の呼び出しに要する償却実行時間は O(m) である。

## 5.2 LinearHashTable:線形探索法

LinearHashTableというデータ構造では、オープンアドレス法と呼ばれる、配列ｔに直接要素を収める手法を用いている。

LinearHashTable の背景となるのは、$i = hash(x)$ となる要素 x をテーブルに格納するときに理想的な場所は t[i] であろうという考え方である。すでにそこに他の要素が格納されている場合、t[(i+1) mod t.length]を試す。それが無理なら t[(i+2) mod t.length] と続いていく。

t の値としては次の 3 種類を使う。

1. データの値: USet に実際に入っている値
2. null:データが入っていないことを示す値
3. del:データが入っていたがそれが削除されたことを示す値

カウンタとしては、LinearHashTable の要素数 n と、データの個数と del の個数の合計 q を使う。つまり、q の値は、t の中の del の個数を n に加えた値である。効率を考えると、t には null になっている場所がたくさん欲しいので、t の大きさを q に比べて十分に大きくする必要がある。そこで、LinearHashTable の操作では、不変条件 $t.length ≥ 2q$ を常に満たすようにする。

```java
T[] t; // the table
int n; // the size
int d; // t.length = 2ˆd
int q; // number of non-null entries in t
```

findの実装：

```java
T find(T x) {
    int i = hash(x);
    while(t[i] != null) {
        if (t[i] != del && x.equals(t[i])) {
            return t[i];
        }
        i = (i == t.length-1) ? 0 : i + 1; // increment i
    }
    return null;
}
```

addの実装：

```java
boolean add(T x) {
    if (find(x) != null) return false;
    if (2*(q+1) > t.length) resize(); // max 50% occupancy
    int i = hash(x);
    while (t[i] != null && t[i] != del)
        i = (i == t.length-1) ? 0 : i + 1; // increment i
    if (t[i] == null) q++;
    n++;
    t[i] = x;
    return true;
}
```

removeの実装：

```java
T remove(T x) {
    int i = hash(x);
    while (t[i] != null) {
        T y = t[i];
        if (y != del && x.equals(y)) {
            t[i] = del;
            n--;
            if (8*n < t.length) resize(); // min 12.5% occupancy
            return y;
        }
        i = (i == t.length-1) ? 0 : i + 1; // increment i
    }
    return null;
}
```

resizeの実装

```java
void resize() {
    d = 1;
    while((1<<d) < 3*n) d++;
    T[] told = t;
    t =  newArray(1<<d);
    q = n;
    // insert everything from told
    for (int k = 0; k < told.length; k++) {
        if (told[k] != null && told[k] != del) {
            int i = hash(told[k]);
            while (t[i] != null)
                i = (i == t.length-1) ? 0 : i + 1;
            t[i] = told[k];
        }
    }
}
```

オープンアドレス法においては、ハッシュ値が $\{0, . . . , t.length − 1\}$ の範囲の一様な確率分布に従う独立な値であると仮定する。=> Tabulation Hashing


### 要約

resize() のコストを無視すると、LinearHashTable における add(x)、remove(x)、find(x) の期待実行時間 は O(1) である。さらに、空の LinearHashTable に対して add(x)、remove(x) からなる m 個の操作 の列を順に実行するとき、resize() にかかる時間の合計は O(m) である。


### Tabulation Hashing

大きさ 2w の巨大な配列 tab を準備し、すべてのエントリを互いに独立なwビットのランダムな整数で初期化するというものがある。こうしておけば、 tab[x.hashCode()] から d ビットの整数を取り出すことで hash(x) を実装できる。

```java
int idealHash(T x) {
    return tab[hashCode(x) >> w-d];
}
```

あいにく、大きさ 2w の配列を 1 つ保持するのはメモリ利用の観点からは禁じ手であ る。そこでTabulation Hashingでは、wビットの整数を、それぞれがrビットのw/r 個の整数から構成されたものとして扱う。 この方法であれば、それぞれ大きさ 2r の 配列が w/r 個あればよい。これらの配列の全エントリを、互いに独立な w ビットの ランダムな整数とする。hash(x) を計算するには、x.hashCode() を w/r 個の r ビッ ト整数に分割し、それぞれを配列の添字として使う。その後、各配列の値からビッ ト単位の排他的論理和を計算し、その結果を hash(x) とする。次のコードは w = 32、 r = 8 の場合のものである。

```java
int hash(T x) {
    int h = x.hashCode();
    return (tab[0][h&0xff]
            ˆ tab[1][(h>>8)&0xff]
            ˆ tab[2][(h>>16)&0xff]
            ˆ tab[3][(h>>24)&0xff])
            >> (w-d);
}
```

この場合、tabは4つの列と28 =256の行からなる二次元配列となる。
任意の x について hash(x) が {0, . . . , 2d − 1} の値を一様な確率で取ることは簡単に検証できる。

## 5.4 ディスカッション

上記とは別のハッシュテーブルの実装として、完全ハッシュ法と呼ばれる種類のものがある。完全ハッシュ法では、find(x) の実行時間が、最悪の場 合でも O(1) となる。

Dos攻撃にも使われる。
https://www.usenix.org/legacy/events/sec03/tech/full_papers/crosby/crosby.pdf




