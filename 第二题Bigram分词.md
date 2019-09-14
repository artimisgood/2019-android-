# 2019年暑假Android实验室考核之算法题二——Bigram分词
#### 题目：
给出第一个词 first 和第二个词 second，考虑在某些文本 text 中可能以 "first second third" 形式出现的情况，其中 second 紧随 first 出现，third 紧随 second 出现。

对于每种这样的情况，将第三个词 "third" 添加到答案中，并返回答案。

 

示例 1：

输入：text = "alice is a good girl she is a good student", first = "a", second = "good"
输出：["girl","student"]


示例 2：

输入：text = "we will we will rock you", first = "we", second = "will"
输出：["we","rock"]


 

提示：


	1 <= text.length <= 1000
	text 由一些用空格分隔的单词组成，每个单词都由小写英文字母组成
	1 <= first.length, second.length <= 10
	first 和 second 由小写英文字母组成


## 解题
- 使用语言：python（原因：同上个算法题类似，本题要求对字符串进行加工、分词，用别的语言会相当麻烦）
- 思路：依次输入text、first、second，将已经输入的text进行分词，新建一个third列表，遍历分好的text，按照要求将目标元素放入third列表中。
- 代码
~~~python
text = input()
first = input()
second = input()
text = text.split(' ')
l = len(text)
third = []
n = 0
for i in range(l):
    if i>l-3:
        break

    if text[i]==first and text[i+1]==second :
        third.append(text[i+2])
        n += 1
print(third)
~~~
