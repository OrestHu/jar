```mermaid
stateDiagram-v2
    direction LR
    
    [*] --> Program: назва програми
    Program --> Start: будь-який символ
    
    Start --> Letter: буква
    Start --> Digit: цифра
    Start --> Another: інший символ
    Start --> Scomment: /
    Start --> Separators: пробіл|табуляція|\n
    Start --> EndOfFile: EOF
    
    Letter --> Letter: буква|цифра
    Letter --> Finish: інший символ
    
    Digit --> Digit: цифра
    Digit --> Finish: інший символ
    
    Another --> Finish: будь-який символ
    
    Scomment --> Comment: /
    Scomment --> Finish: інший символ
    
    Comment --> Start: \n
    
    Separators --> Start: будь-який символ
    
    Finish --> Start: будь-який символ, крім EOF
    Finish --> EndOfFile: EOF
    
    EndOfFile --> EndOfFile: EOF
    EndOfFile --> [*]
    
    note right of Letter: Розпізнавання ідентифікаторів<br/>та ключових слів
    note right of Digit: Розпізнавання<br/>числових констант
    note right of Another: Розпізнавання<br/>спеціальних символів
    note right of Comment: Ігнорування<br/>коментарів
    note right of Separators: Пропуск пробільних<br/>символів
