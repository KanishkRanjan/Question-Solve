Given an integer n, your task is to complete the function **convertToRoman** which prints the corresponding roman number of n. Various symbols and their values are given below  
Note:- There are a few exceptions for some numbers like 4 in roman is IV,9 in roman is IX, similarly, 40 is XL while 90 is XC. Similarly, 400 is CD while 900 is CM

I 1  
V 5  
X 10  
L 50  
C 100  
D 500  
M 1000
```
	class Solution{
  public:
    string convertToRoman(int n) {
        string strrom[][10]={{"","I","II","III","IV","V","VI","VII","VIII","IX"},{"","X","XX","XXX","XL","L","LX","LXX","LXXX","XC"},
                            {"","C","CC","CCC","CD","D","DC","DCC","DCCC","CM"},{"","M","MM","MMM","","","","","",""}};
            int i=0;
            string str="";
            while(n){
            str = strrom[i][n % 10] + str;
            n /= 10;
            i++;
        }
        return str;
    }
};
```



**Step 1**

  

-   Initially number = 3549
-   Since 3549 >= 1000 ; largest base value will be 1000 initially.
-   Divide 3549/1000. Quotient = 3, Remainder =549. The corresponding symbol **M** will be repeated thrice.
-   We append the Result value in the 2nd List.
-   Now Remainder is not equal to 0 so we call the function again.

**Step 2**

  

-   Now, number = 549
-   1000 > 549 >= 500 ; largest base value will be 500.
-   Divide 549/500. Quotient = 1, Remainder =49. The corresponding symbol **D** will be repeated once & stop the loop.
-   We append the Result value in the 2nd List.
-   Now Remainder is not equal to 0 so we call the function again.

**Step 3**

  

-   Now, number = 49
-   50 > 49 >= 40 ; largest base value is 40.
-   Divide 49/40. Quotient = 1, Remainder = 9. The corresponding symbol **XL** will be repeated once & stop the loop.
-   We append the Result value in the 2nd List.
-   Now Remainder is not equal to 0 so we call the function again.

**Step 4**

  

-   Now, number = 9
-   Number 9 is present in list ls so we directly fetch the value from dictionary dict and set Remainder=0 & stop the loop.
-   Remainder = 0. The corresponding symbol **IX** will be repeated once and now remainder value is 0 so we will not call the function again.

**Step 5**

  

-   Finally, we join the 2nd list values.
-   The output obtained **MMMDXLIX.**


```
// C++ Program to convert decimal number to
// roman numerals
#include <bits/stdc++.h>
using namespace std;

// Function to convert decimal to Roman Numerals
int printRoman(int number)
{
    int num[] = {1,4,5,9,10,40,50,90,100,400,500,900,1000};
    string sym[] = {"I","IV","V","IX","X","XL","L","XC","C","CD","D","CM","M"};
    int i=12;    
    while(number>0)
    {
      int div = number/num[i];
      number = number%num[i];
      while(div--)
      {
        cout<<sym[i];
      }
      i--;
    }
}

//Driver program
int main()
{
    int number = 3549;

    printRoman(number);

    return 0;
}

```


  

**Another Approach 3:**:   
In this approach we have to first observe the problem. The number given in problem statement can be maximum of 4 digits. The idea to solve this problem is: 

  

1.  Divide the given number into digits at different places like one's, two's, hundred's or thousand's.
2.  Starting from the thousand's place print the corresponding roman value. For example, if the digit at thousand's place is 3 then print the roman equivalent of 3000.
3.  Repeat the second step until we reach one's place.

  

**Example**:   
Suppose the input number is 3549. So, starting from thousand's place we will start printing the roman equivalent. In this case we will print in the order as given below:   
**First**: Roman equivalent of 3000   
**Second**: Roman equivalent of 500   
**Third**: Roman equivalent of 40   
**Fourth**: Roman equivalent of 9   
So, the output will be: **MMMDXLIX**

