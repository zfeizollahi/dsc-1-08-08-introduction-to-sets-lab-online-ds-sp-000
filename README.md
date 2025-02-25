
# Introduction to Sets - Lab

## Introduction

Probability theory is all around. A common example is in the game of poker or related card games, where players try to calculate the probability of winning a round given the cards they have in their hands. Also in the business context probabilities play an important role. Operating in an volatile economy, companies need to take uncertainty into account and this is exactly where probability theory plays a role.

As mentioned in the lesson before, a good understanding of probability starts with understanding of sets and set operations. That's exactly what you'll learn in this lab!

## Objectives

You will be able to:

- Have a better sense of what sets, universal sets, and subsets are
- Know how to perform common set operations in Python 
- Learn how to use Venn Diagrams to understand about the relationships between sets


## Exploring set operations using a Venn Diagram

Let's start with a pretty conceptual example. Let's consider the following sets:

   - $\Omega$ = positive integers between [1, 12]
   - $A$= even numbers between [1, 10]
   - $B = \{3,8,11,12\}$
   - $C = \{2,3,6,8,9,11\}$
    

#### a. Illustrate all the sets in a Venn Diagram like the one below. The rectangular shape represents the universal set.

![title](venn_diagr.png)

#### b. Using your Venn Diagram, list the elements in each of the following sets:

- $ A \cap B$
- $ A \cup C$
- $A^c$ 
- The absolute complement of B
- $(A \cup B)^c$
- $B \cap C'$
- $A\backslash B$
- $C \backslash (B \backslash A)$ 
- $(C \cap A) \cup (C \backslash B)$
        
#### c. As seen in the lecture, you can easily create sets in Python as well. For the remainder of this exercise, let's  create sets A, B and C and universal set U in Python and test out the results you came up with.


```python
# Create set A
A = set(range(2,11,2))
'Type A: {}, A: {}'.format(type(A), A)
```




    "Type A: <class 'set'>, A: {2, 4, 6, 8, 10}"




```python
# Create set B
B = set([3,8,11,12])
'Type B: {}, B: {}'.format(type(B), B)
```




    "Type B: <class 'set'>, B: {8, 11, 3, 12}"




```python
# Create set C
C = set([2,3,6,8,9,11])
'Type C: {}, C: {}'.format(type(C), C)
```




    "Type C: <class 'set'>, C: {2, 3, 6, 8, 9, 11}"




```python
# Create universal set U
U = set(range(1, 13, 1))
'Type U: {}, U: {}'.format(type(U), U)
```




    "Type U: <class 'set'>, U: {1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12}"



Now, verify your answers in section 1 by using the correct methods in Python. To provide a little bit of help, you can find a table with common operations on sets below.

| Method        |	Equivalent |	Result |
| ------                    | ------       | ------    |
| s.issubset(t)             |	s <= t     | test whether every element in s is in t
| s.issuperset(t)           |	s >= t     | test whether every element in t is in s
| s.union(t)                |	s $\mid$ t | new set with elements from both s and t
| s.intersection(t)         |	s & t      | new set with elements common to s and t
| s.difference(t)           |	s - t 	   | new set with elements in s but not in t
| s.symmetric_difference(t) |	s ^ t      | new set with elements in either s or t but not both

#### 1. $ A \cap B$


```python
A_inters_B =  A.intersection(B)
A_inters_B
```




    {8}



#### 2. $ A \cup C $


```python
A_union_C = A.union(C)
A_union_C
```




    {2, 3, 4, 6, 8, 9, 10, 11}



#### 3.  $A^c$ (you'll have to be a little creative here!)


```python
A_comp = U.difference(A) # or A_comp = U-A
A_comp
```




    {1, 3, 5, 7, 9, 11, 12}



#### 4.  $(A \cup B)^c $


```python
A_union_B_comp = U - (A | B) 
A_union_B_comp
```




    {1, 5, 7, 9}




```python
U.difference(A.union(B))
```




    {1, 5, 7, 9}



