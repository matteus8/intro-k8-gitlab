# What is Kubernetes
Kubernetes is, in fancy terms, a container orchastation manager. But what the junk is this. Essentially without getting real techinical, kubernetes is a super sonic virtual assistant that can help install applications really fast. For the purpose of deploying gitlab it's really important to undertand what containers are and how kubernetes uses them.  

> FUN FACT: **Kubernetes** can be shortened to **K8's**. This is because Kubernetes start with K and ends with S with eight letter between. **K_U_B_E_R_N_E_T_E_S** (K8'S)

## What is a Virtual Machine (VM) and what is a container
There are like a gazillion videos explaining the diffrance between a container and a VM. People much more qualified then me can use graphics and illustrations. Just google this "what is the diffrance between a container and virtual machine".

Okay, did you do that, got it? cool.

## How does kubernetes work with containers
1. Containers:
* Because containers are essentially the application packaged up all nicely. You, as an SA, can now tell kubernetes to take that image (not to be confused with a container; they are different), and use it in the cluster.

2. How do we tell Kubernetes what to do?
* Use a yaml file:
  * A .yaml file or .yml (they are the same essentially) will list the intructions for Kubernetes. This file structure is very specific. Again there are many videos and graphics out there on the syntax (formatting) of this .yaml file.

3. Do we need just one file or lots of files?

This depands...

K8's can use just one file like this, with the deliminator '**---**' as the seperator for certain resource:

### Two Object Resources In One File
```
    apiVersion: apps/v1
    kind: Deployment
    metadata:
    name: myapp-deployment
    spec:
    replicas: 3
    selector:
        matchLabels:
        app: myapp
    template:
        metadata:
        labels:
            app: myapp
        spec:
        containers:
        - name: myapp-container
            image: myapp:latest
            ports:
            - containerPort: 80

    ---

    apiVersion: v1
    kind: Service
    metadata:
    name: myapp-service
    spec:
    selector:
        app: myapp
    ports:
    - protocol: TCP
        port: 80
        targetPort: 80
    type: LoadBalancer
```

BUT, it's better to seperate these into two files in most cases, like this...

### Two Object Resources In Two Files
FILE 1
```
    apiVersion: apps/v1
    kind: Deployment
    metadata:
    name: myapp-deployment
    spec:
    replicas: 3
    selector:
        matchLabels:
        app: myapp
    template:
        metadata:
        labels:
            app: myapp
        spec:
        containers:
        - name: myapp-container
            image: myapp:latest
            ports:
            - containerPort: 80

```
FILE 2
```
    apiVersion: v1
    kind: Service
    metadata:
    name: myapp-service
    spec:
    selector:
        app: myapp
    ports:
    - protocol: TCP
        port: 80
        targetPort: 80
    type: LoadBalancer
```

Now I know, you are very confused. Why create two files when you can have one. Well, now lets have a little chat about Kuberenetes diabolical ways, and how it does buisness. 

## K8 Words(resources)

To better underantd how these files interact with K8's,you must underatnd the world of Kubernetes has it's own language. If you are not familier with these terms or resources, as I refer to them, just refrance the below real quick:

- Objects = Mostly the applications themselves (think pods)

- Services = Mostly Networking Related resources (how to access the applications)

- Namespace = Groupings of items (think isolatation)

- Manifest/Configuration/Blueprint = could have many meanings, but in short, these words are like a universal way of saying "that kubernetes yaml file or files"

Okay, yes, this is WAY over simplified and there are like a trillion other words and terms related to kubernetes, but to not overwhelm you, this is the basics.

## Putting this all togeather
Lets look back at our two .yaml files from above

FILE 1
```
    apiVersion: apps/v1
    kind: Deployment
    metadata:
    name: myapp-deployment
    spec:
    replicas: 3
    selector:
        matchLabels:
        app: myapp
    template:
        metadata:
        labels:
            app: myapp
        spec:
        containers:
        - name: myapp-container
            image: myapp:latest
            ports:
            - containerPort: 80
```

FILE 2
```
    apiVersion: v1
    kind: Service
    metadata:
    name: myapp-service
    spec:
    selector:
        app: myapp
    ports:
    - protocol: TCP
        port: 80
        targetPort: 80
    type: LoadBalancer
```

Did you see that...

* the **kind:** for file 1 is? 
* and what about for file 2?

## Conclusion
I hope this somehow put togeather the mystery of kubernetes. It's not magic, it's just a bunch of .yaml files telling an virtualized super system admin what to do.

Of course this sounds much simpliar then it is. But we must go slow before we go fast.