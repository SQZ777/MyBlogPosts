# Python - Mutable Default Arguments

過去遇到毛毛蟲總是會想著「為什麼」這個要出現毛毛蟲，而這一次出現毛毛蟲也同樣想了這個「為什麼」，而且覺得比較特別，所以就把他筆記一下w

先來寫了以下這段 code

```python
def add_something_to_array(element, array=[]):
    array.append(element)
    return array

my_array_a = add_something_to_array("a")
print(my_array_a)
```

結果也會很簡單的回覆給我 ['a']

![Python%20-%20Mutable%20Default%20Arguments%20e2af678c58414d67a6b28172e481fbe7/Untitled.png](Python%20-%20Mutable%20Default%20Arguments%20e2af678c58414d67a6b28172e481fbe7/Untitled.png)

## 但是

如果第二次呼叫他的時候，問題就會出現了

把 code 先改成以下的樣子

```python
def add_something_to_array(element, array=[]):
    array.append(element)
    return array

my_array_a = add_something_to_array("a")
print(my_array_a)
my_array_b = add_something_to_array("b")
print(my_array_a)
print(my_array_b)
```

來看看執行的結果

![Python%20-%20Mutable%20Default%20Arguments%20e2af678c58414d67a6b28172e481fbe7/Untitled%201.png](Python%20-%20Mutable%20Default%20Arguments%20e2af678c58414d67a6b28172e481fbe7/Untitled%201.png)

就會發現到裡面這個 array，會被外部重複使用，原因是什麼呢?

Python 在定義 function 的預設參數時，只會被定義一次，而不是在每次呼叫的時候重新定義一次，所以上面這一小段 code: array = [] 才會一直被重複使用。

## 那該怎麼做呢?

你應該要避免在預設的參數裡面設定一個可變動的變數，將可變動的預設參數改為 None，在程式碼裡面判斷並賦予原本預設的可變動變數，如下

```python
def add_something_to_array(element, array=None):
    if array is None:
        array=[]
    array.append(element)
    return array

my_array_a = add_something_to_array("a")
print(my_array_a)
my_array_b = add_something_to_array("b")
print(my_array_a)
print(my_array_b)
```

~~當初在 code review 的時候遇到這樣寫法，還以為是在炫技，抱歉是我錯了~~

執行結果如下，這樣一切就會跟我們預想的結果相同啦!

![Python%20-%20Mutable%20Default%20Arguments%20e2af678c58414d67a6b28172e481fbe7/Untitled%202.png](Python%20-%20Mutable%20Default%20Arguments%20e2af678c58414d67a6b28172e481fbe7/Untitled%202.png)

參考來源: [https://docs.python-guide.org/writing/gotchas/](https://docs.python-guide.org/writing/gotchas/)