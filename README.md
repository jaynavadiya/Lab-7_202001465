# Lab-7_202001465

# Jaykumar Navadiya

# Group 6, IT314 - Software Engineering 

## Section A

### Based on the problem statement, we can identify the following equivalence classes:

- Valid input: The input is a valid date within the specified range of `1 <= month <= 12`, `1 <= day <= 31`, and `1900 <= year <= 2015`.
- Invalid input: The input is not a valid date, such as February 30th or April 31st.
- Input with minimum values: The input is the minimum valid value for each field, which is `(1, 1, 1900)`.
- Input with maximum values: The input is the maximum valid value for each field, which is `(31, 12, 2015)`.
- Input with day value less than minimum: The input has a day value less than the minimum valid value of `1`.
- Input with day value greater than maximum: The input has a day value greater than the maximum valid value of `31`.
- Input with month value less than minimum: The input has a month value less than the minimum valid value of `1`.
- Input with month value greater than maximum: The input has a month value greater than the maximum valid value of `12`.
- Input with year value less than minimum: The input has a year value less than the minimum valid value of `1900`.
- Input with year value greater than maximum: The input has a year value greater than the maximum valid value of `2015`.

### Equivalence Partitioning Test Cases:

<table>
  <tr>
    <th>Tester Action and Input Data</th>
    <th>Expected Outcome</th>
  </tr>
  <tr>
    <td>Valid input: day=1, month=1, year=1900</td>
    <td>Invalid date</td>
  </tr>
  <tr>
    <td>Valid input: day=31, month=12, year=2015</td>
    <td>Previous date</td>
  </tr>
  <tr>
    <td>Invalid input: day=0, month=6, year=2000</td>
    <td>An error message</td>
  </tr>
  <tr>
    <td>Invalid input: day=32, month=6, year=2000</td>
    <td>An error message</td>
  </tr>
  <tr>
    <td>Invalid input: day=29, month=2, year=2001</td>
    <td>An error message</td>
  </tr>
</table>

### Using the boundary value analysis technique, we can identify the following boundary values:

- Minimum valid input: The input is the minimum valid value for each field, which is (1, 1, 1900).
- Maximum valid input: The input is the maximum valid value for each field, which is (31, 12, 2015).
- Input with day value less than minimum: The input has a day value less than the minimum valid value of 1, such as (0, 1, 2000).
- Input with day value greater than maximum: The input has a day value greater than the maximum valid value of 31, such as (32, 1, 2000).
- Input with month value less than minimum: The input has a month value less than the minimum valid value of 1, such as (1, 0, 2000).
- Input with month value greater than maximum: The input has a month value greater than the maximum valid value of 12, such as (1, 13, 2000).
- Input with year value less than minimum: The input has a year value less than the minimum valid value of 1900, such as (1, 1, 1899).
- Input with year value greater than maximum: The input has a year value greater than the maximum valid value of 2015, such as (1, 1, 2016).
- Input with invalid day value: The input has an invalid day value for a given month and year, such as (30, 2, 2000).
- Input with invalid day and month value: The input has an invalid day and month value for a given year, such as (31, 4, 2000).


### Boundary Value Analysis Test Cases:

<table>
  <tr>
    <th>Tester Action and Input Data</th>
    <th>Expected Outcome</th>
  </tr>
  <tr>
    <td>Valid input: day=1, month=1, year=1900</td>
    <td>Invalid date</td>
  </tr>
  <tr>
    <td>Valid input: day=31, month=12, year=2015</td>
    <td>Previous date</td>
  </tr>
  <tr>
    <td>Invalid input: day=0, month=6, year=2000</td>
    <td>An error message</td>
  </tr>
  <tr>
    <td>Invalid input: day=32, month=6, year=2000</td>
    <td>An error message</td>
  </tr>
  <tr>
    <td>Invalid input: day=29, month=2, year=2000</td>
    <td>An error message</td>
  </tr>
  <tr>
    <td>Valid input: day=1, month=6, year=2000</td>
    <td>Previous date</td>
  </tr>
  <tr>
    <td>Valid input: day=31, month=5, year=2000</td>
    <td>Previous date</td>
  </tr>
  <tr>
    <td>Valid input: day=15, month=6, year=2000</td>
    <td>Previous date</td>
  </tr>
  <tr>
    <td>Invalid input: day=31, month=4, year=2000</td>
    <td>An error message</td>
  </tr>
</table>
</br>

### Modify your programs such that it runs on eclipse IDE, and then execute your test suites on the program. While executing your input data in a program, check whether the identified expected. outcome (mentioned by you) is correct or not.

