#### I. JavaScript functions - Exercises, Practice, Solution
---

**1. Write a JavaScript function that reverse a number.**
Sample Data and output: 
Example x = 32243; 
Expected Output: 34223
Assume n = 1000. 
Convert a number to a string :

**Code :** -> ```n = n + "";```

**Note :** There are different ways to convert number to string : Có nhiều cách khác nhau để chuyển đổi số thành chuỗi.

**String literal** -> ```str = "" + num + "";```

**String constructor** -> ```str = String(num);```

**toString** -> ```str = num.toString();```

**String Literal simple** -> str = "" + num;

The ```split()``` method is used to split a String object into an array of strings by separating the string into substrings.

**Code :** console.log('1000'.split(""));

**Output :** ```["1", "0", "0", "0"]```

The ```reverse()``` method is used to reverse an array in place. The first array element becomes the last and the last becomes the first.

**Code :** ```console.log(["1", "0", "0", "0"].reverse());```

**Output :** ```["0", "0", "0", "1"]```

The ```join()``` method is used to join all elements of an array into a string.

**Code :** ```console.log(["1", "0", "0", "0"].reverse().join(""));```

**Output :** ```"0001"```

>JavaScript Code:
```javascript
function reverse_a_number(n) {
  n = n + "";
  return n.split("").reverse().join("");
}
console.log(reverse_a_number(32243));
```

>Result:
```javascript
34223
```

**2. Write a JavaScript function that checks whether a passed string is palindrome or not?**

- Viết một hàm JavaScript để kiểm tra xem chuỗi đã qua có phải là palindrome hay không? 
- Một chuỗi được gọi là Palindrome nếu sau khi đảo ngược các ký tự của nó, ta nhận được chuỗi ban đầu. Ví dụ: chuỗi "MADAM" là Palindrome.
- The ```toLowerCase()``` method converts a string to lowercase letters.
- The ```replace()``` method searches a string for a specified value, or a regular expression, and returns a new string where the specified values are replaced.(Phương thức ```replace()``` tìm kiếm một chuỗi cho một giá trị được chỉ định, hoặc một biểu thức chính quy, và trả về một chuỗi mới mà các giá trị được chỉ định được thay thế.)
- ```array.slice(start, end)```: The ```slice()``` method returns the selected elements in an array, as a new array object. Phương thức slice () trả về các phần tử đã chọn trong một mảng, như một đối tượng mảng mới.
- Use negative numbers to select from the end of an array(Sử dụng số âm để chọn từ cuối mảng)
- **Note:** A palindrome is word, phrase, or sequence that reads the same backward as forward, e.g., madam or nurses run. (Lưu ý: Một palindrome là từ, cụm từ hoặc trình tự đọc ngược lại tương tự như chuyển tiếp, ví dụ: madam hoặc các y tá chạy.)
- Thay đổi chuỗi thành chữ thường và loại bỏ tất cả các ký tự không phải là chữ và số
- Kiểm tra xem chuỗi có rỗng hay không
- Kiểm tra xem chiều dài của chuỗi có bằng nhau hay không
- Nếu chiều dài của chuỗi là 1 sau đó nó sẽ trở thành một palindrome
- Nếu chiều dài của chuỗi là lẻ bỏ qua nhân vật trung gian
- Lặp qua để kiểm tra ký tự đầu tiên cho nhân vật cuối cùng và sau đó di chuyển tiếp theo

// So sánh các ký tự và thả chúng nếu chúng không khớp
>JavaScript Code:
```javascript
// Write a JavaScript function that checks whether a passed string is palindrome or not? 
function check_Palindrome(str_entry) {
  // Change the string into lower case and remove  all non-alphanumeric characters
  var cstr = str_entry.toLowerCase().replace(/[^a-zA-Z0-9]+/g, '');
  var ccount = 0;
  // Check whether the string is empty or not
  if (cstr === "") {
    alert("Nothing found!");
    return false;
  }
  // Check if the length of the string is even or odd 
  if ((cstr.length) % 2 === 0) {
    ccount = (cstr.length) / 2;
  } else {
    // If the length of the string is 1 then it becomes a palindrome
    if (cstr.length === 1) {
      alert("Entry is a palindrome.");
      return true;
    } else {
      // If the length of the string is odd ignore middle character
      ccount = (cstr.length - 1) / 2;
    }
  }
  // Loop through to check the first character to the last character and then move next
  for (var x = 0; x < ccount; x++) {
    // Compare characters and drop them if they do not match 
    if (cstr[x] != cstr.slice(-1 - x)[0]) {
      alert("Entry is not a palindrome.");
      return false;
    }
  }
  alert("The entry is a palindrome.");
  return true;
}
check_Palindrome('madam');
check_Palindrome('nurses run');
check_Palindrome('fox');
```

