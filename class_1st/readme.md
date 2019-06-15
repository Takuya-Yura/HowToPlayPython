   
# pythonの書き方(初級編)
         
## ファイルの形式について  
   + 拡張子  
     拡張子は｢.py｣  
   + 他の言語と違うところ
     1. 関数ブロックを**中括弧**ではなく**タブ**による階層表示で表す
     2. 関数区切りは何も記載しない
     3. 変数に対する型宣言は不要(型推論)
     4. 明示的に型指定する場合は｢変数:型｣で記載

    ```c
    //C言語による関数
    int test(int a){
        int b = a + 4;
        return b;
    }
    ```
    ```python
    #pythonによる関数
    def main(a:int):
        b = a + 4
        return b
    ```

## メイン処理の書き方  
   ```python
   #任意の関数
   def main(args):

        b = args + 4
        return b
   ```
   ```python
   #直接本ファイルが実行された場合のみ実施
   if __name__ == '__main__':
        main(1)
   ```

## 変数定義  
   上記2のとおり型宣言無しで変数を宣言可能(型推論)  
   以下のように変数の型を明示的に宣言することも可能
   ```python
   def main(args):

      b:int = args + 4
      return b
   ```
   
## 四則演算
   
   + x+y  
     xとyの和

   + x-y  
     xとyの差

   + x*y  
     xとyの積

   + x/y  
     xとyの商

   + x//y  
     ｘとyの商の整数部(商が5.12の時は｢5｣, -5.12の時は｢-6｣)

   + x%y  
     xとyの商あまり

   + x**y  
     xのy乗
  

## 条件文  
   
  ｢else if｣ではなく｢elif｣

  ```python
    if 条件式1:
        `条件式1がTrueのときに行う処理`
    elif 条件式2:
        `条件式1がFalseで条件式2がTrueのときに行う処理`
    elif 条件式3:
        `条件式1, 2がFalseで条件式3がTrueのときに行う処理`
    ...
    else:
        `すべての条件式がFalseのときに行う処理`
  ```
  + x is y  
    xとｙが同じオブジェクトならTrue
  + x is not y  
    xとyが異なるオブジェクトならTrue 
  + x in y  
    xがyに含まれていればTrue 
  + x not in y
    xがyに含まれていなければTrue 

  ※条件文として｢ a < x < b　｣のような書き方も可能


## 関数定義1  

### 定義側

  引数名=Xの記載によってデフォルト値設定が可能
  ```python
  def 関数名(引数1, 引数2, 引数3=10...):
      処理
  ```



### 呼び出し側
  引き数名を付帯させる場合は入力順序自由
  ```python
  関数名(引数2=10, 引数1=3...)
  ```
   

## 関数定義(タプル)

### 定義側
  ```python
  def 関数名(a, b, c):
      処理(a=0, b=1, c=2 として扱われる)
  ```

### 呼び出し側
  引き数名を付帯させる場合は入力順序自由
  ```python
  a = [0, 1, 2]
  関数名(*a)
  ```

## 関数定義(辞書)

### 定義側
  ```python
  def 関数名(a, b, c):
      処理(a=1, b=10, c=100 として扱われる)
  ```

### 呼び出し側
  引き数名を付帯させる場合は入力順序自由
  ```python
  x = {'a': 1, 'b': 10, 'c': 100}
  関数名(**x)
  ```

## ライブラリの読み込み  

### 読み込み方法
```python
  import <モジュール名> 
  from <モジュール名> import <オブジェクト名>
```


### モジュールをインポートする順番

  1. 標準ライブラリ
  2. サードパーティライブラリ
  3. ローカルライブラリ(自作)

### インポート例   
   ```python

      # as でモジュールを略称することができる
      import numpy as np

      A = np.array([[1.,3.] ,[4.,2.]]) # 行列Aの生成
      B = np.array([1.,1.])   # 行列Bの生成

      X = np.linalg.solve(A, B)
      print( "X=\n" + str(X) )

   ```

  ```python
      # mathモジュールのpiメソッドとsqrtメソッドを呼び出し
      from math import pi, sqrt
      print( sqrt(9) )

   ```

  ### !!実行ファイルより上の階層にあるモジュールをインポートするには!!

  pythonでは実行モジュールの位置をルートとして認識するため相対パスでインポートしても認識できない｡ 
  以下のように動的にパスをセットして読み出す  

  ```python
      import sys
      sys.path.append('../modules')
      print(sys.path)
      import echo

  ```

  python3.4以降ならばpathlibを使用するのが一般的か
  ```python
      # root/base.py
      import sys
      import pathlib
      # base.pyのあるディレクトリの絶対パスを取得
      current_dir = pathlib.Path(__file__).resolve().parent
      # モジュールのあるパスを追加
      sys.path.append( str(current_dir) + '/../' )

      # モジュールのインポート
      import echo
      echo.say_name()
      # => I'm echo

  ```


## 別ファイル参照

``import {.pyを除いたファイル名}``

     
##  デバッグ(VisualStudioCodeによる)

pyファイルをアクティブ(選択している状態)でF5を押すとVSCodeの上部に｢Debug Configuration｣を選択する欄が出力されるので｢Python File｣を選択する
実行結果が画面下のターミナルに表示される