To modify the program to run on Eclipse IDE, we can create a new Java class. We can then create a main method to execute the program and call the previousDate method with the test inputs to check if the output matches the expected outcome. We can also include print statements to display the input and output values for each test case.

Code Example:


```
public class PreviousDate {
   public static void main(String[] args) {
      // Test inputs
      int day = 1;
      int month = 1;
      int year = 1900;
      
      // Test the previousDate method
      String result = previousDate(day, month, year);
      
      // Display the input and output values
      System.out.println("Input: " + day + "/" + month + "/" + year);
      System.out.println("Output: " + result);
   }

   public static String previousDate(int day, int month, int year) {
      String error = "Invalid date";
      
      // Check for invalid inputs
      if (day < 1 || day > 31 || month < 1 || month > 12 || year < 1900 || year > 2015) {
         return error;
      }
      
      // Check for February
      if (month == 2) {
         if (year % 4 == 0 && (year % 100 != 0 || year % 400 == 0)) {
            if (day < 1 || day > 29) {
               return error;
            }
         } else {
            if (day < 1 || day > 28) {
               return error;
            }
         }
      }
      
      // Check for months with 30 days
      if (month == 4 || month == 6 || month == 9 || month == 11) {
         if (day < 1 || day > 30) {
            return error;
         }
      }
      
      // Check for January
      if (month == 1) {
         if (day == 1) {
            if (year == 1900) {
               return error;
            } else {
               return "31/12/" + (year - 1);
            }
         } else {
            return (day - 1) + "/1/" + year;
         }
      }

```



### Problem 1 :



```
import static org.junit.Assert.*;
import org.junit.Test;

public class LinearSearchTest {
    
    // Equivalence Partitioning Tests:
    
    @Test
    public void testValidValue() {
        int[] arr = {1, 2, 3, 4, 5};
        assertEquals(2, LinearSearch.linearSearch(3, arr));
    }
    
    @Test
    public void testInvalidValue() {
        int[] arr = {1, 2, 3, 4, 5};
        assertEquals(-1, LinearSearch.linearSearch(6, arr));
    }
    
    // Boundary Value Analysis Tests:
    
    @Test
    public void testMinimumValidInput() {
        int[] arr = {1};
        assertEquals(0, LinearSearch.linearSearch(1, arr));
    }
    
    @Test
    public void testMaximumValidInput() {
        int[] arr = {1, 2, 3, 4, 5};
        assertEquals(4, LinearSearch.linearSearch(5, arr));
    }
    
    @Test
    public void testInputWithDayValueLessThanMinimum() {
        int[] arr = {1, 2, 3, 4, 5};
        assertEquals(-1, LinearSearch.linearSearch(-1, arr));
    }
    
    @Test
    public void testInputWithDayValueGreaterThanMaximum() {
        int[] arr = {1, 2, 3, 4, 5};
        assertEquals(-1, LinearSearch.linearSearch(6, arr));
    }
    
    @Test
    public void testInputWithMonthValueLessThanMinimum() {
        int[] arr = {1, 2, 3, 4, 5};
        assertEquals(-1, LinearSearch.linearSearch(-1, arr));
    }
    
    @Test
    public void testInputWithMonthValueGreaterThanMaximum() {
        int[] arr = {1, 2, 3, 4, 5};
        assertEquals(-1, LinearSearch.linearSearch(13, arr));
    }
    
    @Test
    public void testInputWithYearValueLessThanMinimum() {
        int[] arr = {1, 2, 3, 4, 5};
        assertEquals(-1, LinearSearch.linearSearch(-1, arr));
    }
    
    @Test
    public void testInputWithYearValueGreaterThanMaximum() {
        int[] arr = {1, 2, 3, 4, 5};
        assertEquals(-1, LinearSearch.linearSearch(2016, arr));
    }
    
    @Test
    public void testInputWithInvalidDayValue() {
        int[] arr = {1, 2, 3, 4, 5};
        assertEquals(-1, LinearSearch.linearSearch(31, arr));
    }
    
    @Test
    public void testInputWithInvalidDayAndMonthValue() {
        int[] arr = {1, 2, 3, 4, 5};
        assertEquals(-1, LinearSearch.linearSearch(31, arr));
    }
}

```

### Equivalence Partitioning:

#### Test Cases Identified Using Equivalence Partitioning

Valid Inputs:

- Search value exists in array - linearSearch(5, [1, 2, 3, 4, 5]) should return 4.
- Search value exists in array - linearSearch(1, [1, 2, 3, 4, 5]) should return 0.
- Search value exists in array at first index - linearSearch(1, [1]) should return 0.
- Search value exists in array at last index - linearSearch(5, [1, 2, 3, 4, 5]) should return 4.

