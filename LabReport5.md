# Lab Report 5
# Part 1 – Debugging Scenario
## 1. The file & directory structure needed
<img width="402" alt="Screenshot 2023-12-03 at 7 51 00 PM" src="https://github.com/jiujiuZ11/cse15l-lab-reports/assets/130422166/9f4ea7fe-f529-4328-a734-62170e6f257e">


## 2. The contents of each file before fixing the bug
### ListExamples.java
```
import java.util.ArrayList;
import java.util.List;

interface StringChecker { boolean checkString(String s); }

class ListExamples {

  // Returns a new list that has all the elements of the input list for which
  // the StringChecker returns true, and not the elements that return false, in
  // the same order they appeared in the input list;
  static List<String> filter(List<String> list, StringChecker sc) {
    List<String> result = new ArrayList<>();
    for(String s: list) {
      if(sc.checkString(s)) {
        result.add(0, s);
      }
    }
    return result;
  }


  // Takes two sorted list of strings (so "a" appears before "b" and so on),
  // and return a new list that has all the strings in both list in sorted order.
  static List<String> merge(List<String> list1, List<String> list2) {
    List<String> result = new ArrayList<>();
    int index1 = 0, index2 = 0;

    while (index1 < list1.size() && index2 < list2.size()) {
        if (list1.get(index1).compareTo(list2.get(index2)) < 0) {
            result.add(list1.get(index1));
            index1++;
        } else if (list1.get(index1).compareTo(list2.get(index2)) > 0) {
            result.add(list2.get(index2));
            index2++;
        } else {
            // Bug: When elements are equal, only add from list1 and increment both indices.
            // This will skip adding the duplicate element from list2.
            result.add(list1.get(index1));
            index1++;
            index2++;
        }
    }

    while (index1 < list1.size()) {
        result.add(list1.get(index1));
        index1++;
    }

    while (index2 < list2.size()) {
        result.add(list2.get(index2));
        index2++;
    }

    return result;
    }
}




```
### ListExamplesTests.java
```
import static org.junit.Assert.*;
import org.junit.*;
import java.util.*;


public class ListExamplesTests {
	@Test(timeout = 500)
	public void testMerge1() {
    		List<String> l1 = new ArrayList<String>(Arrays.asList("x", "y"));
		List<String> l2 = new ArrayList<String>(Arrays.asList("a", "b"));
		assertArrayEquals(new String[]{ "a", "b", "x", "y"}, ListExamples.merge(l1, l2).toArray());
	}
	
	@Test(timeout = 500)
        public void testMerge2() {
		List<String> l1 = new ArrayList<String>(Arrays.asList("a", "b", "c"));
		List<String> l2 = new ArrayList<String>(Arrays.asList("c", "d", "e"));
		assertArrayEquals(new String[]{ "a", "b", "c", "c", "d", "e" }, ListExamples.merge(l1, l2).toArray());
        }

	@Test(timeout = 500)
	public void testMergeWithDuplicates() {
		List<String> l1 = Arrays.asList("a", "c", "e");
		List<String> l2 = Arrays.asList("b", "c", "d");
		
		// Expected to contain all elements, including the duplicate 'c'
		List<String> expected = Arrays.asList("a", "b", "c", "c", "d", "e");
		List<String> actual = ListExamples.merge(l1, l2);
		
		assertArrayEquals("Merge does not handle duplicates correctly", expected.toArray(), actual.toArray());
		}

}

```
### test.sh
```
javac -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar *.java
java -cp .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar org.junit.runner.JUnitCore ListExamplesTests

```

## 3. The full command line (or lines) I ran to trigger the bug
bash test.sh
<img width="1440" alt="Screenshot 2023-12-03 at 8 05 23 PM" src="https://github.com/jiujiuZ11/cse15l-lab-reports/assets/130422166/9079609d-ffad-4d01-9ae5-11bb3c7976d9">

### In the post, the student described:
"I've been debugging our ListExamples class and noticed something odd with the merge method, particularly when dealing with duplicates. The test testMergeWithDuplicates is failing, showing that the expected array length is different from the actual one. It seems like when there are duplicate elements in the input lists, one of the duplicates is missing in the merged output. This is clear from the failure message: 'expected:<[c]> but was:<[d]>', indicating that one of the 'c' elements is missing. My guess is that the merge method isn't handling the addition of duplicate elements from both lists correctly."

## 4. A description of what to edit to fix the bug
### Response from a TA:
"Good analysis on the test result. It does seem like the issue is related to how duplicates are handled. To further investigate, could you check the loop conditions and the if-else logic in the merge method? Specifically, look at how you're comparing and adding elements from both lists when they are equal. Adding some print statements to log the elements being added to the merged list might also help you see where the method is deviating from the expected behavior."
### Student got from trying:
<img width="1440" alt="Screenshot 2023-12-03 at 8 11 05 PM" src="https://github.com/jiujiuZ11/cse15l-lab-reports/assets/130422166/ce56c822-c31c-461e-a9a7-5291c6080f81">


### Clear description of what the bug is:
The bug in the merge method arises from the way it handles equal elements in the two input lists. When it encounters equal elements, the method is currently designed to add the element from list1 to the result and then increment both index1 and index2. This causes the method to skip adding the duplicate element from list2. The correct behavior should be to add both elements when they are equal before incrementing the indices. As a result of this bug, the merged list ends up missing duplicates, leading to the test failures as the expected and actual list lengths and contents don't match.

# Part 2 – Reflection
During the second half of this quarter, I learned about Vim. Initially introduced through the vimtutor, I found Vim's modal editing - separating the tasks of inserting text and manipulating text - both challenging and fascinating. It was a departure from the typical text editors I was accustomed to. Despite recognizing Vim's potential for efficiency, I still need more practiced. I often found myself fumbling with commands, which highlighted the vast difference between Vim and the editors I was accustomed to.



