# static-test-tech-ex

## 2. Static Code Analysis of Triangle Program

#### a) Analysis tool

Installed "complexity-report", a tool for statically analyzing Javascript (Node.js) code. The tool is run from the command line
and produces an output file with metrics.

#### b) Results of initial anlysis

The first analysis produced a bunch of metrics. The first one i looked at was the Cyclomatic Complexity of the code. The focus on the metrics of the functions the Triangle Object used to determine the properties of the triangle:

| Function      | CC           |
| ------------- |-------------:|
| isEquilateral |  1     |
| isIsosceles   |  3     |
| isScalene     |  1     |

Looking at the numbers in relation to the purpose of the functions, they seem pretty reasonable.

The Triangle is constructed from 3 integers, representing side lengths, and these values are stored as a, b and c.

The function "isEquilateral" will check if all the sides are the same, therefore there is only 1 test case needed to check the happy path, that is any test case where a triangle is created from 3 matching side lengths (a, b and c's values are the same). The same goes for "isScalene", where the happy path test case consists of 3 unique input values for sidelengths, (a, b and c are all different). "isIsosceles", has 3 cases where the it returns true:

 - a and b are equal
 - a and c are equal
 - b and c are equal
 
This means we need 3 test cases to check all the happy path cases.

With this in mind, it would be hard to reduce the CC value for the function. You could reduce the amount of conditional statements by instead iterating over the 3 values, counting occurences of unique values, and return true if the occurence of a value equated to 2, but this would probably make the function harder to understand and would not really serve to improve maintainablitiy, performance or anything like that.