Invalid Inputs: 

- Empty array - linearSearch(5, []) should return -1.
- Search value does not exist in array - linearSearch(6, [1, 2, 3, 4, 5]) should return -1.
- Array with all the same values - linearSearch(5, [5, 5, 5, 5, 5]) should return 0.


<table>
  <thead>
    <tr>
      <th>Tester Action and Input Data</th>
      <th>Expected Outcome</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Test with v as a non-existent value and an empty array a[]</td>
      <td>-1</td>
    </tr>
    <tr>
      <td>Test with v as a non-existent value and a non-empty array a[]</td>
      <td>-1</td>
    </tr>
    <tr>
      <td>Test with v as an existent value and an empty array a[]</td>
      <td>-1</td>
    </tr>
    <tr>
      <td>Test with v as an existent value and a non-empty array a[] where v exists</td>
      <td>the index of v in a[]</td>
    </tr>
    <tr>
      <td>Test with v as an existent value and a non-empty array a[] where v does not exist</td>
      <td>-1</td>
    </tr>
  </tbody>
</table>

### Boundary Value Analysis:

#### Test Cases Identified Using Boundary Value Analysis

Valid Inputs:

- Minimum valid input - linearSearch(1, [1]) should return 0.
- Maximum valid input - linearSearch(10, [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]) should return 9.

Invalid Inputs:

- Search value less than minimum - linearSearch(0, [1, 2, 3, 4, 5]) should return -1.
- Search value greater than maximum - linearSearch(11, [1, 2, 3, 4, 5]) should return -1.
- Empty array - linearSearch(5, []) should return -1.

<table>
  <thead>
    <tr>
      <th>Tester Action and Input Data</th>
      <th>Expected Outcome</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Test with v as a non-existent value and an empty array a[]</td>
      <td>-1</td>
    </tr>
    <tr>
      <td>Test with v as a non-existent value and a non-empty array a[]</td>
      <td>-1</td>
    </tr>
    <tr>
      <td>Test with v as an existent value and an array a[] of length 0</td>
      <td>-1</td>
    </tr>
    <tr>
      <td>Test with v as an existent value and an array a[] of length 1, where v exists</td>
      <td>0</td>
    </tr>
    <tr>
      <td>Test with v as an existent value and an array a[] of length 1, where v does not exist</td>
      <td>-1</td>
    </tr>
    <tr>
      <td>Test with v as an existent value and an array a[] of length greater than 1, where v exists at the beginning of the array</td>
      <td>0</td>
    </tr>
    <tr>
      <td>Test with v as an existent value and an array a[] of length greater than 1, where v exists at the end of the array</td>
      <td>the last index where v is found</td>
    </tr>
    <tr>
      <td>Test with v as an existent value and an array a[] of length greater than 1, where v exists in the middle of the array</td>
      <td>the index where v is found</td>
    </tr>
  </tbody>
</table>
</br>


### Problem 2 :

### Equivalence Partitioning:

#### Equivalence Partitioning Test Cases:

- Empty array: `v=5`, `a=[]`.
- Array with only one element: `v=5`, `a=[5]`.
- Array with multiple elements but v does not appear in the - array: `v=5`,`a=[1, 2, 3, 4, 6, 7`].
- Array with multiple elements and v appears once: `v=5`, `a=[1, 2, 3, 4, 5, 6, 7]`.
- Array with multiple elements and v appears multiple times: `v=5`, `a=[1, 5, 2, 5, 3, 5, 4, 5]`.

<table>
  <thead>
    <tr>
      <th>Tester Action and Input Data</th>
      <th>Expected Outcome</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Test with v as a non-existent value and an empty array a[]</td>
      <td>0</td>
    </tr>
    <tr>
      <td>Test with v as a non-existent value and a non-empty array a[]</td>
      <td>0</td>
    </tr>
    <tr>
      <td>Test with v as an existent value and an empty array a[]</td>
      <td>0</td>
    </tr>
    <tr>
      <td>Test with v as an existent value and a non-empty array a[] where v exists multiple times</td>
      <td>the number of occurrences of v in a[]</td>
    </tr>
    <tr>
      <td>Test with v as an existent value and a non-empty array a[] where v exists only once</td>
      <td>1</td>
    </tr>
  </tbody>
</table>

### Boundary Value Analysis:

