# 1. 陣列(array)
- 由一群**相同型態的變數**所組成的一種**資料結構**。  
- 陣列中個別的**元素(element)** 是以 **索引值(index)** 來標示存放的位置。
    - |score[0]|score[1]|score[2]|
      |--------|--------|--------|
      |第一個|第二個|第三個|
    - index從**0**開始。 
    - -1 為最後
- 陣列存放元素的複雜程度，分為一維，二維，三維等等陣列。  

# 2. 一維陣列(1-Dimensional array)
## 2.1 1-Dimensional array declearation
```c
資料型態 陣列名稱[個數];

int score[3];  宣告整數陣列，且可以存放3個elements。
```
宣告後，編譯器將分配一個**連續**區塊的記憶體。

### 範例一 殘值:超出index，或是中間的某個index沒設值。
```c
// 由output得知，score[2]和score[4]的值為原先留在**記憶體內的殘值**。
int main() {
    
    int i, score[4];
    
    score[0] = 0;
    score[1] = 2;
    /*score[2] = 4; 此行故意不給score[2]設值*/
    score[3] = 6;
    
    for(i=0; i<=4; i++) /*故意列印出score[4]*/
    {
        printf("score[%d] = %d\n", i, score[i]);
    }
    
    return 0;
```
## 2.2 陣列初值的設定
```c
int num[5] = {1, 2, 3, 4, 5};

int num[] = {1, 2, 3}; /*若宣告時沒有將元素個數列出，編譯器會視給予得初值來決定陣列的大小。 3個初值，所以num的大小為3*/

int num[3] = {1, 2, 3, 4, 5}  // excess element in array initializer.

int i;
int num[5] = {1, 2, 3}; // 有5個空位，已經填3個，剩餘2個座位=0
for(i=0; i < 5; i++)
{
    printf("%d ", num[i]);
}

```

## 2.3 查詢陣列所佔的記憶體空間

### 範例一 sizeof()
```c
int main() {
    
    int num[3] = {1, 2, 3};
    
    int x = sizeof((num));    /*陣列所佔的位元組*/
    int y = sizeof((num[0])); /*單個元素所佔的位元組*/
    
    int z = x / y;            /*陣列大小*/
    printf("%d %d\n", x, y);
    printf("%d", z);
    
    return 0;
}
```

## 2.4 陣列的輸入與輸出
### 範例一 由user輸入各element
```c
// &位址符號，把輸入的資料存放在指位址的記憶體內
scanf("%d", &num[i]);
```
```c
int main() {
    
    int i, num[3];
    for(i = 0; i <= 2; i++)  // 透過for loop來執行每一個element
    {
        printf("Enter a number: ");
        scanf("%d", &num[i]);  // &位址符號，把輸入的資料存放在指位址的記憶體內
    }
    
    /*列印出每一個個元素*/
    for(i = 0; i < 3; i++)  
    {
        printf("num[%d] = %d\n", i, num[i]);
    }
}
```
### 範例二 尋找MAX和min元素
```c
int main() {
    
    int num[5] = {1, 2, 3, 4, 99};
    int MAX = num[0], min = num[0]; /*先把最大及最小值設在第一個元素*/
    int i;
    for(i = 1; i < 5; i++) /*利用for loop去判斷每個元素*/
    {
        if(num[i] > MAX)   /*如果我比你大，我是max*/
        {
            MAX = num[i];
        }
        if(num[i] < min)
        {
            min = num[i];
        }
    }
    printf("Max = %d, min = %d", MAX, min);

    return 0;
}
```
### 範例三 尋找MAX和min元素
當不知道user要輸入多少資料時，使用do-while。  
比較範例二。
```c
#define MAX 10
int main()
{   
    int score[MAX]; /*最多可以有10個element*/
    int i=0, num;
    int sum = 0;
    printf("請輸入成績，要結束請輸入0\n");
    
    do
    {
        printf("請輸入成績: ");
        scanf("%d", &score[i]);
    }while(score[i++]>0);     // 當輸入0時，跳出去 do while。  
    // 判斷score[0]是否>0，然後i=i+1，i = 1
    // 判斷score[1]是否>0，然後i=i+1，i = 2
    // 判斷score[2]是否>0，然後i=i+1，i = 3
    // 判斷score[3]是否>0，然後i=i+1，i = 4
    // 判斷score[4]是否>0，然後i=i+1，i = 5
    // 預設 score[10] = {60, 70, 80, 90, 0, 0, 0, 0, 0, 0}; 
    
    // 跳出while loop i 也會加1，此題跳出迴圈後i = 5
    num = i - 1; /*輸入0結束，因此總數要-1*/
    
    for(i = 0; i < num; i++)
    {
        sum += score[i];
    }   
    printf("平均分數: %f", (float)sum/num); //轉換資料類型    
    return 0;
}
```