#### 5. $B \cap C' $


```python
B_inters_C_comp =  B.intersection(U.difference(C))
B_inters_C_comp
```




    {12}



#### 6. $A\backslash B$


```python
A_min_B = A - B
A_min_B
```




    {2, 4, 6, 10}




```python
A.difference(B)
```




    {2, 4, 6, 10}



#### 7. $C \backslash (B \backslash A) $


```python
C_min_B_min_A= C - (B - A)
C_min_B_min_A
```




    {2, 6, 8, 9}



#### 8.  $(C \cap A) \cup (C \backslash B)$


```python
C_inters_A_union_C_min_B= (C & A) | (C - B)
C_inters_A_union_C_min_B
```




    {2, 6, 8, 9}



## The Inclusion Exclustion Principle

Use A, B and C from exercise one to verify the inclusion exclusion principle in Python. What you'll do is translate the left hand side of the equation for the inclusion principle in the object `left_hand_eq`, and the right hand side in the object `right_hand_eq` and see if the results are the same.


```python
left_hand_eq = len(A | B | C)
print(left_hand_eq)  # 9
```

    9



```python
right_hand_eq = len(A) + len(B) + len(C) + len(A & B) - len(A & C) - len(B & C) - len(A & B & C)
print(right_hand_eq) # 9
```

    9



```python
left_hand_eq == right_hand_eq # needs to say "True"
```




    True



## Set Operations in Python

Mary is preparing for a road trip from her hometown, Boston, to Chicago. She has quite a few pets, yet luckily, so do her friends. They try to make sure that they take care of each other's pets while someone is away on a trip. A month ago, each respective person's pet collection was given by the following three sets:


```python
Nina = set(["Cat","Dog","Rabbit","Donkey","Parrot", "Goldfish"])
Mary = set(["Dog","Chinchilla","Horse", "Chicken"])
Eve = set(["Rabbit", "Turtle", "Goldfish"])
```

In this exercise, you'll be able to use the following operations:

|Operation                          |	Equivalent |	Result|
| ------                            | ------       | ------   |
|s.update(t)                        | 	$s \mid t$ 	   |return set s with elements added from t|
|s.intersection_update(t)           | 	s &= t     |	return set s keeping only elements also found in t|
|s.difference_update(t)             |	s -= t 	   |return set s after removing elements found in t|
|s.symmetric_difference_update(t)   |	s ^= t 	   |return set s with elements from s or t but not both|
|s.add(x)                           |	           |	add element x to set s|
|s.remove(x)                        |	           |	remove x from set s|
|s.discard(x)                       |	           |	removes x from set s if present|
|s.pop()                            | 	           |	remove and return an arbitrary element from s|
|s.clear()            	            |  	           |remove all elements from set s|

Sadly, Eve's turtle passed away last week. Let's update her pet list accordingly.


```python
Eve.remove('Turtle')
Eve # should be {'Rabbit', 'Goldfish'}
```




    {'Goldfish', 'Rabbit'}



This time around, Nina promised to take care of Mary's pets while she's awat. but also wants to make sure her pets are well taken care of. As Nina is already spending a considerable amount of time taking care of her own pets, adding a few more won't make that much of a difference. Nina does want to update her list while Marie is away. 


```python
Nina.update(Mary)
Nina # {'Chicken', 'Horse', 'Chinchilla', 'Parrot', 'Rabbit', 'Donkey', 'Dog', 'Cat', 'Goldfish'}
```




    {'Cat',
     'Chicken',
     'Chinchilla',
     'Dog',
     'Donkey',
     'Goldfish',
     'Horse',
     'Parrot',
     'Rabbit'}



Mary, on the other hand, wants to clear her list altogether while away:


```python
Mary.clear()
Mary  # set()
```




    set()



Look at how many species Nina is taking care of right now.


```python
n_species_Nina = len(Nina)
n_species_Nina # 9
```




    9