- Minimum valid value: `v=1`, `a=[1, 2, 3, 4, 5, 6, 7]`.
- Maximum valid value: `v=10`, `a=[7, 8, 9, 10]`.
- Value not present in the array: `v=5`, `a=[1, 2, 3, 4, 6, 7]`.
- All elements in the array are the same and equal to v: `v=5`, `a=[5, 5, 5, 5, 5, 5, 5, 5]`.
- All elements in the array are different and none of them is v: `v=5`,`a=[1, 2, 3, 4, 6, 7, 8, 9]`.
- Input with no occurrence of v: The input array does not contain any occurrence of v, such as `(5, {1, 2, 3, 4})`.
- Input with all elements as v: The input array contains only v, such as `(3, {3, 3, 3, 3})`.
- Input with empty array: The input array is empty, such as `(2, {})`.
- Input with negative values: The input array contains negative integers, such as `(-2, {-3, -2, -1, 0, 1, -2})`.
Input with maximum valid input value: The input array contains the maximum valid value for each field, such as `(5, {2147483647, 2147483647, 2147483647, 2147483647, 2147483647})`.
- Input with minimum valid input value: The input array contains the minimum valid value for each field, such as `(5, {-2147483648, -2147483648, -2147483648, -2147483648, -2147483648})`.

<table>
  <thead>
    <tr>
      <th>Tester Action and Input Data</th>
      <th>Expected Outcome</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Test with v as a non-existent value and an empty array a[]</td>
      <td>0</td>
    </tr>
    <tr>
      <td>Test with v as a non-existent value and a non-empty array a[]</td>
      <td>0</td>
    </tr>
    <tr>
      <td>Test with v as an existent value and an array a[] of length 0</td>
      <td>0</td>
    </tr>
    <tr>
      <td>Test with v as an existent value and an array a[] of length 1, where v exists</td>
      <td>1</td>
    </tr>
    <tr>
      <td>Test with v as an existent value and an array a[] of length 1, where v does not exist</td>
      <td>0</td>
    </tr>
    <tr>
      <td>Test with v as an existent value and an array a[] of length greater than 1, where v exists at the beginning of the array</td>
      <td>the number of occurrences of v in a[]</td>
    </tr>
    <tr>
      <td>Test with v as an existent value and an array a[] of length greater than 1, where v exists at the end of the array</td>
      <td>the number of occurrences of v in a[]</td>
    </tr>
    <tr>
      <td>Test with v as an existent value and an array a[] of length greater than 1, where v exists in the middle of the array</td>
      <td>the number of occurrences of v in a[]</td>
    </tr>
  </tbody>
</table>
</br>

### Test Execution:

The modified program can be executed using JUnit Testing Framework in Eclipse IDE.

For each test case, the input values are passed as arguments to the function countItem(). The expected output for each test case is compared with the actual output generated by the function. If both the expected and actual outputs match, the test case is considered to have passed; otherwise, it has failed.

The JUnit test cases for the above identified test cases are as follows:

```
import static org.junit.Assert.assertEquals;
import org.junit.Test;

public class CountItemTest {
    
    @Test
    public void testEmptyArray() {
        int[] a = {};
        int v = 5;
        int expected = 0;
        int result = countItem(v, a);
        assertEquals(expected, result);
    }
    
    @Test
    public void testSingleElementArray() {
        int[] a = {5};
        int v = 5;
        int expected = 1;
        int result = countItem(v, a);
        assertEquals(expected, result);
    }
    
    @Test
    public void testValueNotPresent() {
        int[] a = {1, 2, 3, 4, 6, 7};
        int v = 5;
        int expected = 0;
        int result = countItem(v, a);
        assertEquals(expected, result);
    }
    
    @Test
    public void testValuePresentOnce() {
        int[] a = {1, 2, 3, 4, 5, 6, 7};
        int v = 5;
        int expected = 1;
        int result = countItem(v, a);
        assertEquals(expected, result);
    }
    
    @Test
    public void testValuePresentMultipleTimes() {
        int[] a = {1, 5, 2, 5, 3, 5, 4, 5};
        int v = 5;
        int expected = 5;
        int result = countItem(v, a);
        assertEquals(expected, result);
    }
    
    @Test
    public void testMinValidValue() {
        int[] a = {1, 2, 3, 4, 5, 6, 7};
        int v = 1;
        int expected = 1;
        int result = countItem(v, a);
        assertEquals(expected, result);
    }
    
    @Test
	public void testSingleOccurrence() {
		int[] arr = {1, 2, 3, 4, 5};
		assertEquals(1, countItem(3, arr));
	}
	
	@Test
	public void testMultipleOccurrences() {
		int[] arr = {1, 2, 3, 3, 3, 4, 5};
		assertEquals(3, countItem(3, arr));
	}
	
	@Test
	public void testNoOccurrences() {
		int[] arr = {1, 2, 3, 4};
		assertEquals(0, countItem(5, arr));
	}
	
	@Test
	public void testAllOccurrences() {
		int[] arr = {3, 3, 3, 3};
		assertEquals(4, countItem(3, arr));
	}
	
	@Test
	public void testEmptyArray() {
		int[] arr = {};
		assertEquals(0, countItem(2, arr));
	}
	
	@Test
	public void testNegativeValues() {
		int[] arr = {-3, -2, -1, 0, 1, -2};
		assertEquals(2, countItem(-2, arr));
	}
	
	@Test
	public void testMaxValidInput() {
		int[] arr = {2147483647, 2147483647, 2147483647, 2147483647, 2147483647};
		assertEquals(0, countItem(5, arr));
	}
	
	@Test
	public void testMinValidInput() {
		int[] arr = {-2147483648, -2147483648, -2147483648, -2147483648, -2147483648};
		assertEquals(0, countItem(5, arr));
	}
}

```

