# palindromePermutation

## Description

>Given a string, write a function to check if it is a permutation of
a palindrome. A palindrome is a word or phrase that is the same forwards and backwards, A
permutation is a rearrangement of letters. The palindrome does not need to be limited to just
dictionary words.

## My Solution

<details>
  <summary>Click to expand!</summary>

#### Javascript
```javascript
function palindromePermutation(inputString) {
  const letterCount = {}
  const lowercaseStr = inputString.toLowerCase()
  let oddCount = 0
 
  for(let i = 0; i < lowercaseStr.length; i++) {
    if(lowercaseStr[i] === ' ') continue
    if(letterCount.hasOwnProperty(lowercaseStr[i])) {
      delete letterCount[lowercaseStr[i]]
      oddCount--
    } else {
      letterCount[lowercaseStr[i]] = 1
      oddCount++
    }
  }
 
  return oddCount > 1 ? false : true
}

// console.log(palindromeRearranging('anona'));
console.log(palindromePermutation('Tacoatc'));
```
#### Python
```python
def palindromePermutation(inputString):
  letterCount = {}
  lowercaseStr = inputString.lower()
  oddCount = 0
  
  for char in lowercaseStr:
    if char == ' ':
      continue

    if char in letterCount:
      del letterCount[char]
      oddCount -= 1
    else:
      letterCount[char] = 1
      oddCount += 1

  return False if oddCount > 1  else True


print(palindromePermutation('aabb'))
```
 ### Explanation

> For this algorithm, we have to ask the interviewer regarding the case sensitivity
and the empty spaces. In this case, I assume that the comparison is going to be
case insensitive, so I turn to lowercase the string first.
I created a dictionary / hashtable and a odd numbers count variable.
Lopping through the string we are going to look for the current character, if it exists,
we delete it, if not we assign a 1 to it( this can be done counting each letter
and checking if is even at the end too). At the same time we set the variable
oddCount increasing it or decreasing it, because at the end, there can't
be more than one character that appear only once.
We check if there is only one odd character or none, if not, then the string
is not a palindrome rearranged, otherwise it is and we return true.

### Time complexity

> O (n)
</details>


## Solution (from the book)

<details>
  <summary>Click to expand!</summary>
  
This is a question where it helps to figure out what it means for a string to be a permutation of a palindrome.
This is like asking what the "defining features" of such a string would be.
A palindrome is a string that is the same forwards and backwards. Therefore, to decide if a string is a permutation
of a palindrome, we need to know if it can be written such that it's the same forwards and backwards.
What does it take to be able to write a set of characters the same way forwards and backwards? We need to
have an even number of almost all characters, so that half can be on one side and half can be on the other
side. At most one character (the middle character) can have an odd count.
For example, we know t a c t coapapa is a permutation of a palindrome because it has two Ts,four As, two Cs, two Ps, and one 0. That 0 would be the center of all possible palindromes.

To be more precise, strings with even length (after removing ail non-letter characters) must have
all even counts of characters. Strings of an odd length must have exactly one character with
an odd count. Of course, an "even" string can't have an odd number of exactly one character,
otherwise it wouldn't be an even-length string (an odd number + many even numbers = an odd
number). Likewise, a string with odd length can't have all characters with even counts (sum of
evens is even). It's therefore sufficient to say that, to be a permutation of a palindrome, a string
can have no more than one character that is odd. This will cover both the odd and the even cases.

</details>

