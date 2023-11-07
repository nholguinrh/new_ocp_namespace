# OpenShift quick access notes

## Problem/Rationale
What if there is a challenge to be solved for a new team, what if this project is temporary and there is a need to understand how this new project uses the resources?

### Let's create a temporary namespace and infraestructure to be used by the team.

**Create an HTPasswd File:**
OpenShift uses the HTPasswd identity provider to manage users. You need to create an HTPasswd file with user credentials. You can use the htpasswd command to create or update this file. If you don't have it installed, you can install it on your system. 
```bash
htpasswd -c /path/to/htpasswdfile username
```

**Create an OpenShift Secret:**
Next, you need to create an OpenShift secret using the HTPasswd file you've just created. Replace htpasswdfile with the path to your HTPasswd file.
```bash
oc create secret generic htpass-secret --from-file=htpasswd=/path/to/htpasswdfile -n openshift-config
```
**Create a ClusterRoleBinding for the User:**
Now, you need to create a ClusterRoleBinding that associates the user with the cluster-admin role. This grants them admin privileges across all namespaces. You can use the following YAML to create the ClusterRoleBinding:
```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: admin-binding
subjects:
- kind: User
  name: username
  apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: ClusterRole
  name: cluster-admin
  apiGroup: rbac.authorization.k8s.io
```
