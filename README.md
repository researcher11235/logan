# LogAn: Log Message Corpus Annotated Using a Unified Template Definition and Parameter Classes

The file [logan_templates.csv](logan_templates.csv) contains our manually annotated templates, including parameter classes.  
The column `ParameterClasses` holds the hierarchical parameter classes as map of `token_index -> class` (0 indexed / python `dict[int, str`). 
Hierarchies in classes are denoted as `ParentClass::ChildClass`.
Note that the parent class `Open Set` is implicit for all classes except `Closed Set`, furthermore the class `Other` as a child of `Open Set` is implicitly stored as the absence of an entry in the map for a variable token (`<*>`).

This leaves us with the following __18__ parameter classes:
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