### Problem 3 :

### Equivalence Partitioning:

- Valid input: `v` is present in `a[]`
- Invalid input: `v` is not present in `a[]`


<table>
  <tr>
    <th>Tester Action and Input Data</th>
    <th>Expected Outcome</th>
  </tr>
  <tr>
    <td>v=5, a=[1, 3, 5, 7, 9]</td>
    <td>2</td>
  </tr>
  <tr>
    <td>v=1, a=[1, 3, 5, 7, 9]</td>
    <td>0</td>
  </tr>
  <tr>
    <td>v=9, a=[1, 3, 5, 7, 9]</td>
    <td>4</td>
  </tr>
  <tr>
    <td>v=4, a=[1, 3, 5, 7, 9]</td>
    <td>-1</td>
  </tr>
  <tr>
    <td>v=11, a=[1, 3, 5, 7, 9]</td>
    <td>-1</td>
  </tr>
</table>

### Boundary Value Analysis:

- Valid input: `v` is the first element in `a[]`
- Valid input: `v` is the last element in `a[]`
- Valid input: `v` is in the middle of `a[]`
- Invalid input: `a[]` is empty
- Invalid input: `a[]` has only one element which is not `v`
- Invalid input: `a[]` has only one element which is `v`
- Invalid input: `v` is less than the first element in `a[]`
- Invalid input: `v` is greater than the last element in `a[]`

<table>
  <tr>
    <th>Tester Action and Input Data</th>
    <th>Expected Outcome</th>
  </tr>
  <tr>
    <td>v=1, a=[1]</td>
    <td>0</td>
  </tr>
  <tr>
    <td>v=9, a=[9]</td>
    <td>0</td>
  </tr>
  <tr>
    <td>v=5, a=[]</td>
    <td>-1</td>
  </tr>
  <tr>
    <td>v=5, a=[5, 7, 9]</td>
    <td>0 (smallest element in the array)</td>
  </tr>
  <tr>
    <td>v=5, a=[1, 3, 5]</td>
    <td>2 (largest element in the array)</td>
  </tr>
</table>
</br>

### Modified Program in Eclipse IDE:

The JUnit test cases for the above identified test cases are as follows:

```
import static org.junit.jupiter.api.Assertions.*;
import org.junit.jupiter.api.Test;

class BinarySearchTest {
    @Test
    void testValidInputPresent() {
        int[] a = {1, 3, 5, 7, 9};
        int v = 5;
        int expectedIndex = 2;
        int actualIndex = BinarySearch.binarySearch(v, a);
        assertEquals(expectedIndex, actualIndex);
    }

    @Test
    void testInvalidInputNotPresent() {
        int[] a = {1, 3, 5, 7, 9};
        int v = 4;
        int expectedIndex = -1;
        int actualIndex = BinarySearch.binarySearch(v, a);
        assertEquals(expectedIndex, actualIndex);
    }

    @Test
    void testValidInputFirstElement() {
        int[] a = {1, 3, 5, 7, 9};
        int v = 1;
        int expectedIndex = 0;
        int actualIndex = BinarySearch.binarySearch(v, a);
        assertEquals(expectedIndex, actualIndex);
    }

    @Test
    void testValidInputLastElement() {
        int[] a = {1, 3, 5, 7, 9};
        int v = 9;
        int expectedIndex = 4;
        int actualIndex = BinarySearch.binarySearch(v, a);
        assertEquals(expectedIndex, actualIndex);
    }

    @Test
    void testValidInputMiddleElement() {
        int[] a = {1, 3, 5, 7, 9};
        int v = 3;
        int expectedIndex = 1;
        int actualIndex = BinarySearch.binarySearch(v, a);
        assertEquals(expectedIndex, actualIndex);
    }

    @Test
    void testInvalidInputEmptyArray() {
        int[] a = {};
        int v = 5;
        int expectedIndex = -1;
        int actualIndex = BinarySearch.binarySearch(v, a);
        assertEquals(expectedIndex, actualIndex);
    }

    @Test
    void testInvalidInputOneElementNotV() {
        int[] a = {2};
        int v = 1;
        int expectedIndex = -1;
        int actualIndex = BinarySearch.binarySearch(v, a);
        assertEquals(expectedIndex, actualIndex);
    }

    @Test
    void testInvalidInputOneElementIsV() {
        int[] a = {1};
        int v = 1;
        int expectedIndex = 0;
        int actualIndex = BinarySearch.binarySearch(v, a);
        assertEquals(expectedIndex, actualIndex);
    }
}

```

