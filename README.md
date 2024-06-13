# FunctionalParsingCompiler
focuses on implementing a robust parser in C++ for a simplified programming language. The parser operates through two primary phases: lexical analysis (tokenization) and semantic analysis (parsing). The lexer breaks down the input code into tokens of various types, while the parser constructs a parse tree based on these tokens, representing the program's hierarchical structure.


## Project Objectives

1. File Input Handling: The program reads input data from a file named "InputFile.txt" containing the code to be processed. 
2. Support for Multiple Data Types: Capable of handling diverse data types such as integers, floats, and more complex types like long long.
3. Control Flow Parsing: Specifically parses if and while statements according to a defined context-free grammar (CFG).
4. Tokenization: Before parsing, the input code undergoes tokenization, identifying keywords, identifiers, operators, numbers, declarations, punctuation, and errors.  
5. Parse Tree Generation: Utilizes a CFG to generate a parse tree that mirrors the syntactic structure of the input code. 
6. Visualization with Graphviz: Provides functionality to visually represent the parse tree using Graphviz. 
7. Comment Removal: Includes a feature to remove both single-line and multi-line comments from the code while ensuring the parser's functionality remains intact.

## Context-Free Grammar (CFG)

     stmts            ----> stmts stmt | E 
     stmt             ----> while_stmt | if_stmt | assign_stmt | declaration_stmt
     declaration_stmt ----> declaration_keyword definition_stmt
     declaration_keyword--> int | char | float | double | short | long long
     definition_stmt  ----> id = expr; |
                            id;
     while_stmt       ----> while(cond){stmts}
     assign_stmt      ----> id = expr;
     if_stmt          ----> if(cond) stmt |
                            if(cond) stmt else_stmt|
                            if(cond) stmt elseif_stmt
     else_stmt        ----> else stmt 
     elseif_stmt      ----> elseif (cond) stmt elseif_stmt | else_stmt | e
     cond             ----> id op factor 
     expr             ----> expr + term | expr - term | term
     term             ----> term * factor | term / factor | factor
     factor           ----> id | digit | (expr)
     id               ----> a-z|A-Z
     digit            ----> 0|..9
     op               ----> >|>=|<|<=|=|==|!=|+|-|*|/

 ## CFG after left recursion left factoring elimination
     stmts            ----> stmt rest
     rest             ----> stmt rest | E
     stmt             ----> while_stmt | if_stmt | assign_stmt | declaration_stmt
     declaration_stmt ----> declaration_keyword | definition_stmt
     declaration_keyword--> int | char | float | double | short | long long
     definition_stmt  ----> id rest4;
     rest4            ----> e | = expr 
     while_stmt       ----> while(cond){stmts}
     assign_stmt      ----> id = expr;
     if_stmt          ----> if(cond)stmt rest3
     rest3            ----> elseif_stmt| else_stmt | E
     else_stmt        ----> else stmt
     elseif_stmt      ----> else if (cond) stmt rest3
     cond             ----> id op factor
     expr             ----> term  Rest1
     Rest1            ----> + term Rest1 | - term Rest1 | E
     term             ----> factor Rest2
     Rest2            ----> * factor Rest2 | / factor Rest2 | E
     factor           ----> id | digit | (expr)
     id               ----> a|..|z|A|..|Z
     digit            ----> 0|..|9
     op               ---->>|>=|<|<=|=|==|!=|+|-|*|/


  ## Input Code Sample: 
    ```c++
    int x = 1 ;
    float y;
    double temp;
    while(x<3)
    {
     y = 10.4;
     // z = 70;
     y = y + 3e1;
     
    }
    if(x==10)
      temp = 3.33;
    else if(x <2)
       temp = 30;
    else
       temp = 0;
    ```

  ## Parse Tree for this sample Code:
![parsetree](https://github.com/sara-salah1/FunctionalParsingCompiler/assets/67710906/856d8726-547e-4501-92cb-fb3086397939)
