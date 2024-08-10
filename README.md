# React-19-boilerplate

This repository holds the some of the important features introduced in React-19.  
Currently the React-19 is in RC ( Release Candidate ) version and this repo is created exploring the RC release of React.

## Table Of Content

1. [Async useTransition hook](#async-usetransition-hook)
2. [Server Actions](#server-actions)
3. [UseOptimistic hook](#useOptimistic-hook)
4. [Form Actions](#form-actions)
5. [UseActionState hook](#useactionState-hook)
6. [UseFormStatus hook](#useformstatus-hook)
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

### Form Actions

Actions and formActions are the client apis which can be used as props to submit forms, buttons and inputs. These are used to trigger the action events.  

This enables developers to manage forms automatically and speeds up the development.

#### Sample Snippet

```

const formAction = () => {
  ...
}

return (
  <form action="formAction">
  ...
  </formAction>
)

```

### useActionState hook

This is little tricky hook which takes 2 arguments : a **formAction** and an **initialState**. And returns a **state** as well as an **action** function.  

The returned action function is used as **Action** to the form on submitting which, the original **formAction** is triggered. The returnd value of that function is what we use as **state** in our form.  

By default, **state** is as same as **initialState** however, on form submissions, it holds the updated value which is being returned from **formAction**

The original **formAction** takes the **initialState** as the first argument and other extra arguments which are passed to **action**  

#### Sample Snippet

```

const formAction = (initialState) => {
  ...
  return 1;
}

const [state, action] = useActionState(formAction, initialState);

<form action="action" >
...
</form>

```

### useFormStatus hook

In React, till R18, there was no in-built api or hook available for the developers to check the form submission status and they had to write the code explicitely to check the status of submissions.  

This was although a minor thing to handle, was remain un-noticed and continued. But in R19, the response we can get the status of form submission via **useFormStatus** hook.  

#### Sample Snippet

```

const Button = () => {
  const { data, pending } = useFormStatus();
  
  return (
    <button> Send { pending && <span>ing...</span> } </button>
  )
}

return (
  <form action="formAction">
  ...
  ...
  <Button />
  ...
  </formAction>
)

```