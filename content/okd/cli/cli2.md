---
title: "Cli2 : Basic Commands"
date: 2022-03-31T15:53:12+09:00
draft: false
weight: 42
---


No		| Command                       | Description
:------	|:-------			            |:-------			            
1       | new-project                   | Request a new Project
2       | new-app                       | Request a new application
3       | projects                      | Display existing project
4       | project                       | Switch to another project


### 1. new-project
``` command
C:\Users\user>oc new-project --help
Create a new project for yourself.

 If your administrator allows self-service, this command will create a new project for you and assign you as the project
admin.

 After your project is created it will become the default project in your config.

Usage:
  oc new-project NAME [--display-name=DISPLAYNAME] [--description=DESCRIPTION] [flags]

Examples:
  # Create a new project with minimal information
  oc new-project web-team-dev

  # Create a new project with a display name and description
  oc new-project web-team-dev --display-name="Web Team Development" --description="Development project for the web
team."

Options:
      --description='': Project description
      --display-name='': Project display name
      --skip-config-write=false: If true, the project will not be set as a cluster entry in kubeconfig after being
created

Use "oc options" for a list of global command-line options (applies to all commands).
```

### 2. new-app
``` command
C:\Users\user>oc new-app --help
Create a new application by specifying source code, templates, and/or images.

 This command will try to build up the components of an application using images, templates, or code that has a public
repository. It will look up the images on the local Docker installation (if available), a container image registry, an
integrated image stream, or stored templates.

 If you specify a source code URL, it will set up a build that takes your source code and converts it into an image that
can run inside of a pod. Local source must be in a git repository that has a remote repository that the server can see.
The images will be deployed via a deployment or deployment configuration, and a service will be connected to the first
public port of the app. You may either specify components using the various existing flags or let oc new-app autodetect
what kind of components you have provided.

 If you provide source code, a new build will be automatically triggered. You can use 'oc status' to check the progress.

Usage:
  oc new-app (IMAGE | IMAGESTREAM | TEMPLATE | PATH | URL ...) [flags]

Examples:
  # List all local templates and image streams that can be used to create an app
  oc new-app --list

  # Create an application based on the source code in the current git repository (with a public remote) and a Docker
image
  oc new-app . --docker-image=registry/repo/langimage

  # Create an application myapp with Docker based build strategy expecting binary input
  oc new-app  --strategy=docker --binary --name myapp

  # Create a Ruby application based on the provided [image]~[source code] combination
  oc new-app centos/ruby-25-centos7~https://github.com/sclorg/ruby-ex.git

  # Use the public Docker Hub MySQL image to create an app. Generated artifacts will be labeled with db=mysql
  oc new-app mysql MYSQL_USER=user MYSQL_PASSWORD=pass MYSQL_DATABASE=testdb -l db=mysql

  # Use a MySQL image in a private registry to create an app and override application artifacts' names
  oc new-app --docker-image=myregistry.com/mycompany/mysql --name=private

  # Create an application from a remote repository using its beta4 branch
  oc new-app https://github.com/openshift/ruby-hello-world#beta4

  # Create an application based on a stored template, explicitly setting a parameter value
  oc new-app --template=ruby-helloworld-sample --param=MYSQL_USER=admin

  # Create an application from a remote repository and specify a context directory
  oc new-app https://github.com/youruser/yourgitrepo --context-dir=src/build

  # Create an application from a remote private repository and specify which existing secret to use
  oc new-app https://github.com/youruser/yourgitrepo --source-secret=yoursecret

  # Create an application based on a template file, explicitly setting a parameter value
  oc new-app --file=./example/myapp/template.json --param=MYSQL_USER=admin

  # Search all templates, image streams, and Docker images for the ones that match "ruby"
  oc new-app --search ruby

  # Search for "ruby", but only in stored templates (--template, --image-stream and --docker-image
  # can be used to filter search results)
  oc new-app --search --template=ruby

  # Search for "ruby" in stored templates and print the output as YAML
  oc new-app --search --template=ruby --output=yaml

Options:
      --allow-missing-images=false: If true, indicates that referenced Docker images that cannot be found locally or in
a registry should still be used.
      --allow-missing-imagestream-tags=false: If true, indicates that image stream tags that don't exist should still be
used.
      --allow-missing-template-keys=false: If true, ignore any errors in templates when a field or map key is missing in
the template. Only applies to golang and jsonpath output formats.
      --as-deployment-config=false: If true create this application as a deployment config, which allows for hooks and
custom strategies.
      --as-test=false: If true create this application as a test deployment, which validates that the deployment
succeeds and then scales down.
      --binary=false: Instead of expecting a source URL, set the build to expect binary contents. Will disable triggers.
      --build-env=[]: Specify a key-value pair for an environment variable to set into each build image.
      --build-env-file=[]: File containing key-value pairs of environment variables to set into each build image.
      --code=[]: Source code to use to build this application.
      --context-dir='': Context directory to be used for the build.
      --docker-image=[]: Name of a Docker image to include in the app.  Note:  not specifying a registry or repository
means defaults in place for client image pulls are employed.
      --dry-run=false: If true, show the result of the operation without performing it.
  -e, --env=[]: Specify a key-value pair for an environment variable to set into each container.
      --env-file=[]: File containing key-value pairs of environment variables to set into each container.
  -f, --file=[]: Path to a template file to use for the app.
      --grant-install-rights=false: If true, a component that requires access to your account may use your token to
install software into your project. Only grant images you trust the right to run with your token.
      --group=[]: Indicate components that should be grouped together as <comp1>+<comp2>.
      --ignore-unknown-parameters=false: If true, will not stop processing if a provided parameter does not exist in the
template.
  -i, --image-stream=[]: Name of an image stream to use in the app.
      --insecure-registry=false: If true, indicates that the referenced Docker images are on insecure registries and
should bypass certificate checking
  -l, --labels='': Label to set in all resources for this application.
  -L, --list=false: List all local templates and image streams that can be used to create.
      --name='': Set name to use for generated application artifacts
      --no-install=false: Do not attempt to run images that describe themselves as being installable
  -o, --output='': Output format. One of:
json|yaml|name|go-template|go-template-file|template|templatefile|jsonpath|jsonpath-as-json|jsonpath-file.
      --output-version='': The preferred API versions of the output objects
  -p, --param=[]: Specify a key-value pair (e.g., -p FOO=BAR) to set/override a parameter value in the template.
      --param-file=[]: File containing parameter values to set/override in the template.
  -S, --search=false: Search all templates, image streams, and Docker images that match the arguments provided.
  -a, --show-all=true: When printing, show all resources (false means hide terminated pods.)
      --show-labels=false: When printing, show all labels as the last column (default hide labels column)
      --show-managed-fields=false: If true, keep the managedFields when printing objects in JSON or YAML format.
      --sort-by='': If non-empty, sort list types using this field specification.  The field specification is expressed
as a JSONPath expression (e.g. '{.metadata.name}'). The field in the API resource specified by this JSONPath expression
must be an integer or a string.
      --source-secret='': The name of an existing secret that should be used for cloning a private git repository.
      --strategy=: Specify the build strategy to use if you don't want to detect (docker|pipeline|source). NOTICE: the
pipeline strategy is deprecated; consider using Jenkinsfiles directly on Jenkins or OpenShift Pipelines.
      --template=[]: Name of a stored template to use in the app.

Use "oc options" for a list of global command-line options (applies to all commands).
```

