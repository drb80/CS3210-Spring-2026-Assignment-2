# Recursive-Descent Parser for a Simple C-like Language

## Name

## Student ID

## Assignment

Write a recursive-descent parser in Java for the language specified below.
For each non-terminal (left-hand side) create a method and recurse when
necessary. For example:

    void statement_list() {
        statement();
        statement_list();
    }

You might want to use streamtokenizer to help with the lexical analysis,
but you are not required to do so. See https://www.geeksforgeeks.org/java/java-io-streamtokenizer-class-set-1/

## Language Features

- **Integer-only type system**: All variables are integers (no declarations needed)
- **Assignments**: `x = expression;`
- **Control flow**: `if/else` and `while` loops
- **Expressions**: Full expression support with proper operator precedence
  - Logical operators: `||`, `&&`
  - Relational operators: `==`, `!=`, `<`, `>`, `<=`, `>=`
  - Arithmetic operators: `+`, `-`
- **Blocks**: `{ ... }`
- **Print statement**: `print(expression);`

## Grammar

```bnf
<program> ::= <statement_list>

<statement_list> ::= <statement>
                   | <statement> <statement_list>

<statement> ::= <assignment>
              | <if_statement>
              | <while_statement>
              | <block>
              | <print_statement>

<assignment> ::= <identifier> "=" <expression> ";"

<if_statement> ::= "if" "(" <expression> ")" <statement>
                 | "if" "(" <expression> ")" <statement> "else" <statement>

<while_statement> ::= "while" "(" <expression> ")" <statement>

<block> ::= "{" <statement_list> "}"
          | "{" "}"

<print_statement> ::= "print" "(" <expression> ")" ";"

<expression> ::= <logical_or>

<logical_or> ::= <logical_and>
               | <logical_or> "||" <logical_and>

<logical_and> ::= <equality>
                | <logical_and> "&&" <equality>

<equality> ::= <relational>
             | <equality> "==" <relational>
             | <equality> "!=" <relational>

<relational> ::= <additive>
               | <relational> "<" <additive>
               | <relational> ">" <additive>
               | <relational> "<=" <additive>
               | <relational> ">=" <additive>

<additive> ::= <primary>
             | <additive> "+" <primary>
             | <additive> "-" <primary>

<primary> ::= <integer>
            | <identifier>
            | "(" <expression> ")"

<identifier> ::= <letter> { <letter> | <digit> | "_" }

<integer> ::= <digit> { <digit> }
```

## How to Compile and Run

```bash
# Compile all files
javac parser.java

# Run the test program
java Main < test.see
```

## Example Program (test.see)

```java
x = 5;
y = 10;

if (x < y) {
    z = x + y;
    print(z);
}

while (x < 20) {
    x = x + 1;
}
```

### A longer syntactically valid program.

```java
/* Compute factorial-like values and demonstrate control flow */

n = 10;
factorial = 1;
i = 1;

/* Calculate factorial */
while (i <= n) {
    factorial = factorial + i;
    i = i + 1;
}

print(factorial);

/* Find largest power of 2 less than n */
power = 1;
while (power + power < n) {
    power = power + power;
}
print(power);

/* Count down from n */
counter = n;
while (counter > 0) {
    print(counter);
    counter = counter - 1;
}

/* Conditional branching examples */
x = 15;
y = 20;

if (x < y) {
    print(1);
} else {
    print(0);
}

/* Nested if statements */
a = 50;
b = 30;
c = 40;

if (a > b) {
    if (a > c) {
        print(a);
    } else {
        print(c);
    }
} else {
    if (b > c) {
        print(b);
    } else {
        print(c);
    }
}

/* Complex expressions */
result = (a + b) - (c + 10);
print(result);

/* Logical operators */
flag1 = 1;
flag2 = 0;

if (flag1 == 1 && flag2 == 0) {
    print(100);
}

if (flag1 == 1 || flag2 == 1) {
    print(200);
}

/* Nested loops */
outer = 0;
while (outer < 3) {
    inner = 0;
    while (inner < 3) {
        sum = outer + inner;
        print(sum);
        inner = inner + 1;
    }
    outer = outer + 1;
}

/* More complex conditions */
val = 42;
if (val >= 40 && val <= 50) {
    if (val != 45) {
        print(val);
    }
}

/* Arithmetic chains */
total = 1 + 2 + 3 + 4 + 5;
print(total);

/* Comparison chains */
min = 5;
max = 100;
test = 50;

if (test > min && test < max) {
    print(1);
}

/* Block statements */
{
    local1 = 10;
    local2 = 20;
    {
        nested = local1 + local2;
        print(nested);
    }
}
```
