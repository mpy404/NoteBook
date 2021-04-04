# String 字符串

## 字符串的特点

- 字符串不可变，它们的值在创建后不能被更改
- 虽然String的值是不可变的，但是它们可以被共享
- 字符串效果上相当于字符串数组（char[]），但是底层原理是字节数组（byte[]）

## String的构造方法

1. 创建一个空白字符串对象，不包含任何内容

   ```java
   String s1 = new String();
   ```

2. 根据字符数组的内容，来创建字符串对象

   ```java
   char[] str = {'a', 'b', 'c'};
   String s2 = new String(str);
   ```

3. 根据字节数组的内容，来创建字符串对象

   ```java
   byte[] bytes = {97, 98, 99};
   String s3 = new String (bytes);
   ```

4. 直接赋值的方式创建字符串对象

   ```
   String str = "abc";
   ```

## String 特点

- 以 " " 方式给出的字符串，只要字符序列相同（顺序和大小写），无论在程序代码中出现几次，JVM都会建立一个String对象，并在字符串池中维护

## String 操作方法

### toString()

- 返回对象的字符串表示形式，建议子类重写该方法

> alt + ins ——> toString()

### equals()

- 比较对象是否相等，默认的也是比较地址，也需要重写

> == 相比较是比较的是两个类的地址是否一样
>
> equals()比较的是两个类的内容是否一样（需要重写）

- 测试类

```java
public static void main(String[] args){
    Test test1 = new Test("Mpy", "20");
    Test test2 = new Test("Mpy", "20");
    // 创建两个对象相比较
    System.out.println(test1.equals(test2));
}
```

- 方法重写

```java
public class Test {
    private String name;
    private String age;
    public Test(){}
    public Test(String name, String age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public String getAge() {
        return age;
    }

    public void setName(String name) {
        this.name = name;
    }

    public void setAge(String age) {
        this.age = age;
    }
   // 重写toString方法
    @Override
    public String toString() {
        return "Test{" +
                "name='" + name + '\'' +
                ", age='" + age + '\'' +
                '}';
    }
    // 重写equals方法
    @Override
    public boolean equals(Object o){
        // this —— 代表的是test1
        // o —— 代表的是test2
        if (this == o){ // 比较两者的地址是否一样，一样直接返回true
            return true;
        }
        if (o == null || getClass() != o.getClaass()){ // 先比较test.equals(test1)中的test1是否为空，在比较两个对象是否来自同一个类
            return false;
        }
        Test test = (Test) o; // 向下强转，可以让test1.age和test2.age可以进行比较
        if (age != test.age){ // 这里的age是this.age也就是test1的age，而后面的test是刚刚强转后的，可以访问自己的变量
            return false;
        }
        // name不等于null，之后调用String的equals方法进行比较
        return name != null ? name.equals(test.name) : test.name == null;
    }
}
```

### charAt() 

- 用于返回指定索引处的字符。索引范围为从 0 到 length() - 1。

- 字符串的遍历

```java
public static void main(String[] args) {
    String str = "abcdefghijklmnopqresuvwxyz";
    for (int i = 0; i < str.length(); i ++){
        System.out.print(str.charAt(i) + " ");
    }
}
```

## 案例

### 字符串的统计

```java
public class Demo{
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        String str_1 = sc.nextline();
        int big = 0;
        int small = 0;
        int number = 0;
        for(int i = 0; i < str_1.length(); i ++) {
            char ch = charAt(i);
            if (ch >= 'A' && ch <= 'Z'){
                big ++;
            }else if(ch >= 'a' && ch <= 'z'){
                small ++;
            }else if(ch >= '0' && ch <= '9'){
                number ++;
            }
        }
        System.out.println(big);
        System.out.println(small);
        System.out.println(number);
    }
}
```

### 字符串的比较

1. 利用`==`
2. `equals()`，将此字符串与指定的字符串相比较（s1.equals(s2）

### 字符串的拼接

```java
package demo1;
import java.util.Scanner;

public class Demo1 {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        String str_1 = sc.nextLine();
        String str_2 = "";
        str_2 += "[";
        for (int i = 0; i < str_1.length(); i ++){
            if(i == (str_1.length() - 1)){
                str_2 += str_1.charAt(i);
            }else{
                str_2 += str_1.charAt(i);
                str_2 += ", ";
            }
        }
        str_2 += "]";
        System.out.println(str_2);
    }
}
```

### 字符串的旋转

```java
package demo1;

import java.util.Scanner;

public class Demo8 {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        String s = sc.nextLine();
        String ss = reverse(s);
        System.out.println(ss);
    }
    public static String reverse(String str){
        String str_1 = "";
        for (int i = str.length() - 1; i >= 0 ; i --){
            str_1 += str.charAt(i);
        }
        return str_1;
    }
}
```

# StringBuilder

- String 与StringBuilder
  - String内容是不可变的
  - StringBuilder内容是可变的

## 构造方法

1. 创建一个空白可变字符串对象，不含任何内容

   ```java
   StringBuilder ss = new StringBuilder();
   ```

2. 根据字符串的内容，来创建可变字符串 对象

   ```java
   StringBuilder ss = new StringBuilder("hello"); 
   ```

## String和StringBuilder转换

1. String Builder转String

   - 通过toString()就可以实现把String Builder转换成String

     ```java
     package demo2;
     
     public class Demo1 {
         public static void main(String[] args) {
             StringBuilder s1 = new StringBuilder();
             s1.append("hello ").append("world");
             System.out.println(s1);
             String s2 = s1.toString();
             System.out.println(s2);
         }
     }
     ```

2. String转StringBuilder

   - 通过构造方法就可以实现吧String转换成String Builder

     ```java
     package demo2;
     
     public class Demo1 {
         public static void main(String[] args) {
             String s3 = "you is sb";
             StringBuilder s4 = new StringBuilder(s3);
             System.out.println(s4);
         }
     }
     ```



- 数组的转换（数组按照StringBuilder输出在按照String返回）

  ```java
  public class Demo2 {
      public static void main(String[] args) {
          int[] arr = {1, 2, 3, 4};
          String s1 = arrayToString(arr);
          System.out.println(s1);
      }
      public static String arrayToString(int[] arr){
          StringBuilder str = new StringBuilder();
          str.append("[");
          for (int i = 0; i < arr.length; i ++){
              if (i== arr.length - 1){
                  str.append(arr[i]);
              }else{
                  str.append(arr[i] + ", ");
              }
          }
          str.append("]");
          String ss = str.toString();
          return ss;
      }
  }
  ```



- 字符串的翻转（String转StringBuilder，调用reverse，再转String）

  ```java
  package demo2;
  
  import java.util.Scanner;
  
  public class Demo3 {
      public static void main(String[] args) {
          Scanner sc = new Scanner(System.in);
          String str = sc.nextLine();
          StringBuilder str1 = new StringBuilder(str);
          str1.reverse();
          String str2 = str1.toString();
          System.out.println(str2);
  
      }
  }
  ```

  - 简易版本

  ```java
  import java.util.Scanner;
  
  public class Demo3 {
      public static void main(String[] args) {
          Scanner sc = new Scanner(System.in);
          String str = sc.nextLine();
          String s = reverse(str);
          System.out.println(s);
  
      }
      public static String reverse(String s){
          return new StringBuilder(s).reverse().toString();
      }
  }
  ```