**3. Write a JavaScript function that generates all combinations of a string.**
- Viết một hàm JavaScript tạo ra tất cả các kết hợp của một chuỗi.
- Example string: 'dog' 
- Expected Output: d,o,do,g,dg,og,dog
- The ```pow(x, y)``` method returns the value of x to the power of y (x mũ y). 
- ```Math.pow(2, 3);``` ==> ```8```; ```Math.pow(4, 3);``` ==> ```64```
>JavaScript Code:
```javascript
//Write a JavaScript function that generates all combinations of a string.
function substrings(str1) {
  var array1 = [];
  for (var x = 0, y = 1; x < str1.length; x++, y++) {
    array1[x] = str1.substring(x, y);
  }
  var combi = [];
  var temp = "";
  var slent = Math.pow(2, array1.length);

  for (var i = 0; i < slent; i++) {
    temp = "";
    for (var j = 0; j < array1.length; j++) {
      if ((i & Math.pow(2, j))) {
        temp += array1[j];
      }
    }
    if (temp !== "") {
      combi.push(temp);
    }
  }
  console.log(combi.join("\n"));
}

substrings("dog");
```

>Result:
```javascript

```

**4. Write a JavaScript function that returns a passed string with letters in alphabetical order.**
Example string: 'webmaster' 
Expected Output: 'abeemrstw'
- Viết một hàm JavaScript trả về một chuỗi được truyền với các chữ cái theo thứ tự chữ cái. 
- The ```split()``` method is used to split a String object into an array of strings by separating the string into substrings.
Code : console.log('32243'.split(""));
Output : ["3", "2", "2", "4", "3"]

- The ```sort()``` method is used to sort the elements of an array in place and returns the array.
Code : console.log(["3", "2", "2", "4", "3"].sort());
Output : ["2", "2", "3", "3", "4"]

- The ```join()``` method is used to join all elements of an array into a string.
Code : console.log(["2", "2", "3", "3", "4"].join(""));
Output : "22334"

>JavaScript Code:
```javascript
function alphabet_order(str)
  {
return str.split('').sort().join('');
  }
console.log(alphabet_order("webmaster"));
```

>Result:
```javascript
abeemrstw
```

**5. Write a JavaScript function that accepts a string as a parameter and converts the first letter of each word of the string in upper case.**
- Viết một hàm JavaScript chấp nhận một chuỗi như một tham số và chuyển đổi chữ cái đầu tiên của mỗi từ của chuỗi thành chữ hoa.
- Example string: 'the quick brown fox' 
- Expected Output: 'The Quick Brown Fox '
- Assume str = "the quick brown fox";

- The ```split()``` method is used to split a String object into an array of strings by separating the string into substrings.
- console.log(str.split(' ')); 
- Output : ```["the", "quick", "brown", "fox"]```
- First substrings -> "the"
- Code to convert first character of the above sting to upper case-> ```array1[x].charAt(0).toUpperCase()```
- ```console.log(array1[x].charAt(0).toUpperCase()); [here x=0] ```
- Output : "T"
- Rest part of the string "the" -> ```array1[x].slice(1)```
- ```console.log(array1[0].slice(1));```
- Output : "he"
- Final string :
- ```console.log(array1[0].charAt(0).toUpperCase()+array1[0].slice(1));```
- Output : "The"
- Now insert the above string into another array :
- ```newarray1.push(array1[x].charAt(0).toUpperCase()+array1[x].slice(1));```
- Used functions :
- The ```charAt()``` method is used to get the specified character from a string.
- Syntax : str.charAt(index). Where index represents an integer between 0 and 1-less-than the length of the string.
- The toUpperCase() method is used to convert the string value to uppercase.
- The ```slice()``` method returns a shallow copy of a portion of an array into a new array object.
- The ```push()``` method is used to add one or more elements to the end of an array and returns the new length of the array.
- After completing the for loop return the final string :
- return newarray1.join(' ');
- The ```join()``` method joins all elements of an array into a string.