Taking care of this many pets is weighing heavy on Nina. She remembered Eve had a smaller collection of pets lately, and that's why she asks Eve to take care of the common species. This way, the extra pets are not a huge effort on Eve's behalf. Let's update Nina's pet collection.


```python
Nina.pop()
Nina.pop()
len(Nina) # 7
```




    7



Taking care of 7 species seems doable for Nina!

## Writing down the elements in a set


Mary dropped off her Pet's at Nina's house, and finally made her way to the highway. Awesome, her vacation has begun!
She's approaching an exit. At the end of this particular highway exit, cars can either turn left (L), go straight (S) or turn right (R). It's pretty busy and there are two cars driving close to her. What we'll do now is create several sets. You won't be using Python here, it's sufficient to write the sets down on paper. A good notion of sets and subsets will help you calculate probabilities in the next lab!

a. Create a set $A$ of all possible outcomes assuming that all three cars drive in the same direction.
           
b. Create a set $B$ of all possible outcomes assuming that all three cars drive in a different direction.
             
c. Create a set $C$ of all possible outcomes assuming that exactly 2 cars turn right.
            
d. Create a set $D$ of all possible outcomes assuming that exactly 2 cars drive in the same direction.

                          
e. Write down the interpretation and give all possible outcomes for the sets denoted by:
 - I. $D'$ 
 - II. $C \cap D$, 
 - III. $C \cup D$. 

## Optional exercise: European Countries

Use set operations to determine which European countries are not in the European Union. You just might have to clean the data first with pandas.


```python
import pandas as pd

#Load Europe and EU
europe = pd.read_excel('Europe_and_EU.xlsx', sheet_name = 'Europe') 
eu = pd.read_excel('Europe_and_EU.xlsx', sheet_name = 'EU')

```


```python
europe.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Rank</th>
      <th>Country</th>
      <th>Population</th>
      <th>% of population</th>
      <th>Average relative annual growth (%)</th>
      <th>Average absolute annual growth</th>
      <th>Estimated doubling time (Years)</th>
      <th>Official figure (where available)</th>
      <th>Date of last figure</th>
      <th>Regional grouping</th>
      <th>Source</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1.0</td>
      <td>Russia</td>
      <td>143964709</td>
      <td>17.15</td>
      <td>0.19</td>
      <td>294285</td>
      <td>368</td>
      <td>146839993</td>
      <td>2017-01-01 00:00:00</td>
      <td>EAEU</td>
      <td>[1]</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2.0</td>
      <td>Germany</td>
      <td>82521653</td>
      <td>9.80</td>
      <td>1.20</td>
      <td>600000</td>
      <td>90</td>
      <td>82800000</td>
      <td>2016-12-31 00:00:00</td>
      <td>EU</td>
      <td>Official estimate</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3.0</td>
      <td>Turkey</td>
      <td>80810000</td>
      <td>9.60</td>
      <td>1.34</td>
      <td>1035000</td>
      <td>52</td>
      <td>77695904</td>
      <td>2016-12-31 00:00:00</td>
      <td>NaN</td>
      <td>[2]</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4.0</td>
      <td>France</td>
      <td>65233271</td>
      <td>7.76</td>
      <td>0.39</td>
      <td>261022</td>
      <td>177</td>
      <td>66991000</td>
      <td>2017-03-01 00:00:00</td>
      <td>EU</td>
      <td>[3]</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5.0</td>
      <td>United Kingdom</td>
      <td>65110276</td>
      <td>7.75</td>
      <td>0.75</td>
      <td>484000</td>
      <td>92</td>
      <td>66573504</td>
      <td>2016-12-30 00:00:00</td>
      <td>EU</td>
      <td>Official estimate</td>
    </tr>
  </tbody>
</table>
</div>




```python
eu.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Rank</th>
      <th>Country</th>
      <th>2017 population</th>
      <th>% of pop.</th>
      <th>Average relative annual growth</th>
      <th>Average absolute annual growth</th>
      <th>Official figure</th>
      <th>Date of last figure</th>
      <th>Source</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Germany</td>
      <td>82800000</td>
      <td>16.18</td>
      <td>0.76</td>
      <td>628876</td>
      <td>82576900</td>
      <td>2017-03-31</td>
      <td>Official estimate</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>France</td>
      <td>67210459</td>
      <td>13.10</td>
      <td>0.40</td>
      <td>265557</td>
      <td>67174000</td>
      <td>2018-01-01</td>
      <td>Monthly official estimate</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>United Kingdom</td>
      <td>65808573</td>
      <td>12.86</td>
      <td>0.65</td>
      <td>428793</td>
      <td>65648100</td>
      <td>2017-06-30</td>
      <td>Official estimate</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>Italy</td>
      <td>60589445</td>
      <td>11.84</td>
      <td>-0.13</td>
      <td>-76001</td>
      <td>60494000</td>
      <td>2018-01-01</td>
      <td>Monthly official estimate</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>Spain</td>
      <td>46528966</td>
      <td>9.09</td>
      <td>0.19</td>
      <td>89037</td>
      <td>46549045</td>
      <td>2017-07-01</td>
      <td>Official estimate</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Use pandas to remove any whitespace from names
