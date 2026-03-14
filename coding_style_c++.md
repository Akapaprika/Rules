# C++ コーディング規約

本プロジェクトではコードの **一貫性・保守性・性能** を確保するために以下のコーディング規約を定める。

本規約は主に

* Google C++ Style Guide
* C++ Core Guidelines

の思想を参考にしている。

---

# 1. 基本方針

本プロジェクトでは **責務の分離 (Separation of Responsibilities)** を最重要原則とする。

設計では以下を徹底する。

* クラスは **単一の責務** を持つ
* 関数は **明確な役割** を持つ
* インターフェースと実装を分離する

理想状態

```
ヘッダを見るだけで API の仕様を理解できる
```

実装は性能最適化のために複雑になってもよい。
ただしその場合は **コメントで理由を説明すること。**

---

# 2. ファイル命名

ファイル名は **snake_case** を使用する。

例

```
game_board.hpp
game_board.cpp
bitboard_utils.hpp
```

---

# 3. 命名規則

| 対象        | ルール         | 例              |
| --------- | ----------- | -------------- |
| クラス       | PascalCase  | `GameBoard`    |
| 構造体       | PascalCase  | `ChainResult`  |
| enum      | PascalCase  | `CellType`     |
| 関数        | lowerCamelCase  | `dropPiece()` |
| 変数        | snake_case  | `chain_count`  |
| 定数        | kPascalCase | `kBoardWidth`  |
| namespace | snake_case  | `puyotan`      |
| macro     | UPPER_CASE  | `MAX_BUFFER`   |

---

# 4. フォーマット

## インデント

```
4スペース
タブ禁止
```

---

## 波括弧

```
if (condition) {
    do_something();
}
```

---

# 5. include

include順序

```
1 自分のヘッダ
2 標準ライブラリ
3 外部ライブラリ
4 プロジェクトヘッダ
```

例

```cpp
#include "game_board.hpp"

#include <array>
#include <vector>

#include "bitboard.hpp"
```

---

# 6. ヘッダと実装

ヘッダファイル `.hpp` は **公開インターフェースを定義する場所** とする。

ヘッダを読むだけで以下が理解できる状態が理想。

```
クラスの役割
関数の目的
API仕様
```

実装の詳細は `.cpp` に記述する。

---

# 7. コメント規則

コメントは以下の2種類を使用する。

```
1. 関数仕様コメント
2. 実装補足コメント
```

---

# 8. 関数仕様コメント

関数の仕様説明は **ヘッダファイル (.hpp)** に記述する。

目的

```
実装を読まなくても API を理解できる状態
```

記載内容

```
関数の目的
引数
戻り値
副作用
```

例

```cpp
// 指定した列にぷよを落下させる
//
// @param column 落下させる列
// @return 落下が成功した場合 true
bool drop_piece(int column);
```

---

# 9. 実装補足コメント

`.cpp` では以下の目的でコメントを書く。

```
アルゴリズム説明
最適化理由
非直感的な処理の説明
等
```

例

```cpp
// ビット演算で連鎖判定を高速化
// 分岐削減のためビットマスクを使用
mask &= (board << 1);
```

---

# 10. メンバ変数

privateメンバ変数は `_` を付ける。

```
int chain_count_;
BitBoard board_;
```

---

# 11. enum

`enum class` を使用する。

```cpp
enum class Cell
{
    Empty,
    Red,
    Green,
    Blue
};
```

---

# 12. const

可能な限り `const` を付ける。

```cpp
int get_score() const;
```

---

# 13. モダンC++の使用

以下を優先する。

```
std::array
std::vector
std::optional
std::unique_ptr
std::span
```

`new / delete` は使用しない。

例

```cpp
auto board = std::make_unique<GameBoard>();
```

---

# 14. ヘッダ内ロジック

ヘッダ内に実装を書くのは以下のみ許可する。

```
inline
constexpr
template
```

それ以外は `.cpp` に実装する。

---

# 15. パフォーマンス

性能最適化は歓迎する。

可読性よりも **パフォーマンスを優先してよい。**

ただし以下をコメントで説明すること。

```
なぜその実装を選択したのか
```
