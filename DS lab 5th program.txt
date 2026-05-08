#include <stdio.h>
#include <ctype.h>

#define MAX 100

int stack[MAX];
int top = -1;

// Push operation
void push(int value)
{
    top++;
    stack[top] = value;
}

// Pop operation
int pop()
{
    return stack[top--];
}

int main()
{
    char postfix[MAX];
    int i, op1, op2, result;

    printf("Enter postfix expression: ");
    scanf("%s", postfix);

    for(i = 0; postfix[i] != '\0'; i++)
    {
        // If character is operand
        if(isdigit(postfix[i]))
        {
            push(postfix[i] - '0');
        }
        // If character is operator
        else
        {
            op2 = pop();
            op1 = pop();

            switch(postfix[i])
            {
                case '+':
                    result = op1 + op2;
                    break;

                case '-':
                    result = op1 - op2;
                    break;

                case '*':
                    result = op1 * op2;
                    break;

                case '/':
                    result = op1 / op2;
                    break;

                case '%':
                    result = op1 % op2;
                    break;

                default:
                    printf("Invalid operator");
                    return 1;
            }

            push(result);
        }
    }

    printf("Result = %d", pop());

    return 0;
}
