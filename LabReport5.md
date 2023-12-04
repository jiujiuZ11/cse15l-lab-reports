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
            index1 += 1;
        } else {
            result.add(list2.get(index2));
            // Introduce a bug: Don't increment index2 if the strings are equal.
            if (!list1.get(index1).equals(list2.get(index2))) {
                index2 += 1;
            }
        }
    }

    while (index1 < list1.size()) {
        result.add(list1.get(index1));
        index1 += 1;
    }
    while (index2 < list2.size()) {
        result.add(list2.get(index2));
        index2 += 1;
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
    public void testMergeInfiniteLoop() {
        List<String> l1 = Arrays.asList("a", "b", "c");
        List<String> l2 = Arrays.asList("b", "c", "d");

        // This will trigger the infinite loop due to the bug in the merge method
        ListExamples.merge(l1, l2);
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
<img width="998" alt="Screenshot 2023-12-03 at 7 50 49 PM" src="https://github.com/jiujiuZ11/cse15l-lab-reports/assets/130422166/06e098da-1f69-41ae-a42e-3b3825bc7e51">
### In the post, the student described:
"I'm encountering a frustrating issue with the merge method in our ListExamples class. In both testMergeInfiniteLoop and testMerge2, the tests are timing out after 500 milliseconds, which suggests the method might be getting stuck in an infinite loop. This seems to happen when there are common elements between the two lists being merged, as seen in testMerge2 where both lists contain 'c'. My guess is that the method isn't handling the iteration over the lists correctly when it encounters duplicate elements, leading to an infinite loop."

## 4. A description of what to edit to fix the bug
### Response from a TA:
"That's a good observation about the potential issue with duplicate elements. To narrow down the problem, can you try adding some print statements in the merge method to log the values of index1 and index2 during each iteration of the while loop? This should give us insight into how these indices are being updated and help identify if they're getting stuck at a certain point. Run the tests again after adding these print statements and observe the output in the terminal."
### Student got from trying:
<img width="1440" alt="Screenshot 2023-12-03 at 7 57 44 PM" src="https://github.com/jiujiuZ11/cse15l-lab-reports/assets/130422166/5147d9d8-c25b-4c14-8688-23a720f26bfc">

### Clear description of what the bug is:
The bug in the merge method occurs due to improper handling of indices when merging two lists with common elements. Specifically, in the while loop that compares elements from list1 and list2, if two elements are equal, the index for list2 (index2) is not incremented. This results in list2.get(index2) repeatedly comparing the same element in subsequent iterations, causing an infinite loop. The issue manifests as a test timeout in JUnit because the loop never terminates, and the ArrayList keeps growing until the timeout limit is reached.

# Part 2 – Reflection
During the second half of this quarter, I learned about Vim. Initially introduced through the vimtutor, I found Vim's modal editing - separating the tasks of inserting text and manipulating text - both challenging and fascinating. It was a departure from the typical text editors I was accustomed to. Despite recognizing Vim's potential for efficiency, I still need more practiced. I often found myself fumbling with commands, which highlighted the vast difference between Vim and the editors I was accustomed to.



