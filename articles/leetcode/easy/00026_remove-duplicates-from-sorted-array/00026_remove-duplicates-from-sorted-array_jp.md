## 26. Remove Duplicates from Sorted Array
「ソート済みの配列から重複を削除する」
https://leetcode.com/problems/remove-duplicates-from-sorted-array
難易度：簡単

ソート済みの配列から重複を削除する問題です。   
配列操作の基礎問題、という感じですね。   
今回は簡単な問題なので私自身のコードで解説してみます。   
ちょっと問題で分かりづらいのが、配列を返すと思いきや、   
配列そのものではなく、配列の長さを返すという点には注意する必要があります。   

## 問題
Given an integer array nums sorted in non-decreasing order,
remove the duplicates in-place such that each unique element appears only once.   
The relative order of the elements should be kept the same.   

Since it is impossible to change the length of the array in some languages,   
you must instead have the result be placed in the first part of the array nums.   
More formally, if there are k elements after removing the duplicates,   
then the first k elements of nums should hold the final result.   
It does not matter what you leave beyond the first k elements.   

Return k after placing the final result in the first k slots of nums.   

Do not allocate extra space for another array.   
You must do this by modifying the input array in-place with O(1) extra memory.   

訳：
整数の配列numsが与えられます。この配列は非減少順にソートされています。   
重複を削除して、各要素が1回だけ現れるようにしてください。   
要素の相対的な順序は変更しないでください。   

配列の長さを変更することができない言語があるため、   
結果を配列numsの最初の部分に配置する必要があります。   
より正確には、重複を削除した後にk個の要素がある場合、   
numsの最初のk個の要素に最終結果を保持する必要があります。   
最初のk個の要素以降に何を残しても構いません。   

最初のkスロットに最終結果を配置した後、   
**kの値を返してください。**   

別の配列の追加のための追加のスペースを割り当てないでください。   
O（1）の追加のメモリを使用して、入力配列を場所で変更する必要があります。   

## 解答
```python
# もしローカルで実行する場合はListをインポートする必要があります。
from typing import List
nums = [1,1,1,2,2,3,3,4] # Input

def remove_duplicates(nums: List[int]):
  d = 0
  for i in range(1,len(nums)):
    if nums[i] == nums[i-1]:
      d+=1
    else:
      nums[i-d] = nums[i]
  return len(nums) - d
print(remove_duplicates(nums)) # 4
```

## 手順
① 各要素の重複をカウントする変数を用意   
② ループを作成   
③ 左隣の要素と比較して重複しているか確認し、配列を操作   
この処理の配列操作を詳しく見てみる   
④ 解答を返す   

## ① 各要素の重複をカウントする変数を用意
ループ内で処理を実行する前に、   
各要素の重複をカウントする変数を用意します。   

d... duplicateの略   
```py
def remove_duplicates(nums: List[int]):

  # 各要素の重複をカウントする変数を用意
  d = 0
```

## ② ループを作成
ループを作成します。   
範囲は配列nums全ての要素。   
nums = [1,1,1,2,2,3,3,4]の場合、8   
```py
def remove_duplicates(nums: List[int]):
  d = 0

  # ループを作成
  for i in range(1,len(nums)):
```

## ③ 左隣の要素と比較して重複しているか確認し、配列を操作
左隣の要素と比較して重複しているか確認します。   
重複している場合は、重複をカウントする変数dに1を足します。   
重複していない場合は、カウントした重複分要素を左にずらします。      
```py
def remove_duplicates(nums: List[int]):
  d = 0
  for i in range(1,len(nums)):

    # 左隣の要素と比較して重複しているか確認
    ## もし重複していれば、重複をカウントする変数dに1を足す
    if nums[i] == nums[i-1]:
      d+=1
    ## 重複していない場合は、カウントした重複分要素を左にずらす
    else:
      nums[i-d] = nums[i]
```

## この処理の配列操作を詳しく見てみる
nums = [1,1,2,2,3,4]の場合、
```py
# 1回目のループ (iはnums[0])):
# d = 0
# nums = [1,1,2,2,3,4]
if nums[i] == nums[i-1]: # 1 == undefined なので、False
  d+=1
else:
  nums[i-d] = nums[i] # nums[0-0] = nums[0] ※ 配列に変化なし

# 2回目のループ (iはnums[1])):
# d = 0
# nums = [1,1,2,2,3,4]
if nums[i] == nums[i-1]: # 1 == 1 なので、True
  d+=1 # d = 1
else:
  nums[i-d] = nums[i] # 処理スキップ

# 3回目のループ (iはnums[2])):
# d = 1
# nums = [1,1,2,2,3,4]
if nums[i] == nums[i-1]: # 2 == 1 なので、False
  d+=1
else:
  nums[i-d] = nums[i] # nums[2-1] = nums[2] ※ nums[1] = 2

# 4回目のループ (iはnums[3])):
# d = 1
# nums = [1,2,2,2,3,4]
if nums[i] == nums[i-1]: # 2 == 2 なので、True
  d+=1 # d = 2
else:
  nums[i-d] = nums[i] # 処理スキップ

# 5回目のループ (iはnums[4])):
# d = 2
# nums = [1,2,2,2,3,4]
if nums[i] == nums[i-1]: # 3 == 2 なので、False
  d+=1
else:
  nums[i-d] = nums[i] # nums[4-2] = nums[4] ※ nums[2] = 3

# 6回目のループ (iはnums[5])):
# d = 2
# nums = [1,2,3,2,3,4]
if nums[i] == nums[i-1]: # 4 == 3 なので、False
  d+=1
else:
  nums[i-d] = nums[i] # nums[5-2] = nums[5] ※ nums[3] = 4

# ループ終了後
# d = 2
# nums = [1,2,3,4,3,4]
```

## ④ 解答を返す
配列の長さから重複をカウントした変数dを引いた値を返します。   
冒頭でも説明したように、   
今回の解答では表示させたい要素の数を返す必要があります。   
LeetCode側でその値を元に操作されたnumsを確認し、成否を判断します。   
```py
def remove_duplicates(nums: List[int]):
  d = 0
  for i in range(1,len(nums)):
    if nums[i] == nums[i-1]:
      d+=1
    else:
      nums[i-d] = nums[i]

  # 解答を返す
  return len(nums) - d
```