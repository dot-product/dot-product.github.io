
## Numpy

We discuss following features of numpy 

   - ndarray (N dimensional Array)
   - Indexing and Slicing
   - Vectorization
   - Broadcasting
   - Important Numpy Operations(functions) in ML/DL Algorithms 
    
    


```python
import numpy as np
```

### ndarray



```python
# create ndarray from a list 

l = [[1,2,3],[4,5,6]]
nd_array = np.array(l, dtype=np.int8)

# shape
print 'shape : \n',nd_array.shape

# size = # of elements

print 'size : \n',nd_array.size

#array from tuples

tup = ((1,2,3),(4,5,6))
tup_array = np.array(tup)
print 'Tuple array  :\n',tup_array

#Number of dimensions
print "Number of Dimensions :\n",nd_array.ndim
```

    shape : 
    (2, 3)
    size : 
    6
    Tuple array  :
    [[1 2 3]
     [4 5 6]]
    Number of Dimensions :
    2


### Indexing and Slicing

   - Slicing returns view of original array. Changing elements in Slice will affect Original Array.
   - copy() function duplicates the array.


```python
X = np.arange(250).reshape(25,10) # arange gives array sequence and reshape converts this sequence into ndarray
print 'Shape of X : \n', X.shape

#access particular element in ith row and jth column
X_ij = X[4,5]
print X_ij

# acess all elements in a row
X_i = X[4,:]
print "Elements in 4 th row \n",X_i

# access all elements in a column
X_j = X[:,5]
print "Elements in 5 th column \n", X_j

# Access last element in 0th row
last = X[0,-1]
print "Last element in 0 th row \n", last


#Indexing with Boolean array ; this kind of indexing is used more in Pandas DataFrames.

Y = np.arange(15)
print "Elements in Y : \n",Y
less_Y = Y<10
print "Boolean array \n",less_Y
print "Elements less than 10 in Y: \n",Y[less_Y]


# Indexing with a list. This is useful if you want to shuffle your data
data = X[:3,:]
index = np.arange(3)
shuf_Y = np.random.shuffle(index)
print "Data before shuffle : \n", data
print "Shuffled index \n", index
print "Shuffled data : \n", data[index]
```

    Shape of X : 
    (25, 10)
    45
    Elements in 4 th row 
    [40 41 42 43 44 45 46 47 48 49]
    Elements in 5 th column 
    [  5  15  25  35  45  55  65  75  85  95 105 115 125 135 145 155 165 175
     185 195 205 215 225 235 245]
    Last element in 0 th row 
    9
    Elements in Y : 
    [ 0  1  2  3  4  5  6  7  8  9 10 11 12 13 14]
    Boolean array 
    [ True  True  True  True  True  True  True  True  True  True False False
     False False False]
    Elements less than 10 in Y: 
    [0 1 2 3 4 5 6 7 8 9]
    Data before shuffle : 
    [[ 0  1  2  3  4  5  6  7  8  9]
     [10 11 12 13 14 15 16 17 18 19]
     [20 21 22 23 24 25 26 27 28 29]]
    Shuffled index 
    [2 1 0]
    Shuffled data : 
    [[20 21 22 23 24 25 26 27 28 29]
     [10 11 12 13 14 15 16 17 18 19]
     [ 0  1  2  3  4  5  6  7  8  9]]


### Vectorization

   - Vectorization makes code more pythonic and efficient.
   - Try to use vectorization where ever possible in ML Algos.
   - Math expressions can be implemented with ease.
   - No explicit looping, which makes concise code with less bugs.
   
   


```python
#X,Y are two lists with 500 elements.
X = [1,2,3,4,5]*100
print "Length of X :\n",len(X)
Y = [6,7,8,9,10]*100
print "Length of Y :\n", len(Y)

X_arr = np.array(X)
Y_arr = np.array(Y)
print 'Shape of X_arr \n',X_arr.shape
print 'Shape of Y_arr \n',Y_arr.shape

```

    Length of X :
    500
    Length of Y :
    500
    Shape of X_arr 
    (500,)
    Shape of Y_arr 
    (500,)



```python
%%timeit -n 1 -r 1
result = []
for x in X:
    for y in Y:
        result.append(x*y)
        
```

    1 loop, best of 1: 50.7 ms per loop



```python
%%timeit -n 1 -r 1
result  = np.multiply(X_arr, Y_arr)
```

    1 loop, best of 1: 26.9 µs per loop


