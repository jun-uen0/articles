# セグメントツリー

## はじめに

セグメントツリーは、動的な範囲クエリを効率的に処理するためのツリーデータ構造です。
このデータ構造が「セグメントツリー」と呼ばれるのは、配列を再帰的に分割し、最小単位が 1 になるまで区間を細かく分割する仕組みに由来します。
この分割の考え方は二分探索法にも似ています。

**トレードオフ:** メモリ消費量が多い。

## 実装方法

### 例: 範囲内の最大値を求める

```py
class SegmentTree:
    def __init__(self, arr):
        self.n = len(arr)
        self.tree_size = 1
        self.init_value = float("-inf")

        while self.tree_size < self.n:
            self.tree_size *= 2

        # データセットの作成
        # 空間計算量: O(2n)
        self.data = [self.init_value] * (2 * self.tree_size)

        # セグメントツリーの構築
        # 時間計算量: O(n)
        for i in range(self.n):
            self.data[self.tree_size + i] = arr[i]
        
        # 時間計算量: O(n)
        for i in range(self.tree_size - 1, 0, -1):
            self.data[i] = max(self.data[i * 2], self.data[i * 2 + 1])

    def update_node(self, index, value):
        node = index - 1 + self.tree_size
        self.data[node] = value

        # 時間計算量: O(log n)
        while node > 1:
            parent = node // 2
            self.data[parent] = max(self.data[parent * 2], self.data[parent * 2 + 1])
            node = parent

    def range_max(self, left, right):
        # 基本ケース: left は right より小さくなければならない
        if left > right:
            return float("-inf")
        
        left += self.tree_size - 1
        right += self.tree_size - 1
        res = float("-inf")
        
        # 時間計算量: O(log n)
        while left <= right:
            if left % 2 == 1:
                res = max(res, self.data[left])
                left += 1
            if right % 2 == 0:
                res = max(res, self.data[right])
                right -= 1
            left //= 2
            right //= 2
        
        return res


# 使用例:
arr = [1, 2, 3, 4, 5, 6, 7]
seg_tree = SegmentTree(arr)

# 値の更新
seg_tree.update_node(1, 2)
seg_tree.update_node(2, 4)
seg_tree.update_node(3, 1)
seg_tree.update_node(4, 5)
seg_tree.update_node(5, 4)
seg_tree.update_node(6, 3)
seg_tree.update_node(7, 2)

# セグメントツリーのクエリ実行
print(seg_tree.range_max(6, 2))  # 無効な範囲 -> -inf を返す
print(seg_tree.range_max(2, 2))  # 4 を返すはず
print(seg_tree.range_max(3, 7))  # 5 を返すはず
```

## いつ使用すべきか？
- 範囲クエリに対して効率的な応答が必要なとき。
- 動的に要素を更新する必要があるとき。

## 実世界での応用例
- **株式市場分析**: 特定の時間範囲内での最大/最小価格を求める。
- **ビッグデータクエリ**: 範囲に基づいた効率的な計算。

## 他のアプローチとの比較

### セグメントツリー vs. フェニックツリー（BIT）
- フェニックツリー（BIT）はシンプルだが、範囲更新が効率的にできない。
- セグメントツリーはより複雑なクエリ（max/min/sum/gcd など）をサポートできる。

### セグメントツリー vs. スパーステーブル
- スパーステーブルはクエリが高速（O(1) vs. O(log n)）。
- ただし、スパーステーブルは静的データにしか対応できず、更新ができない。

## 使用を避けるべきケース
- **メモリ消費が大きい** (O(2n))ため、メモリが限られている場合は避ける。
- **更新がほとんど発生しない場合**: Python の `max()` を使うほうが簡単（O(n)）。