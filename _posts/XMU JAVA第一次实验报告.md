## JAVA实验报告1   
#### 一、数字金字塔

##### 题目

输入一个正整数n(n<16)，输出一个如图的数字金字塔（下图是当n=7的输出）。不考虑输入错误的情形。
要求使用Scanner作为输入，System.out.print作为输出。

![\[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-iw8ZVssN-1588171052993)(C:\Users\HUAWEI\AppData\Roaming\Typora\typora-user-images\image-20200331144513941.png)\]](https://img-blog.csdnimg.cn/20200429223850472.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L21hdGFmZWl5YW5sbA==,size_16,color_FFFFFF,t_70)


##### 思路

用两个for循环嵌套就可以解决了，注意一下边界的问题

顺序结构设计，先打印空格，再打印递减数字，再打印递增数字，KO

##### 代码

```java
package com.company;
import java.util.*;
public class Main {

    public static void main(String[] args) {
	// write your code here
        Scanner input = new Scanner(System.in);
        int n;
        n = input.nextInt();
        for(int i=1;i<=n;i++){
            for(int j=1;j<=n-i;j++)
                System.out.print("   ");  //打印空格
            for(int j=i;j>=1;j--)
                System.out.printf("%3d",j);  //打印前面数字
            for(int j=2;j<=i;j++)
                System.out.printf("%3d",j);  //打印后面数字
            System.out.println();
        }
    }
}


```

##### 效果图

![\[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-ySpC2fdQ-1588171052994)(C:\Users\HUAWEI\AppData\Roaming\Typora\typora-user-images\image-20200331160322590.png)\]](https://img-blog.csdnimg.cn/20200429223910586.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L21hdGFmZWl5YW5sbA==,size_16,color_FFFFFF,t_70)


#### 二、PI的近似值

##### 题目

使用下式计算PI的近似值并显示。其中i的值由用户输入。
要求使用JOptionPane.showInputDialog作为输入，JOptionPane.showMessageDialog作为输出。
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200429223934868.png)


##### 思路

用一重循环就能解决问题，用一个flag标志位控制正负号，分分钟写完

##### 代码

```java
package com.company;
import javax.swing.*;
import java.util.*;
public class Main {

    public static void main(String[] args) {
	// write your code here
        String ii = JOptionPane.showInputDialog("please input i:");
        int i = Integer.parseInt(ii);
        int flag = -1;
        double item,sum=0;
        for (int n = 1; n <= i; n++) {
            flag *= -1;
            item = flag * 1.0 / (2 * n - 1);
            sum += item;
        }
        JOptionPane.showMessageDialog(null,"π的近似值=" + (sum * 4));
        System.out.println("π的近似值=" + sum * 4);
    }
}
```

##### 效果图

![\[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-pcCunHyF-1588171052998)(C:\Users\HUAWEI\AppData\Roaming\Typora\typora-user-images\image-20200331150256435.png)\]](https://img-blog.csdnimg.cn/202004292239578.png)




#### 三、回文素数

##### 题目

回文素数指某一个数既是回文数、又是素数，例如2, 3, 5, 7, 11, 101, 131,… 编程找出前100个回文素数，并且要求按照每行10个的格式输出。
输出方式任选。

##### 思路

按照模块化求解，先用两个函数判断是不是回文数以及是不是素数，再在主函数里调用判断，注意格式化输出，达到美观对齐的效果。

判断回文数用字符串的形式处理较为方便，不用一位一位去提取数字

判断素数用了两个技巧，如果是2的偶数则返回0，之后每次判断直接加2就行，上界为Math.sqrt(number)，时间复杂度大大降低。

总体来说是较为繁琐的，时间复杂度O(n*n)

##### 代码

```java
package com.company;

import javax.swing.plaf.synth.SynthSliderUI;
import java.util.Scanner;

public class Main {
    //判断回文数，用string类处理较为方便hhh
    public static int huiwenshu(String number) {
        int length = number.length();
        for (int i = 0; i <= length / 2; i++) {
            if (number.charAt(i) != number.charAt(length - i - 1)) {
                return 0;
            }
        }
        return 1;
    }

    //判断素数
    public static int sushu(int number) {
        if (number == 1 || number % 2 == 0 && number != 2) {
            return 0;
        } else {
            for (int i = 3; i <= Math.sqrt(number); i += 2) {
                if (number % i == 0) {
                    return 0;
                }
            }
        }
        return 1;
    }

    public static void main(String[] args) {
        Scanner input = new Scanner(System.in);
        int count = 0;
        for (int i = 2; count<100; i++) {
            if (sushu(i) == 1) {
                String b = String.valueOf(i);
                if (huiwenshu(b) == 1) {
                    System.out.printf("%10s", b);
                    count++;
                    if(count%10==0)
                        System.out.println();
                }
            }
        }
    }

}

```

##### 效果图

![\[外链图片转存失败,源站可能有防盗链机制,建议将图片保存下来直接上传(img-mHtkjYBt-1588171052999)(C:\Users\HUAWEI\AppData\Roaming\Typora\typora-user-images\image-20200331153529614.png)\]](https://img-blog.csdnimg.cn/20200429224018612.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L21hdGFmZWl5YW5sbA==,size_16,color_FFFFFF,t_70)




#### 四、数组合并

##### 题目

写一个合并数组的方法，将两个已排序的数组合并成一个有序的大数组。方法的原型如下：
public static int[] merge(int[] list1, int[] list2)
要求提供一个测试的main函数，让用户输入两个数组的大小及元素值，最后调用上述方法并输出合并结果。
输入输出方式任选。
例如用户输入2 1 5 3 2 5 10，表示第一个数组有2个元素{1,5}；第二个数组有3个元素{2,5,10}，输出合并结果为：1 2 5 5 10

##### 思路

采用归并排序算法中的merge过程来和平两个已经排好序的数组。设置三个指针，p1、p2是检测指针，k是存放指针。如果p1,p2都还没有越界，则判断list[p1],list[p2]的大小，将小的那个放入代存放数组tmp中，同时指针加一。设计思路清晰。

##### 代码

```java
package com.company;
import com.sun.org.apache.xerces.internal.impl.xs.SchemaNamespaceSupport;

import java.util.*;
public class Main {
    //归并排序中的Merge算法
    public static int[] merge(int[] list1, int[] list2){
        int []tmp=new int[list1.length+list2.length];
        int p1=0,p2=0,k=0;  //p1、p2是检测指针，k是存放指针
        while(p1<list1.length && p2<list2.length){
            if(list1[p1]<=list2[p2])
                tmp[k++]=list1[p1++];
            else
                tmp[k++]=list2[p2++];
        }
        while(p1<list1.length) tmp[k++]=list1[p1++];
        while(p2<list2.length) tmp[k++]=list2[p2++];
        return tmp;
    }
    //打印数组
    public static void print(int[] list){
        for(int i=0;i<list.length;i++)
            System.out.print(list[i]+" ");
    }
    public static void main(String[] args) {
        int length1,length2;
        Scanner input = new Scanner(System.in);
        length1 = input.nextInt();
        int[] list1 = new int[length1];
        //读入数组
        for(int i=0;i<length1;i++)
            list1[i] = input.nextInt();
        length2 = input.nextInt();
        int[] list2 = new int[length2];
        for(int i=0;i<length2;i++)
            list2[i] = input.nextInt();
//        print(list1);
//        print(list2);
        int[] mergedarray;
        mergedarray = merge(list1,list2);
        print(mergedarray);
    }
}

```

##### 效果图
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200429224048871.png)

