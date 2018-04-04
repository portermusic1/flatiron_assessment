# Flatiron School Data Science Assessment 

## Introduction:

In the real world as data scientists and statisticians, we often talk about the
abstract idea of a population and a sample. Simply put, a __POPULATION__ is a
collection of elements in its entirety, and as analysts, we're often concerned
with studying interesting phenotypes of the elements as a whole.

Within a population containing n elements, there exists 2<sup>n</sup> different
combinations. Each individual combination represents a __SAMPLE__ of the
larger population, and due to the differences in element groupings,
each sample's phenotype naturally differs from one and another.

As researchers we're either compelled or forced (due to lack of an 
entire population to test) to study an individual sample, or the
differences between multiple samples, all with the purpose of further
understanding the greater population in question as a whole.


## Learning Objectives:

By studying a simulated real-world analyst problem, we will:
1) Develop a functional mathematical language to
    describe populations and samples using _Set Theory_
2) Implement some of this language in Python
    while discussing the version's pros and cons
3) Learn about the Python 'sets' module, which contains highly optimized data
    structures and operations for set theory programming


## The Problem:

### Background:


Imagine a high school made up of 17 students. A survey was given to the entire
student population by the school's administration to help understand the
student's differences in subject preferences.

The administration believes that by creating new courses based on student's
subject preferences, they may see a statistically significant improvement in classroom participation.

### Data:

Below are the survey results:

| Student | Comp. Sci. | English | Gym | History | Math | Science |
| --- | --- | --- | --- | --- | --- | --- |
Bernarda  | 0 | 1 | 0 | 0 | 0 | 1 |
Britt     | 1 | 0 | 0 | 0 | 1 | 1 |
Bryan     | 0 | 0 | 0 | 0 | 0 | 0 |
Chris     | 0 | 1 | 1 | 0 | 1 | 1 |
Collin    | 1 | 0 | 0 | 1 | 1 | 0 |
Dominica  | 0 | 1 | 0 | 0 | 1 | 1 |
Evelynn   | 0 | 1 | 1 | 0 | 1 | 1 |
Grace     | 1 | 1 | 0 | 1 | 0 | 0 |
Greg      | 0 | 1 | 0 | 1 | 0 | 1 |
Janell    | 0 | 1 | 0 | 1 | 0 | 1 |
Leslie    | 1 | 1 | 0 | 1 | 1 | 1 |
Manny     | 1 | 1 | 1 | 0 | 1 | 1 |
Mary      | 0 | 0 | 1 | 1 | 1 | 0 |
Ray       | 0 | 0 | 0 | 0 | 0 | 0 |
Romeo     | 1 | 0 | 0 | 0 | 1 | 1 |
Sharmaine | 1 | 1 | 1 | 1 | 1 | 0 |
Tammy     | 1 | 0 | 1 | 1 | 1 | 1 |


### Initial Execution:

Before the administration can even test their hypothesis, for each subject,
they need to use this data to group the entire student population into
separate subpopulations based on course preference.
These subpopulations  will represent the first set of samples.

Using Python variables and lists:

```
comp_sci   = ['Sharmaine', 'Collin', 'Romeo', 'Britt', 'Manny', 'Leslie', 'Tammy', 'Grace']
english    = ['Janell', 'Evelynn', 'Sharmaine', 'Bernarda', 'Manny', 'Greg', 'Leslie','Chris', 'Grace', 'Dominica']
gym        = ['Evelynn', 'Sharmaine', 'Manny', 'Tammy', 'Chris', 'Mary']
history    = ['Janell', 'Sharmaine', 'Collin', 'Greg', 'Leslie', 'Tammy', 'Grace', 'Mary']
math_class = ['Evelynn', 'Sharmaine', 'Collin', 'Romeo', 'Britt', 'Manny', 'Leslie', 'Tammy', 'Chris', 'Mary', 'Dominica']
science    = ['Janell', 'Evelynn', 'Bernarda', 'Romeo', 'Britt', 'Manny', 'Greg', 'Leslie', 'Tammy', 'Chris', 'Dominica']
```

Now that we've converted our survey data into the above subpopulation lists, the administration can start asking interesting questions about their student's choices.

For example, one administrator believes those students who like *Math* and *Computer Science* should be moved into a newly created course called *Data Science 101*.

Let's find which students should be in this new class using operations familiar to us already in Python.

We'll start by looking at one element from the *Math* subpopulation at a time, and check to see if that element exists within the *Computer Science* subpopulation. If it does exist in both subpopulations, we'll add the student's name to a list called *data_science*, which represents all of the students that should be placed in the new _Data Science 101_ course.

In Python:

```
data_science = [] # the roster of students who should be in the new data science course

for student_m in math_class: # for each student that likes math
    for student_cs in comp_sci: # search the comp_sci subpopulation and
        if student_m == student_cs: # check to see if they also like comp_sci
            data_science.append(student_m) # then add their name to the roster if so
        else:
            pass # otherwise do not add the student to the roster and skip

>>> print data_science
['Sharmaine', 'Collin', 'Romeo', 'Britt', 'Manny', 'Leslie', 'Tammy']
```

### Mathematical Background: Set Theory Introduction

The administration now has a list of students that should be in the new *Data Science 101* course.

