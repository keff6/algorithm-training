# urlify

## Description

> Write a method to replace all spaces in a string with '%20'. You may assume that the string
has sufficient space at the end to hold the additional characters, and that you are given the "true"
length of the string.

## My Solution

<details>
  <summary>Click to expand!</summary>

#### Javascript
```javascript
function urlify(str) {
  const arrFromStr = str.trim().split('')
  for(let i = 0; i < arrFromStr.length; i++) {
    if(arrFromStr[i] === ' ') {
      arrFromStr[i] = '%20'
    }
  }
  return arrFromStr.join('')
}

console.log(urlify('Mr John Smith  ')); // returns Mr%20John%20Smith
```
#### Python
```python
def urlify(str):
  arrayFromStr = list(str.strip())
  for i,char in enumerate(arrayFromStr):
    if char == ' ':
      arrayFromStr[i] = '%20'
  
  return ''.join(arrayFromStr)


print(urlify('Mr John Smith  ')); # returns Mr%20John%20Smith
```
 ### Explanation

> To solve this algorithm first step is to convert the string into an array. Here I make the assumption that spaces at the begining and at the end of the string have to be trimmed. After that I loop through the array looking for the space char ' ' and replacing it with '%20'.
At the end I use the join function (javascript and python) to joint the array into a string again and return it.

### Time complexity

> O (n)
</details>


## Solution (from the book)

<details>
  <summary>Click to expand!</summary>
  
  A common approach in string manipulation problems is to edit the string starting from the end and working
backwards. This is useful because we have an extra buffer at the end, which allows us to change characters
without worrying about what we're overwriting.

We will use this approach in this problem. The algorithm employs a two-scan approach. In the first scan, we
count the number of spaces. By tripling this number, we can compute how many extra characters we will
have in the final string. In the second pass, which Is done in reverse order, we actually edit the string. When
we see a space, we replace it with %20. If there is no space, then we copy the original character.
```
void replaceSpaces(char[] s t r , int trueLength) {
	int spaceCount = 0, index, i = 0;
	for ( 1 = 0 ; i < trueLength; i++) {
		if (str[i] == ' ') {
			spaceCount++;
		}
 	}
 	index = trueLength + spaceCount * 2;
	if (trueLength < s t r . l e n g t h ) str[trueLength] = * \ 0 ' ; // End array
	for (i = trueLength - 1; i >= 0; i - - ) {
		if ( s t r [ i ] == ' ') {
			str[index - 1] = ' 0 ' ;
			strfindex - 2] = ' 2 ' ;
			str[index - 3] = '%';
			index = index - 3;
		} else {
			str[index - 1] = str[i];
			index--;
		}
	}
}
```

We have implemented this problem using character arrays, because Java strings are immutable, if we used
strings directly, the function would have to return a new copy of the string, but it woufd allow us to implement
this in just one pass.


</details>

