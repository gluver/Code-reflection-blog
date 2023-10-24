第五章 栈与队列part02
今日内容： 

● 20. 有效的括号
● 1047. 删除字符串中的所有相邻重复项
● 150. 逆波兰表达式求值

 详细布置 

 20. 有效的括号 

讲完了栈实现队列，队列实现栈，接下来就是栈的经典应用了。 

大家先自己思考一下 有哪些不匹配的场景，在看视频 我讲的都有哪些场景，落实到代码其实就容易很多了。

题目链接/文章讲解/视频讲解：https://programmercarl.com/0020.%E6%9C%89%E6%95%88%E7%9A%84%E6%8B%AC%E5%8F%B7.html  
```python
class Solution:
    def isValid(self, s: str) -> bool:
        if len(s)%2!=0:
            return False
        close_brackets=[]
        pair={'(':')','{':'}','[':']'}
        for b in s:
            if b in '([{':
                close_brackets.append(pair[b])
            elif b in ')]}':
                if len(close_brackets)==0 or close_brackets.pop() !=b:
                    return False
        if len(close_brackets)!=0:
            return False
        else:
            return True
```

 1047. 删除字符串中的所有相邻重复项 

栈的经典应用。 

要知道栈为什么适合做这种类似于爱消除的操作，因为栈帮助我们记录了 遍历数组当前元素时候，前一个元素是什么。

题目链接/文章讲解/视频讲解：https://programmercarl.com/1047.%E5%88%A0%E9%99%A4%E5%AD%97%E7%AC%A6%E4%B8%B2%E4%B8%AD%E7%9A%84%E6%89%80%E6%9C%89%E7%9B%B8%E9%82%BB%E9%87%8D%E5%A4%8D%E9%A1%B9.html 

**二刷可以尝试双指针法实现**
```python
class Solution:
    def removeDuplicates(self, s: str) -> str:
        res=[]
        for c in s:
            if len(res)==0 or c!=res[-1]:
                res.append(c)
            else:
                res.pop()
        #注意需要返回字符串        
        return "".join(res)
```
 150. 逆波兰表达式求值 

本题不难，但第一次做的话，会很难想到，所以先看视频，了解思路再去做题 

题目链接/文章讲解/视频讲解：https://programmercarl.com/0150.%E9%80%86%E6%B3%A2%E5%85%B0%E8%A1%A8%E8%BE%BE%E5%BC%8F%E6%B1%82%E5%80%BC.html  
```python
class Solution:
    def evalRPN(self, tokens: List[str]) -> int:
        st=[]
        for tok in tokens:
            if tok not in '+-*/':
            # detect if integer
                st.append(int(tok))
            else:
                b=st.pop()
                a=st.pop()
                # print(f"{a}{tok}{b}")
                if tok=='/':
                    # truncte to zero , math.trunc
                    st.append(int(a/b))
                elif tok=='+':
                    st.append(a+b)
                elif tok=='-':
                    st.append(a-b)
                elif tok=='*':
                    st.append(a*b)
        return st.pop()
```