## 陣列邊界的檢查 (不懂!!)
c語言**不會**檢查index的大小，也就是說當index超過陣列長度時，c並不會不讓使用者繼續使用該陣列，它只是將多餘的值放在陣列外的記憶體中，這樣可能會蓋掉其他的資料，或程式碼，因此產生不可預期的錯誤
**(run-time error)**
- int arr[3] = {1, 2, 3, 4}; // 4將被放到陣列外的記憶體中

### 範例一 陣列界線的檢查程式: 輸入五筆資料後，結束，確保不會超過arrary的大小
```c
#define MAX 5
int main()
{
    int score[MAX]; /*宣告此陣列可以存放MAX個整數*/
    int i=0, num;
    float sum=0.0f;
    
    printf("請輸入成績，要結束請輸入0:\n");
    
    do
    {
        if(i == MAX) /*先檢查目前有沒有超過array的大小，當i == MAX時，表示陣列已滿*/
        {
            printf("陣列空間已使用完畢!!\n");
            i++; /*i = 6, 因為下面num = i - 1*/
            break;
        }
        printf("請輸入成績: ");
        scanf("%d", &score[i]);
    }
    while(score[i++]>0); /*輸入0，結束*/
    
    num = i - 1;  
    for(i=0; i<num; i++)
    {
        sum += score[i];
    }
    printf("平均成績為%.2f\n", sum/num);
}

```
## flag
flag 是專門記錄搜尋的結果
- flag = 1 找到符合
- flag = 0 沒找到符合
### 範例一 在陣列中尋找是否有你要的值    
```c
#define SIZE 6
int main()
{
    int i, num, flag = 0;
    int A[SIZE] = {33, 75, 69, 41, 33, 19};
    
    printf("array A 的元素為: ");
    for(i = 0; i<SIZE; i++)
        printf("%d ", A[i]);
        
    printf("\n請輸入欲搜尋的整數: ");
    scanf("%d", &num);
    
    for(i=0; i<SIZE; i++)
    {
        if(A[i]==num) /*判斷輸入的值是否和元素相同*/
        {
            printf("找到了");
            flag=1; /*flag = 1 代表有找到相同的值*/
        }
    }
    
    if(flag == 0)
        printf("沒有找到相同的值\n");
            
    return 0;
}
```
```
## 一維陣列的應用--**氣泡排序法(bubble sort)**
讓數值大的數字慢慢往右移，就像在水裡氣泡上浮一樣。  
從左到右，把數字**兩兩比對**，若前比後大，則前後交換。 

### 舉例: 將下列數值從小到大排序。
26 5 81 7 63
#### 第一次搜尋:    
5 26 81 7 63 (5<26，對調)
5 26 81 7 63 (26<81，不變)
5 26 7 81 63 (81>7，對調)
5 26 7 63 81 (81 > 63，對調)  
由結果得知，第一次搜尋，最大移到最右邊  

#### 第二次搜尋: 次大，到位(到應該的位置(倒數第二))
5 26 7 63 81 (5<26，不變)
5 7 26 63 81 (26>7，對調)
#### 第三次搜尋: 第三大，到位
#### 第四次搜尋: 第四大，到位
### 總結: n筆數據，搜尋n-1次

```c
void show(int a[]), bubble(int a[]); /*宣告兩個函數*/

int main()
{
    int data[5] = {1, 4, 2, 5, 3};
    bubble(data);
    show(data);
    return 0;
}

void show(int a[]) /*print array*/
{   
    int i;
    for(i = 0; i < 5; i++)
    {
        printf("%d ", a[i]);
    }
}

