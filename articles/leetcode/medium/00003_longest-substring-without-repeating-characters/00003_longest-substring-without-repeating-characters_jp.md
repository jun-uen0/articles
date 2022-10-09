## 3. Longest Substring Without Repeating Characters
URL: https://leetcode.com/problems/longest-substring-without-repeating-characters
難易度：Medium

5回もWAを出してしまいました。
いくつかテストを通して満足し、コードの確認を行わず提出してしまったためです。
実務で行うサーバーサイドのコーディングは人命や大きな金額に影響する場合があります。
最後まで抜け目なく確認することが大切です。
という自戒の念を抱くことができたことが大きな収穫でした。笑
今回はMediumの割には問題がシンプルで、助かりました。

## 問題文
Given a string, find the length of the longest substring without repeating characters.
訳：文字列が与えられるので、重複しない最長の部分文字列の長さを求めてください。

substring: 連続する文字列
subsequence: 連続しなくてもよい文字列

## 例
```py
例1
Input: "abcabcbb"
Output: 3
Explanation: The answer is "abc", with the length of 3.
-> "abc"が最長の部分文字列で、長さは3です。

例2
Input: "bbbbb"
Output: 1
Explanation: The answer is "b", with the length of 1.
-> "b"が最長の部分文字列で、長さは1です。

例3
Input: "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3.
Note that the answer must be a substring, "pwke" is a subsequence and not a substring.
-> "wke"が最長の部分文字列で、長さは3です。
ただし、部分文字列である必要があります。"pwke"は部分文字列ではなく、部分列です。
```

## 解答
まずは全体の解答コードから
```py
s = 'pwawkew'
def lengthOfLongestSubstring(s: str):

  if len(s) == 0: return 0
  if len(s) == 1: return 1
  
  cnt = 0
  tmp = [s[0]]

  for i in range(1,len(s)):
    if s[i] in tmp:
      tmp = tmp[tmp.index(s[i])+1:]
    tmp.append(s[i])
    if len(tmp) > cnt:
      cnt = len(tmp)
  return cnt

print(lengthOfLongestSubstring(s))
```

## ① 基本ケース
sが0の場合、0を返す
sが1の場合、1を返す
```py
def lengthOfLongestSubstring(s: str):

  # 基本ケース
  if len(s) == 0: return 0
  if len(s) == 1: return 1
```

## ② 重複しないsubstringを作る
```py
def lengthOfLongestSubstring(s: str):

  if len(s) == 0: return 0
  if len(s) == 1: return 1

  # 重複しないsubstringを作る
  # tmpにsの最初の要素を入れる
  tmp = [s[0]]

  for i in range(1,len(s)):

    # tmp = [p,w,a] で s[i] = w の場合、
    # tmpの中をwのインデックス(2)の次の要素からスライスする
    # tmp = [a]となり、次のループでtmp = [a,w]となる
    # [p,w,a,w]となり得ないので、重複しないsubstringをループ毎に作っていく
    if s[i] in tmp:
      tmp = tmp[tmp.index(s[i])+1:]
    tmp.append(s[i])
```

## ③ 最長のsubstringの長さをカウントしていく
②でループ毎に重複しないsubstringを作っていくことができた。
次にループ毎にその作ったsubstringの長さをカウントしていく。
```py
def lengthOfLongestSubstring(s: str):

  if len(s) == 0: return 0
  if len(s) == 1: return 1
  tmp = [s[0]]

  # 最長のsubstringの長さをカウントしていく
  # カウントを行う変数cntを定義、初期値は0
  cnt = 0

  for i in range(1,len(s)):
    if s[i] in tmp:
      tmp = tmp[tmp.index(s[i])+1:]
    tmp.append(s[i])

    # もしtmpの長さがcntより長い場合、
    # cntをtmpの長さに更新する
    if len(tmp) > cnt:
      cnt = len(tmp)

  # ループを抜けたら、最長のsubstringの長さを返す
  return cnt
```
