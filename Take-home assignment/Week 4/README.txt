// Problem 1: Implement Queue using Stacks
class MyQueue:

    def __init__(self):
        self.input = []
        self.output = []

    def push(self, x: int) -> None:
        self.input.append(x)

    def pop(self) -> int:
        self.peek()
        return self.output.pop()

    def peek(self) -> int:
        if not self.output:
            while self.input:
                self.output.append(self.input.pop())
        return self.output[-1]

    def empty(self) -> bool:
        return not self.input and not self.output

// Problem 2: Decode String
class Solution:
    def decodeString(self, s: str) -> str:
        stack = []

        for i in range(len(s)):
            if s[i] != "]":
                stack.append(s[i])
            else:
                substr = ""
                while stack[-1] != "[":
                    substr = stack.pop() + substr
                stack.pop()

                k = ""
                while stack and stack[-1].isdigit():
                    k = stack.pop() + k
                stack.append(int(k) * substr)

        return "".join(stack)

// Problem 3:  Number of People Aware of a Secret
class Solution:
    def peopleAwareOfSecret(self, n: int, delay: int, forget: int) -> int:
        dp, md = [1] + [0] * (forget - 1), 10**9 + 7
        for i in range(1, n):
            dp[i % forget] = (md + dp[(i + forget - delay) % forget] - dp[i % forget] + (0 if i == 1 else dp[(i - 1) % forget])) % md
        return sum(dp) % md
