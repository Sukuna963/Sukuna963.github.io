---
layout: post
title: "HackerRank"
author: "Leonardo Marques"
categories: dsa
tags: [dsa, programming language, python]
image: 
---

### Solve Me First

```python
def solveMeFirst(a, b):
	# Hint: Type return a+b below

    return a + b


num1 = int(input())
num2 = int(input())
res = solveMeFirst(num1, num2)
print(res)
```

### Simple Array Sum

```python
#!/bin/python3

import math
import os
import random
import re
import sys

#
# Complete the 'simpleArraySum' function below.
#
# The function is expected to return an INTEGER.
# The function accepts INTEGER_ARRAY ar as parameter.
#

def simpleArraySum(ar):
    # Write your code here
    
    return sum(ar)
    
if __name__ == '__main__':
    fptr = open(os.environ['OUTPUT_PATH'], 'w')

    ar_count = int(input().strip())

    ar = list(map(int, input().rstrip().split()))

    result = simpleArraySum(ar)

    fptr.write(str(result) + '\n')

    fptr.close()

```

### Compare the Triplets
```python
#!/bin/python3

import math
import os
import random
import re
import sys

#
# Complete the 'compareTriplets' function below.
#
# The function is expected to return an INTEGER_ARRAY.
# The function accepts following parameters:
#  1. INTEGER_ARRAY a
#  2. INTEGER_ARRAY b
#

def compareTriplets(a, b):
    scorers = [0, 0]
    
    for alice_score, bob_score in zip(a, b):
        if alice_score > bob_score:
            scorers[0] += 1
             
        if alice_score < bob_score:
            scorers[1] += 1
            
    return scorers
    

if __name__ == '__main__':
    fptr = open(os.environ['OUTPUT_PATH'], 'w')

    a = list(map(int, input().rstrip().split()))

    b = list(map(int, input().rstrip().split()))

    result = compareTriplets(a, b)

    fptr.write(' '.join(map(str, result)))
    fptr.write('\n')

    fptr.close()
```