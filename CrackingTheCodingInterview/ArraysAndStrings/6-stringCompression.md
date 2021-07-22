# String compression

## Description

> Implement a method to perform basic string compression using the counts of repeated characters. For example, the string aabcccccaaa would become a2blc5a3. If the "compressed" string would not become smaller than the original string, your method should return
the original string. You can assume the string has only uppercase and lowercase letters (a - z).

## My Solution

<details>
  <summary>Click to expand!</summary>

#### Javascript
```javascript
function compressString(str) {
  const len = str.length;
  if (len <= 1) return str
 
  let currentChar = str[0]
  let currentCount = 1
  let result = '';
 
  for(let i = 1; i < len; i++) {
    if(currentChar === str[i]) {
      currentCount++
    } else {
      result += currentChar + currentCount.toString()
      currentChar = str[i]
      currentCount = 1
    }
  }
  result += currentChar + currentCount.toString()
 
  return result.length < len ? result : str
}

const strt ='aabcccccaaa'

console.log(compressString(strt))
```
#### Python
```python
def compressString(strn):
  leng = len(strn)
  if leng <= 1: return strn
 
  compareChar = strn[0]
  count = 1
  result = ''
 
  for char in strn:
    if compareChar == char:
      count += 1
    else:
      result += compareChar + str(count)
      compareChar = char
      count = 1

  result += compareChar + str(count)
 
  return result if len(result) < leng else strn

print(compressString('a'))
```
 ### Explanation

> The idea is to take the first character of the string and start comparing it with all the n elements on the array, with a count of times the charactrers are equal. Once the 2 chars compared are not equal, we add the char and the count to the string result. 

### Time complexity

> O (n)
</details>


## Solution or tips (from the book)

<details>
  <summary>Click to expand!</summary>
  
  On the solutions from the book, an important caveat is that stringbuilder is better that use += string concatenation. However that function does not apply for every language and in case of javascript, for example, in the past using built in functions like concat or join was suggested, however, nowadays the browsers treat += with high efficiency.
</details>

