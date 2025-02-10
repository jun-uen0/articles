## 69. Sqrt(x)
「平方根」   
https://leetcode.com/problems/sqrtx

私の解答では計算量がO(n)となり、実行時間が長くなりました。   
計算量をO(logn)にするために、二分探索法を使用した解答で今回は解説します。   
いつか自分の解答で解説できるよう、邁進していきたいと思います。   

参考のコード: [Python binary search solution (O(lgn))](https://leetcode.com/problems/sqrtx/discuss/25061/Python-binary-search-solution-(O(lgn)))   

## 問題文
Given a non-negative integer x,   
compute and return the square root of x.   

Since the return type is an integer,   
the decimal digits are truncated,    
and only the integer part of the result is returned.    

訳：   
負ではない整数xが渡されます。     
xの平方根を求め、returnしてください。   
戻り値は整数型なので、小数点以下は切り捨てられます。   

truncate = 切り捨てる   

**Inputの例**
```py
Example 1:
Input: x = 4
Output: 2

Example 2:
Input: x = 8
Output: 2
説明：8の平方根は2.82842...ですが、小数点以下は切り捨てられるので、2がreturnされます。
```

## 解答
計算量：O(LogN)   
```py
# Input
x = 10

def sqrtx(x):
  l, r = 0, x
  while l <= r:
    mid = l + (r-l)//2
    if mid * mid <= x < (mid+1)*(mid+1):
      return mid
    elif x < mid * mid:
      r = mid - 1
    else:
      l = mid + 1

print(sqrtx(x)) # 3
```

## ① 変数の用意
l... 左端の値   
r... 右端の値   
```py
# xを引数にとる関数sqrtxとして定義
def sqrtx(x):
  # 変数の用意
  l, r = 0, x
```

## ② ループ処理を定義
左端が右端以下の間、ループ処理を行う   
今回の処理では、左端と右端の値をループ処理の中で更新していく   
ループを繰り返すごとに、左端と右端の値は、それぞれ、中央値に近づいていく。   
最悪の場合、左端と右端の値は、中央値になる。(同じ値になる)   
```py
def sqrtx(x):
  l, r = 0, x

  # ループ処理を定義
  while l <= r:
```

## ③ lとrの中間値を求める
例: l=0, r=10の場合、   
mid = 0 + (10-0)//2 = 5   
※ 「//」は切り捨て除算 (9//2 = 4)   
```py
def sqrtx(x):
  l, r = 0, x
  while l <= r:

    # lとrの中間値を求める
    mid = l + (r-l)//2
```

## ④ (基本ケース) xの平方根、もしくはその近似値をreturnする
midの2乗がxより小さく、mid+1の2乗がx以上の場合、midをreturnする   
以下の場合、midが問題の解答となるので、midをreturnする。   

なぜこの計算で10の平方根が求まるかというと、   
例えば、xが10、midが3の場合、if文の条件式は「9(3*3) <= 10 < 16(4*4)」となる。   
10の平方根は3.1622776601683795で、   
3.1622776601683795の整数部分は3であるため、midの値である3をreturnする。   

基本ケースとして、ループ処理内の最初に記述する。   
```py
def sqrtx(x):
  l, r = 0, x
  while l <= r:
    mid = l + (r-l)//2

    # xの平方根、もしくはその近似値をreturn
    if mid * mid <= x < (mid+1)*(mid+1):
      return mid
```

## ⑤ 検索範囲の右側を除外する
xがmidの2乗より小さい場合   
例えばxが10、midが5の場合、10 < 25(5*5)   
右端(r)を4(5-1)にする   
次のループから計算範囲が0~4になる   
```py
def sqrtx(x):
  l, r = 0, x
  while l <= r:
    mid = l + (r-l)//2
    if mid * mid <= x < (mid+1)*(mid+1):
      return mid
    
    # 検索範囲の右側を除外
    elif x < mid * mid:
      r = mid - 1
```
## ⑥ 検索範囲の左側を除外する
xがmidの2乗以上の場合   
例えばxが10、midが3の場合、9(3*3) <= 10   
左端(l)を4(3+1)にする   
次のループでは計算範囲が4~10になる   
```py
def sqrtx(x):
  l, r = 0, x
  while l <= r:
    mid = l + (r-l)//2
    if mid * mid <= x < (mid+1)*(mid+1):
      return mid
    elif x < mid * mid:
      r = mid - 1
    
    # 検索範囲の左側を除外
    else:
      l = mid + 1
```

## ⑦ 結果を出力
```py
# Input
x = 10

def sqrtx(x):
  l, r = 0, x
  while l <= r:
    mid = l + (r-l)//2
    if mid * mid <= x < (mid+1)*(mid+1):
      return mid
    elif x < mid * mid:
      r = mid - 1
    else:
      l = mid + 1

print(sqrtx(x)) # 3
```