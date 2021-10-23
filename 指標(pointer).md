# pointer概述
指標可以存取變數的值，就像是利用變數名稱存取變數內容。  
指標可以看成一種特殊的變數，用來存放變數在**記憶體中的位址**  
位址(address): when we declare a variable, the compiler will assign a memory space with **unique number** called "address" to it.

**依址取值**(adress -> variable value): 當指標ptr指向變數a之後，如果要存取變數a時，便可利用指標ptr找到變數a的address，再由該位址取出所儲存的變數值。  
```
指標ptr指向變數a (ptr存放的是 adress of a)
```
![圖片01](./pointer01.JPG)
宣告一個變數a，值為20，ptr存放a的adress(1400)。compiler也會安排adress給指標變數(1408)

**位元組定址法** 用決定變數的位址，也就是給予記憶體內的每個位元組一個adress，而**變數的adress即是它所佔的位元組裡，第一個位元組的位址**，如下圖。
![圖片02](./pointer02.JPG)

# 為甚麼使用指標
1. 使函數在傳遞陣列或字串更有效率
2. 較複雜的資料結構，如linked list, binary tree，需透過pointer協助，才能將資料連接再一起。
3. 函數需要pointer傳達記憶體訊息，例如malloc(), fopen()。

# 記憶體的位址
 %d 十進位表示位址  
 %p 十六進位表示位址
 ```c
 int main()
{
    int a, b = 5;
    double c = 3.14;
    printf("a = %d, sizeof(a) = %d, address = %d\n", a, sizeof(a), &a); /*沒給a值，所以會是殘值*/
    printf("b = %d, sizeof(b) = %d, address = %d\n", b, sizeof(b), &b); /*&位址符號*/
    printf("c = %f, sizeof(c) = %d, address = %d", c, sizeof(c), &c);   /*%d -> 十進位表示位址*/
    return 0;
}

 ```
 
 # 指標變數的宣告
 pointer所存放的內容為其他變數的address，所以我們根據指標所存放的address，可以找到它所指向的變數內容。  
 SYNTAX  
 ```
 1. data_type *pointer variable
 2. data_type* pointer variable
 ```
 "*"將普通變數變成指標變數。  
 data_type 為指標所指向之變數的型態。  
 
 ### 範例一 
 ```c
 int *ptr;       /*宣告一個指向整數的pointer_variable, ptr*/
 int num = 20;
 ptr = &num;     /*設值給ptr*/
 ```
 
 ### 範例二 同時宣告2個指標變數
 ```
 int* ptr1,ptr2;
 int *ptr1, *ptr2;
 ```
 
 
 # 指標變數的使用
 1. 位址運算子 &
 - 取出**變數位址**
 - 範例: &num (取出num的位址)
 2. 依址取址運算子 *
 - 取出指標變數所指向的**變數內容**
 - 範例: *ptr = &num 
 - 
### 範例一
```c
int main()
{
    int a = 20, *ptr;
    ptr = &a;
    printf("a = %d, &a = %p\n", a, &a); /*列印出a值，a的位址*/
    printf("*ptr = %d, ptr = %p, &ptr = %p", *ptr, ptr, &ptr);

    return 0;
}
```

### 範例二 更改一個相同型態的指向對象
```c
int main()
{
    int a = 5, b = 3;
    int *ptr;
    
    ptr = &a; /*ptr指向a*/
    printf("&a = %p, &ptr = %p, *ptr = %d\n", &a, &ptr, *ptr);
    
    ptr = &b; /*更改指向對象為b*/
    printf("&b = %p, &ptr = %p, *ptr = %d\n", &b, &ptr, *ptr);
}
```
從中得知只要是變數型態相同，指標可以更改他的指向，使他指向另一個變數。  

指標變數不論他所指向之變數的型態為何，編譯器都會給他4個位元組存放其他變數位址。

# 宣告指標變數所指向之型態的重要性
- 一旦宣告指標變數指標變數所指向的型態後，便不能更改。
- 不可把A型態的指標指向B型態的變數。
- 
### 範例一 錯誤 分配錯誤的資料型態
```c
int a = 10, *ptri;
float b = 1.5, *ptrf;

ptri = &b; /*Error*/
ptrf = &a; /*Error*/
```
# 指標與函數
### 範例一
```c
void address(int *); /*prototype中不必變數名稱，所以*表示傳入的是指向變數*/

int main()
{
    int a=12;
    int *ptr = &a;
    
    address(&a); /*傳入位址*/
    address(ptr);/*傳入位址*/
}

/*定義了一個可以接收指向整數型態的指標(也就是可以接收一個存放整數的位址)*/
void address(int *p1)  /* *p1=&a */
{
    printf("位於address: %p , 儲存的變數為%d\n", p1, *p1);
}
```
### 範例二 透過位址改變呼叫端的內容
```c
void add10(int *);

int main()
{
    int a=5;
    printf("before calling add10(), a = %d\n", a);
    
    add10(&a); /*傳入a的位址*/
    
    printf("after calling add10(), a = %d\n", a);
    
}

void add10(int *p1) /* p1 = &a */
{
    *p1 = *p1 + 10;  /*直接在a的記憶體中上修改, 所以不用return*/
}
```

### 範例三 swap a, b值 錯誤版
```c
void swap(int, int);

int main()
{
    int a=5, b=100;
    printf("before calling swap(), a = %d, b = %d\n", a, b);
    
    swap(a, b);
    printf("after calling swap(), a = %d, b = %d\n", a, b);
    
}

void swap(int x, int y)
{
    int temp = x;
    x = y;
    y = temp;
}
```
為甚麼錯誤呢? 因為在swap()裡，x,y 屬於local variable，當swap()執行結束時，x,y的值即從記憶體空間抹除。  
解決方法，直接在記憶體上修改。
### 修改後
```c
void swap(int *, int *);

int main()
{
    int a=5, b=100;
    printf("before calling swap(), a = %d, b = %d\n", a, b);
    
    swap(&a, &b); 
    printf("after calling swap(), a = %d, b = %d\n", a, b);
    
}

void swap(int *x, int *y) 
{
    int temp = *x;
    *x = *y;
    *y = temp;
}
```
