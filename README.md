# Conventions

### Naming, declarations

##### Variables
- camel case
- descriptive

NO:

`let String = "Bob";`

YES:

`let firstName = "Bob"`

###### Booleans
- is/has prefix

NO:

`let mobile = true`

YES:

`let isMobile = true`

###### Functions
- nouns and verbs as prefixes
- use object parameter if function has potential to change over time/ has multiple optional parameters, for base utils use simpler declarations
- descriptive parameter names

NO:

`let bob = () => "Bob"`

`let bobGet = () =>"Bob"`

```
let getBob = (a, b, c , d, e) =>...
getBob(1, 2, undefined, undefined, 3);
```

YES:

`let  getBob = () =>"Bob"`

```
let getBob = ({ age, maxDistance, minDistance, height }) =>...
getBob({ maxDistance: 100, age: 20 })
```
```
let addNumbers = (a, b) => a + b;
```

###### Consts
- uppercase, snake case

NO:

`let mobileBreakpoint = 200;`

YES:

`let MOBILE_BREAKPOINTS = 200`