>JavaScript Code 1:
```javascript
function uppercase(str){
  return str.charAt(0).toUpperCase() + str.slice(1);
}
console.log(uppercase("abcde"));
```
>Result:
```javascript
Abcde
```

>JavaScript Code 2:
function uppercase(str) {
  var array1 = str.split(' ');
  var newarray1 = [];
  for (var x = 0; x < array1.length; x++) {
    newarray1.push(array1[x].charAt(0).toUpperCase() + array1[x].slice(1));
  }
  return newarray1.join(' ');
}
console.log(uppercase("the quick brown fox"));
```

>Result:
```javascript
The Quick Brown Fox
```

**6. Write a JavaScript function that accepts a string as a parameter and find the longest word within the string.**
- Write a JavaScript function that accepts a string as a parameter and find the longest word within the string.
- Viết một hàm JavaScript chấp nhận một chuỗi như một tham số và tìm thấy từ dài nhất trong chuỗi.
- Sample Data and output: 
- Example string: 'Web Development Tutorial' 
- Expected Output: 'Development'

**Explanation:**
- Assume str = '@Web Development #Tutorial';
- The ```match()``` method is used to retrieve the matches when matching a string against a regular expression.
- The match() method searches a string for a match against a regular expression, and returns the matches, as an Array object.(Phương thức match () tìm kiếm một chuỗi cho một đối sánh với một biểu thức chính quy và trả về các đối sánh, như một đối tượng Array.)
- Therefore ```str.match(/\w[a-z]{0,}/gi)``` will ```return ["Web", "Development", "Tutorial"]```.
- For loop checks the length of the array element and compare with previous one and finally return the longest string.
- The length property represents an unsigned, 32-bit integer that is always numerically greater than the highest index in the array.
```Syntax -> arr.length```

>JavaScript Code:
```javascript
function find_longest_word(str) {
  var array1 = str.match(/\w[a-z]{0,}/gi);
  var result = array1[0];

  for (var x = 1; x < array1.length; x++) {
    if (result.length < array1[x].length) {
        result = array1[x];
    }
  }
  return result;
}
console.log(find_longest_word('Web Development Tutorial'));
```

>Result:
```javascript
Development
```

**7. Write a JavaScript function that accepts a string as a parameter and counts the number of vowels within the string.**
**Note:** As the letter 'y' can be regarded as both a vowel and a consonant, we do not count 'y' as vowel here.
**Sample Data and output:** 
**Example string:** 'The quick brown fox' 
**Expected Output:** 5
**Explanation:** 
- The ```indexOf()``` method returns the index within the calling String object of the first occurrence of the specified value, starting the search at fromIndex. Returns -1 if the value is not found.
Syntax -> ```str.indexOf(searchValue[, fromIndex])```
**Parameters :**
- ```searchValue``` : A string representing the value to search for. 
- ```fromIndex(Optional)```-> The index at which to start the searching forwards in the string. It can be any integer.
- The character(s) of the string will be counted as vowel if the condition (```vowel_list.indexOf(str1[x]) !== -1```) matched.

>JavaScript Code:
```javascript
function vowel_count(str1) {
  var vowel_list = 'aeiouAEIOU';
  var vcount = 0;

  for (var x = 0; x < str1.length; x++) {
    if (vowel_list.indexOf(str1[x]) !== -1) {
      vcount += 1;
    }

  }
  return vcount;
}
console.log(vowel_count("The quick brown fox"));
```

>Result:
```javascript
5
```

**8. Write a JavaScript function that accepts a number as a parameter and check the number is prime or not.**

- Viết một hàm JavaScript chấp nhận một số như một tham số và kiểm tra số đó là số nguyên tố hay không.
- Số nguyên tố là số tự nhiên chỉ có hai ước số dương phân biệt là 1 và chính nó. Các số có nhiều hơn 2 ước số dương được gọi là hợp số.
- Do số 1 chỉ có một (1) ước số dương là chính nó, nên số 1 không phải là số nguyên tố và cũng không phải là hợp số.
- Các số nguyên tố từ 2 đến 100:
```2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31, 37, 41, 43, 47, 53, 59, 61, 67, 71, 73, 79, 83, 89, 97```
- Số 2 là số nguyên tố nhỏ nhất, và cũng là số nguyên tố chẵn duy nhất. 

>JavaScript Code:
```javascript
function test_prime(n) {

  if (n === 1) {
    return false;
  } else if (n === 2) {
    return true;
  } else {
    for (var x = 2; x < n; x++) {
      if (n % x === 0) {
        return false;
      }
    }
    return true;
  }
}