eu['Country'] = eu['Country'].apply(lambda x: x.strip())
europe['Country'] = europe['Country'].apply(lambda x: x.strip())
```


```python
europe.head(3) #preview dataframe
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Rank</th>
      <th>Country</th>
      <th>Population</th>
      <th>% of population</th>
      <th>Average relative annual growth (%)</th>
      <th>Average absolute annual growth</th>
      <th>Estimated doubling time (Years)</th>
      <th>Official figure (where available)</th>
      <th>Date of last figure</th>
      <th>Regional grouping</th>
      <th>Source</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1.0</td>
      <td>Russia</td>
      <td>143964709</td>
      <td>17.15</td>
      <td>0.19</td>
      <td>294285</td>
      <td>368</td>
      <td>146839993</td>
      <td>2017-01-01 00:00:00</td>
      <td>EAEU</td>
      <td>[1]</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2.0</td>
      <td>Germany</td>
      <td>82521653</td>
      <td>9.80</td>
      <td>1.20</td>
      <td>600000</td>
      <td>90</td>
      <td>82800000</td>
      <td>2016-12-31 00:00:00</td>
      <td>EU</td>
      <td>Official estimate</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3.0</td>
      <td>Turkey</td>
      <td>80810000</td>
      <td>9.60</td>
      <td>1.34</td>
      <td>1035000</td>
      <td>52</td>
      <td>77695904</td>
      <td>2016-12-31 00:00:00</td>
      <td>NaN</td>
      <td>[2]</td>
    </tr>
  </tbody>
</table>
</div>




```python
eu.head(3)
```


```python
s = pd.Series([1, 2, 3, 1, 1, 4])

In [2]: s.unique()
Out[2]: array([1, 2, 3, 4])

In [3]: set(s)
Out[3]: {1, 2, 3, 4}
```


```python
eu_set = set(eu["Country"].unique())
europe_set = set(europe['Country'].unique())
```


```python
europe_set - eu_set
```




    {'Albania',
     'Andorra',
     'Armenia',
     'Azerbaijan',
     'Belarus',
     'Bosnia and Herzegovina',
     'Faroe Islands (Denmark)',
     'Georgia',
     'Gibraltar (UK)',
     'Guernsey (UK)',
     'Iceland',
     'Isle of Man (UK)',
     'Jersey (UK)',
     'Kosovo',
     'Liechtenstein',
     'Macedonia',
     'Moldova',
     'Monaco',
     'Montenegro',
     'Norway',
     'Russia',
     'San Marino',
     'Serbia',
     'Svalbard (Norway)',
     'Switzerland',
     'Turkey',
     'Ukraine',
     'Vatican City',
     'Åland Islands (Finland)'}



## Summary

In this lab, you practiced your knowledge on sets, such as common set operations, the use of Venn Diagrams, the inclusion exclusion principle, and how to use sets in Python! 
