## 1456. Maximum Number of Vowels in a Substring of Given Length
「Substringにある母音の最大数」
 
https://leetcode.com/problems/maximum-number-of-vowels-in-a-substring-of-given-length/  

やってみると簡単な問題なのだが、問題文がわかりずらい。   
Substringという新しい概念があったせいもあるかもしれない。   
英語でも母音が「あ、い、う、え、お」と認識されているのは意外だった。   
え、そんなのも母音として認識されてるの？みたいな文字も含まれてるのかと思っていた。   
今回の解説では私の解答ではなく、別の方の回答を参考に作成した。   

参考のコード: [[Java/Python 3] Slide Window O(n) codes](https://leetcode.com/problems/maximum-number-of-vowels-in-a-substring-of-given-length/discuss/648559/JavaPython-3-Slide-Window-O(n)-codes)   
ユーザーURL: [rock](https://leetcode.com/rock)  

## 問題文
Given a string s and an integer k,  
return the maximum number of vowel letters in any substring of s with length k.   
Vowel letters in English are 'a', 'e', 'i', 'o', and 'u'.    

訳：   
**string型s**と**integer型s**が渡されます。  
**長さkを使用しsから抽出した全てのsubstringから、   
母音の数を数え、最も多かった母音数をreturn**してください。  
ここでの母音は「'a', 'e', 'i', 'o', 'u'」です。

**Inputの例**
```py

Input: s = "abciiidef", k = 3
Output: 3
説明: substring「iii」は3つの母音を含んでます。
#「abc」「bci」「cii」「iii」「iid」「def」

Input: s = "aeiou", k = 2
Output: 2
説明: 全ての2文字から成るsubstringは2つの母音を含んでます。
#「ae」「ei」「io」「ou」

Input: s = "leetcode", k = 3
Output: 2
説明: 3文字から成るsubstring、「lee」「eet」「ode」は2つの母音を含んでます。
※ いずれの3文字から成るsubstringは3つ以上の母音を含んでません。
# 「lee」「eet」「etc」「tco」「cod」「ode」
```

## 解答
```py
# Input
s = "abciiidef"
k = 3

vowels = {'a', 'e', 'i', 'o', 'u'}
ans = cnt = 0
for i, v in enumerate(s):
  if v in vowels:
    cnt += 1
  if i >= k and s[i-k] in vowels:
    cnt -= 1
  ans = max(cnt, ans)
print(ans) # 3
```

## ① 変数の用意
母音を格納する辞書型のvowels   
ansとcntに初期値0を代入   
ansは最後にreturnする変数として  
cntは母音の数を数えるための変数として   
```py
s = "abciiidef"
k = 3

vowels = {'a', 'e', 'i', 'o', 'u'}
ans = cnt = 0
```

## ② for loopの作成
要素番号と要素を同時に使用するため  
enumerateを活用する  
文字列sのfor loop内のみで回答を得る  
```py
s = "abciiidef"
k = 3

vowels = {'a', 'e', 'i', 'o', 'u'}
ans = cnt = 0

for i, v in enumerate(s):
  # 処理
print(ans) # ansで回答を得る
```

## ③ 母音を見つけたらカウントアップする
sのfor loop中に母音を見つけたらcntに1を加える
```py
s = "abciiidef"
k = 3

vowels = {'a', 'e', 'i', 'o', 'u'}
ans = cnt = 0

for i, v in enumerate(s):

  # カウントアップ
  if v in vowels:
    cnt += 1

print(ans)
```

## ④ カウントアップのしすぎを回避する
for loop中に要素番号がk以上になってからはカウントアップのしすぎを回避する必要がある   
例えばsが「abciiidef」の場合、ループの4回目になると母音が2つ見つかる。(「a」と「i」)   
ただし、この4回目のループでは要素番号0、「a」の値はカウントされるべきではない。   
そのため、この場合の要素番号0がもし母音だったらカウントを1減らす必要がある。   
for loop中にiがk以上になった場合、全ての要素で以下の要素番号をチェックする必要がある。   

`s[i-k]`

```py
s = "abciiidef"
k = 3

vowels = {'a', 'e', 'i', 'o', 'u'}
ans = cnt = 0

for i, v in enumerate(s):

  # カウントアップ
  if v in vowels:
    cnt += 1
  
  # カウントダウン
  if i >= k and s[i-k] in vowels:
    cnt -= 1

print(ans)
```

## ⑤ for loopごとにans、cntの最大値をansに代入
for loopごとにカウントした値の最大値をansに格納していく   
cntの値はfor loopの中で変動するため、この処理が必要となる。   
全てのsubstringから母音の最大数を取得し、  
さらにその中の最大数を回答として取得する必要があるため。 

```py
s = "abciiidef"
k = 3

vowels = {'a', 'e', 'i', 'o', 'u'}
ans = cnt = 0

for i, v in enumerate(s):

  # カウントアップ
  if v in vowels:
    cnt += 1
  
  # カウントダウン
  if i >= k and s[i-k] in vowels:
    cnt -= 1
  
  # Substringごとに
  # 今回のループ時の最大値と
  # 今回以前のループ時の最大値を比べ、
  # 大きい方をansに格納する
  ans = max(cnt, ans)

print(ans)
```