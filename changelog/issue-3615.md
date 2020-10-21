audience: general
level: major
reference: issue 3615
---
RFC 165 has been implemented, allowing for greater administrator control over
"public" endpoints. Previously these were guarded by no scopes and could be
accessed by anyone with no way to limit this. In this release all
unauthenticated API calls are now granted the scope `assume:anonymous`.
Additionally, most previously unprotected endpoints are now guarded by at
least one scope, to enable the following:

* To maintain current behavior, the `anonymous` will need to be granted to some scopes. Refer to
`the [anonymous scope section](https://docs.taskcluster.net/docs/manual/design/apis/hawk/authorized-scopes) in the docs.
* To entirely lock down the cluster from anonymous access, do not grant any
  scopes to role `anonymous`
* Pick and choose specific "public" endpoints to make available to anonymous
  requests

Performance testing (refer to
https://github.com/taskcluster/taskcluster/issues/3698 for more details):
* CPU has seen an increase of 0%-15%
* Memory has seen no increase