console.log(test_prime(37));
```

>Result:
```javascript
true
```

**9. Write a JavaScript function which accepts an argument and returns the type.**
- Viết một hàm JavaScript chấp nhận đối số và trả về kiểu.
- **Note** : There are six possible values that typeof returns: object, boolean, function, number, string, and undefined.

>JavaScript Code:
```javascript
function detect_data_type(value) {
  var dtypes = [Function, RegExp, Number, String, Boolean, Object],
    x, len;

  if (typeof value === "object" || typeof value === "function") {
    for (x = 0, len = dtypes.length; x < len; x++) {
      if (value instanceof dtypes[x]) {
        return dtypes[x];
      }
    }
  }

  return typeof value;
}
console.log(detect_data_type(12));
console.log(detect_data_type('w3resource'));
console.log(detect_data_type(false));
```

>Result:

```javascript
number
string
boolean
```

**10. Write a JavaScript function which returns the n rows by n columns identity matrix**

>JavaScript Code:
```javascript
function matrix(n) {
  var i;
  var j;

  for (i = 0; i < n; i++) {
    for (j = 0; j < n; j++) {
      if (i === j) {
        console.log(' 1 ');
      } else {
        console.log(' 0 ');
      }
    }
    console.log('----------');
  }
}
matrix(4);
```

>Result:
```javascript
1 
 0 
 0 
 0 
----------
 0 
 1 
 0 
 0 
----------
 0 
 0 
 1 
 0 
----------
 0 
 0 
 0 
 1 
----------
```

**11. Write a JavaScript function which will take an array of numbers stored and find the second lowest and second greatest numbers, respectively.**
- Viết một hàm JavaScript sẽ lấy một mảng số được lưu trữ và tìm số thứ hai thấp nhất thứ hai và thứ hai lớn nhất, tương ứng.
- The ```sort()``` method sorts the items of an array: Phương thức ```sort()``` loại các item của một mảng.
- The ```sort``` order can be either alphabetic or numeric, and either ascending (up) or descending (down): Thứ tự sắp xếp có thể là chữ cái hoặc chữ số, hoặc tăng dần (lên) hoặc giảm dần (xuống).
- By default, the ```sort()``` method sorts the values as strings in alphabetical and ascending order: Theo mặc định, phương thức sort () sắp xếp các giá trị dưới dạng các chuỗi theo thứ tự chữ cái và thứ tự tăng dần.

>JavaScript Code:
- Sort the numbers in the array in ascending order(Sắp xếp các số trong mảng theo thứ tự tăng dần)
- The first item in the array (```points[0]```) is now the lowest value(Mục đầu tiên trong mảng (`` `points [0]` ``) bây giờ là giá trị thấp nhất)
```javascript
var points = [40, 100, 1, 5, 25, 10];
document.getElementById("demo").innerHTML = points;
function myFunction() {
  points.sort(function(a, b){return a-b});
  document.getElementById("demo").innerHTML = points[0];
}
```

>JavaScript Code:
- Sort the numbers in the array in descending order(Sắp xếp các số trong mảng theo thứ tự giảm dần)
- The first item in the array (```points[0]```) is now the highest value(Mục đầu tiên trong mảng (```points[0]```) bây giờ là giá trị cao nhất)
```javascript
var points = [40, 100, 1, 5, 25, 10];
document.getElementById("demo").innerHTML = points;
function myFunction() {
  points.sort(function(a, b){return b-a});
  document.getElementById("demo").innerHTML = points[0];
}
```

>JavaScript Code:
```javascript
function Second_Greatest_Lowest(arr_num) {
  arr_num.sort(function(x, y) {
    return x - y;
  });
  var uniqa = [arr_num[0]];
  var result = [];

  for (var j = 1; j < arr_num.length; j++) {
    if (arr_num[j - 1] !== arr_num[j]) {
      uniqa.push(arr_num[j]);
    }
  }
  result.push(uniqa[1], uniqa[uniqa.length - 2]);
  return result.join(',');
}