The idea of testing conditions between multiple sets as we did with the nested for loop above is not unique to coding, but comes from a field of math called Set Theory. That specific example finds the __INTERSECTION__ between two sets, that is, it returns the collection of elements that are _CONTAINED WIHTIN BOTH SETS_. An intersection is an example of a __SET OPERATION__: an operations that can be performed on sets.

There are several other operations, but the main four are the _UNION_, _INTERSECTION_, _DIFFERENCE_, and _SYMMETRIC DIFFERENCE_. 

### The Pythons 'sets' Module

Unfortunately, our implementation is actually quite slow. For this example with small lists, it runs pretty quickly, but imagine in a real world situation where we'd like to give a course preference survey to every high school student in the United States.

Given this much larger population, we'd expect to have a larger number of students contained in our subject preference subpopulations.

For a large  number of students like this, our for loop becomes inefficient, and the run-time of the algorithm increases exponentially as the number of students grow.

Fortunately, Python has the computationally efficient "sets" module that we can use, and it allows us to express our subpopulation in terms of a Python data structure called the *Set* - an unordered collection of unique elements.

### Working with the 'sets' Module

Let's convert our subpopulation lists into python sets:

```
import sets

comp_sci   = sets.Set(comp_sci)
english    = sets.Set(english)
gym        = sets.Set(gym)
history    = sets.Set(history)
math_class = sets.Set(math_class)
science    = sets.Set(science)

>>> print comp_sci
Set(['Sharmaine', 'Collin', 'Romeo', 'Britt', 'Manny', 'Leslie', 'Tammy', 'Grace'])
```

Super easy! Python even has set operations built in so we don't have to write our own versions as we did to create the *Data Science 101* roster!
 
Let's re-write our for-loop based intersection using the operations from the Python 'sets' module:

```
data_science = math_class.intersection(comp_sci) # using the intersection method on the "math-class" set

>>> print data_science
Set(['Sharmaine', 'Collin', 'Romeo', 'Britt', 'Manny', 'Leslie', 'Tammy'])
```

We completed the intersection in one line using Python's set module!
Not only is it easier to write and read, it's much more computationally efficient than the nested for loop method, and this added efficiency is necessary in real-world data science tasks.

For some syntax sugar, we can also re-write the intersection as:
 
```
data_science = math_class & comp_sci # using the & character for the intersection

>>> print data_science
Set(['Sharmaine', 'Collin', 'Romeo', 'Britt', 'Manny', 'Leslie', 'Tammy'])
```

### Three More Set Operations;  Union, Difference, and Symmetric Difference

#### Union

Turns out the administration believes that there are students in the class that would benefit from an entirely literature based curriculum. The administration believes that students that prefer either English or History tend to be the most literature inclined, and want place these students in a new course called "Book Based Learning 101" - Sounds fun!

To do this, we need the set operation called the __UNION__, which, given two sets A and B, returns a new set that contains elements that were in either set A or set B.

```
book_based_learning = english.union(history) # the union or
book_based_learning = english | history      # using the "|" char to represent the union operation

>>> print book_based_learning
Set(['Janell', 'Evelynn', 'Sharmaine', 'Collin', 'Bernarda', 'Mary', 'Manny', 'Greg', 'Leslie', 'Tammy', 'Chris', 'Grace', 'Dominica'])
```
#### Difference

In our imaginary school, it's believed that student's who like gym tend to disturb the STEM students (students who like math, science, and computer science) the most. The school principal wants to create a course called _Advanced STEM_, but wants to make sure no students who like gym are in the course. 

For this, we'll need the __DIFFERENCE__ operation, which given two sets A and B, returns a set that contains elements from set A, but not set B.

```
stem = math_class & science & comp_sci # find the intersection between the math, science, and computer science courses

>>> print stem
Set(['Britt', 'Manny', 'Leslie', 'Tammy', 'Romeo'])

advanced_stem = stem.difference(gym) # the difference or
advanced_stem = stem - gym           # using the '-' character to represent the difference

>>> print advanced_stem
Set(['Britt', 'Leslie', 'Romeo'])
```

#### Symmetric Difference

Let's look back at our new courses _Data Science 101_ and _Advanced STEM_

The admin is interested in looking to see the relationship between students in the _Data Science 101_ class and the _Advanced STEM_ class. In particular, they're interested in seeing which students are in one or the other subjects, but NOT both.

For this, we'll need the __SET DIFFERENCE__ operation, which given two sets A and B, returns a set that contains elements from set A or B, but not both.

```
one_course_or_the_other  = data_science.symmetric_difference(advanced_stem) # the symmetric difference
one_course_or_the_other  = data_science ^ advanced_stem # using the '^' character to represent the symmetric difference

>>> print one_course_or_the_other
Set(['Collin', 'Manny', 'Sharmaine', 'Tammy'])
```

## Summary:
In this lesson, we learned about Set Theory and how it can be incorporated into common data science and statistical problems. Given a real-world problem, we found our way to a solution by forming our problem in such a way that can be tackled using efficient set operations with both custom code we wrote, and using the python 'sets' module. By tackling the problem both ways, we were able to find the most computationally efficient tactic (the python set module) and learned why it's necessary in the real world.

#### Authors
This README.md file was created by Justin M. Porter for the purpose of the Flatiron School prospective employment writing assessment.
