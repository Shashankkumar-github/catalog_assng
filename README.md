## Problem Statement

In this assignment, you'll work on a simplified version of Shamir's Secret Sharing algorithm.

Consider an unknown polynomial of degree m. You would require m+1 roots of the polynomial to solve for the coefficients, represented as k = m + 1.

An unknown polynomial of degree m can be represented as:

f(x) = a_m x^m + a_{m-1} x^{m-1} + ... + a_1 x + c

Where:

- f(x) is the polynomial function
- m is the degree of the polynomial
- a_m, a_{m-1}, ..., a_1, c are coefficients (real numbers)
- a_m ≠ 0 (since it's the highest degree term, ensuring the polynomial is of degree m)

This representation shows that a polynomial of degree m is a sum of terms, where each term is a coefficient multiplied by a power of x. The highest power of x is m, and the powers decrease by 1 for each subsequent term until we reach the constant term c, which has no x.

The task is to find the constant term i.e, ‘c’ of the polynomial with the given roots. However, the points are not provided directly but in a specific format.

You need to read the input from the test cases provided in JSON format.
Sample Test Case:
{
    "keys": {
        "n": 4,
        "k": 3
    },
    "1": {
        "base": "10",
        "value": "4"
    },
    "2": {
        "base": "2",
        "value": "111"
    },
    "3": {
        "base": "10",
        "value": "12"
    },
    "6": {
        "base": "4",
        "value": "213"
    }
}
**n:** The number of roots provided in the given JSON
**k:** The minimum number of roots required to solve for the coefficients of the polynomial
k = m + 1, where m is the degree of the polynomial

### Root Format Example:
**"2": {
    "base": "2",
    "value": "111"
}
Consider the above root as (x, y):

- x is the key of the object (in this case, x = 2)
- y value is encoded with a given base
- Decode y value: 111 in base 2 is 7
- Therefore, x = 2 and y = 7

You can use any known method to find the coefficients of the polynomial, such as:

- Lagrange interpolation
- Matrix method
- Gauss elimination

Solve for the constant term of the polynomial, typically represented as c.

### Assignment Checkpoints:

- **1. Read the Test Case (Input) from a  separate JSON file**
    - Parse and read the input provided in JSON format from a separate file, which contains a series of polynomial roots
- **2. Decode the Y Values**
    - Correctly decode the Y values that are encoded using different bases
- **3. Find the Secret (C)**
    - Calculate the secret c using the decoded Y values and any known method**
    - **Constraints:**

- All the coefficients a_m, a_{m-1}, ..., a_1, c are positive integers.
- The coefficients are within the range of a 256-bit number.
- The minimum number of roots provided (n) will always be greater than or equal to k (the minimum number of roots required).
- The degree of the polynomial (m) is determined as m = k−1, where k is provided in the input.

  
**Output:** Print secret for both the testcases simultaneously.

**Hint:** Although you can't test your code against the test case in a testing environment, you can double-check it manually by solving the polynomial on paper and comparing the outputs.

Find the second testcase here.
{
"keys": {
    "n": 10,
    "k": 7
  },
  "1": {
    "base": "6",
    "value": "13444211440455345511"
  },
  "2": {
    "base": "15",
    "value": "aed7015a346d63"
  },
  "3": {
    "base": "15",
    "value": "6aeeb69631c227c"
  },
  "4": {
    "base": "16",
    "value": "e1b5e05623d881f"
  },
  "5": {
    "base": "8",
    "value": "316034514573652620673"
  },
  "6": {
    "base": "3",
    "value": "2122212201122002221120200210011020220200"
  },
  "7": {
    "base": "3",
    "value": "20120221122211000100210021102001201112121"
  },
  "8": {
    "base": "6",
    "value": "20220554335330240002224253"
  },
  "9": {
    "base": "12",
    "value": "45153788322a1255483"
  },
  "10": {
    "base": "7",
    "value": "1101613130313526312514143"
  }
}




Solution ;----


This JavaScript code defines a class named Catalog that implements a method for finding a secret constant using Lagrange interpolation. The secret constant is derived from a set of points provided in JSON format. The code also includes example test cases that demonstrate how the class can be used.

Class Declaration:

The Catalog class contains three static methods: decodeValue, lagrangeInterpolation, and findSecretConstant.
Method: decodeValue(base, value):

This helper function converts a given string value from a specified base (numerical base) to its decimal integer equivalent.
It uses the built-in parseInt function, which takes two parameters: the string to convert and the base of the number system.
Method: lagrangeInterpolation(points, k):

This method implements Lagrange interpolation, which is a polynomial interpolation technique.
It takes an array of points (each point being a pair of x and y values) and a number k, which represents how many points are used for reconstruction.
The method calculates the constant term of the polynomial that passes through the given points using the Lagrange formula:
For each point, it calculates a corresponding Lagrange basis polynomial li and accumulates the contribution to the constant term constant.
Finally, it returns the computed constant term.
Method: findSecretConstant(inputJson):

This method takes a JSON object inputJson as input, which contains the points (in the form of keys and values) needed to find the secret constant.
It extracts the number of keys (n) and the number of keys needed for reconstruction (k).
It initializes an empty array points to store the decoded x and y values.
For each entry in the inputJson, it skips the keys metadata and:
Parses the key as the x-value and retrieves the corresponding base and value.
Decodes the value using the decodeValue method and stores the point as an array in the points array.
After sorting the points based on their x-values (for good practice), it calls the lagrangeInterpolation method to compute and return the secret constant.
Test Cases
Two test case objects, jsonString1 and jsonString2, are defined at the bottom of the code:

Each test case contains a set of points along with their respective bases and values.
The first test case has 4 keys and requires 3 for reconstruction, while the second test case has 10 keys and requires 7.
Execution
The script calls the findSecretConstant method for both test cases and stores the results in secretConstant1 and secretConstant2.
Finally, it prints the secret constants calculated for both test cases to the console.
Key Features
Decoding Values: The code supports decoding values from various numerical bases, which is crucial for the reconstruction of the polynomial.
Lagrange Interpolation: The implementation of Lagrange interpolation allows for efficient polynomial reconstruction based on given data points.
Flexibility: The code is designed to handle a variable number of input keys and can be easily extended to include additional functionality.
