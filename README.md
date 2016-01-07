# ZigZag-Conversion
LeetCodeOJ Algorithms Question6 ZigZag Conversion

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

	题目中考虑的都是三行的，如果换成四行怎么办，换成两行怎么办。观察之后发现它本身成反写N排列，脑海中出现两种思路。
	1. 根据N排序后找规律，根据不同的numRows,找出排序后对应的关系比如，numRows=3 ,则排序后的值为0,4,8,1,3,5,7,2,6；numRows=4，则排序后的值为0,6,12,1,5,7,11,2,4,8,10,3,9；numRows=5，则排序后的值为0,8,16,1,7,9,15,2,6,10,14,3,5,11,13,4,12。但是没找出非常符合逻辑的规律
	2. 将String遍历，在遍历过程中将其分组，慢慢将之归入不同的String中，再按顺序将排序后的String相加起来，就可以得到。在尝试中发现貌似可行，按此逻辑开始编码。
	后来将两者结合发现，按照取余进行存储排序，将i对temp(2*numRows-2)进行取余，如果temp<numRows则归入不同的余数中，如果temp>=numRows，则归入不同的(temp-余数),这样能符合向下的正序和向上的逆序。
	
code:

	public class Solution {
    public static String convert(String s, int numRows) {
        String result = "";
        Map<Integer, String> map = new HashMap<Integer, String>();
        if (s == "" || s == null) {
            return "";
        }
        int temp = (2 * numRows - 2)==0? 1 : (2 * numRows - 2);
        for (int i = 0; i < s.length(); i++) {
            if (String.valueOf(s.charAt(i)).equals("") || String.valueOf(s.charAt(i)).equals(" ")) {
                continue;
            }
            int remainder = i % temp;
            if (remainder >= numRows){
                remainder = temp - remainder;
            }

            if (map.get(remainder) == null) {
                map.put(remainder, String.valueOf(s.charAt(i)));
            } else {
                String str = map.get(remainder);
                str = str + String.valueOf(s.charAt(i));
                map.put(remainder, str);
            }

        }
        Iterator iter = map.entrySet().iterator();
        while (iter.hasNext()) {
            Map.Entry entry = (Map.Entry) iter.next();
            Object val = entry.getValue();
            if (val != null) {
                result += val.toString();
            }
        }
        return result;
    }
	}