### Broad Casting

   - numpy uses broadcasting while performing any operations on two arrays.
   - It broadcasts smaller array to larger array so that they both are compatible.
   
 Two dimensions are equal iff 
 
   -  Both are equal (or)
   -  One of them is 1
 


```python
a = np.array([1,2,3])
b = np.array([2,2,2])

```


```python
#both have same effect, later one uses broadcasting.
result = a*b
result1 = a*2
```


```python
# adding constant to array. This is used in ML algos, where bias is added to weight, data inner product
print "Before adding a constant \n",a
const_sum = a + 5
print "After Constatn addition \n", const_sum

A = np.arange(6).reshape(3,2)
print "A : Before adding a constant \n",A
const_sum = A + 5
print "A : After adding constant \n",const_sum

# broadcast constants columnwise
print 'Shape of A \n', A.shape
bias = np.array([3,5])
print 'Shape of bias \n', bias.shape
const_sum = A + bias.T
print 'Sum of A, bias \n', const_sum

# broadcast constants rowwise
bias = np.array([3,5,7]).reshape(3,1)
print 'Shape of bias',bias.shape
const_sum = A + bias.reshape((3,1))
print 'Sum of A, bias \n ', const_sum

```

    Before adding a constant 
    [1 2 3]
    After Constatn addition 
    [6 7 8]
    A : Before adding a constant 
    [[0 1]
     [2 3]
     [4 5]]
    A : After adding constant 
    [[ 5  6]
     [ 7  8]
     [ 9 10]]
    Shape of A 
    (3, 2)
    Shape of bias 
    (2,)
    Sum of A, bias 
    [[ 3  6]
     [ 5  8]
     [ 7 10]]
    Shape of bias (3, 1)
    Sum of A, bias 
      [[ 3  4]
     [ 7  8]
     [11 12]]



```python
# broad cast on different axes
import random
image = np.array(random.sample(xrange(50),4*4*3)).reshape(4,4,3)
scale = np.array([2,3,4]).reshape(1,1,3)

print "Shape of Image :\n ",image.shape
print "Shape of Scale : \n ",scale.shape

print "Image  : \n", image
print "Scale  :  \n",scale

result = np.multiply(image,scale)

print "Result after Scaling across different axes : \n", result

```

    shape of Image :
      (4, 4, 3)
    Shape of scale : 
      (1, 1, 3)
    Image  : 
    [[[12 29 46]
      [38 13 39]
      [45 16  2]
      [18 24 23]]
    
     [[31  1 43]
      [30  9 33]
      [21  5 10]
      [19 32 40]]
    
     [[44 25 37]
      [15 28  8]
      [27 48 14]
      [47 36  4]]
    
     [[ 3 20 42]
      [ 0 26 49]
      [35  6  7]
      [34 17 41]]]
    Scale  :  
    [[[2 3 4]]]
    Result after Scaling across different axes : 
    [[[ 24  87 184]
      [ 76  39 156]
      [ 90  48   8]
      [ 36  72  92]]
    
     [[ 62   3 172]
      [ 60  27 132]
      [ 42  15  40]
      [ 38  96 160]]
    
     [[ 88  75 148]
      [ 30  84  32]
      [ 54 144  56]
      [ 94 108  16]]
    
     [[  6  60 168]
      [  0  78 196]
      [ 70  18  28]
      [ 68  51 164]]]


### Important Matrix Operations 



```python
# Lets define two matrics 

A = np.random.randn(2,3)
B = np.random.randn(3,2)

print 'Matrix A : \n', A
print "Matrix B : \n", B

# Transpose of A
A_T = A.T
print "Shape of A : \n", A.shape
print "Shape of A_T: \n",A_T.shape

# Matrix Addition
A_plus_B = A_T + B


# Matrix Subtraction
A_minus_B = A_T - B


# Multply matrix with constant
alpha = 0.5
alpha_mul_B = alpha * B

# Divide matrix with constant

alpha_div_B = B/alpha

# Inverse of Matrix

C = np.array([[1,5],[3,2]])
C_inv = np.invert(C)


# Sum elements w.r.t axis.

column_sum = np.sum(B, axis=0) # columwise sum
row_sum    = np.sum(B, axis=1) # rowwise sum
print "Matrix Shape : \n",B.shape
print "Column Sum shape: \n",column_sum.shape
print "Row sum shape: \n", row_sum.shape


# Elementwise multiplicaiton 
ele_mul = A_T * B 

# Dot product 
dot_prod = np.dot(A,B)  # In python > 3.5 we can use @ for dot product






```
