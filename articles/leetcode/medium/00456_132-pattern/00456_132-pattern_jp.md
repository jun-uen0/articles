## 456. 132 Pattern
URL: https://leetcode.com/problems/132-pattern   
タイトル: 132 Pattern   
難易度：中   

タグに二分探索法とついていて、二分探索法を使って解く問題だと思っていましたが、二分探索法は関係なく、単純にスタックを使って解く問題でした。   
但し、単純なコードで表せるにもかかわらず、結局自分のコードでは解くことができませんでした。   
問題がAcceptedになるにはO(N)の計算量で実装する必要があるのですが、そこまで辿り着くことができませんでした。   
今回は[NeetCode](https://www.youtube.com/c/NeetCode)の解答を元に解説をしていきたいと思います。   

参考のコード解説：[132 Pattern - Leetcode 456 - Python - YouTube](https://www.youtube.com/watch?v=q5ANAl8Z458&t)   

## 問題
Given an array of n integers nums, a 132 pattern is a subsequence of three integers nums[i], nums[j] and nums[k]
such that i < j < k and nums[i] < nums[k] < nums[j].   

Return true if there is a 132 pattern in nums, otherwise, return false.   

訳：   
n個の整数の配列numsが与えられる。   
132パターンとは、nums[i], nums[j], nums[k]の3つの整数の部分列で、   
i < j < k かつ nums[i] < nums[k] < nums[j] となるものである。   
numsに132パターンがあればtrueを返し、なければfalseを返せ。   

sequence... 順序付けられたものの集まり   

## コード
```py
# ローカルで実行するため、引数を変更しています。
def find132pattern(nums):
  stack = []
  curMin = nums[0]
  for n in nums[1:]:
    while stack and n >= stack[-1][0]:
      stack.pop()
    if stack and n > stack[-1][1]:
      return True
    stack.append([n,curMin])
    curMin = min(curMin,n)
  return False
```

## ① 初期値の設定
stack:   
値を格納していくスタックを用意します。   
初期値は空のリストです。   

curMin:   
現在の最小値を格納していく変数を用意します。   
初期値は配列の最初の要素とします。   
```py
def find132pattern(nums):

  # 初期値の設定
  stack = [] # 空のリストを用意
  curMin = nums[0] # 配列の最初の要素を用意
```

## ② Forループの作成
処理を実行するためのForループを作成します。   
範囲は配列の2番目から最後までとします。   
配列の2番目からとする理由は既に最初の要素をcurMinに格納しているためです。   
```py
def find132pattern(nums):
  stack = []
  curMin = nums[0]

  # Forループの作成
  for n in nums[1:]:
```

## ③ スタックに値を格納
スタックに値を格納する処理を実装します。   
最初のループではstackに[2,1]が格納され、   
stack = [[2,1]]   
となります。   
```py
def find132pattern(nums):
  stack = []
  curMin = nums[0]

  for n in nums[1:]:

    # スタックに値を格納
    stack.append([n,curMin])
```

## ④ 最小値を更新
最小値を更新する処理を実装します。   
スタックに追加したばかりのnとcurMinを比較し、   
nの方が小さければcurMinをnに更新します。   
```py
def find132pattern(nums):
  stack = []
  curMin = nums[0]

  for n in nums[1:]:
    stack.append([n,curMin])

    # 最小値を更新
    curMin = min(curMin,n)
```

## ⑤ スタックから値を取り出す
スタックから値を取り出す処理を実装します。   
nとスタックの最後の要素の0番目の値を比較します。   
nがスタックの最後の要素の0番目の値以上であれば、   
スタックから値を取り出します。   
```py
def find132pattern(nums):
  stack = []
  curMin = nums[0]

  for n in nums[1:]:

    # スタックから値を取り出す
    while stack and n >= stack[-1][0]:
      stack.pop()

    stack.append([n,curMin])
    curMin = min(curMin,n)
```

## ⑥ 132パターンの判定
最後に132パターンの判定を実装します。   
スタックの最後の要素の1番目の値とnを比較します。   
nがスタックの最後の要素の1番目の値より大きければ、   
132パターンが存在すると判定します。   
```py
def find132pattern(nums):
  stack = []
  curMin = nums[0]

  for n in nums[1:]:
    while stack and n >= stack[-1][0]:
      stack.pop()

    # 132パターンの判定
    if stack and n > stack[-1][1]:
      return True

    stack.append([n,curMin])
    curMin = min(curMin,n)
  return False
```

## 各ループの処理
nums = [1,2,0,3,-1,6,3]として、   
実際に各ループの処理を見てみましょう。   
考え方としては、各ループでスタックに   
左の値(132パターンの最小値)と   
真ん中の値(132パターンの最大値)を格納し、   
numsの値を右の値(132パターンの中間値)として   
判定していきます。   
```py
nums = [1,2,0,3,-1,6,3]
  ...
  for n in nums[1:]:
  
    ## 1回目のループ
    # stack = [], curMin = 1, n = 2
    while stack and n >= stack[-1][0]: # False: stackが空
      stack.pop()
    if stack and n > stack[-1][1]: # False: stackが空
      return True
    stack.append([n,curMin]) # stackを更新 -> [[2,1]]
    curMin = min(curMin,n) # curMinを更新 -> 1
  
    ## 2回目のループ
    # stack = [[2,1]], curMin = 1, n = 0
    while stack and n >= stack[-1][0]: # False: 0 >= 2
      stack.pop()
    if stack and n > stack[-1][1]: # False: 0 > 1
      return True
    stack.append([n,curMin]) # stackを更新 -> [[2,1],[0,1]]
    curMin = min(curMin,n) # curMinを更新 -> 0

    ## 3回目のループ
    # stack = [[2,1],[0,1]], curMin = 0, n = 3
    while stack and n >= stack[-1][0]: # True: 3 >= 0 | True: 3 >= 2
      stack.pop() # stackを更新 / 2回pop() -> []
    if stack and n > stack[-1][1]: # False: stackが空
      return True
    stack.append([n,curMin]) # stackを更新 -> [[3,0]]
    curMin = min(curMin,n) # curMinを更新 -> 0

    ## 4回目のループ
    # stack = [[3,0]], curMin = 0, n = -1
    while stack and n >= stack[-1][0]: # False: -1 >= 3
      stack.pop()
    if stack and n > stack[-1][1]: # False: -1 > 0
      return True
    stack.append([n,curMin]) # stackを更新 -> [[3,0],[-1,0]]
    curMin = min(curMin,n) # curMinを更新 -> -1
  
    ## 5回目のループ
    # stack = [[3,0],[-1,0]], curMin = -1, n = 6
    while stack and n >= stack[-1][0]: # True: 6 >= -1 | True: 6 >= 3
      stack.pop() # stackを更新 / 2回pop() -> []
    if stack and n > stack[-1][1]: # False: stackが空
      return True
    stack.append([n,curMin]) # stackを更新 -> [[6,-1]]
    curMin = min(curMin,n) # curMinを更新 -> -1
  
    ## 6回目のループ
    # stack = [[6,-1]], curMin = -1, n = 3
    while stack and n >= stack[-1][0]: # False: 3 >= 6
      stack.pop()
    if stack and n > stack[-1][1]: # True: 3 > -1
      return True # [-1,6,3]で132パターンを検出 / Trueを返す
    
  return False
```