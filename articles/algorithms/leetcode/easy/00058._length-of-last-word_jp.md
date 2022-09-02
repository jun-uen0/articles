## 58. Length of Last Word
https://leetcode.com/problems/length-of-last-word   
「最後の単語の文字列」  

非常に簡単な問題です。   
解答に使用するプログラム言語の理解にうってつけかもしれません。こいった簡単な問題からでも進められるのは良いですね。敷居を高く感じずに済みます。

## 問題文
> Given a string `s` consisting of words and spaces, return *the length of the last word in the string.*  
A word is a maximal substring consisting of non-space characters only.

> 訳：   
**文字とスペースから成るstring**が渡されます。  
**最後の単語の文字数をreturn**してください。  
単語は、スペース以外の文字のみで構成されます。

**Inputの例**
```py
Input: s = "luffy is still joyboy"
Output: 6
Explanation: The last word is "joyboy" with length 6.
```
## 私の解答方法
① スペースでsplitする(同時にlistへ追加)     
② listの最後の要素の文字列を返す    

## Inputされる値
```py
# inputされる値とその型を調べる

print(s)
print(type(s))

# luffy   is still  joyboy
# <class 'str'>
```
## ① スペースでsplitする
```py
# splitを使って空白()で文字列を分割　　
# 同時にlistへ追加   
# どれだけスペースの数は関係ないようです。

split_s = s.split()

# ['luffy', 'is', 'still', 'joyboy']
```

## ② リストの最後の要素の文字列を返す
①で作成したリストの最後の要素を`[-1]`で取得し、   
`len()`で要素の文字数を取得します
```py
s.split()[-1] # joyboy
len(s.split()[-1]) # 6 <- 解答
```

## 解答
```
class Solution:
  def lengthOfLastWord(self, s: str) -> int:
    return len(s.split()[-1])
```