void bubble(int a[]) /*bubble sort*/
{   
    int i, j, temp; 
    for(i = 1; i < 5; i++)/*第i次搜尋, i<5 因為搜尋4次*/
    {
        for(j = 0; j < 4; j++)/*第j個元素，j<4 因為[j+1]*/
        {
            if(a[j] > a[j+1])
            {
               temp = a[j]; /*創建一個temp暫時存放a[j]*/
               a[j] = a[j + 1];
               a[j + 1] = temp;
            }
        }
    }
}
```
bubble sort雖然結果正確，但是儘管資料已完成排序，也必須不斷的重複比較，直到外層迴圈執行完畢為止，較浪費時間。  
為了改進此缺點，下面範例引進了一個旗標變數(flag)，用來控制進入外層迴圈的時機。  
出發點: 如果已經達到正確排序(無調換)，就不要進行下一波的搜尋 -> 外層for loop新增新的condition(!flag)

```c
void show(int a[]), bubble(int a[]); 

int main()
{
    int data[5] = {1, 4, 2, 5, 3};
    bubble(data);
    show(data);
    return 0;
}

void show(int a[])
{   
    int i;
    for(i = 0; i < 5; i++)
    {
        printf("%d ", a[i]);
    }
}

void bubble(int a[])
{   
    int i, j, temp; 
    int flag = 0; /*設定flag = 0*/
    for(i = 1; i < 5 && (!flag); i++) /*!flag = true*/
    {   
        flag = 1; /*如果沒調換，flag = 1*/
        for(j = 0; j< (5 - i); j++)
        {
            if(a[j] > a[j+1])
            {
               temp = a[j];
               a[j] = a[j + 1];
               a[j + 1] = temp;
               flag = 0; /*flag = 0*/
            }
        }
    }
}
```
搜尋過程中，若有2元素調換，則**flag = 0**; 無調換則**flag = 1**，不符合條件，不用下一回合的搜尋，陣列已完成排序。

# 2. 二維陣列
多個一維陣列組成。
## 2.1 2-dimensions array的宣告與初值的設定
```
資料型態 陣列名稱 [row][column]; 
資料型態 陣列名稱 [row][column]  = {{第一列初值}, {第二列初值}, {...}};

注意: 橫為row，直為column

二維及二維以上在設定初值時，可省略第一個索引值，以方便的增減陣列大小。  
int temp[][3] = {{1, 2, 3}, {4, 5, 6}}
```
### 範例一 2x4的陣列:由2個一維陣列組成。
| |春|夏|秋|冬|
|--|--|--|--|--|
|甲|30|35|26|32| 
|乙|33|34|30|29|
  
```c
int sale[2][4] = {{30, 35, 26, 32},
                  {33, 34, 30, 29}}
```

### 範例二 二維陣列元素的存取 nasted for loop
第一個for loop 負責 row.  
第二個for loop 負責 column(即每列的每一個元素).
```c
int main()
{
   int i, j, sale[2][4], sum = 0;
   
    for(i = 0; i < 2; i++)                            // 從外圍的元素開始
       for(j = 0; j < 4; j++)                         // 內部的內部元素
       {
           printf("業務員%d的第%d季業績: ", i+1, j+1); 
           scanf("%d", &sale[i][j]);                  // 00, 01, 02, 03; 10, 11, 12, 13
       }
    /*輸出銷售量並計算總數*/   
    for(i = 0; i < 2; i++)                            
    {
        printf("\n業務員%d的業績分別為", i + 1);
        for(j = 0; j < 4; j++)
        {
            printf("%d ", sale[i][j]);
            sum += sale[i][j];
        }       
    }
    printf("\n2021年總銷量為: %d", sum);
    return 0;
}
```
### 範例三 二維矩陣的相加
數學上的矩陣(matrix)結構和二維陣列類似，因而可以利用二維陣列儲存矩陣。兩個相同維度的陣列，可以進行加法的運算。  
A = [1, 2, 3], B = [3, 0, 2], 求A + B = ?  
    [5, 6, 8]      [3, 5, 7]

```c
#define ROW 2
#define COL 3

