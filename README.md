# React-19-boilerplate

This repository holds the some of the important features introduced in React-19.  
Currently the React-19 is in RC ( Release Candidate ) version and this repo is created exploring the RC release of React.

## Table Of Content

1. [Async useTransition hook](#async-usetransition-hook)
2. [Server Actions](#server-actions)
3. [UseOptimistic hook](#useOptimistic-hook)
4. UseActionState hook
5. Form Actions
6. UseFormStatus hook
7. Use hook
8. Server components
9. Hydration error reporting improvements
10. Ref as props
11. Simplified context provider usage
12. Ref cleanup functions
13. Initial value for useDeferredValue
14. Support for async scripts
15. Support for custom elements
16. Support for document metadata
17. Enhanced stylesheet management
18. React 19’s new APIs for resource optimization

---

### Async useTransition hook

React, till 17th version had no any proper hook to handle the async changes. But in R18, useTransaction hook enables developers to handle this condition directly ( instead of creating separate hook or handling in a different function ) by giving a boolean `loading` flag.  

In R19, React team goes one step futher and enables the support for async functions with this hook.

#### Sample Snippet

```
  const [isPending, startTransition] = useTransition();
  const [users, setUsers] = useState([]);

  const getUsersData = () => {
    startTransition(async () => {
        try{
            const data = await getUsers();
            setUsers(data);
        } catch (e) {
            // custom error handling | console.log(e)
        }
    })
  };
```

---

### Server Actions

Functions ( or Actions ) with labelled as `"use server"` are treated as server actions.

Unlike other general functions ( actions ), server actions are the special kind of functions which are executed at the server side.
This ensures quality time and reduces most of the unnecessary stuffs with regular development.

#### Sample Snippet

```
async fuction getLikes () {
    "use server"
    ...
}
```

### UseOptimistic Hook

The traditional React, in general, updates the DOM after once the server response. When in case of slow response cases, we used to have `loading` based approach to change a particular state and get acknowledgement from the server. ( for Ex: like, comment or send request etc )  

But R19 enables us to change the state and update the DOM even before the server response and so, improves the user experience.  
This phenomena of optimistically updating the DOM is achieved with the `useOptimistic` hook ( Client Api ) which takes initial state and the update function as arguments and executes optimistically.

#### Sample Snippet

```

import { useOptimistic } from 'react'

const optimistic = useOptimistic(initialState, updateFunction);

```

### useActionState hook

This is little tricky hook; It takes 2 arguments : a **formAction** and an **initialState**. And returns a **state** as well as an action function.  
The returned action function is used as **Action** to the form on submitting which, the original **formAction** is triggered. The returnd value of that function is what we use as **state** in our form.  
By default, **state** is as same as **initialState** however, on form submissions, it holds the updated value which is being returned from **formAction**