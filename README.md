# React-19-boilerplate

This repository holds the some of the important features introduced in React-19.  
Currently the React-19 is in RC ( Release Candidate ) version and this repo is created exploring the RC release of React.

## Table Of Content

1. [Async useTransition hook](#async-usetransition-hook)
2. [Server Actions](#server-actions)
3. UseOptimistic hook
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