int main()
{
   int A[ROW][COL] = {{1, 2, 3}, {5, 6, 8}};
   int B[ROW][COL] = {{3, 0, 2}, {3, 5, 7}};
   
   printf("Matrix A+B =\n");
   
   int i, j;
   for(i=0; i<ROW; i++)     /*外層控制列*/
   {
       for(j=0; j<COL; j++) /*內層控制行*/
       {
           printf("%3d", A[i][j]+B[i][j]);  // matrix 相同位置相加
       }
       printf("\n");
   }

    return 0;
}
```
# 3. 三維陣列
多個二維陣列組成
2x4x3 =  2個4x3的二維陣列，如下圖:
int A[2][4][3] = 
補圖p 9-24
### 範例三 找出最大element
```c
int main()
{
    int A[2][4][3] = {{{1, 2, 3},
                       {4, 5, 6},
                       {7, 8, 9},
                       {10, 11, 12}},
                      {{13, 14, 15},
                       {16, 17, 18},
                       {19, 20, 21},
                       {22, 23, 24}}};
    int i, j, k, max = A[0][0][0]; /*假設第一個元素最大*/
    
    for(i=0; i<2; i++)
        for(j=0; j<4; j++)
            for(k=0; k<3; k++)
            {
                if(max<A[i][j][k])
                    max = A[i][j][k]; /*如果下一個元素比max大，則他為max*/ 
            }
    printf("max = %d", max);
}
```

# 多維陣列
- n維，n個for loop
- n維陣列 = 多個n-1維陣列組成
- A[x][y][z]....[]，分別為第一維度，第二維度，第三維度，第n維度
- int a[][][][][].... 
       外------>內

# 傳遞陣列給函數
- 傳遞**陣列位址**給函數，而不是陣列中每個元素的值
```c

傳回值型態 函數名稱(資料型態 陣列名稱[]); /*函數原型*/ 
int main()
{
    資料型態 陣列名稱[個數];
    ...
    函數名稱(陣列名稱);
    ...
 }
 傳回值型態 函數名稱(資料型態 陣列名稱[])  /*[]內可以不填元素個數*/
 {
    ...
 }
```
### 範例一 把一維陣列傳遞給函數show
```c
void show(int arr[]);        /*宣告函數prototype，記得要 陣列名稱[]*/

int main()
{
    int A[4] = {1, 2, 3, 4}; /*設定陣列A初值*/
    printf("陣列的內容為: ");
    show(A);                 /*呼叫函數show()，傳遞陣列A到函數show()裡，傳遞的內容並不是陣列A的內容，而是**陣列A的位址** */

    return 0;
}

void show(int arr[]) /*一維陣列時，[]內可以不用打元素個數*/
{
    int i;
    for(i=0; i<4; i++)
    {
        printf("%d ", arr[i]);
    }
    
}
```

# 函數傳遞引數的機制
- call by value
- 陣列名稱是存放陣列位址的變數。
- 陣列位址 == 第一個元素的位址。
- main()裡的陣列，和傳到某函數裡的陣列是一樣的，只是名稱不同。
### 範例一  call by value(傳值呼叫)
圖: p 9-31

```c
void func(int);
int main()
{
    int a = 10;
    printf("於main()裡，a的位址為: %p\n", &a);
    
    func(a); // 傳遞a到func
    return 0;
}

void func(int a)   // 複製a的值，給A，兩個變數在不同的address
{
    printf("於func()裡，A的位址為: %p", &a);

}
```

### 範例二 call by address(傳址呼叫)
```c
void func(int a[]);

int main()
{
    int i, a[3] = {8, 13, 20};
    
    for(i=0; i<3; i++)
    {
       printf("a[%d]=%2d,位址為%p\n", i, a[i], &a[i]);
       printf("陣列a的位址 = %p", a);
    }
    
    func(a);       // 傳遞變數a的位址   
}

void func(int A[]) // 接收變數a的位址
{   
    int i;
     for(i=0; i<3; i++)
    {
       printf("A[%d]=%2d,位址為%p\n", i, A[i], &A[i]); 
       printf("陣列A的位址 = %p", A);
    }   
}
```
### 範例三 calling by address
由於array在各程式傳遞的是**位址**，所以值會變修改。
```c
void show(int arr[]);
void add2(int arr[]);

int main()
{   
    int A[3] = {1, 2, 3};
    printf("before calling add(), A = ");
    show(A);
    
    add2(A); 
    printf("after calling add(), A = ");
    show(A);
    
    return 0;
}

void show(int arr[])
{
    int i;
    for(i=0; i<3; i++)
        printf("%d ", arr[i]);
    printf("\n");
}
void add2(int arr[])
{
    int i;
    for(i=0; i<3; i++)
        arr[i] += 2;
}
```
# 陣列位址
陣列名稱本身就是存放陣列位址的變數。
