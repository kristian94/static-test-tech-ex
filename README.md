# static-test-tech-ex

triangle ex repo: https://github.com/kristian94/triangle

## 2. Static Code Analysis of Triangle Program

#### a) Analysis tool

I installed "complexity-report", a tool for statically analyzing Javascript (Node.js) code. The tool is run from the command line
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

#### c)

Metrics for my application can be found here:

 - Before refactoring: https://github.com/kristian94/static-test-tech-ex/blob/master/metrics/metrics-pre.json

 - After refactoring: https://github.com/kristian94/static-test-tech-ex/blob/master/metrics/metrics-post.json

#### d)

The tool uses McCabe's CC variation

#### e, d)

The refactoring i did was based on the results of my unit tests (https://github.com/kristian94/triangle/blob/master/test.js)
The tests revealed that my "isIsosceles" function would also return true for triangles with 3 of the same side. 

![alt text](https://github.com/kristian94/static-test-tech-ex/blob/master/img/not%20passed.PNG)

I edited the function to return false in cases where the sides were all equal, which made the tests pass:

![alt text](https://github.com/kristian94/static-test-tech-ex/blob/master/img/passed.PNG)

## 3. Peer Review Checklist

The checklist is a number of practices that can be applied when reviewing the code of a fellow programmer, and is divided
into 10 tips. The first tip is to review fewer than 400 lines of code at a time. The reasoning behind this, is that the brain
can only effectively process so much information, so to get a quality review, this limit should not be exceeded. Tip #2 is to
take your time and not rush the review. This is, in accordance with tip #1, about keeping the quality of the review at a
certain level. If the review is not accurate and does not discover a high enough percentage of the bugs in the code, it can
be more misleading than helpful, since the code might not get reviewed a second time. Tip #3 is to not review for more than 60
minutes at a time. Again about keeping focus. #4 is to set goals and capture metrics. This is about measuring the effectiveness
of the review, so you can look for ways to improve the review process. #5 is that authros should annotate their code before the
review. If you have a particularly complex piece of code, annotations can be very helpful in understanding the purpose of the
code. This will make it clearer for the reviewer, where he/she needs to look for bugs in the code. #6 is to use checklists. This
is to prevent that the same mistakes are made over and over. #7 is to establish a process for fixing defects found. This is about
establishing guidelines for how to fix the bugs that are found after the review. The bugs need to be communicated effectively
to the dev, so that they can be fixed reliably. #8 is to foster a positive code review culture. Code reviews can be a delicate
matter, since the responsible dev can feel attacked. It is important to communicate in a constructive way, so that the 
relationship between the team members is not strained. 9# is to embrace the subconscious implications of the peer review. The
review in itself brings value, but the benefit of having a good review culture is that the developers will work under the 
assumption that their code is to be reviewed, and (without realising it) they will be more inclined to produce code that is 
of a higher quality. #10 is to practice lightweight code reviews. Code reviews can be time consuming and should not take
up too much of the dev teams time. There are many different ways to do it, some are more rigid and others a lighter.

## 4. Example Code Review

In the example it looks like the static variable "people" is accessed from a non-static context. I would expect the code to fail and an
exception to be raised due to this. To my knowledge you would have to access a static variable in such a context by it's class name eg:
```
Catalog.people
```
My proposed fix is to prepend all the people references with "Catalog."

## 5. Coding Standards Document

There are many standards you can apply to maintain a higher standard of coding quality. Personally, one of the most important things i look out for is the size of my files. A single file should not contain several thousand lines of code, since this makes it overly complex and harder to maintain. When i write code i try to look for oppoturnities to split my code into self-contained modules, that have as a little external dependencies as possible. When code is too reliant on other pieces of code, it creates dependencies that are hard to resolve, and it makes it difficult to make changes without breaking anything. Another thing i like to do is to always declare variables as immutable (unless i know it has to mutate). This prevents a lot of side-effects and makes your code a bit more predictable, and variables should rarely have to mutate anyway. I try to keep functions as pure as possible. This means a function should not have any side effects, and should, given the same input, always return a certain output. Functions should also be kept single-purpose to ensure reusability and easier maintainability. When working with arrays i generally use map or reduce functions over for-loops, as these produce cleaner and more readable code. I try to be consistent with variable naming, and I avoid single-letter variables.