```
// C++ Program for above approach
#include <bits/stdc++.h>
using namespace std;

// Function to calculate roman equivalent
string intToRoman(int num)
{
    // storing roman values of digits from 0-9
    // when placed at different places
    string m[] = { "", "M", "MM", "MMM" };
    string c[] = { "",  "C",  "CC",  "CCC",  "CD",
                   "D", "DC", "DCC", "DCCC", "CM" };
    string x[] = { "",  "X",  "XX",  "XXX",  "XL",
                   "L", "LX", "LXX", "LXXX", "XC" };
    string i[] = { "",  "I",  "II",  "III",  "IV",
                   "V", "VI", "VII", "VIII", "IX" };

    // Converting to roman
    string thousands = m[num / 1000];
    string hundreds = c[(num % 1000) / 100];
    string tens = x[(num % 100) / 10];
    string ones = i[num % 10];

    string ans = thousands + hundreds + tens + ones;

    return ans;
}

// Driver program to test above function
int main()
{
    int number = 3549;
    cout << intToRoman(number);
    return 0;
}
```


**Another Approach 2:**:   
In this approach we consider the main significant digit in the number. Ex: in 1234, main significant digit is 1. Similarly in 345 it is 3.   
In order to extract main significant digit out, we need to maintain a divisor (lets call it div) like 1000 for 1234 (since 1234 / 1000 = 1) and 100 for 345 (345 / 100 = 3).   
Also, lets maintain a dictionary called romanNumeral = {1 : 'I', 5: 'V', 10: 'X', 50: 'L', 100: 'C', 500: 'D', 1000: 'M'}


  

**Following is the algorithm:**   
 

  
  
  

**if main significant digit <= 3**  
 

  

-   romanNumeral[div] * mainSignificantDigit  
     

  

**if main significant digit == 4**  
 

  

-   romanNumeral[div] + romanNumeral[div * 5]  
     

  

**if 5 <= main significant digit <=8**  
 

  

-   romanNumeral[div * 5] + (romanNumeral[div] * ( mainSignificantDigit-5))

  

**if main significant digit ==9**  
 

  

-   romanNumeral[div] + romanNumeral[div*10]

  

**Example**:   
Suppose the input number is 3649.   
 

  
  
  

**Iter 1**  
 

  

-   Initially number = 3649
-   main significant digit is 3. Div = 1000.
-   So, romanNumeral[1000] * 3
-   gives: MMM

  

  
 

  
  
  

**Iter 2**

  

-   now, number = 649
-   main significant digit is 6. Div = 100.
-   So romanNumeral[100*5] + (romanNumeral[div] * ( 6-5))
-   gives: DC

  

  
 

  
  
  

**Iter 3**  
 

  

-   now, number = 49
-   main significant digit is 4. Div = 10.
-   So romanNumeral[10] + romanNumeral[10 * 5]
-   gives: XL

  

  
 

  
  
  

**Iter 4**

  

-   now, number = 9
-   main significant digit is 9. Div = 1.
-   So romanNumeral[1] * romanNumeral[1*10]
-   gives: IX

  

Final result by clubbing all the above: MMMDCXLIX  

  ```
  
 #include <bits/stdc++.h>
#include <unordered_map>

using namespace std;

string integerToRoman(int num) {
  unordered_map<int, char> roman; // move outside
  roman[1] = 'I';
  roman[5] = 'V';
  roman[10] = 'X';
  roman[50] = 'L';
  roman[100] = 'C';
  roman[500] = 'D';
  roman[1000] = 'M';
  roman[5000] = 'G';
  roman[10000] = 'H';
  
  string tmp = to_string(num);
  const int numDigits = tmp.length();
  
  string res = "";
  for(int i=0;i<numDigits;++i) {
    const char src = tmp[i]; // orig
    const int number = (src - '0'); // convert to integer
    const int place = (numDigits-1)-i;
    const int absolute = pow(10, place);
    
    if (number == 9) {
        res.append(1, roman[absolute]);
        res.append(1, roman[(number+1) * absolute]);
    }  else
    if (number >= 5) {
        res.append(1, roman[5*absolute]);
        res.append(number-5, roman[absolute]);
    }  else
    if (number >= 4) {
        res.append(1, roman[absolute]);
        res.append(1, roman[5*absolute]);
    } else {
        res.append(number, roman[absolute]);
    }
  }
  return res;
}

int main() {
  cout << integerToRoman(3549) << endl;
  return 0;
}

// This code is contributed by elviscastillo.
```