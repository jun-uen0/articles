## 二分探索法 (Binary Search)
二分探索法はターゲットの数字がリスト内にあるかを調べることができます。      
その処理をO(logN)で行うことができます。    

```py
# 数字「5」はリスト内にある？

trgt = 5
lst = [1,2,5,8,12,19,34]
```

## 前提
リスト内の要素はnumber型   
リストはマージ済み

## 手順
① リストの真ん中の値、(もしくは中心から一つ左)の数字を取得   
② ターゲットの数字と取得した数字を比較する    
③-① 上記の結果、同じであれば要素番号を返す   
③-② 上記の結果、ターゲットの数字が取得した数字より大きければ、真ん中の値で分割したリストの右側で①から処理を再開する    
③-③ 上記の結果、ターゲットの数字が取得した数字より小さければ、真ん中の値で分割したリストの左側で①から処理を再開する  
④ なければNoneを返す  

## ① リストの真ん中の値の数字を取得

```py
trgt = 5
lst = [1,2,5,8,12,19,34]

# lstの真ん中の値を取得
mid = len(lst) // 2 # 3
mid_n = lst[mid] # 8
```

## ② ターゲットの数字と取得した数字を比較する
ターゲットの値は5   
中心の値は8   
-> ターゲットの数字が取得した数字より小さい   

## ③-① 比較の結果をもとに処理を分岐
②の結果、ターゲットの数字が取得した数字より小さいことが分かったため、   
リストを真ん中の値で分割し、左側のリストで①から処理を再開する。

```py
# 分割し、そのままlstに代入
lst = lst[:mid] # [1,2,5]
```

## (2回目) ① リストの真ん中の値の数字を取得
```py
# trgt = 5
# lst = [1,2,5]

mid = len(lst) // 2 # 1
mid_n = lst[mid] # 2
```

## (2回目) ② ターゲットの数字と取得した数字を比較する 
ターゲットの値は5   
中心の値は2   
-> ターゲットの数字が取得した数字より大きい

## (2回目) ③ 比較の結果をもとに処理を分岐
②の結果、ターゲットの数字が取得した数字より大きいことが分かったため、   
リストを真ん中の値で分割し、右側のリストで①から処理を再開する。   

```py
# 分割し、そのままlstに代入
lst = lst[(mid+1):] # [5]
```

## (3回目) ① リストの真ん中の値の数字を取得
```py
# trgt = 5
# lst = [5]

mid = len(lst) // 2 # 0
mid_n = lst[mid] # 5
```
## (3回目) ② ターゲットの数字と取得した数字を比較する
ターゲットの値は5   
中心の値は5   
-> ターゲットの数字と取得した数字が同じ値なので要素番号を返す

## 処理回数について
要素数が7のリストからターゲットの数字があるかどうか、3回の処理で判別することができた。リスト数が少ないと大した違いはないが、1000万の要素数を持つリストだとしても、二分探索法を使えば24回の処理で判別することができる。
```py
(1回) 10000000
(2回) 5000000
(3回) 2500000
(4回) 1250000
(5回) 625000
(6回) 312500
(7回) 156250
(8回) 78125
(9回) 39062
(10回) 19531
(11回) 9765
(12回) 4882
(13回) 2441
(14回) 1220
(15回) 610
(16回) 305
(17回) 152
(18回) 76
(19回) 38
(20回) 19
(21回) 10
(22回) 5
(23回) 2
(24回) 1
```

処理を経るごとに検索対象のリストが半分になっていく。   
検索回数がO(Log N)回となる。   

## コード成形 (反復処理)
```py
def binary_search_itr(lst, target):
  start = 0
  end = len(lst) - 1

  # リストが空になるまでループする
  while start <= end:
    mid = (start + end) // 2
    # もしターゲットと真ん中の値が同じであれば要素番号を返す
    if lst[mid] == target:
      return mid
    # リストの右側での検索に移動
    if lst[mid] > target:
      end = mid - 1 # リストの最大要素番号を更新
    # リストの左側での検索に移動
    else:
      start = mid + 1　# リストの最小要素番号を更新
  
  # リスト内にターゲットがないことが分かった
  return None

my_list = [1, 3, 5, 7, 9]
print(binary_search_itr(my_list, 3))  # 1
print(binary_search_itr(my_list, -1)) # None
```

## コード成形 (回帰処理)
```py
def binary_search_rcr(lst, target, start, end):
  # リストが空になるまでループする
	while start <= end:
		mid = (end + start) // 2

    # もしターゲットと真ん中の値が同じであれば要素番号を返す
		if lst[mid] == target:
			return mid

    # リストの右側での検索に移動
		elif lst[mid] > target:
			end = mid - 1
      # この関数を回帰的に処理する
			return binary_search_rcr(lst, target, start, end)
    
    # リストの左側での検索に移動
		else:
			start = mid + 1
			return binary_search_rcr(lst, target, start, end)
  
  # リスト内にターゲットがないことが分かった
	return None

my_list = [1, 3, 5, 7, 9]
print(binary_search_rcr(my_list, 9, 0, len(my_list)-1)) # 4
print(binary_search_rcr(my_list, 10, 0, len(my_list)-1)) # None
```
