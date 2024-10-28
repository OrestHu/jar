```mermaid
stateDiagram-v2
    [*] --> Start

    Start --> Letter: letter
    Start --> Digit: digit
    Start --> DelimiterState: delimiter
    Start --> OperatorState: operator
    Start --> QuoteState: quote
    Start --> CommentStart: /
    Start --> Whitespace: space/tab/newline
    Start --> [*]: EOF

    Letter --> Letter: letter/digit/_
    Letter --> Finish: other
    
    Digit --> Digit: digit
    Digit --> Finish: other

    DelimiterState --> Finish: save_token
    
    OperatorState --> OperatorState2: potential_two_char
    OperatorState --> Finish: other
    OperatorState2 --> Finish: save_token

    QuoteState --> StringContent: \"
    QuoteState --> CharContent: '
    
    StringContent --> StringContent: not \"
    StringContent --> Finish: \"
    
    CharContent --> CharContent: not '
    CharContent --> Finish: '

    CommentStart --> LineComment: /
    CommentStart --> Finish: other
    
    LineComment --> LineComment: not newline
    LineComment --> Start: newline
    
    CommentStart --> BlockComment: {
    BlockComment --> BlockComment: not }
    BlockComment --> Start: }

    Whitespace --> Start: process_next

    Finish --> Start: process_next
    
    note right of Letter
        Keywords, Identifiers,
        Program names
    end note

    note right of QuoteState
        String and Char
        literals
    end note

    note right of CommentStart
        Line and Block
        comments
    end note
    StringContent --> StringContent: not \"
    StringContent --> Finish: \"
    
    CharContent --> CharContent: not '
    CharContent --> Finish: '

    CommentStart --> LineComment: /
    CommentStart --> Finish: other
    
    LineComment --> LineComment: not newline
    LineComment --> Start: newline
    
    CommentStart --> BlockComment: {
    BlockComment --> BlockComment: not }
    BlockComment --> Start: }

    Whitespace --> Start: process_next

    Finish --> Start: process_next
    
    note right of Letter
        Keywords, Identifiers,
        Program names
    end note

    note right of QuoteState
        String and Char
        literals
    end note

    note right of CommentStart
        Line and Block
        comments
    end not
