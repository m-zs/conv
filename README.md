## Process

### 1. Collecting requirements <a href="#step1" id="step1"/>

1. Create main refactor task.
2. Analize module code and app view, list expected features and validate their behavior. The list should be accepted by PM/PO and will be used to support test creation.
3. If any mistakes or inaccuracies are found following steps should be consulted with the PM/PO.
4. Update list if (3) applies.
5. Create smaller refactor tasks and estimate them.

<br>

### 2. Codebase refactor <a href="#step2" id="step2"/>

1. Create main refactor branch, add feature readme based on [step 1](#step1).
2. Create a new refactor subtask branch that will be reviewed and merged into the main branch after work is complete.
3. Change main and subtask statuses to "In progress".
4. Consult other developers if there is a different way of implementation to improve overall quality (applies to more complicated features).
5. Refactor code following [code conventions](#code-conventions)
6. If any mistakes or inaccuracies are found following steps should be consulted with the PM/PO.
7. Remember to add unit/ integration tests to refactored code following [test conventions].
8. Commit changes using [git conventions]
9. When work is complete - create a merge request for the subtask branch targeting the main refactor branch.
10. Request code review from at least two reviewers.
11. If new task/ issue related to module appears - it should be consulted with the PM/PO if refactor will fix it. 
12. Depending on the priority:
 - If priority is high - pin task related to refactor task. Do the fixes on main app, and move them on refactor branch.
 - If priority is low - pin task related to refactor task. Do the fixes on refactor branch.
13. After the merge request get approved, merge changes to main refactor branch using commit squashing.
14. If there is a possibility to test changes - move task to "To be tested" status and mention testers. Otherwise move it to "Done" status.

<br>

### 3. Testing (when to add e2e? cypress for integration for each subtask?) <a href="#step3" id="step3"/>

1. After each [step 1](#step2) (if possible) - chages should be tested manually and accepted. 
2. After all subtasks are merged and tested, refactor task should be moved on "To be tested" for last sanity checks and PM/Po approval.

<br>

### 4. Integrating with current app <a href="#step4" id="step4"/>

1. When feature is approved, consult with PO/PM when changes can be added (early in sprint will be optimal).
2. Add main refactor task to release.
3. Merge refactor branch to release branch.
4. Make sure all related test are passing.
5. Release

<br>

### 5. Process summary, preparation for next interation <a href="#step5" id="step5"/>

1. Can be done on sprint review/ other dedicated meeting
2. Pros and cons should be disscussed to improve next iteration.
3. Create textual summary (where it should be saved?).
4. Update process docs id required.
5. Select next module to work on.
6. Reiterate starting on [step 1](#step1).

<br>

------------

<br>

## Code Conventions <a href="#code-conventions" id="code-conventions"/>

### Naming, declarations

##### Variables
- camel case
- descriptive

NO:

`let String = "Bob";`

YES:

`let firstName = "Bob"`

<br>

##### Booleans
- is/has prefix

NO:

`let mobile = true`

YES:

`let isMobile = true`

<br>

##### Functions
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

<br>

##### Consts
- uppercase, snake case

NO:

`let mobileBreakpoint = 200;`

YES:

`let MOBILE_BREAKPOINT = 200`

<br>

------------

<br>

## Folder structure <a href="#folder-structure" id="folder-structure"/>

    .
    └── src 
        ├── api
        |   ├── index.ts # (Barrel file)
        |   ├── queryKeys.ts # (Query ids)
        |   ├── queryClient.ts # (Query client with configuration)
        |   ├── apiProvider.ts # (Api client with configuration)
        |   ├── types.ts # (Shared types)
        |   ├── utils.ts # (Utils)
        |   ├── utils.test.ts # (Utils tests)
        |   ├── endpoints
        |   |     └── users
        |   |           ├── index.ts # (Barrel file)
        |   |           ├── hooks
        |   |           |    ├── index.ts # (Barrel file)
        |   |           |    └── useGetUsers.ts # (Hook implementation)
        |   |           └── requests
        |   |               ├── index.ts # (Barrel file)
        |   |               └── getUsers.ts # (Api request implementation)
        |   └── interceptors # (Interceptors added to api provider)
        |        └── exampleInterceptor
        |            ├── index.ts # (Barrel file)
        |            ├── exampleInterceptor.ts # (Interceptor implementation)
        |            └── exampleInterceptor.test.ts # (Interceptor tests)
        ├── config
        |   ├── env.ts
        |   ├── access.ts
        |   └── index.ts
        ├── routing
        |   ├── ExampleRouter.tsx
        |   └── Router.tsx
        ├── localization
        |   ├── translations
        |   |   ├── pl.json
        |   |   └── en.json
        |   ├── index.ts
        |   ├── types.ts
        |   └── LocalizationProvider.tsx
        ├── components
        |    └── ExampleComponent
        |        ├── index.ts  # (Barrel file)
        |        ├── ExampleSub.tsx # (Child component)
        |        ├── ExampleSub.test.ts # (Component tests)
        |        ├── utils.ts # (Local utils)
        |        ├── utils.test.ts # (Utils tests)
        |        └── styles.css # (Component specific styles)
        ├── styles
        ├── types
        |   ├── index.ts # (Types barrel file)
        |   └── example.ts # (Types related to example)
        ├── utils
        |   ├── index.ts # (Utils barrel file)
        |   └── example-group # (Utils group related to a topic)
        |       ├── index.ts # (Group barrel file)
        |       └── doExample # (Util folder)
        |           ├── doExample.ts # (Util implementation)
        |           └── doExample.test.ts # (Util tests)
        ├── hooks
        │   └── useHook
        │       ├── index.ts # (Barrel file)
        |       ├── useHook.ts # (Hook implementation)
        |       ├── useHook.test.ts # (Hook tests)
        |       ├── utils.ts # (Utils)
        |       └── utils.test.ts # (Utils tests)
        └── features
            └── Example
                ├── README.md # (Feature readme with specs and solution design summary)
                ├── index.ts  # (Barrel file)
                ├── Example.tsx # (Main component)
                ├── Example.test.ts # (Main component tests)
                ├── utils.ts # (Main/shared feture specific utils)
                ├── utils.test.ts # (Utils tests)
                ├── styles.css # (Main component styles)
                ├── types.ts # (Shared local types)
                └── components # (Shared local types)
                    └── ExampleSub
                        ├── index.ts  # (Barrel file)
                        ├── ExampleSub.tsx # (Child component)
                        ├── ExampleSub.test.ts # (Component tests)
                        ├── utils.ts # (Local utils)
                        ├── utils.test.ts # (Utils tests)
                        └── styles.css # (Component specific styles)