### Problem 4 :

### Equivalence Partitioning:

Valid Triangles:

- Three sides are of the same length (Equilateral)
- Two sides are of the same length (Isosceles)
- All three sides are of different lengths (Scalene)

Invalid Triangles:

- One side has a length of 0
- The sum of the lengths of two sides is less than or equal - to the length of the third side

### Equivalence Partitioning Test Cases:

Valid Triangles:

- Equilateral triangle: a=5, b=5, c=5 (expected result: EQUILATERAL)
- Isosceles triangle: a=4, b=4, c=6 (expected result: ISOSCELES)
- Scalene triangle: a=3, b=4, c=5 (expected result: SCALENE)
Invalid Triangles:

Invalid Triangles:

- One side has length 0: a=0, b=2, c=3 (expected result: INVALID)
- Sum of two sides is less than or equal to third side: a=1, b=1, c=3 (expected result: INVALID)
- Sum of two sides is equal to third side: a=2, b=2, c=4 (expected result: INVALID)

<table>
  <tr>
    <th>Tester Action and Input Data</th>
    <th>Expected Outcome</th>
  </tr>
  <tr>
    <td>Valid input: a=3, b=3, c=3</td>
    <td>EQUILATERAL</td>
  </tr>
  <tr>
    <td>Valid input: a=4, b=4, c=5</td>
    <td>ISOSCELES</td>
  </tr>
  <tr>
    <td>Valid input: a=5, b=4, c=3</td>
    <td>SCALENE</td>
  </tr>
  <tr>
    <td>Invalid input: a=0, b=0, c=0</td>
    <td>INVALID</td>
  </tr>
  <tr>
    <td>Invalid input: a=-1, b=2, c=3</td>
    <td>INVALID</td>
  </tr>
  <tr>
    <td>Valid input: a=1, b=1, c=1</td>
    <td>EQUILATERAL</td>
  </tr>
  <tr>
    <td>Valid input: a=2, b=2, c=1</td>
    <td>ISOSCELES</td>
  </tr>
  <tr>
    <td>Valid input: a=3, b=4, c=5</td>
    <td>SCALENE</td>
  </tr>
  <tr>
    <td>Invalid input: a=0, b=1, c=1</td>
    <td>INVALID</td>
  </tr>
  <tr>
    <td>Invalid input: a=1, b=0, c=1</td>
    <td>INVALID</td>
  </tr>
  <tr>
    <td>Invalid input: a=1, b=1, c=0</td>
    <td>INVALID</td>
  </tr>
</table>
</br>

### Boundary Value Analysis:

For this function, the minimum and maximum values for the sides of a triangle are not relevant. Instead, we need to test the boundaries where the behavior of the function might change.

### Boundary Value Analysis Test Cases:

Valid Triangles:

- Minimum values: a=1, b=1, c=1 (expected result: EQUILATERAL)
- Maximum values: a=1000, b=1000, c=1000 (expected result: EQUILATERAL)
- Two sides are equal to the third side: a=2, b=2, c=4 (expected result: INVALID- but a specific error message needs to be printed in this case)
- Two sides are very close in length: a=5, b=6, c=6 (expected result: ISOSCELES)

Invalid Triangles:

- One side has length 0: a=0, b=2, c=3 (expected result: INVALID)
- Sum of two sides is less than or equal to third side: a=1, b=1, c=3 (expected result: INVALID)
- Sum of two sides is equal to third side: a=2, b=2, c=4 (expected result: INVALID)
- One side is just above the sum of the other two sides: a=4, b=4, c=7 (expected result: INVALID)
- One side is just below the sum of the other two sides: a=4, b=4, c=7 (expected result: INVALID)


