# LogAn: Log Message Corpus Annotated Using a Unified Template Definition and Parameter Classes

The file [logan_templates.csv](logan_templates.csv) contains our manually annotated templates, including parameter classes.  
The column `ParameterClasses` holds the hierarchical parameter classes as map of `token_index -> class` (0 indexed / python `dict[int, str`). 
Hierarchies in classes are denoted as `ParentClass::ChildClass`.
Note that the parent class `Open Set` is implicit for all classes except `Closed Set`, furthermore the class `Other` as a child of `Open Set` is implicitly stored as the absence of an entry in the map for a variable token (`<*>`).

This leaves us with the following __18__ explicitly stored parameter classes:
```
Action
Location
Location::IP-Port::IP
Location::IP-Port::Port
Location::MAC
Location::Path
Location::URL
Object
Object::ComputingResource
Object::Process
Object::Session
Object::User
Object::ValueExpression
Other::ClosedSet
StatusMessage
Time
Time::Duration
Time::Timestamp
```

The exact tokenizer function we used (Python 3.12.3):
```python
import re

def tokenize(s: str) -> list[str]:
    """
    Tokenizes a string by splitting on whitespace and common punctuation/delimiter characters.

    Splits on:
      - Whitespace runs
      - A period followed by whitespace or end-of-string (sentence-ending dot)
      - Assignment/separator characters: = : , ; 
      - Bracket pairs: () [] {}
      - Angle brackets and quotes: < > " '

    Tokens that are empty or purely whitespace are discarded.

    Args:
        s: The input string to tokenize.

    Returns:
        A list of non-empty, non-whitespace token strings.
    """
    DELIMITERS = [
        r"\s+",           # Whitespace runs
        r"\.(?=[\s$])",   # Sentence-ending dot (before whitespace or end-of-string)
        r"[=:,;]",        # Assignment and separator punctuation
        r"[(){}\[\]]",    # Bracket pairs (round, curly, square)
        r"[<>\"']",       # Angle brackets and quotes
    ]

    return [token for token in re.split(r"(" + "|".join(DELIMITERS) + r")", s) if token and not token.isspace()]
```
