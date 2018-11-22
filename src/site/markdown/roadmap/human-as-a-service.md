# Human as a service

Humans and computers interact asynchronously by exchanging messages/invocations. 
For example a computer may "invoke" human by sending a text message, by showing a notification in the UI, or making an automated phone call.
While it might be traditionally though that humans are in control, it all depends on which party has initiated an interaction sequence.

With [stored promises](stored-promises.html) humans may be invoked asynchronously in the same way as systems:

```
var expenseApprover = ...;
expenseApprover.approve(expense).timeout(7, TimeUnit.DAYS).then(...);
```

In the above example expenseApprover may represent a group of people who may approve expenses. When ``approve()`` is invoked those people are notified in some way that there is an expense to approve and are provided a URL to review and either approve or reject.

If expense is not approved in 7 days the approval promise gets rejected and the then() handler may escalate the issue, e.g. "invoke" approver supervisors.

Use of stored promises allows to unify system/humans invocations and, for example, build solutions/processes which initially include human invocations with such invocations being gradually automated. For example:

```
var builder = ...;
builder.buildAndDeploy(artifact source repo URL).then(notify requestor);
```

Such code may initially send an e-mail message to a build engineer or a distribution list and then ``builder`` may initiate a build on a build server. 

