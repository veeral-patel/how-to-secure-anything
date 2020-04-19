# CH12: Authorization

from "Engineering Trustworthy Systems" by Saydjari

## What is access control?

- Think of it as a function:

```
authorized(subject, object, action) = true iff subject is allowed to perform the action on the object
```

- You could have authorization checks, written in your code, which compute the answer programmatically
- Or, you could have a 2 dimensional access control matrix (subject x object). Each matrix entry then lists the allowed actions
- Discretionary access control = users can grant to files to other users, and remove access
- Mandatory access control = authz rules are set and can't be changed by users
- DAC = access control matrix is editable, MAC = it's un-editable