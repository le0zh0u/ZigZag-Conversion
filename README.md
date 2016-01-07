# ZigZag-Conversion
LeetCodeOJ Algorithms Question3 ZigZag Conversion

Question Name :
ZigZag Conversion

The string `"PAYPALISHIRING"` is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)

````
P   A   H   N
A P L S I I G
Y   I   R
````
And then read line by line: `"PAHNAPLSIIGYIR"`
Write the code that will take a string and make this conversion given a number of rows:

````
string convert(string text, int nRows);
````
`convert("PAYPALISHIRING", 3)` should return `"PAHNAPLSIIGYIR"`.

thinking:

	题目中考虑的都是三行的，如果换成四行怎么办，换成两行怎么办。观察之后发现它本身成反写N排列，打算以这个思路进行码代码。