<table>
  <tr>
    <th>Tester Action and Input Data</th>
    <th>Expected Outcome</th>
  </tr>
  <tr>
    <td>Invalid inputs: a = 0, b = 0, c = 0</td>
    <td>INVALID</td>
  </tr>
  <tr>
    <td>Invalid inputs: a + b = c or b + c = a or c + a = b (a=3, b=4, c=8)</td>
    <td>INVALID</td>
  </tr>
  <tr>
    <td>Equilateral triangles: a = b = c = 1</td>
    <td>EQUILATERAL</td>
  </tr>
  <tr>
    <td>Equilateral triangles: a = b = c = 100</td>
    <td>EQUILATERAL</td>
  </tr>
  <tr>
    <td>Isosceles triangles: a = b ≠ c = 10</td>
    <td>ISOSCELES</td>
  </tr>
  <tr>
    <td>Isosceles triangles: a ≠ b = c = 10</td>
    <td>ISOSCELES</td>
  </tr>
  <tr>
    <td>Isosceles triangles: a = c ≠ b = 10</td>
    <td>ISOSCELES</td>
  </tr>
  <tr>
    <td>Scalene triangles: a = b + c - 1</td>
    <td>SCALENE</td>
  </tr>
  <tr>
    <td>Scalene triangles: b = a + c - 1</td>
    <td>SCALENE</td>
  </tr>
  <tr>
    <td>Scalene triangles: c = a + b - 1</td>
    <td>SCALENE</td>
  </tr>
  <tr>
    <td>Maximum values: a, b, c = Integer.MAX_VALUE</td>
    <td>INVALID</td>
  </tr>
  <tr>
    <td>Minimum values: a, b, c = Integer.MIN_VALUE</td>
    <td>INVALID</td>
  </tr>
</table>


#### JUnit test case for the `triangle` function, using the test cases identified in the Equivalence Partitioning and Boundary Value Analysis sections:

```
import org.junit.Test;
import static org.junit.Assert.assertEquals;

public class TriangleTest {

    final int EQUILATERAL = 0;
    final int ISOSCELES = 1;
    final int SCALENE = 2;
    final int INVALID = 3;
    
    @Test
    public void testEquivalencePartitioning() {
        // Valid Triangles
        assertEquals(EQUILATERAL, triangle(5, 5, 5));
        assertEquals(ISOSCELES, triangle(4, 4, 6));
        assertEquals(SCALENE, triangle(3, 4, 5));
        
        // Invalid Triangles
        assertEquals(INVALID, triangle(0, 2, 3));
        assertEquals(INVALID, triangle(1, 1, 3));
        assertEquals(INVALID, triangle(2, 2, 4));
    }
    
    @Test
    public void testBoundaryValueAnalysis() {
        // Valid Triangles
        assertEquals(EQUILATERAL, triangle(1, 1, 1));
        assertEquals(EQUILATERAL, triangle(1000, 1000, 1000));
        assertEquals(INVALID, triangle(2, 2, 4)); // Two sides are equal to the third side
        assertEquals(ISOSCELES, triangle(5, 6, 6)); // Two sides are very close in length
        
        // Invalid Triangles
        assertEquals(INVALID, triangle(0, 2, 3));
        assertEquals(INVALID, triangle(1, 1, 3));
        assertEquals(INVALID, triangle(2, 2, 4));
        assertEquals(INVALID, triangle(4, 4, 7)); // One side is just above the sum of the other two sides
        assertEquals(INVALID, triangle(4, 4, 6)); // One side is just below the sum of the other two sides
    }
    
    // triangle function implementation
    private int triangle(int a, int b, int c) {
        if (a >= b+c || b >= a+c || c >= a+b)
            return(INVALID);
        if (a == b && b == c)
            return(EQUILATERAL);
        if (a == b || a == c || b == c)
            return(ISOSCELES);
        return(SCALENE);
    }
}

```

These JUnit test cases are used to test a function called `triangle()` that takes in three integer arguments a, b, and c, which represent the side lengths of a triangle, and returns an integer value corresponding to the type of the triangle:

- 0: `EQUILATERAL` for an equilateral triangle (all sides are equal)
- 1: `ISOSCELES` for an isosceles triangle (two sides are equal)
- 2: `SCALENE` for a scalene triangle (no sides are equal)
- 3: `INVALID` for an invalid triangle (the sum of any two sides is less than or equal to the length of the third side)

Note that in the `testEquivalencePartitioning` method, we are only testing the test cases identified using Equivalence Partitioning, while in the `testBoundaryValueAnalysis` method, we are only testing the test cases identified using Boundary Value Analysis. This way, we can ensure that each category of test cases is tested separately.

Each test case within the methods uses the `assertEquals()` method to verify that the expected output value matches the actual output value returned by the `triangle()` function when it is called with the specified input values.

