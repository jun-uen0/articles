## 349. Intersection of Two Arrays
URL: https://leetcode.com/problems/intersection-of-two-arrays   
難易度: 簡単   

簡単な問題です。   
ただ、私は二分探索を使って解きましたが、あまりにも冗長なコードとなってしまい、他の人の解答からもっと簡潔なコードを見つけました。   
私のコードは48行あるのですが、今回解説するコードはたったの一行です。   
いかにプログラム言語の特性やルール、記法や応用も兼ねた知識が重要なのかを実感しました。   
とても反省してます。   

参考のコード: [[Java/Python 3] Slide Window O(n) codes]https://donic0211.medium.com/leetcode-349-intersection-of-two-arrays-9f99b27cf247)    

## 問題文
Given two integer arrays nums1 and nums2, return an array of their intersection.   
Each element in the result must be unique and you may return the result in any order.   

訳：   
整数の配列nums1とnums2が与えられる。二つの配列の共通部分を返せ。   
結果の配列の要素は重複しないこと。順番は問わない。   

## 例
```py
Example 1:
Input: nums1 = [1,2,2,1], nums2 = [2,2]
Output: [2]

Example 2:
Input: nums1 = [4,9,5], nums2 = [9,4,9,8,4]
Output: [9,4]
※ [4,9]でもOK
```

## コード
```py
def intersection(nums1, nums2):
  return list(set(nums1) & set(nums2))
```

## 手順
① Setを使って重複を除く   
② 二つのSetの共通部分を取得する   
③ Listに変換する   

## ① Setを使って重複を除く
```py
nums1 = [4,9,5,4]
nums2 = [9,4,9,8,4]

def intersection(nums1, nums2):

  # Setを使って重複を除く
  st_1 = set(nums1) # {4, 5, 9}
  st_2 = set(nums2) # {8, 9, 4}
```

## ② 二つのSetの共通部分を取得する
```py
def intersection(nums1, nums2):
  st_1 = set(nums1) # {4, 5, 9}
  st_2 = set(nums2) # {8, 9, 4}

  # 二つのSetの共通部分を取得する
  intersection = st_1 & st_2 # {4, 9}
```

## ③ Listに変換する
```py
def intersection(nums1, nums2):
  st_1 = set(nums1) # {4, 5, 9}
  st_2 = set(nums2) # {8, 9, 4}
  intersection = st_1 & st_2 # {4, 9}

  # Listに変換する
  return list(intersection) # [4, 9]

  # 上記4行のコードを1行にまとめると
  return list(set(nums1) & set(nums2)) # [4, 9]
```

## Setの特性
[セット (set) - 日本語](https://utokyo-ipp.github.io/appendix/2-set.html)
Setは重複を許さないデータ型です。   
Setは順序を持たないので、インデックスを使って要素を取得することはできません。   
ただ今回の場合は、要素を取得する必要がないので問題ありません。   

## 私の解答
下記に私の解答を記載します。   
大変冗長なコードになってしまいました。   
しかも、上記のコードよりも遅いです。   
リストから重複を削除する関数、二分探索を行う関数を自作し、   
それらを使って解きました。   
```py
# リストから重複を削除する関数
def rm_d(lst):
  lst.sort()
  d = 0
  for i in range(1,len(lst)):
    if lst[i] == lst[i-1]:
      d+=1
    else:
      lst[i-d] = lst[i]
  return lst[0:len(lst)-d]

# 二分探索
def bs(trgt,lst,r,l):
  while r <= l:
    m = (r+l)//2
    if lst[m] == trgt:
      return True
    elif lst[m] > trgt:
      l = m-1
      return bs(trgt,lst,r,l)
    else:
      r = m+1
      return bs(trgt,lst,r,l)
  return False

def intersection(nums1,nums2):
  no_d_1 = rm_d(nums1)
  no_d_2 = rm_d(nums2)
  st = []

  if len(no_d_1) <= len(no_d_2):
    for _,v in enumerate(no_d_1):
      if bs(v,no_d_2,0,len(no_d_2)-1):
        st.append(v)
  else:
    for _,v in enumerate(no_d_2):
      if bs(v,no_d_1,0,len(no_d_1)-1):
        st.append(v)
  
  return st
```