console.log(Second_Greatest_Lowest([1, 2, 3, 4, 5]));
```
>Result:
```javascript
2, 4
```

**12. Write a JavaScript function which says whether a number is perfect.**
**Note** : According to Wikipedia : In number theory, a perfect number is a positive integer that is equal to the sum of its proper positive divisors, that is, the sum of its positive divisors excluding the number itself (also known as its aliquot sum). Equivalently, a perfect number is a number that is half the sum of all of its positive divisors (including itself).
- Theo Wikipedia: Trong lý thuyết số, một con số hoàn hảo là một số nguyên dương bằng tổng các ước số dương của nó, đó là, tổng số ước số dương của nó không bao gồm con số chính nó (còn gọi là tổng số của nó). Tương đương, một số hoàn hảo là một số là một nửa tổng của tất cả các ước số tích cực của nó (bao gồm cả chính nó).
**Example** : The first perfect number is 6, because 1, 2, and 3 are its proper positive divisors, and 1 + 2 + 3 = 6. Equivalently, the number 6 is equal to half the sum of all its positive divisors: ( 1 + 2 + 3 + 6 ) / 2 = 6. The next perfect number is 28 = 1 + 2 + 4 + 7 + 14. This is followed by the perfect numbers 496 and 8128.
- Số hoàn hảo đầu tiên là 6, bởi vì 1, 2, và 3 là các ước số tích cực thích hợp của nó, và 1 + 2 + 3 = 6. Tương đương, số 6 bằng một nửa tổng của tất cả các ước số dương của nó: (1 + 2 + 3 + 6) / 2 = 6. Số hoàn hảo tiếp theo là 28 = 1 + 2 + 4 + 7 + 14. Tiếp theo là số hoàn hảo 496 và 8128.

>JavaScript Code:
```javascript
function is_perfect(number) {
  var temp = 0;
  for (var i = 1; i <= number / 2; i++) {
    if (number % i === 0) {
      temp += i;
    }
  }

  if (temp === number && temp !== 0) {
    console.log("It is a perfect number.");
  } else {
    console.log("It is not a perfect number.");
  }
}
is_perfect(28);
```

>Result:
```javascript
It is a perfect number.
```

**13. Write a JavaScript function to compute the factors of a positive integer.**
- Viết một hàm JavaScript để tính toán các yếu tố của một số nguyên dương.

>JavaScript Code:
```javascript
function factors(n) {
  var num_factors = [],i;
  for (i = 1; i <= Math.floor(Math.sqrt(n)); i += 1)
    if (n % i === 0) {
      num_factors.push(i);
      if (n / i !== i)
        num_factors.push(n / i);
    }
  num_factors.sort(function(x, y) {
    return x - y;
  }); // numeric sort
  return num_factors;
}
console.log(factors(15)); // [1,3,5,15] 
console.log(factors(16)); // [1,2,4,8,16] 
console.log(factors(17)); // [1,17]
```

>Result:
```javascript
[1,3,5,15]
[1,2,4,8,16] 
[1,17]
```

**14. Write a JavaScript function to compute the value of bn where n is the exponent and b is the bases. Accept b and n from the user and display the result.**
- Viết một hàm JavaScript để tính giá trị của b mũ n trong đó n là số mũ và b là các căn cứ. Chấp nhận b và n từ người dùng và hiển thị kết quả.
- Khi chạy vong lặp nó luôn luôn trả vể giá trị cuối cùng lớn nhất.
  + ban đầu i = 1, ans = 1 thì ==> ans = 3 * 1 = 3. 
  + Tiếp đến i = 2 thì ans = 3 ==> ans = 3 * 3 = 9.
  + Tiếp đến i = 3 thì ans = 9 ==> ans = 3 * 9 = 27.
>JavaScript Code:
```javascript
function exp(b, n) {
  var ans = 1;
  for (var i = 1; i <= n; i++) {
    ans = b * ans;
  }
  return ans;
}
console.log(exp(3, 3));
```

>ES6 Version:

```

