# 函數

## 一. 函數的基本架構

### 1.宣告函數原型(prototype)
```
傳回值型態 函數名稱(引數型態1, 引數型態2....);
void star();
int sum(int, int);
```
目的在於告訴編譯器在程式碼將使用這個函數。  
可置於main()裡面和外面，置於裡面時只能被main()裡面的敘述呼叫。  

### 2.傳回值型態
函數結束時，要傳值回去給呼叫端的"資料型態"  
例如: void 沒有回傳值和引數

### 3.引數函數
要傳入給此函數的引數型態

### 4.註
函數可以有多個傳入的引數，但是只能有一個回傳值。  
例如 此函數接收2個整數引數，回傳值為他們的和
```
int add(int, int);
```


## 二. 函數的定義
可以放在任意位置，習慣上是放在main()後面。
```
return_type function_name(type1 argument1, type2 argument2, ..)
{
    variable Declaration   
    body of the function
    return 運算式
}
```
```
int add(int num1, int num2)
{
    int sum;
    sum = num1+num2;
    return sum;
}
```
簡化:
```
int add(int num1, int num2)
{
    return num1 + num2;
}
```
函數可以放在程式中的任一位置，傳統為放在main()後面，如果放在main()前面，則不用宣告函數原型。

## 三. calling a function
第一種: 直接呼叫function
```
hello()
```
第二種: 將傳回值放在variable，用在通常函數有回傳值
```
int sum = add(1, 5)
```

### 範例一
```
void star(); /*function declaration*/

int main()
{
    star(); /*function call*/
    printf("Welcome\n");
    star();

    return 0;
}
/*Function definition*/
void star()
{
    printf("******\n");
    return;      /*函數結束時，傳值給呼叫端(本題為main())*/                
                 /*此題由於沒有傳回值，所以不用接任何東西, 且可以省略*/
}
```
### 範例二
```
int add(int, int);

int main()
{
    int sum = add(1000, 999);
    printf("the result is %d", sum);
}

int add(int num1, int num2)
{
    return num1 + num2;
}
```

## 四. 遞迴函數(recursive)
**函數本身呼叫自己** 
解題技巧: 帶數字到題目，找出前後關係，統整出數學公式，再依照數學式打上code。
### 範例一 factorial function 
```c
int main()
{
    int n;
    printf("Enter n ");
    scanf("%d", &n);

    printf("%d", fac(n));
    
    return 0
}

int fac(int n)
{
    if(n > 0)
    {
        return n * fac(n-1); /*f(n) = n * f(n-1)*/
    }
    else
        return 1; /*0階 = 1*/
}
```

### 範例二 Fibonacci number
|n|1|2|3|4|5|
|-|-|-|-|-|-|
|value|1|1|2|3|5|
```c
int fib(int);
int main()
{   
    int m;
    printf("Enter a month: );
    scanf("%d", &m);
    
    printf("fib(%d) = %d", m, fib(m));

    return 0;
}

int fib(int m)
{
    if(m == 1 || m == 2)
        return 1;
    else
        return (fib(m-1) + fib(m-2));
}
```
## 引數傳遞的機制
之後補上

# 四. 前置處理器 
在編譯之前就會先進行處理，在把處理後的結果與程式碼一起給編譯器
## #define
```
#define 識別名稱 代換標記
#define TL "Tonny Lee"
```
將常用的常數/字串/函數替換成一個**自訂的識別名稱**，增加程式的易讀性 
識別名稱通常**大寫**且**不能**有空格  
想像成variabe name = value

### 範例一
```c
#define TL "Tonny Lee"

int main()
{
    printf(TL);
    return 0;
}

```

### 範例二
如果代換標記的內容很長時，可以用\來分段。
```c
#define alphabet "A, B, C, D, E, F, G, \
H, I, ..., Y, Z"  /*如果上下要連接，注意不能縮排*/
int main()
{
    printf(alphabet);
    return 0;
}
```
### 範例三
#defind 能防止常數在其他地方被修改
```c
#define PI 3.14

int main()
{
    printf("PI = %f", PI);
    
    PI = 3.1416 /*修改PI值會出現錯誤 (3.14 = 3.1416)*/ 
    
    return 0;
}
```

### **#define PI 3.14** 和 **int glo_var = 3.14 的差別**
**變數**需要**使用記憶體**，執行時必須從記憶體裡取值。  
#defind 則在編譯前就先以常數替換掉，所以使用#define較**省記憶體空間**且**有效率**

## 補充 const
利用const(constant)關鍵字來宣告並設定初值，使得該變數的值不能再被修改。放置位置可同#define
```c
const double pi = 3.14;
```

## 利用#define取代簡易的函數
define另一個功能是巨集(macro)。  
macro: 一個簡單的指令能替代多個操作步驟。

### 範例一
```c
#include <stdio.h>
#define SQUARE n*n /* 定義SQUARE為n*n */
int main()
{   
    int n;
    printf("Input an Integer: ");
    scanf("%d", &n);
    
    printf("%d*%d=%d\n", n, n, SQUARE); /*SQUARE*/

    return 0;
}

```

### 範例二 使用有引數的macro
有點像函數。
```c
#include <stdio.h>
#define SQUARE(X) X*X                      /*x = 5*/
int main()
{   
    int n;
    printf("Input an Integer: ");
    scanf("%d", &n);                       /*input 5*/
    
    printf("%d*%d=%d\n", n, n, SQUARE(n)); /* SQUARE(5)，傳回#define...*/

    return 0;
}
```

### 範例三 錯誤 13*13=25
正解只需括弧起來。(X)*(X)
```c
#include <stdio.h>
#define SQUARE(X) X*X                         
int main()
{   
    int n;
    printf("Input an Integer: ");
    scanf("%d", &n);                           /*n = 12*/
    
    printf("%d*%d=%d\n", n, n, SQUARE(n + 1)); /* SQUARE(n+1) == n+1*n+1 */

    return 0;
}
```

### 使用函數?巨集?
macro不需要像函數一樣要宣告等等，因為#define所處理的只是字串，將A替換成B，所以他不用考慮變數型態問題。  
macro    效率高，空間大。  
function 效率低，空間低。

## #include
#include除了可以包括C所提供的標頭檔之外，也可以包括自己所撰寫的標頭檔。  
例如，在程式裡會常用到的公式，如圓，長方形等等的面積，就可以利用#define將這些公式以macro定義，然後存到標頭檔內，讓#include來含括。

### 範例一 使用自訂的標頭檔
步驟一: 開啟任何編輯器，然後撰寫程式。  
步驟二: 存檔(~.h)  
步驟三: 在其他程式中 #include"自己撰的標頭檔路徑" ; #include<標準標頭檔>
範例
```c
# include"Documents\1022area.h"
```
