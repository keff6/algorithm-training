# isUnique

## Description

>Implement an algorithm to determine if a string has all unique characters. What if you
cannot use additional data structures?

## My Solution

<details>
  <summary>Click to expand!</summary>

#### Javascript
```javascript
function isUnique(string) {
  const dictionary = {}
  
  for(let i = 0; i < string.length; i++) {
    if(dictionary.hasOwnProperty(string[i])){
      return false
    }
    dictionary[string[i]] = true
  }
  return true
}

// test
console.log(isUnique('chuc')) // false
```
#### Python
```python
def isUnique(string):
  dictionary = {}

  for char in string:
    if char in dictionary:
      return False
    else:
      dictionary[char] = True

  return True

#test
print(isUnique('chuk')) # true
```
 ### Explanation

> The idea is to create a dictionary with every character of the string. so adding a char would look like `a: true ` . If the character to add happens to be already added to the dictionary, then the string not only contains unique characters, so the algorithm returns `false`. If the string can be added to the dictionary until the end, it means evary character was unique, so it returns `true`.
In case I can't use a data structure, I may sort the string first and then start comparing neighbors looking for equality.

### Time complexity

> O (n)
</details>


## Solution (from the book)

<details>
  <summary>Click to expand!</summary>
  
  You should first ask your interviewer if the string is an ASCII string or a Unicode string. Asking this question
will show an eye for detail and a solid foundation in computer science. We'll assume for simplicity the character
set is ASCII. If this assumption is not valid, we would need to increase the storage size.
One solution is to create an array of boolean values, where the flag at index i indicates whether character
i in the alphabet is contained in the string. The second time you see this character you can immediately
return f a l s e .
We can also immediately return f a l s e if the string length exceeds the number of unique characters in the
alphabet. After all, you can't form a string of 280 unique characters out of a 128-character alphabet.

The code below implements this algorithm,
```
boolean isUniqueChars(String s t r) {
  if (str.length() > 128) return false;

  boolean[] char_set = new boolean[128];
  for (int i = 0; i < str.length(); i++) {
   int val = str.charAt(i);
   if (char_set[val]) { // Already found this char in string
    return false; >
    return true;
   }
```

The time complexity for this code isO(n), where n is the length of the string. The space complexity is 0( 1),
(You could also argue the time complexity is 0 ( 1 ) , since the for loop will never iterate through more than
128 characters.) If you didn't want to assume the character set is fixed, you could express the complexity as
0 ( c ) spaceand 0 ( m i n ( C j n)) or 0 ( c ) time, where c is the size of the character set.

We can reduce our space usage by a factor of eight by using a bit vector. We will assume, in the below code,
that the string only uses the lowercase letters a through z. This will allow us to use just a single i n t .

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
If we can't use additional data structures, we can do the following:
1. Compare every character of the string to every other character of the string. This will take 0(nz ) time
and0(1) space.
2. If we are allowed to modify the input string, we could sort the string in 0 ( n l o g ( n ) ) time and then
linearly check the string for neighboring characters that are identical. Careful, though: many sorting
algorithms take up extra space.
These solutions are not as optimal in some respects, but might be better depending on the constraints of
the problem
</details>