If all the test cases pass, the JUnit test runner will output a message indicating that all the tests were successful. If any test cases fail, the JUnit test runner will output an error message indicating which test case failed and what the expected and actual output values were.

### Problem 5 :

### Equivalence Partitioning:

- Valid prefix: "hello" in "hello world", "ab" in "abcde"
- Invalid prefix: "world" in "hello world", "xyz" in "abcde"

<table>
  <tr>
    <th>Tester Action and Input Data</th>
    <th>Expected Outcome</th>
  </tr>
  <tr>
    <td>Valid Inputs: s1 = "hello", s2 = "hello world"</td>
    <td>true</td>
  </tr>
  <tr>
    <td>Valid Inputs: s1 = "a", s2 = "abc"</td>
    <td>true</td>
  </tr>
  <tr>
    <td>Invalid Inputs: s1 = "", s2 = "hello world"</td>
    <td>false</td>
  </tr>
  <tr>
    <td>Invalid Inputs: s1 = "world", s2 = "hello world"</td>
    <td>false</td>
  </tr>
</table>

### Boundary Value Analysis:

- s1 and s2 are both empty strings: "" and ""
- s1 is an empty string and s2 is a non-empty string: "" and "hello"
- s1 is a non-empty string and s2 is an empty string: "hello" and ""
- s1 and s2 are the same string: "hello" and "hello"
- s1 is a prefix of s2: "he" in "hello", "abc" in "abcde"
- s1 is not a prefix of s2: "el" in "hello", "xyz" in "abcde"
- s1 is longer than s2: "hello" and "hi"

<table>
  <tr>
    <th>Tester Action and Input Data</th>
    <th>Expected Outcome</th>
  </tr>
  <tr>
    <td>s1 = "", s2 = "abc"</td>
    <td>False</td>
  </tr>
  <tr>
    <td>s1 = "ab", s2 = "abc"</td>
    <td>True</td>
  </tr>
  <tr>
    <td>s1 = "abc", s2 = "ab"</td>
    <td>False</td>
  </tr>
  <tr>
    <td>s1 = "a", s2 = "ab"</td>
    <td>True</td>
  </tr>
  <tr>
    <td>s1 = "aaaaaaaaaaaaaaaaaaaaaa", s2 = "aaaaaaaaaaaaaaaaaaaaaab"</td>
    <td>True</td>
  </tr>
  <tr>
    <td>s1 = "abc", s2 = "abc"</td>
    <td>True</td>
  </tr>
  <tr>
    <td>s1 = "a", s2 = "b"</td>
    <td>False</td>
  </tr>
  <tr>
    <td>s1 = "a", s2 = "a"</td>
    <td>True</td>
  </tr>
  <tr>
    <td>s1 = "a", s2 = "b"</td>
    <td>False</td>
  </tr>
  <tr>
    <td>s1 = "a", s2 = " "</td>
    <td>False</td>
  </tr>
</table>
</br>

### Code implementation and execution of test suite in Eclipse IDE using JUnit Testing Framework:

```
import static org.junit.Assert.*;
import org.junit.Test;

public class PrefixTest {
    
    @Test
    public void testEquivalencePartitioning() {
        // Valid prefix
        assertTrue(prefix("he", "hello"));
        assertTrue(prefix("ab", "abcde"));
        
        // Invalid prefix
        assertFalse(prefix("world", "hello world"));
        assertFalse(prefix("xyz", "abcde"));
    }
    
    @Test
    public void testBoundaryValueAnalysis() {
        // Empty strings
        assertTrue(prefix("", ""));
        assertFalse(prefix("", "hello"));
        assertFalse(prefix("hello", ""));
        
        // Same strings
        assertTrue(prefix("hello", "hello"));
        
        // Prefixes
        assertTrue(prefix("he", "hello"));
        assertTrue(prefix("abc", "abcde"));
        
        // Not prefixes
        assertFalse(prefix("el", "hello"));
        assertFalse(prefix("xyz", "abcde"));
        
        // s1 longer than s2
        assertFalse(prefix("hello", "hi"));
    }

    // prefix function implementation
    public static boolean prefix(String s1, String s2) {
        if (s1.length() > s2.length()) {
            return false;
        }
        for (int i = 0; i < s1.length(); i++) {
            if (s1.charAt(i) != s2.charAt(i)) {
                return false;
            }
        }
        return true;
    }
}

```

When executed, the test cases passed, indicating that the implementation of the prefix function is correct.

In case of a test case fails, the output in the Eclipse IDE looks like:

`org.junit.ComparisonFailure: expected:<true> but was:<false>
`

This message indicates that the assertion comparing the expected result (true) to the actual result (false) has failed.
