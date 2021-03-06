# 1. 字串
- 字串是由字元陣列所組成的(即陣列的元素是字元)。  
```c
char char_array[6] = {'H', 'e', 'l', 'l','o', '\0'};
int arr[3] = {1, 2, 3}
```
- 字元常數 -> 'a'  
- 字串常數 -> "a"，"Hello World"
- \0 字串結束字元: 辨認字串結束的位置。

# 2. 字串的宣告與初值的設定
### 範例一
```c
char name[6] = "Hello"; /*雖然Hello只有5個字元，但編譯器會自動在字串結尾處加上\0，因此必須+1 */
char name[] = "Hello";  /*不填入陣列大小，讓編譯器自動依照字串大小來配置記憶體空間。*/
```

# 3. 字串的輸入與輸出函數
scanf()讀取字串時的限制 -> 不能讀取字串裡的空白(tonny lee -> tonny)。  
因此c提供**get(), puts()** 函數，原型都是定義在**stdio.h**。

## 3.1 gets(get string)

```
gets(字元陣列名稱)
```

## 3.2 puts(put string) 
puts會自動換行，因此printf較常用。  

```
puts(字元陣列名稱); 
puts(name);

puts(字串常數);
puts("Hi");
```
### 範例一 輸入名字
```c
int main()
{   
    char name[15];
    puts("What is your name?");
    
    gets(name);  /*scanf("%s", name);*/
    
    puts("Hi"); 
    puts(name);
    puts("how are you?");
    return 0;
}
```

### 範例二 LowwerToUpper
透過ASCII轉換。
```c
void toUpper(char s[]);

int main()
{   
    char str[15];
    printf("Enter a string: ");
    
    gets(str); 
    
    toUpper(str);
    printf("轉換後為: %s", str);
    return 0;
}

void toUpper(char s[])
{
    int i=0;
    while(s[i]!='\0')             /*如果字串還沒結束，執行以下程式*/
    {
        if(s[i]>=97 && s[i]<=122) /*如果是小寫字母*/
            s[i] = s[i]-32;       /*小寫ASCII-32變大寫*/
        i++;
    }
}
```
# 4. String Arrary
- 多個字串組成。
- 二維陣列儲存。

## 4.1 字串陣列的宣告與初值的設定

```
"字串常數" 是一維陣列，所以不用{}包覆。
char 字元陣列名稱[字串個數][字串長度] = {"字串常數1", "字串常數2", ..., "字串常數n"}; //宣告同時設值
char member[3][10] = {"tony", "tom", "lily"};
```

### 範例一 string array元素的引用及存取
```c
int main()
{
    char member[3][10] = {"tony", "tom", "lily"};  // member[0] = tonny
    int i;
    
    for(i=0; i<3; i++)
    {
        printf("member[%d] = %s\n", i, member[i]);
    }
    return 0;
} 
```
### 範例二 字串陣列的複製: 將arr1的內容複製到arr2
```c
int main()
{
    char arr1[3][10] = {"tony", "tom", "lily"};
    char arr2[3][10];
    int i, j;
    
    /*將arr1複製到arr2*/
    for(i=0; i<3; i++)             /*每個字串*/
    {
        for(j=0; j<10; j++)        /*每個字母*/
            if(arr1[i][j] == '\0') /*當字元為\0跳出for loop*/
                break;
            else
                arr2[i][j] = arr1[i][j];
        arr2[i][j] = '\0';         /*再把\0補上*/
    }
    
    for(i=0; i<3; i++)
        printf("arr2[%d] = %s\n", i, arr2[i]);
    
    return 0;
}
```
