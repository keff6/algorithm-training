# checkPermutation

## Description

> Given two strings, write a method to decide if one is a permutation of the other.

## My Solution

<details>
  <summary>Click to expand!</summary>

#### Javascript
```javascript
function checkPermutation(string1, string2){
  // Step 1: if the string length is not the same return false
  if(string1.length !== string2.length){
    return false
  }

  const stringOneCharacters = {}

  // Step 2: create a dictionary with letters on string1
  for (let i = 0; i < string1.length; i++){
    if (stringOneCharacters.hasOwnProperty(string1[i])) {
      stringOneCharacters[string1[i]] += 1
    } else{
      stringOneCharacters[string1[i]] = 1
    }
  }
 
  // Step 3: loop through string2 and decrease the letter amount if is in the dictionary, if not return False
  for (let i = 0; i < string2.length; i++){
    if(!stringOneCharacters.hasOwnProperty(string2[i])) {
      return false
    } else {
      stringOneCharacters[string2[i]] -= 1
    }
  }

  // Step 4: if all values in the dictionary are 0 return true, otherwise return false
  return Object.values(stringOneCharacters).every(val => val === 0)
}
 
// test
console.log(checkPermutation('oneee', 'neee'))
```
#### Python
```python
def checkPermutation(string1, string2):
  # Step 1: if the string length is not the same return false
  if len(string1) != len(string2):
    return False

  stringOneCharacters = {}

  # Step 2: create a dictionary with letters on string1
  for char in string1:
    if char in stringOneCharacters:
      stringOneCharacters[char] += 1
    else:
      stringOneCharacters[char] = 1
  
  # Step 3: loop through string2 and decrease the letter amount if is in the dictionary, if not return False
  for char in string2:
    if char not in stringOneCharacters:
      return False
    else:
      stringOneCharacters[char] -= 1

  # Step 4: if all values in the dictionary are 0 return true, otherwise return false
  for num in stringOneCharacters.values():
    if num != 0:
      return False

  return True

# test
print(checkPermutation('one', 'neO'))
```
 ### Explanation

> The first thing is to check if the length of both strings is equal, if not, we can return false immediately. If they have the same length, we can continue with the creation of a dictionary based on the first string chars and theri number of appearences. After that, we loop through the second string looking for every char in the dictionary, if char exist in the dictionary then decrese the counter, if not, it means the string two is not a permutation of the firts one so we return false.
At last, we check it all the values in the dictionary are 0, if so, return true, else false.
Notice that this algorithm assumes that the string comparison is not case sensitive, but in a real interview it would be better to ask for clarification.

### Time complexity

> O (n)
</details>


## Solution (from the book)

<details>
  <summary>Click to expand!</summary>
  
  Like in many questions, we should confirm some details with our interviewer. We should understand if the
permutation comparison is case sensitive. That is; is God a permutation of dog? Additionally, we should
ask if whitespace is significant. We will assume for this problem that the comparison is case sensitive and
whitespace is significant. So, "god " is different from "dog".
Observe first that strings of different lengths cannot be permutations of each other. There are two easy
ways to solve this problem, both of which use this optimization.

If two strings are permutations, then we know they have the same characters, but in different orders. Therefore,
sorting the strings will put the characters from two permutations in the same order. We just need to
compare the sorted versions of the strings.
```
String sort(Strings) {
	char[] content = s.toCharArrayO;
	java.util.Arrays.sort(content);
	return new String(content);
}

boolean permutation(String s. String t) {
	if (s.lengthQ != t. lengthQ) {
		return false
	}

	return sort(s) , equals(sort(t));
}
```

Though this algorithm is not as optimal in some senses, it may be preferable in one sense: it's clean, simple
and easy to understand. In a practical sense, this may very well be a superior way to implement the problem.
However, if efficiency is very important, we can implement it a different way.

```
boolean isUniqueChars(String stn) {
  int checker = 0;
  for (int i = 0; i < Str.length; i++) {
   int val« s t r.c h a r A t(i) - raJ;
   if ((checker & (1 << v a l)) > 0) {
    return false;
   }
   checker |= (1 << v a l);

  )
```
We can also use the definition of a permutation—two words with the same character counts—to implement
this algorithm. We simply iterate through this code, counting how many times each character appears.
Then, afterwards, we compare the two arrays.

```
boolean permutation(String s, String t) {
	if (s.length() 1= t . l e n g t h Q ) {
	return false;
}

int[] letters = new int[128]; // Assumption

	char[] s_array = s.toCharArrayQ;
	for (char c : s^array) { // count number of each char in s,
		lettersfc]++;
	}

	for (int i = 0; i < t.lengthQ ; i++) {
		int c = (int)t.charAt(i);
		letters[c]--;
		if (lettersfc] < 0) {
			return false;
		}
	}
	return true;
}
```
Note the assumption on line 6, In your interview, you should always check with your interviewer about the
size of the character set. We assumed that the character set was ASCII.

</details>

