第三章 哈希表part01

 今日任务 

● 哈希表理论基础 
● 242.有效的字母异位词 
● 349. 两个数组的交集 
● 202. 快乐数
● 1. 两数之和   

 详细布置 

 哈希表理论基础 

建议：大家要了解哈希表的内部实现原理，哈希函数，哈希碰撞，以及常见哈希表的区别，数组，set 和map。  

什么时候想到用哈希法，当我们遇到了要快速判断一个元素是否出现集合里的时候，就要考虑哈希法。  这句话很重要，大家在做哈希表题目都要思考这句话。 

文章讲解：https://programmercarl.com/%E5%93%88%E5%B8%8C%E8%A1%A8%E7%90%86%E8%AE%BA%E5%9F%BA%E7%A1%80.html  


 242.有效的字母异位词 

建议： 这道题目，大家可以感受到 数组 用来做哈希表 给我们带来的遍历之处。 

题目链接/文章讲解/视频讲解： https://programmercarl.com/0242.%E6%9C%89%E6%95%88%E7%9A%84%E5%AD%97%E6%AF%8D%E5%BC%82%E4%BD%8D%E8%AF%8D.html  
``` python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        s_dict={}
        for chr in s:
            if chr not in s_dict:
                s_dict[chr]=1
            else:
                s_dict[chr]+=1
        for chr in t:
            if chr not in s_dict:
                return False
            else:
                s_dict[chr]-=1
   
        return not any(s_dict.values())
```

由于唯一元素数量一直，也可使用数组

```python
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        char_count=[0 for _ in range(26)]
        for c in s:
            char_count[ord(c)-ord('a')]+=1
        for c in t:
            char_count[ord(c)-ord('a')]-=1
        return not any(char_count)
```
 349. 两个数组的交集 

建议：本题就开始考虑 什么时候用set 什么时候用数组，本题其实是使用set的好题，但是后来力扣改了题目描述和 测试用例，添加了 0 <= nums1[i], nums2[i] <= 1000 条件，所以使用数组也可以了，不过建议大家忽略这个条件。 尝试去使用set。 

题目链接/文章讲解/视频讲解：https://programmercarl.com/0349.%E4%B8%A4%E4%B8%AA%E6%95%B0%E7%BB%84%E7%9A%84%E4%BA%A4%E9%9B%86.html  
``` python
class Solution:
    def intersection(self, nums1: List[int], nums2: List[int]) -> List[int]:
        table={}
        for n in nums1:
            table[n]=table.get(n,0)+1
        res=[]
        for n in nums2:
            if n in table:
              res.append(n)
              table.pop(n) 
        return res
```        
 202. 快乐数 

建议：这道题目也是set的应用，其实和上一题差不多，就是 套在快乐数一个壳子 

题目链接/文章讲解：https://programmercarl.com/0202.%E5%BF%AB%E4%B9%90%E6%95%B0.html  

``` python
class Solution:
    def isHappy(self, n: int) -> bool:
        existed=set()
        def extract_digits(n):
            res=[]
            while n != 0:
                res.append(n%10)
                n=n//10 
            return   res                                                      
            
        while n not in existed:
            existed.add(n)
            n=sum([x**2 for x in extract_digits(n)])
            if n==1:
                return True
            
        return False
```

 1. 两数之和 

建议：本题虽然是 力扣第一题，但是还是挺难的，也是 代码随想录中 数组，set之后，使用map解决哈希问题的第一题。 

建议大家先看视频讲解，然后尝试自己写代码，在看文章讲解，加深印象。 

题目链接/文章讲解/视频讲解：https://programmercarl.com/0001.%E4%B8%A4%E6%95%B0%E4%B9%8B%E5%92%8C.html 

``` python
class Solution:
     def twoSum(self,nums:List[int], target:int) -> List[int]:
        hash = {}
        for i,num in enumerate(nums):
            hash[target-num]=i
        for i,num in enumerate(nums):
            try:
                if hash[num]!=i:
                    return i,hash[num]
            except:
                pass
```