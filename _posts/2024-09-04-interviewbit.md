---
layout: post
title: "InterviewBit"
author: "Leonardo Marques"
categories: dsa
tags: [dsa, programming language, java]
image: interviewbit/interviewbit.jpg
---

***InterviewBit is one of the most popular interview preparation websites. Hundreds of thousands of elite software engineers around the globe have joined the platform to upskill themselves.***

# Problem Solving:

### Majority Element

```java
/*
    INFO: https://en.wikipedia.org/wiki/Boyer%E2%80%93Moore_majority_vote_algorithm
*/

public class Solution {
    public int majorityElement(final int[] A) {
        int counter = 1;
        int candidate = A[0];
        
        for(int i=1; i < A.length; i++) {
            if(counter == 0) {
                candidate = A[i];
            }
            
            if(A[i] == candidate) {
                counter++;
            } else {
                counter--;
            }
        }
        
        return candidate;
    }
}
```

### Unique Binary Search Trees

```java
class TreeNode {
    int val;
    TreeNode left;
    TreeNode right;
    TreeNode(int x) { val = x; }
}

public class Solution {
	public ArrayList<TreeNode> generateTrees(int a) {
        return trees(1, a);
    }
    
    private ArrayList<TreeNode> trees(int start, int end) {
        ArrayList<TreeNode> nodes = new ArrayList<>();
        
        if(start > end) {
            nodes.add(null);
            return nodes;
        }
        
        for(int i=start; i <= end; i++) {
            ArrayList<TreeNode> left = trees(start, i-1);
            ArrayList<TreeNode> right = trees(i+1, end);
            
            for(TreeNode l : left) {
                for(TreeNode r : right) {
                    TreeNode root = new TreeNode(i);
                    root.left = l;
                    root.right = r;
                    nodes.add(root);
                }
            }
        }
        
        return nodes;
    }       
}
```