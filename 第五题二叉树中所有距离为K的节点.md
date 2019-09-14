# 2019年暑假Android实验室考核算法题五————二叉树中的所有距离为K的节点
### 题目
给定一个二叉树（具有根结点 root）， 一个目标结点 target ，和一个整数值 K 。

返回到目标结点 target 距离为 K 的所有结点的值的列表。 答案可以以任何顺序返回。

 




示例 1：

输入：root = [3,5,1,6,2,0,8,null,null,7,4], target = 5, K = 2

输出：[7,4,1]

解释：
所求结点为与目标结点（值为 5）距离为 2 的结点，
值分别为 7，4，以及 1

注意，输入的 "root" 和 "target" 实际上是树上的结点。
上面的输入仅仅是对这些对象进行了序列化描述。


 

提示：


1.给定的树是非空的，且最多有 K 个结点。
2.树上的每个结点都具有唯一的值 0 <= node.val <= 500 。
3.目标结点 target 是树上的结点。
4.0 <= K <= 1000.

## 解题：
- 语言：python
- 思路：主要思路是应用两次深度优先遍历，将所有符合条件的节点找出。
- 代码：
~~~ python
class Solution(object):
    def distanceK(self,root,target,K):

        goal = []#所求的节点放置的空列表

        def ROOT(root,K1):#求到目标节点的子节点（一次深度优先遍历）
            if root == None:
                return
            if K1==0:
                goal.append(root.val)
            else:
                ROOT(root.left,K1-1)
                ROOT(root.right,K1-1)#迭代求所有子节点

        def gather(root):
            if root==None:
                return -1
            if root==target:#若目标节点就是根节点
                ROOT(root,K)
                return 1
                
            L = gather(root.left)#迭代回去（第二次深度优先遍历）
            R = gather(root.right)

            if L!=-1:
                if L==K:
                    goal.append(root.val)#一个个遍历判断左儿子节点
                else:
                    ROOT(root.right,K-L-1)
                return L+1

            if R!=-1:
                if R==K:
                    goal.append(root.val)#同上面的道理一样，一个个遍历判断右儿子节点
                else:
                    ROOT(root.left,K-R-1)
                return R+1
            return -1
        gather(root)
        return goal
~~~

