# Python コーディング規約

本プロジェクトではコードの **一貫性・保守性・可読性** を確保するために以下のコーディング規約を定める。

本規約は主に以下のガイドラインを参考にしている。

* PEP 8 – Style Guide for Python Code
* PEP 257 – Docstring Conventions

---

# 1. 基本方針

本プロジェクトでは **責務の分離 (Separation of Responsibilities)** を重要な設計原則とする。

設計では以下を徹底する。

* クラスは **単一の責務** を持つ
* 関数は **明確な役割** を持つ
* モジュールの役割を明確にする

理想状態

```
関数・クラスのdocstringを読むだけでAPIを理解できる
```

---

# 2. ファイル命名

Pythonのモジュール名は **snake_case** を使用する。

例

```
game_board.py
chain_detector.py
bitboard_utils.py
```

---

# 3. 命名規則

| 対象      | ルール        | 例                 |
| ------- | ---------- | ----------------- |
| クラス     | PascalCase | `GameBoard`       |
| 関数      | snake_case | `drop_piece()`    |
| 変数      | snake_case | `chain_count`     |
| 定数      | UPPER_CASE | `BOARD_WIDTH`     |
| モジュール   | snake_case | `game_board`      |
| private | `_name`    | `_internal_state` |

例

```python
class GameBoard:
    def drop_piece(self, column: int) -> bool:
        pass
```

---

# 4. フォーマット

## インデント

```
4スペース
タブ禁止
```

---

## 行の長さ

```
最大79文字
```

（PEP8標準）

---

# 5. import

import順序

```
1 標準ライブラリ
2 サードパーティ
3 プロジェクトモジュール
```

例

```python
import os
import sys

import numpy as np

from puyotan.board import GameBoard
```

---

# 6. Docstring

Pythonでは関数説明は **docstring** を使用する。

目的

```
実装を読まなくてもAPI仕様を理解できる状態
```

例

```python
def drop_piece(column: int) -> bool:
    """
    指定した列にぷよを落下させる。

    Parameters
    ----------
    column : int
        落下させる列

    Returns
    -------
    bool
        落下が成功した場合 True
    """
```

---

# 7. コメント

コメントは以下の用途で使用する。

```
アルゴリズムの説明
非直感的な処理の説明
最適化の理由
```

例

```python
# ビット演算を使って高速に接続判定を行う
mask &= board << 1
```

---

# 8. 型ヒント

可能な限り **型ヒント (Type Hint)** を使用する。

例

```python
def compute_score(chain: int) -> int:
    return chain * 10
```

---

# 9. 定数

定数は **モジュールレベルで定義する。**

```python
BOARD_WIDTH = 6
BOARD_HEIGHT = 12
```

---

# 10. パフォーマンス

Pythonでは通常 **可読性を優先する。**

ただしパフォーマンスが重要な場合は

* アルゴリズム改善
* ベクトル化
* C拡張

などを検討する。
