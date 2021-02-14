# jupyter-machine-learning ( Jupyter Setup in Kubernetes Cluster  )

Helm Charts to deploy Jupyter in Kubernetes Cluster for Machine Learning 

* Prerequisite 

    * kubernetes Setup kubectl 
    * kubernetes cluster 
    * Helm setup  

* Installing the Docker image with jupyter/all-spark-notebook 

    [See here](https://jupyter-docker-stacks.readthedocs.io/en/latest/)
   for more Docker images details.

    ```
    $ cd helm/jupyter/
    $ helm install jupyter . -f values.yaml
    ```

* Upgrade Jupyter 

    ```
    $ helm upgrade jupyter . -f values.yaml
    ```

* Access jupyter with locally

    ```
    $ export POD_NAME=$(kubectl get pods --namespace default -l "app.kubernetes.io/name=jupyter,app.kubernetes.io/instance=jupyter" -o jsonpath="{.items[0].metadata.name}")

    $ export CONTAINER_PORT=$(kubectl get pod --namespace default $POD_NAME -o jsonpath="{.spec.containers[0].ports[0].containerPort}")

    $ kubectl --namespace default port-forward $POD_NAME 8080:$CONTAINER_PORT

    ```


* Find the existing token from Jupyter instance 

    ```
    $ export POD_NAME=$(kubectl get pods --namespace default -l "app.kubernetes.io/name=jupyter,app.kubernetes.io/instance=jupyter" -o jsonpath="{.items[0].metadata.name}")

    $ kubectl exec -it $POD_NAME /bin/sh

    ```

* Print token from existing notebook after ssh into pod

    ```
    $ jupyter notebook list
    ```

* Open jupyter locally 

    [http://localhost:8080/](http://localhost:8080/)

* Delete deployment 
    ```
    $ helm delete jupyter
    ```