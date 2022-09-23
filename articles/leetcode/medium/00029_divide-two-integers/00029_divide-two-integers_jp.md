## 29. Divide Two Integers
「二つの整数の割り算」   
https://leetcode.com/problems/divide-two-integers   
難易度：中   

今日はTimothy H Changさんの解答を参考にさせていただきました。   

参考のコード: [Leetcode - Divide Two Integers (Python)](https://www.youtube.com/watch?v=6kFp_s_UtPE)      

## 問題文
Given two integers dividend and divisor, divide two integers without using multiplication, division, and mod operator.   

The integer division should truncate toward zero, which means losing its fractional part. For example, 8.345 would be truncated to 8, and -2.7335 would be truncated to -2.   

Return the quotient after dividing dividend by divisor.   

Note: Assume we are dealing with an environment that could only store integers within the 32-bit signed integer range: [−231, 231 − 1]. For this problem, if the quotient is strictly greater than 231 - 1, then return 231 - 1, and if the quotient is strictly less than -231, then return -231..       

訳：   
整数dividendとdivisorが与えられます。   
乗算、除算、剰余演算子を使わずに、二つの整数の割り算を行ってください。   

整数の割り算は、小数点以下を切り捨てるようにしてください。      
例えば、8.345は8に切り捨てられ、-2.7335は-2に切り捨てられます。   

dividendをdivisorで割った商をreturnしてください。   

注意：32ビット符号付き整数の範囲内でしか扱えないと仮定してください。[−231, 231 − 1]。   
この問題では、商が231 - 1より大きい場合は、231 - 1をreturnし、   
商が-231より小さい場合は、-231をreturnしてください。   

truncate = 切り捨てる  
fractional part = 小数点以下    
quotient = 商   

**Inputの例**
```py
# 例1:
Input: dividend = 10, divisor = 3
Output: 3
説明：10/3 = 3.33333.. は切り捨てられて3になります。

# 例2:
Input: dividend = 7, divisor = -3
Output: -2
説明: 7/-3 = -2.33333.. は-2に切り捨てられます。
```

## 解答
計算量：O(LogN)   
```py
# Input
dividend = 10
divisor = -10

def divide_faster() -> int: 
  if dividend == 0:
    return 0
  
  dividend_abs = abs(dividend)
  divisor_abs = abs(divisor)
  
  output = 0
  while dividend_abs >= divisor_abs:
    temp = divisor_abs
    mul = 1
    while dividend_abs >= temp:
      dividend_abs -= temp
      output += mul
      mul += mul
      temp += temp

  if (dividend > 0 and divisor < 0) or (dividend < 0 and divisor > 0):
    output = -output
  
  return min(2147483647,max(-21474836478, output))

print(divide_faster()) # -3
```

## 手順
① 基本ケースを考える   
② dividendとdivisorの絶対値を取得   
③ dividendの絶対値がdivisorの絶対値で割り切れる間、処理を行うループを作成   
③-① ループ処理の中に計算用の変数を二つ用意   
④ dividendの絶対値がtemp以上の間、処理を行うループを作成   
④-① ループ処理の中で割られる数から割る数を引く   
⑤ ③以降のループ処理について、詳しく調査   
⑥ 絶対値oupoutの正負を条件式で判定、変換   
⑦ 最終的な解答を返す   

## ① 基本ケースを考える
dividendが0の場合は、0を返す。   
```py
def divide_faster() -> int:

  # 基本ケース
  if dividend == 0:
    return 0
```

## ② dividendとdivisorの絶対値を取得
それぞれの絶対値で計算を行う。なぜなら、負の数を扱うため。   
一旦整数で計算し、もしdividendかdivisorが負の数だったら、最後outputを負の数に変換する。   
```py
def divide_faster() -> int:
  if dividend == 0:
    return 0

  # dividendとdivisorの絶対値を取得
  dividend_abs = abs(dividend)
  divisor_abs = abs(divisor)

  # outputを0に初期化
  output = 0
```

## ③ dividendの絶対値がdivisorの絶対値で割り切れる間、処理を行うループを作成
dividendの絶対値がdivisorの絶対値以上の間というのは、   
dividendの絶対値がdivisorの絶対値で割り切れる間ということ。
```py
def divide_faster() -> int:
  if dividend == 0:
    return 0

  dividend_abs = abs(dividend)
  divisor_abs = abs(divisor)
  output = 0

  # dividendの絶対値がdivisorの絶対値で割り切れる間、処理を行う
  while dividend_abs >= divisor_abs:
```

## ③-① ループ処理の中に計算用の変数を二つ用意
temp:   
割る数(divisor_abs)で初期化   
この値は次のループから指数関数的に増加する   

mul:   
1で初期化   
この値もtemp同様次のループから指数関数的に増加する   
```py
def divide_faster() -> int:
  if dividend == 0:
    return 0

  dividend_abs = abs(dividend)
  divisor_abs = abs(divisor)
  output = 0

  while dividend_abs >= divisor_abs:
    # ループ処理の中に計算用の変数を二つ用意
    temp = divisor_abs # 割る数をtempに代入
    mul = 1 # 商をmulに代入
```

## ④ dividendの絶対値がtemp以上の間、処理を行うループを作成
ここでの割る数はtemp、   
割られる数はdividend_abs。   
```py
def divide_faster() -> int:
  if dividend == 0:
    return 0

  dividend_abs = abs(dividend)
  divisor_abs = abs(divisor)
  output = 0

  while dividend_abs >= divisor_abs:
    temp = divisor_abs
    mul = 1

    # 割られる数が割る数以上の間、処理を行う
    while dividend_abs >= temp:
```

## ④-① ⑤の処理に使用する変数を更新する
dividend_abs:   
dividend_absにtempの値を引く。   
割られる数の絶対値(dividend_abs)から割る数(temp)を引く。   
もし割られる数が割る数より小さくなったら、③のループに戻らずループ処理から抜けることになる。   

output:   
outputにmulを足す。   
outputは最終的な解答になる。   
初期値は0で、ループを繰り返すごとにmulの値を足していく。   

mul:   
mulを2倍にする。   
mulの値は直接解答である商の値(絶対値)になる。   

temp:   
tempを2倍にする。   
tempの数を使用し、ループを繰り返すごとにdividend_absの値を引いていく。   
```py
def divide_faster() -> int:
  if dividend == 0:
    return 0

  dividend_abs = abs(dividend)
  divisor_abs = abs(divisor)
  output = 0

  while dividend_abs >= divisor_abs:
    temp = divisor_abs
    mul = 1

    while dividend_abs >= temp:

      # 処理に使用する変数を更新
      dividend_abs -= temp # 割られる数から割る数を引く
      output += mul # outputにmulの値を足す
      mul += mul # mulの値を2倍にする
      temp += temp # tempの値を2倍にする
```

## ③以降のループ処理について、詳しく調査
ループ③以降の処理の中で何が起きてるか、   
実際に数字を入れて計算してみる。   
例えば、dividend_absが100、divisor_absが3の場合を考える。   
```py
dividend_abs = 10
divisor_abs = 3

while dividend_abs >= divisor_abs: # 100 >= 3
  temp = divisor_abs # temp = 3
  mul = 1

  # ループ1 (while dividend_abs >= temp: # 100 >= 3)
    dividend_abs -= temp # 100 - 3 = 97
    output += mul # 0 + 1 = 1
    mul += mul # 1 + 1 = 2
    temp += temp # 3 + 3 = 6

  # ループ2 (while dividend_abs >= temp: # 97 >= 6)
    dividend_abs -= temp # 97 - 6 = 91
    output += mul # 1 + 2 = 3
    mul += mul # 2 + 2 = 4
    temp += temp # 6 + 6 = 12
  
  # ループ3 (while dividend_abs >= temp: # 91 >= 12)
    dividend_abs -= temp # 91 - 12 = 79
    output += mul # 3 + 4 = 7
    mul += mul # 4 + 4 = 8
    temp += temp # 12 + 12 = 24
  
  # ループ4 (while dividend_abs >= temp: # 79 >= 24)
    dividend_abs -= temp # 79 - 24 = 55
    output += mul # 7 + 8 = 15
    mul += mul # 8 + 8 = 16
    temp += temp # 24 + 24 = 48
  
  # ループ5 (while dividend_abs >= temp: # 55 >= 48)
    dividend_abs -= temp # 55 - 48 = 7
    output += mul # 15 + 16 = 31
    mul += mul # 16 + 16 = 32
    temp += temp # 48 + 48 = 96
  
  # ループ6 (while dividend_abs >= temp: # 7 >= 96)
    # 条件式に当てはまらないため、ループから抜ける
    # 現在outputの値は31
    # よって、dividend_absが100、divisor_absが3の場合の解答は31となる
```

この処理が早い理由は、全ての処理で100を3で引き、   
カウントを行うのでなく、処理を繰り返すごとに割る数を2倍にしているから。   
もしこの計算が100/3の場合だったら処理の回数は通常100/3=33回になる。   
しかし、上記の例で示す通り、この手法を活用すれば処理の回数はたった6回に収まる。   

## ⑥ 絶対値oupoutの正負を条件式で判定、変換
dividendが負でdivisorが正の場合、もしくは   
dividendが正でdivisorが負の場合、   
outputの値を負にする   
```py
def divide_faster() -> int: 
  if dividend == 0:
    return 0
  
  dividend_abs = abs(dividend)
  divisor_abs = abs(divisor)
  
  output = 0
  while dividend_abs >= divisor_abs:
    temp = divisor_abs
    mul = 1
    while dividend_abs >= temp:
      dividend_abs -= temp
      
      output += mul
      mul += mul
      temp += temp

  # 絶対値oupoutの正負を条件式で判定、変換
  if (dividend > 0 and divisor < 0) or (dividend < 0 and divisor > 0):
    output = -output
```

## ⑦ 最終的な解答を返す
通常ならば、outputの値をそのまま返す。   
ただし、outputの値が32bit整数の範囲を超えている場合は、   
32bit整数の最大値(2^31 - 1)を返す。   
```py
def divide_faster() -> int: 
  if dividend == 0:
    return 0
  
  dividend_abs = abs(dividend)
  divisor_abs = abs(divisor)
  
  output = 0
  while dividend_abs >= divisor_abs:
    temp = divisor_abs
    mul = 1
    while dividend_abs >= temp:
      dividend_abs -= temp
      
      output += mul
      mul += mul
      temp += temp

  if (dividend > 0 and divisor < 0) or (dividend < 0 and divisor > 0):
    output = -output
  
  # 最終的な解答を返す
  return min(2147483647,max(-21474836478, output))
```