---
title: "CLI3 : oc apply"
date: 2022-04-13T09:35:35+09:00
draft: false
weight: 43
---

{{% notice info %}}
oc apply는 파일 또는 stdin을 통해 리소스 구성을 적용합니다. 
{{% /notice %}}


```
>oc apply --help
Apply a configuration to a resource by filename or stdin. The resource name must be specified. This resource will be
created if it doesn't exist yet. To use 'apply', always create the resource initially with either 'apply' or 'create
--save-config'.

 JSON and YAML formats are accepted.

 Alpha Disclaimer: the --prune functionality is not yet complete. Do not use unless you are aware of what the current
state is. See https://issues.k8s.io/34274.

Usage:
  oc apply (-f FILENAME | -k DIRECTORY) [flags]

Examples:
  # Apply the configuration in pod.json to a pod.
  oc apply -f ./pod.json

  # Apply resources from a directory containing kustomization.yaml - e.g. dir/kustomization.yaml.
  oc apply -k dir/

  # Apply the JSON passed into stdin to a pod.
  cat pod.json | oc apply -f -

  # Note: --prune is still in Alpha
  # Apply the configuration in manifest.yaml that matches label app=nginx and delete all the other resources that are
not in the file and match label app=nginx.
  oc apply --prune -f manifest.yaml -l app=nginx

  # Apply the configuration in manifest.yaml and delete all the other configmaps that are not in the file.
  oc apply --prune -f manifest.yaml --all --prune-whitelist=core/v1/ConfigMap

Available Commands:
  edit-last-applied Edit latest last-applied-configuration annotations of a resource/object
  set-last-applied  Set the last-applied-configuration annotation on a live object to match the contents of a file.
  view-last-applied View latest last-applied-configuration annotations of a resource/object

Options:
      --all=false: Select all resources in the namespace of the specified resource types.
      --allow-missing-template-keys=true: If true, ignore any errors in templates when a field or map key is missing in
the template. Only applies to golang and jsonpath output formats.
      --cascade='background': Must be "background", "orphan", or "foreground". Selects the deletion cascading strategy
for the dependents (e.g. Pods created by a ReplicationController). Defaults to background.
      --dry-run='none': Must be "none", "server", or "client". If client strategy, only print the object that would be
sent, without sending it. If server strategy, submit server-side request without persisting the resource.
      --field-manager='kubectl-client-side-apply': Name of the manager used to track field ownership.
  -f, --filename=[]: that contains the configuration to apply
      --force=false: If true, immediately remove resources from API and bypass graceful deletion. Note that immediate
deletion of some resources may result in inconsistency or data loss and requires confirmation.
      --force-conflicts=false: If true, server-side apply will force the changes against conflicts.
      --grace-period=-1: Period of time in seconds given to the resource to terminate gracefully. Ignored if negative.
Set to 1 for immediate shutdown. Can only be set to 0 when --force is true (force deletion).
  -k, --kustomize='': Process a kustomization directory. This flag can't be used together with -f or -R.
      --openapi-patch=true: If true, use openapi to calculate diff when the openapi presents and the resource can be
found in the openapi spec. Otherwise, fall back to use baked-in types.
  -o, --output='': Output format. One of:
json|yaml|name|go-template|go-template-file|template|templatefile|jsonpath|jsonpath-as-json|jsonpath-file.
      --overwrite=true: Automatically resolve conflicts between the modified and live configuration by using values from
the modified configuration
      --prune=false: Automatically delete resource objects, including the uninitialized ones, that do not appear in the
configs and are created by either apply or create --save-config. Should be used with either -l or --all.
      --prune-whitelist=[]: Overwrite the default whitelist with <group/version/kind> for --prune
      --record=false: Record current kubectl command in the resource annotation. If set to false, do not record the
command. If set to true, record the command. If not set, default to updating the existing annotation value only if one
already exists.
  -R, --recursive=false: Process the directory used in -f, --filename recursively. Useful when you want to manage
related manifests organized within the same directory.
  -l, --selector='': Selector (label query) to filter on, supports '=', '==', and '!='.(e.g. -l key1=value1,key2=value2)
      --server-side=false: If true, apply runs in the server instead of the client.
      --show-managed-fields=false: If true, keep the managedFields when printing objects in JSON or YAML format.
      --template='': Template string or path to template file to use when -o=go-template, -o=go-template-file. The
template format is golang templates [http://golang.org/pkg/text/template/#pkg-overview].
      --timeout=0s: The length of time to wait before giving up on a delete, zero means determine a timeout from the
size of the object
      --validate=false: If true, use a schema to validate the input before sending it
      --wait=false: If true, wait for resources to be gone before returning. This waits for finalizers.

Use "oc <command> --help" for more information about a given command.
Use "oc options" for a list of global command-line options (applies to all commands).
```