### 3. projects
``` command
C:\Users\user>oc projects
You have access to the following projects and can switch between them with ' project <projectname>':

    openshift
    openshift-apiserver
    openshift-apiserver-operator
    openshift-authentication
    openshift-authentication-operator
    openshift-cloud-controller-manager
    openshift-cloud-controller-manager-operator
    openshift-cloud-credential-operator
    openshift-cluster-csi-drivers
    openshift-cluster-machine-approver
    openshift-cluster-node-tuning-operator
    openshift-cluster-samples-operator
    openshift-cluster-storage-operator
    openshift-cluster-version
    openshift-config
    openshift-config-managed
    openshift-config-operator
    openshift-console
    openshift-console-operator
    openshift-console-user-settings
    openshift-controller-manager
    openshift-controller-manager-operator
    openshift-dns
    openshift-dns-operator
    openshift-etcd
    openshift-etcd-operator
    openshift-host-network
    openshift-image-registry
    openshift-infra
    openshift-ingress
    openshift-ingress-canary
    openshift-ingress-operator
    openshift-insights
    openshift-kni-infra
    openshift-kube-apiserver
    openshift-kube-apiserver-operator
    openshift-kube-controller-manager
    openshift-kube-controller-manager-operator
    openshift-kube-scheduler
    openshift-kube-scheduler-operator
    openshift-kube-storage-version-migrator
    openshift-kube-storage-version-migrator-operator
    openshift-kubevirt-infra
    openshift-machine-api
    openshift-machine-config-operator
    openshift-marketplace
    openshift-monitoring
    openshift-multus
    openshift-network-diagnostics
    openshift-network-operator
    openshift-node
    openshift-oauth-apiserver
    openshift-openstack-infra
    openshift-operator-lifecycle-manager
    openshift-operators
    openshift-ovirt-infra
    openshift-ovn-kubernetes
    openshift-service-ca
    openshift-service-ca-operator
    openshift-terminal
    openshift-user-workload-monitoring
    openshift-vsphere-infra
    podnaming-test
    quay

Using project "okd-tutorial" on server "https://api.your-okd.com:6443".
```

### 4. project
```
C:\Users\user>oc project openshift-operators
Now using project "openshift-operators" on server "https://api.your-okd.com:6443".
```