You are given two long numbers **N1** and **N2** in a string. You need to find out if the product of these numbers generate an even number or an odd number, If it is an even number print 1 else print 0.


**Input:** 
N1 = "12"
N2 = "15"
**Output:** 1
**Explanation**: 12 * 15 = 180 which is an 
even number.


  

To solve this problem, we should be thorough with the following property:

Odd*Odd=Odd

Odd*Even=Even

Even*Even=Even

Also, don't check for the full number, as we can know if a number is even or odd just by looking at the last digit of the number.


```
int EvenOdd(string n1 , string n2)
{
    // getting their last digits
   int n1_last=n1[n1.length()-1]-'0';
   int n2_last=n2[n2.length()-1]-'0';

    //if and only if both last digits are odd then product will be odd.
   if(n1_last%2==0&&n2_last%2==0)
       return 1;
       
    else if(n1_last%2!=0&&n2_last%2!=0)
       return 0;

    return 1;

}
```