>Result:
```javascript

```

**15. Write a JavaScript function to extract unique characters from a string.**
- Viết một hàm JavaScript để trích các ký tự độc nhất từ một chuỗi.
- **Example string :** "thequickbrownfoxjumpsoverthelazydog"
- **Expected Output :** "thequickbrownfxjmpsvlazydg"

>JavaScript Code:
```javascript
function unique_char(str1) {
  var str = str1;
  var uniql = "";
  for (var x = 0; x < str.length; x++) {

    if (uniql.indexOf(str.charAt(x)) == -1) {
      uniql += str[x];

    }
  }
  return uniql;
}
console.log(unique_char("thequickbrownfoxjumpsoverthelazydog"));
```
>Result:
```javascript
thequickbrownfxjmpsvlazydg
```

**16. Write a JavaScript function to get the number of occurrences of each letter in specified string**
- Viết một hàm JavaScript để nhận số lần xuất hiện của mỗi ký tự trong chuỗi được chỉ định.
>JavaScript Code:
```javascript
function Char_Counts(str1) {
  var uchars = {};
  str1.replace(/\S/g, function(l) { uchars[l] = (isNaN(uchars[l]) ? 1 : uchars[l] + 1); });
  return uchars;
}
console.log(Char_Counts("The quick brown fox jumps over the lazy dog"));
```

>Result:
```javascript
{"T":1,"h":2,"e":3,"q":1,"u":2,"i":1,"c":1,"k":1,"b":1,"r":2,"o":4,"w":1,"n":1,"f":1,"x":1,"j":1,"m":1,"p":1,"s":1,"v":1,"t":1,"l":1,"a":1,"z":1,"y":1,"d":1,"g":1}
```

**17. Write a JavaScript function that generates a string id (specified length) of random characters.**
- Viết một hàm JavaScript tạo ra một id chuỗi (chiều dài xác định) của các ký tự ngẫu nhiên.
- Sample character list : "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789"

>JavaScript Code:
```javascript
function makeid(l) {
  var text = "";
  var char_list = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789";
  for (var i = 0; i < l; i++) {
    text += char_list.charAt(Math.floor(Math.random() * char_list.length));
  }
  return text;
}
console.log(makeid(8));
```

>Result:
```javascript
dppxWjgO
```

**18. Write a JavaScript function to get all possible subset with a fixed length (for example 2) combinations in an array.**
- Viết một hàm JavaScript để nhận được tất cả các tập hợp con có thể có kết hợp chiều dài cố định (ví dụ 2) trong một mảng.
- Sample array : [1, 2, 3] and subset length is 2 
- Expected output : [[2, 1], [3, 1], [3, 2], [3, 2, 1]]
>JavaScript Code:
```javascript
function subset(arra, arra_size) {
  var result_set = [],
    result;


  for (var x = 0; x < Math.pow(2, arra.length); x++) {
    result = [];
    i = arra.length - 1;
    do {
      if ((x & (1 << i)) !== 0) {
        result.push(arra[i]);
      }
    } while (i--);

    if (result.length >= arra_size) {
      result_set.push(result);
    }
  }

  return result_set;
}

console.log(subset([1, 2, 3], 2));
```

>Result:
```javascript
[[2,1],[3,1],[3,2],[3,2,1]]
```

**19. Write a JavaScript function that accepts two arguments, a string and a letter and the function will count the number of occurrences of the specified letter within the string.**
- Viết một hàm JavaScript chấp nhận hai đối số, một chuỗi và một chữ cái và chức năng sẽ đếm số lần xuất hiện của ký tự được chỉ định bên trong chuỗi.
- Sample arguments: 'w3resource.com', 'o' 
- Expected output: 2
>JavaScript Code:
```javascript
function char_count(str, letter) {
  var letter_Count = 0;
  for (var position = 0; position < str.length; position++) {
    if (str.charAt(position) == letter) {
      letter_Count += 1;
    }
  }
  return letter_Count;
}

console.log(char_count('w3resource.com', 'o'));
```

