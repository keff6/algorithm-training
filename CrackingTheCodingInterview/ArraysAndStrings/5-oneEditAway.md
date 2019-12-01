# oneEditAway

## Description

>There are three types of edits that can be performed on strings: insert a character,
remove a character, or replace a character. Given two strings, write a function to check if they are
one edit (or zero edits) away.
EXAMPLE
p a l e , pie -> true
p a l e s , pale -> true
p a l e , bale -> true
p a l e , bake -> false

## My Solution

<details>
  <summary>Click to expand!</summary>

#### Javascript
```javascript
function oneEditAway(str1, str2) {
  const lenDifference = Math.abs(str1.length - str2.length)
  
  // Step 1: If the difference in length between both strings is > 1 return false
  if(lenDifference > 1) return false
  
  // Step 2: if both strings are equals there is no need to look for changes
  if(str1 === str2) return true
  
  // Step 3: CASE 1 -> replace
  let changes = 0
  
  if(str1.length === str2.length) {
    for(let i = 0; i < str1.length; i++) {
      if(str1[i] !== str2[i]) {
        changes++
      }
      if(changes > 1) return false
    }
  } else if(str1.length - 1 === str2.length) { // CASE 2 -> Remove one character
    return oneElementRemoved(str2, str1)
  } else if(str1.length + 1 === str2.length) { // CASE 3 -> Add one character
    return oneElementRemoved(str1, str2)
  }
  
  return true
}

function oneElementRemoved(str1, str2) {
  let index1 = 0
  let index2 = 0

  while(index1 < str1.length && index2 < str2.length) {
    if(str1[index1] !== str2[index2]) {
      if(index1 !== index2) {
        return false
      }
      index2++
    } else {
      index1++
      index2++
    }
  }
  return true
}

console.log(oneEditAway('pale','page')); //true
```
#### Python
```python
def oneEditAway(str1, str2):
  lenDifference = abs(len(str1) - len(str2))
  
  # Step 1: If the difference in length between both strings is > 1 return false
  if(lenDifference > 1): return False
  
  # Step 2: if both strings are equals there is no need to look for changes
  if(str1 == str2): return True
  
  # Step 3: CASE 1 -> replace
  changes = 0
  
  if(len(str1) == len(str2)):
    for i in  range(len(str1)):
      if(str1[i] != str2[i]):
        changes += 1
      
      if(changes > 1): return False
    
  elif(len(str1) - 1 == len(str2)): # CASE 2 -> Remove one character
    return oneElementRemoved(str2, str1)
  elif(len(str1) + 1 == len(str2)):  # CASE 3 -> Add one character
    return oneElementRemoved(str1, str2)
  
  return True


def oneElementRemoved(str1, str2):
  index1 = 0
  index2 = 0

  while(index1 < len(str1) and index2 < len(str2)): 
    if str1[index1] != str2[index2]:
      if index1 != index2:
        return False
      index2 += 1
    else:
      index1 += 1
      index2 += 1
  
  return True

print(oneEditAway('pelas','pela')); #true
```
 ### Explanation

> To solve this problem, i decided to divide the solution in 2 separate functions. The main function and one to check if exactly one character was added to one string.
* I compare both strings length first, if the difference is > 1, then i can return false.
* If boths strings are equal, that means that I can return true right away
* CASE 1 - strings have the same length: then is necesary to loop ant try to find if there are more than 1 difference between strings.
* CASE 2 - remove one character and CASE 3 - add one character are going to use the helper function oneElementRemoved to determine if the only change is the add/removal of a character.


### Time complexity

> O (n)
</details>


## Solution (from the book)

<details>
  <summary>Click to expand!</summary>
  
