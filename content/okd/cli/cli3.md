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
>git@github.com:bluewhale-users/okd-tutorial3.git
Cloning into 'okd-tutorial3'...
remote: Enumerating objects: 16, done.
remote: Counting objects: 100% (16/16), done.
remote: Compressing objects: 100% (14/14), done.
remote: Total 16 (delta 4), reused 0 (delta 0), pack-reused 0
Receiving objects: 100% (16/16), done.
Resolving deltas: 100% (4/4), done.
```

### 2. oc login후 작업 프로젝트 확인(okd-tutorials)
```
>oc login --token=sha256~5xJaXd-nYyZcB5-2ckPv-bJeLKc8mShxO-F3RrS0JIU --server=https://api.your-okd.com:6443
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