- [tutorial github](https://github.com/bluewhale-users/okd-tutorial3)

### 1. 리파지터리를 Clone
```
>git clone git@github.com:bluewhale-users/okd-tutorial3.git
Cloning into 'okd-tutorial3'...
remote: Enumerating objects: 16, done.
remote: Counting objects: 100% (16/16), done.
remote: Compressing objects: 100% (14/14), done.
remote: Total 16 (delta 4), reused 0 (delta 0), pack-reused 0
Receiving objects: 100% (16/16), done.
Resolving deltas: 100% (4/4), done.
```

- 폴더 구조
```
D:\GIT\OKD-TUTORIAL3
|   LICENSE
|   README.md
|
\---manifests
        deployment.yml
        route.yml
        service.yml
```

### 2. oc login후 작업 프로젝트 확인(okd-tutorials)
```
>oc login --token=sha256~5xJaXd-nYyZcB5-2ckPv******************** --server=https://api.your-okd.com:6443
Logged into "https://api.your-okd.com:6443" as "user@your-okd.com" using the token provided.

You have access to 94 projects, the list has been suppressed. You can list all projects with 'oc projects'

Using project "okd-tutorials".
```

### 3. 폴더 이동
```
>cd okd-tutorial3
>cd manifests
```

### 5. deployment 적용
```
>oc apply -f deployment.yml
deployment.apps/tutorial-frontend created
```

- deployment.yaml
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: tutorial-frontend
  annotations:
    fluxcd.io/automated: "true"
spec:
  replicas: 1
  selector:
    matchLabels:
      app: tutorial-frontend
  strategy:
    rollingUpdate:
      maxSurge: 1
      maxUnavailable: 1
  minReadySeconds: 5
  template:
    metadata:
      labels:
        app: tutorial-frontend
    spec:
      containers:
      - name: tutorial-frontend
        image: docker.io/spcsenti/tutorial2-src:latest
        ports:
        - containerPort: 3000
        resources:
          requests:
            cpu: 250m
          limits:
            cpu: 500m
```

{{< figure src="/cli/cli3_1.jpg" >}}

### 6. service 적용
```
>oc apply -f service.yml
service/tutorial-frontend created
```

- service.yaml
```
apiVersion: v1
kind: Service
metadata:
  name: tutorial-frontend
spec:
  type: LoadBalancer
  ports:
    - port: 3000
      targetPort: 3000
  selector:
    app: tutorial-frontend
```

### 7. route 적용
```
>oc apply -f route.yml
route.route.openshift.io/tutorial-frontend created
```

- route.yaml
```
apiVersion: route.openshift.io/v1
kind: Route
metadata:
  labels:
    app: tutorial-frontend
  name: tutorial-frontend
spec:
  port:
    targetPort: 3000
  to:
    kind: Service
    name: tutorial-frontend
    weight: 100
```

- 토폴로지 화면에서 open url을 눌러 확인  
{{< figure src="/cli/cli3_2.jpg" >}}

### 8. 동작 확인
{{< figure src="/cli/cli3_3.jpg" >}}

### 9. 생성 리소스 삭제

```
oc delete ([-f FILENAME] | [-k DIRECTORY] | TYPE [(NAME | -l label | --all)]) [flags]
```

```
>oc delete --help
Delete resources by filenames, stdin, resources and names, or by resources and label selector.

 JSON and YAML formats are accepted. Only one type of the arguments may be specified: filenames, resources and names, or
resources and label selector.

 Some resources, such as pods, support graceful deletion. These resources define a default period before they are
forcibly terminated (the grace period) but you may override that value with the --grace-period flag, or pass --now to
set a grace-period of 1. Because these resources often represent entities in the cluster, deletion may not be
acknowledged immediately. If the node hosting a pod is down or cannot reach the API server, termination may take
significantly longer than the grace period. To force delete a resource, you must specify the --force flag. Note: only a
subset of resources support graceful deletion. In absence of the support, --grace-period is ignored.

 IMPORTANT: Force deleting pods does not wait for confirmation that the pod's processes have been terminated, which can
leave those processes running until the node detects the deletion and completes graceful deletion. If your processes use
shared storage or talk to a remote API and depend on the name of the pod to identify themselves, force deleting those
pods may result in multiple processes running on different machines using the same identification which may lead to data
corruption or inconsistency. Only force delete pods when you are sure the pod is terminated, or if your application can
tolerate multiple copies of the same pod running at once. Also, if you force delete pods the scheduler may place new
pods on those nodes before the node has released those resources and causing those pods to be evicted immediately.

 Note that the delete command does NOT do resource version checks, so if someone submits an update to a resource right
when you submit a delete, their update will be lost along with the rest of the resource.

Usage:
  oc delete ([-f FILENAME] | [-k DIRECTORY] | TYPE [(NAME | -l label | --all)]) [flags]

Examples:
  # Delete a pod using the type and name specified in pod.json.
  oc delete -f ./pod.json

  # Delete resources from a directory containing kustomization.yaml - e.g. dir/kustomization.yaml.
  oc delete -k dir

  # Delete a pod based on the type and name in the JSON passed into stdin.
  cat pod.json | oc delete -f -

  # Delete pods and services with same names "baz" and "foo"
  oc delete pod,service baz foo

  # Delete pods and services with label name=myLabel.
  oc delete pods,services -l name=myLabel

  # Delete a pod with minimal delay
  oc delete pod foo --now

  # Force delete a pod on a dead node
  oc delete pod foo --force

  # Delete all pods
  oc delete pods --all

Options:
      --all=false: Delete all resources, including uninitialized ones, in the namespace of the specified resource types.
  -A, --all-namespaces=false: If present, list the requested object(s) across all namespaces. Namespace in current
context is ignored even if specified with --namespace.
      --cascade='background': Must be "background", "orphan", or "foreground". Selects the deletion cascading strategy
for the dependents (e.g. Pods created by a ReplicationController). Defaults to background.
      --dry-run='none': Must be "none", "server", or "client". If client strategy, only print the object that would be
sent, without sending it. If server strategy, submit server-side request without persisting the resource.
      --field-selector='': Selector (field query) to filter on, supports '=', '==', and '!='.(e.g. --field-selector
key1=value1,key2=value2). The server only supports a limited number of field queries per type.
  -f, --filename=[]: containing the resource to delete.
      --force=false: If true, immediately remove resources from API and bypass graceful deletion. Note that immediate
deletion of some resources may result in inconsistency or data loss and requires confirmation.
      --grace-period=-1: Period of time in seconds given to the resource to terminate gracefully. Ignored if negative.
Set to 1 for immediate shutdown. Can only be set to 0 when --force is true (force deletion).
      --ignore-not-found=false: Treat "resource not found" as a successful delete. Defaults to "true" when --all is
specified.
  -k, --kustomize='': Process a kustomization directory. This flag can't be used together with -f or -R.
      --now=false: If true, resources are signaled for immediate shutdown (same as --grace-period=1).
  -o, --output='': Output mode. Use "-o name" for shorter output (resource/name).
      --raw='': Raw URI to DELETE to the server.  Uses the transport specified by the kubeconfig file.
  -R, --recursive=false: Process the directory used in -f, --filename recursively. Useful when you want to manage
related manifests organized within the same directory.
  -l, --selector='': Selector (label query) to filter on, not including uninitialized ones.
      --timeout=0s: The length of time to wait before giving up on a delete, zero means determine a timeout from the
size of the object
      --wait=true: If true, wait for resources to be gone before returning. This waits for finalizers.

Use "oc options" for a list of global command-line options (applies to all commands).
```


- deployment 삭제
  
```
>oc delete -f deployment.yml
deployment.apps "tutorial-frontend" deleted
```

{{< figure src="/cli/cli3_4.jpg" >}}

- service 삭제
{{< figure src="/cli/cli3_5.jpg" >}}

```
>oc delete -f service.yml
service "tutorial-frontend" deleted
```

{{< figure src="/cli/cli3_6.jpg" >}}

- route 삭제

{{< figure src="/cli/cli3_7.jpg" >}}

```
>oc delete -f route.yml
route.route.openshift.io "tutorial-frontend" deleted
```

{{< figure src="/cli/cli3_8.jpg" >}}