There is a "brute force"algorithm to do this. We could check all possible strings that are one edit away by testing the removal of each character (and comparing), testing the replacement of each character (and comparing), and then testing the insertion of each possible character (and comparing).
That would be too slow, so let's not bother with implementing it.
This is one of those problems where it's helpful to think about the "meaning" of each of these operations.
What does it mean for two strings to be one insertion, replacement, or removal away from each other?
• Replacement: Consider two strings, such as b a l e and pale, that are one replacement away. Yes, that
does mean that you could replace a character in b a l e to make pale. But more precisely, it means that
they are different only in one place.
• Insertion: The strings apple and a p l e are one insertion away. This means that if you compared the
strings, they would be identical—except for a shift at some point in the strings.
• Removal: The strings apple and a p l e are also one removal away, since removal is just the inverse of
insertion.
We can go ahead and implement this algorithm now. We'll merge the insertion and removal check into one step, and check the replacement step separately.
Observe that you don't need to check the strings for insertion, removal, and replacement edits. The lengths of the strings will indicate which of these you need to check.

```
boolean oneEditAway(String first , String second) {
	if(first.length() == second.lengthQ) {
		return oneEditReplace(first, second);
	} else if(first.length() + 1 == second.length()) {
		return oneEditInsert(first, second);
	} else if(first.length() - 1 == second.length()) {
		return oneEditInsert(second, first);
	}
	return false;
}

boolean oneEditReplace(String s1 , String s2) {
	boolean foundDifference = false;
	for(int i = 0; i < sl.length(); i++) {
		if (sl.charAt(i) 1= s2,charAt(i)) {
			if (foundDifference) {
				return false
			}
			foundDifference = true;
		}
	}
	return true;
}

/* Check if you can insert a character into si to make s2. */
boolean oneEditlnsert(String sl , String s2) {
	int indexl = 0;
	int index2 = 0;
	while (index2 < s2.1ength() && indexl < s i . lengthQ) {
		if (sl.charAt(indexl) !» s2.charAt(index2)) {
		if (indexl != index2) {
			return false;
		}
		index2++;
		} else {
			indexl++;
			index2++;
		}
	}
	return true
}
```
This algorithm (and almost any reasonable algorithm) takes 0(n) time, where n is the length of the shorter string,
Why is the runtime dictated by the shorter string instead of the longer string?
If the strings are the same length (plus or minus one character), then it doesn't matter whether we use the longer string or the shorter string to define the runtime. If the strings are very different lengths, then the algorithm will terminate in 0(1) time. One really, really long string therefore won't significantly extend the runtime. It increases the runtime only if both strings are long.
We might notice that the code for oneEditReplace is very similar to that for oneEditlnsert. We can merge them into one method.
To do this, observe that both methods follow similar logic compare each character and ensure that the strings are only different by one. The methods vary in how they handle that difference. The method oneEditReplace does nothing other than flag the difference, whereas oneEditlnsert increments the pointer to the longer string. We can handle both of these in the same method.

```
boolean oneEditAway(String first , String second) {
	/* Length checks. */
	if (Math.abs(first.length() - second. lengthQ) > 1) {
		return false;
	}
	
	/* Get shorter and longer string . */
	String si = first.length < second.length ? first : second;
	String s2 = first.length < second.length() ? second : first;

	int indexl = 0;
	int index2 = 0;
	boolean foundDifference = false;
	while (index2 < s2.1ength() && indexl < sl.length()) {
		if (sl.charAt(indexl) 1= s2.charAt(index2)) {

			/* Ensure that this is the first difference found.*/
			if (foundDifference) return false;
			foundDifference = true;
		
			if (si.length() == s2.1ength()) { // On replace, move shorter pointer
				indexi++;
			}
		} else {
			indexl++; // If matching, move shorter pointer
		}
			index2++; // Always move pointer for longer string
		}
		return true;
	}

```

Some people might argue the first approach is better, as it is clearer and easier to follow. Others, however, will argue that the second approach is better, since it's more compact and doesn't duplicate code (which can facilitate maintainability).
You don't necessarily need to "pick a side."You can discuss the tradeoffs with your interviewer.

</details>

