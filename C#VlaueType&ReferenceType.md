[TOC]

---

## Value Type

### 種類

- Structs
  - Integral Types
  - Floating-Point Types
  - bool
  - struct 自定義結構 
    - Datetime
- enum

###特性

- 不具有繼承的特性（只放數值、字元、位元組）
- 不需要進行垃圾回收
- 不需要對型別做驗證和判斷
- 指派 = 複製
- 不能指向 null

---

## Reference Type

### 種類

- class
- interface
- delegate
- dynamic
- object
- String
  - String、string 傻傻分不清。
    - String 是 class，string 是 關鍵字。差別在於使用 String 就要 using 該 class 的空間（System.String）進來

###特性

- 指派是指向記憶體位置
- 參考型別的實體物件都會建立再堆積中

---

## 破除迷思
- Value Type 是存在於堆疊；但，在兩個地方會被放到堆積中

  - 在方法內宣告的區域變數
  - 在方法上的參數

- 叫用方法所傳參數，其傳遞物件的方式不是傳址，是「複製」一份記憶體位置。如下舉例，

  ```c#
  // 假設 Test 有 Name 屬性，並初始化
  var test = new Test("test");
  // 叫用一個方法，裡面做 test = null
  ChangeToNull(test);
  Console.WriteLine(test.Name); // result: test 不會變 null
  ```

  - 呈上結果得知，不管用何種方式，物件絕對不會被當作參數傳遞。

- 結構是輕量級類別？

  - 原因來自結構屬於 Value Type，因此不應該有方法或其他行為。
    - 事實上，DateTime 是典型用結構但有方法的型別。
  - 在部分特例上，Reference Type 的效能會比較好
    - 比如 ArryList，改成 Value Type 就耗效能了，因為傳遞參數時會被全部複製一份。