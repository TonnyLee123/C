# pointer概述
指標可以存取變數的值，就像是利用變數名稱存取變數內容。  
指標可以看成一種特殊的變數，用來存放變數在**記憶體中的位址**  
位址(address): when we declare a variable, the compiler will assign a memory space with **unique number** called "address" to it.
![圖片01](./pointer01.JPG)

```
指標ptr指向變數a
```
**依址取值**(adress -> variable value): 當指標ptr指向變數a之後，如果要存取變數a時，便可利用指標ptr找到變數a的address，再由該位址取出所儲存的變數值。

位元組定址法
