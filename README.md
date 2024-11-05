# Bead-Sequence-Weaving

You have two sequences of colored beads, A and B, and you want to weave them together to form a new sequence, C. Your task is to check if it’s possible to combine the beads from A and B to create C, while keeping the order of beads in A and B the same as in their original sequences.

Input
The first line of the input contains a single line contains three strings A, B and C separated by spaces.

Constraints
1 ≤ |A|, |B|, |C| ≤ 5000

def can_weave(A, B, C):
    lenA, lenB, lenC = len(A), len(B), len(C)
    
    if lenA + lenB != lenC:
        return 0
    
    dp = [[False] * (lenB + 1) for _ in range(lenA + 1)]
    dp[0][0] = True  
    
    for i in range(lenA + 1):
        for j in range(lenB + 1):
            if i > 0 and dp[i - 1][j] and A[i - 1] == C[i + j - 1]:
                dp[i][j] = True
            if j > 0 and dp[i][j - 1] and B[j - 1] == C[i + j - 1]:
                dp[i][j] = True
    
    return 1 if dp[lenA][lenB] else 0

A, B, C = input().split()
print(can_weave(A, B, C))