>Result:
```javascript
2
```

**20. Write a JavaScript function to find the first not repeated character.**
- Viết một hàm JavaScript để tìm ký tự đầu tiên không lặp lại.
- Sample arguments : 'abacddbec' 
Expected output : 'e' 

>JavaScript Code:
```javascript
function find_FirstNotRepeatedChar(str) {
  var arra1 = str.split('');
  var result = '';
  var ctr = 0;

  for (var x = 0; x < arra1.length; x++) {
    ctr = 0;

    for (var y = 0; y < arra1.length; y++) {
      if (arra1[x] === arra1[y]) {
        ctr += 1;
      }
    }

    if (ctr < 2) {
      result = arra1[x];
      break;
    }
  }
  return result;
}
console.log(find_FirstNotRepeatedChar('abacddbec'));
```

>Result:
```javascript
e
```

**21. Write a JavaScript function that accept a list of country names as input and returns the longest country name as output**
- Viết một hàm JavaScript chấp nhận một danh sách các tên quốc gia làm đầu vào và trả về tên nước dài nhất là đầu ra
- The reduce() method reduces the array to a single value.(Phương thức reduce () làm giảm mảng thành một giá trị.)
- The reduce() method executes a provided function for each value of the array (from left-to-right).(Phương thức reduction () thực hiện một hàm được cung cấp cho mỗi giá trị của mảng (từ trái sang phải).)
- The return value of the function is stored in an accumulator (result/total).(Giá trị trả lại của hàm được lưu trữ trong một accumulator (kết quả / tổng số).)

>JavaScript Code:
```javascript
function Longest_Country_Name(country_name) {
  return country_name.reduce(function(lname, country) {
      return lname.length > country.length ? lname : country;
    },
    "");
}
console.log(Longest_Country_Name(["Australia", "Germany", "United States of America"]));
```

>Result:
```javascript
"United States of America"
```

**22. Write a JavaScript function to find longest substring in a given a string without repeating characters.**
- Viết một hàm JavaScript để tìm chuỗi con dài nhất trong một chuỗi cho trước mà không lặp lại các ký tự.

>JavaScript Code:
```javascript
function longest_substring_without_repeating_characters(input) {
  var chars = input.split('');
  var curr_char;
  var str = "";
  var longest_string = "";
  var hash = {};
  for (var i = 0; i < chars.length; i++) {
    curr_char = chars[i];
    if (!hash[chars[i]]) {
      str += curr_char;
      hash[chars[i]] = { index: i };
    } else {
      if (longest_string.length <= str.length) {
        longest_string = str;
      }
      var prev_dupeIndex = hash[curr_char].index;
      var str_FromPrevDupe = input.substring(prev_dupeIndex + 1, i);
      str = str_FromPrevDupe + curr_char;
      hash = {};
      for (var j = prev_dupeIndex + 1; j <= i; j++) {
        hash[input.charAt(j)] = { index: j };
      }
    }
  }
  return longest_string.length > str.length ? longest_string : str;
}
console.log(longest_substring_without_repeating_characters("google.com"));

console.log(longest_substring_without_repeating_characters("example.com"));
```

>Result:
```javascript
gle.com
xample.co
```

**23. Write a JavaScript program to pass a 'JavaScript function' as parameter.**
- Viết một chương trình JavaScript để truyền một 'chức năng JavaScript' làm tham số.

>JavaScript Code:
```javascript
function addStudent(id, refreshCallback) {
  refreshCallback();
}
function refreshStudentList() {
  console.log('Hello');
}
addStudent(1, refreshStudentList);
```

>Result:
```javascript
Hello
```

**24. Write a JavaScript function to get the function name.**
- Viết một hàm JavaScript để có được tên hàm.

>JavaScript Code:
```javascript
function abc() {
  console.log(arguments.callee.name);
}

abc();
```

>Result:
```javascript
abc
```
