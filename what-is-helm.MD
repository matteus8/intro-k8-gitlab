# What is Helm
Helm, also populary know as 'the Helm Chart' is a simple way of saying 'all them yaml files'.
If your familier with package managers in linux (like apt or yum or dnf) helm is just that,
a package manager for Kubernetes. 

Read the ['what-is-kubernetes'](./what-is-kubernetes.MD) for a better understand of .yaml files.

It's important to note here that:
- Helm ≠ Helm Chart ≠ Manifest, **BUT**:
    - Helm uses Helm charts as its input.
    - Helm charts generate manifests (YAML files) to apply to your cluster.

Helm is a tool used to manage super large kubernetes deployment. These deployments have many K8 resource yaml files. It's important to note that Helm uses a very specific directory structure. It will almost always look something like this:
```bash
my-helm-chart/
├── Chart.yaml          # Metadata about the Helm chart
├── values.yaml         # Default values for the chart
├── templates/          # Directory for Kubernetes resource templates
│   ├── deployment.yaml # Example Deployment manifest
│   ├── service.yaml    # Example Service manifest
│   ├── ingress.yaml    # Example Ingress manifest
│   ├── _helpers.tpl    # Helper templates (optional)
│   └── NOTES.txt       # Post-installation notes (optional)
├── charts/             # Directory for dependencies (optional)
├── crds/               # Custom Resource Definitions (optional)
├── templates/tests/    # Directory for test templates (optional)
│   └── test-connection.yaml
└── README.md           # Documentation for the chart (optional)
```

Now before you panic, remember what we said, helm is a package manager. You will likley never have to see this **entire** chart unless you are building it yourself. Helm, the package manager, has already bundled all this up for us to use. Just like if you were to zip a file in windows or perhaps create a tar ball in linux ```using tar -cvf```.

Helm has already created the package (zip/tarball equivalant), so all you have to do is install it.

## Steps to Install a Chart

### 1. Add the bitnami chart repositroy to your local Helm setup. 

    ```helm repo add bitnami https://charts.bitnami.com/bitnami```
    > Bitnami is a popular repository with many usefull charts. Bitnami is one big open-source software company (though its now owned by VMWare) that helps variouse projects package their application for kubernetes using helm. You can learn more about them [here](https://www.vmware.com/products/app-platform/tanzu-application-catalog)

What does this command mean:
* When you add a Helm repositroy, your essentially saying: "hey, on my local computer, I've got a little directory/folder (let's call it my  'helm_metadata_bucket'") where Helm keeps track of pointers to online repositories.

* The ```helm repo add <name> <url>``` command does not download the actual chart files (like YAML templates) yet.
Instead it adds some local metadata to your local bucket that says "Here's where I can find the chart stored at < url >."
* Think of it like bookmarking a website in your browser - your just saving the location (URL) for future use, not downlaoding the entire site.

### Step 2: Update the Repository and Search for Charts
After adding a repository, you’ll want to update your local Helm metadata to make sure you have the latest list of charts available from that repository. This ensures you're working with up-to-date information. You can do this with the command ```helm repo update```.

Once your repository metadata is updated, you can search for a specific chart. For example, if you’re looking for a chart related to nginx in the Bitnami repository:
```helm search repo bitnami/nginx```.

### Step 3: Install the Chart
Now that you’ve added the repository and updated your local Helm metadata, it’s time to install the chart! Installing a chart means downloading the necessary files and deploying the associated Kubernetes resources ([like deployments, services, ConfigMaps, etc.](./what-is-kubernetes.MD)) to your cluster. There are two ways to do this:

#### Option 1 - Install the Chart directly to the cluster
With this meathod, helm will do the following behind the scenes:
1. checks your local metadata bucket created in step 1
2. pull down the chart files from the url, which are tyically packaged as a .tgz (think of a tarball or zip file)
3. create a temporary directory
4. unpack the .tgz into the temp directory
5. reads the conents and install to your k8's cluster

You can do all this simply by running this command:
```helm install <random-name> bitnami/nginx```
* the < random-name > is just a label (a name) your personally are giving the chart, nothing fancy. Just to help you identify this deployment later.

* the < bitnami/nginx > ... This tells Helm to install the nginx chart from the Bitnami repository.
    * In short this command just says "Hey Helm, install the nginx chart from the Bitnami repository and call this release < random-name >". Everything else happens in the backaground.

#### Option 2 - Download the files to your local computer
If you have to get all the files locally-maybe for an air gapped deplyment, to do some serious development, or just need to edit the value.yaml file- this is the option for you.
> values.yaml is the primary way to make changes to any helm chart and we will talk more about shortly. 

To download and unpack the chart locally, use this command:
```bash
helm pull <repo-name>/<chart-name> --untar
```
This command will download the appropriate chart and automatically unzip/untar it in your current directory (the one from which you ran the command).