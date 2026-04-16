Algorithm infixToPostfix(expression)
    stack = empty Stack
    postfix = empty String
    
    FOR each character ch in expression:
        IF isOperand(ch):
            postfix += ch
        
        ELSE IF ch == '(':
            stack.push(ch)
        
        ELSE IF ch == ')':
            WHILE stack.top() != '(':
                postfix += stack.pop()
            stack.pop()  // Remove '('
        
        ELSE IF isOperator(ch):
            WHILE !stack.isEmpty() AND 
                  precedence(stack.top()) >= precedence(ch) AND
                  stack.top() != '(':
                postfix += stack.pop()
            stack.push(ch)
    
    WHILE !stack.isEmpty():
        postfix += stack.pop()
    
    RETURN postfix

Function precedence(operator):
    IF operator == '+' OR operator == '-':
        RETURN 1
    ELSE IF operator == '*' OR operator == '/':
        RETURN 2
    ELSE IF operator == '^':
        RETURN 3
    RETURN 0
