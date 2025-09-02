# infix-to-postfix
converting infix to postfix
def precedence(op):
    if op == '+' or op == '-':
        return 1
    if op == '*' or op == '/':
        return 2
    if op == '^':
        return 3
    return 0

def infix_to_postfix(expression):
    stack = []
    output = []
    for char in expression:
        if char.isalnum():  # Operand
            output.append(char)
        elif char == '(':
            stack.append(char)
        elif char == ')':
            while stack and stack[-1] != '(':
                output.append(stack.pop())
            if stack and stack[-1] == '(':
                stack.pop()
        else:  # Operator
            while stack and precedence(char) <= precedence(stack[-1]):
                output.append(stack.pop())
            stack.append(char)
    while stack:
        output.append(stack.pop())
    return ''.join(output)

# Example usage:
if __name__ == "__main__":
    expr = "a+b*(c^d-e)^(f+g*h)-i"
    print("Infix:   ", expr)
    print("Postfix: ", infix_to_postfix(expr))
