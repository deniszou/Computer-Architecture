# Housing Price Predictor
Part 1: One-Shot Learning (50 points)
In the rst part, you will write a C program that implements simple \one-shot" machine learning algo-
rithm for predicting house prices in your area.
There is signicant hype and excitement around articial intelligence (AI) and machine learning.
CS 211 students will get a glimpse of AI/ML by implementing a simple machine learning algorithm to
predict house prices based on historical data.
For example, the price of the house (y) can depend on certain attributes of the house: number of
bedrooms (x1), total size of the house (x2), number of baths (x3), and the year the house was built (x4).
Then, the price of the house can be computed by the following equation:
y = w0 + w1:x1 + w2:x2 + w3:x3 + w4:x4 (1)
Given a house, we know the attributes of the house (i.e., x1, x2, x3, x4). However, we don't know
the weights for these attributes: w0, w1, w2, w3 and w4. The goal of the machine learning algorithm in
our context is to learn the weights for the attributes of the house from lots of training data.
Let's say we have N examples in your training data set that provide the values of the attributes and
the price. Let's say there are K attributes. We can represent the attributes from all the examples in the
training data as a Nx(K + 1) matrix as follows, which we call X:
[
1, x0;1, x0;2, x0;3, x0;4
1, x1;1, x1;2, x1;3, x1;4
1, x2;1, x2;2, x2;3, x2;4
1, x3;1, x3;2, x3;3, x3;4
...
1, xn;1, xn;2, xn;3, xn;4
]
where n is N 􀀀 1. We can represent the prices of the house from the examples in the training data
as a Nx1 matrix, which we call Y .
[
y0
y1
...
yn
]
Similarly, we can represent the weights for each attribute as a (K + 1)x1 matrix, which we call W.
1
[
w0
w1
...
wk
]
The goal of our machine learning algorithm is to learn this matrix from the training data.
Now in the matrix notation, entire learning process can be represented by the following equation,
where X, Y , and W are matrices as described above.
X*W = Y 
Using the training data, we can learn the weights using the below equation:
W = (XT *X)^(-1)*XT *Y
where XT is the transpose of the matrix X, (XT *X)^(-1) is the inverse of the matrix XT *X.
Your main task in this part to implement a program to read the training data and
learn the weights for each of the attributes. You have to implement functions to multiply matrices,
transpose matrices, and compute the inverses of the matrix. You will use the learned weights to predict
the house prices for the examples in the test data set.
Want to learn more about One-shot Learning? The theory behind this learning is not important
for the purposes of this class. The algorithm you are implementing is known as linear regression with
least square error as the error measure. The matrix ((XT *X)^(-1)*XT ) is also known as the pseudo-inverse
of matrix X.

Your goal is to write a program to compute the inverse of a matrix to perform one-shot learning.
Input/Output specification
Usage interface
Your program for this part will be executed as follows:
./first <train-data-file-name> <test-data-file-name>
where <train-data-file-name> is the name of the training data file with attributes and price of
the house. You can assume that the training data file will exist and that it is well structured. The
<test-data-file-name> is the name of the test data file with attributes of the house. You have to
predict the price of the house for each entry in the test data file.
Input specification
The input to the program will be a training data file and a test data file.
Structure of the training data file
The first line in the training file will be an integer that provides the number of attributes (K) in the
training set. The second line in the training data file will be an integer (N) providing the number of
training examples in the training data set. The next N lines represent the N training examples. Each
line for the example will be a list of comma-separated double precision 
oating point values. The first
K double precision values represent the values for the attributes of the house. The last double precision
value in the line represents the price of the house.
An example training data file (train1.txt) is shown below:

4

7

3.000000,1.000000,1180.000000,1955.000000,221900.000000
3.000000,2.250000,2570.000000,1951.000000,538000.000000
2.000000,1.000000,770.000000,1933.000000,180000.000000
4.000000,3.000000,1960.000000,1965.000000,604000.000000
3.000000,2.000000,1680.000000,1987.000000,510000.000000
4.000000,4.500000,5420.000000,2001.000000,1230000.000000
3.000000,2.250000,1715.000000,1995.000000,257500.000000
In the example above, there are 4 attributes and 7 training data examples. Each example has values
for the attributes and last value is the price of the house. To illustrate, consider the training example
below

3.000000,1.000000,1180.000000,1955.000000,221900.000000

The first attribute has value 3.000000, the second attribute has value 1.000000, third attribute has value
1180.000000, and the fourth attribute has value 1955.000000. The price of the house for these set of
attributes is provided as the last value in the line: 221900.000000

Structure of the test data file

The first line in the training file will be an integer (M) that provides the number of test data points in
the file. Each line will have K attributes. The value of K is defined in the training data file. Your goal
is predict the price of house for each line in the test data file. The next M lines represent the M test
points for which you have to predict the price of the house. Each line will be a list of comma-separated
double precision 
oating point values. There will be K double precision values that represent the values
for the attributes of the house.
An example test data (test1.txt) is shown below:

2

3.000000,2.500000,3560.000000,1965.000000
2.000000,1.000000,1160.000000,1942.000000

It indicates that you have to predict the price of the house using your training data for 2 houses. The
attributes of each house is listed in the subsequent lines.
Output specification
Your program should print the price of the house for each line in the test data file. Your program should
not produce any additional output. If the price of the house is a fractional value, then your program
should round it to the nearest integer, which you can accomplish with the following printf statement:
printf("%0.0lf\n", value);
where value is the price of the house and its type is double in C.
Your program should predict the price of the entry in the test data file by substituting the attributes
and the weights (learned from the training data set) in Equation (1).
A sample output of the execution when you execute your program as shown below,

5

./first train1.txt test1.txt

should be

737861
203060
