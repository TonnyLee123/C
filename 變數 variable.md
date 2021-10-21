# 區域/ 全域/ 靜態變數 (local/ global/ static variable)

## 1.local variable
宣告於**函數內**的變數。  
**活動範圍(scope)**(變數可以被使用的範圍): 始於**宣告之處**，終於**函數結束**之時。  
**生命週期(life cycle)**(variable保留在記憶體的時間):一旦函數A執行完畢，則函數A裡的variable會被銷毀。
不同函數裡，可以declear相同變數名稱。因為他們有個各自的記憶空間。
```c
int main()
{
    int n;                __
    printf("Enter n ");     |n
    scanf("%d", &n);        |的
                            |活
    printf("%d", fac(n));   |動
                            |範
    return 0             __ |圍
}
```
## 2.global varible
宣告於**函數外**的變數。  
每個函數及程式區段皆可以使用(好處:方便)。
```c
void func();
int a;  /*declear a global variable*/

int main()
{   
    a = 100;
    printf("呼叫func之前 a = %d\n", a);
    
    func();
    printf("呼叫func之後 a = %d\n", a);
    
    return 0;
}

void func()
{
    a=300;
    printf("於func()裡 a = %d\n", a);
}
```

## global varible name == local varible name
local variable **不受** global 影響
```c
int a = 999;
int main()
{
    int a = 1;
    printf("%d", a);
    
    return 0;
}
```
## static variable
宣告於**函數內**的變數 -> scope:此函數內。  
配置**固定的記憶體空間**(即使函數結束時，變數的值還是可以被保存)
```c
static int num;
```
```c
void func();

int main()
{
    func();
    func();
    func();

    return 0;
}

void func()
{
    static int a = 100;
    printf("%d\n", a);
    a += 200;   /* new value for a, and will not be removed */
}
```
比較此方程式
```c
void func();

int main()
{
    func();
    func();
    func();

    return 0;
}

void func()
{
    int a = 100;   ->local
    printf("%d\n", a);
    a += 200; /*雖然此時a = 300，但是當此函數結束時，300會被移除*/
}
```
