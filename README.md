# Banker

A programming language that ensures you have enough assertions.

For familiarity, the semantics are similar to Brainfuck.
This ensures that even novice programmers can quickly pick up the language
  and begin producing stellar applications.

In order to make sure that such programmers write safe code, all statements
are charged to a bank. If the bank is empty, the program exits. The bank
can be filled up by executing assertions. Therefore, in order to write
anything, one must have one assertion per every ten other statements executed.

## Syntax and Semantics

A translation guide to C is here. Each program starts with

    char arr[1024];
    char *ptr = arr;
    int bank = 0;

Here are the commands:

- `>` is `++ptr;`
- `<` is `--ptr;`
- `+` is `++*ptr;`
- `-` is `--*ptr;`
- `[` is `while(*ptr){;`
- `]` is `}`
- `.` is `putchar(*ptr);`
- `,` is `*ptr = getchar();`
- `=(assertion)` is `bank+=11;if(!assertion){printf("Assertion failed!\n");exit(1);}` where `assertion` conforms to the Assertion Meta-Language.

Between each statement is the following safety check: `if(--bank<0){printf("Bank underflow error!\n")exit(2);}`

### Assertion Meta-Language

An assertion is an inequality or equality with special variables $0 to $1023 which refer
to the cells of `arr`. For example, `=(4*$5 - 1 <= $99/2)` translates to
`bank+=11;if(!(4*arr[5] - 1 <= arr[99]/2)){...}`.

## Usage

First, compile with `./bankerc foo.bank` to get an executable `foo`. You must have a C compiler installed (it will be called with `cc`) and Ruby.

