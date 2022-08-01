
1. Downlaod and install python 3 on local machine (if not already installed): https://www.python.org/downloads/
2. ```cd``` to project directory and create a virtual enviroment
    ```
    $ python3 -m venv env
    ```
3. Activate virtual enviroment
    ```
    $ source env/bin/activate
    ```
4. Install dependencies
    ```
    $ pip3 install -r requirements.txt
    ```
5. Create and add an SSH key to your digital ocean account:
https://docs.digitalocean.com/products/droplets/how-to/add-ssh-keys/to-team/
6. Create a digital ocean access token for API requests:
https://docs.digitalocean.com/reference/api/create-personal-access-token/
7. Add the token to your environment:
    ```sh
    $ export DIGITAL_OCEAN_ACCESS_TOKEN=[your_token]
    ```
8. Spin up the cluster
    ```sh
    $ bash create.sh
    ```
9. Add kube config to local machine
Copy and paste the output from script below line "*++++++ Copy the below output and paste into kube config on local machine ++++++*" into the open text file. Save and close.
    ```
    $ cd ~/.kube
    ```
    ```
    $ open -a TextEdit config
    ```
    
10. Test local machine has cluster access
    ```
    $ kubectl get nodes -o wide
    ```
11. Create app namespace and set context
    ```
    $ kubectl create namespace {namespace} (example: elasticsearch-ns)
    ```
    ```
    $ kubectl config set-context kubernetes-admin@kubernetes --namespace={namespace name}
    ```
12. Install Traefik
    ```
    $ helm repo add traefik https://helm.traefik.io/traefik
    ```
    ```
    $ helm repo update
    ```
    ```
    $ helm install traefik traefik/traefik --namespace traefik --create-namespace
    ```
13. Access traefik dashboard 
    ```
    $ kubectl get pods -n traefik
    ```
    ```
    $ kubectl port-forward {pod name} 9000:9000 -n traefik
    ```
    Go to http://127.0.0.1:9000/dashboard/#/ to ensure traefik is up and running.

14. Add all required K8 resorces to cluster using the command ```kubectl apply -f {path/to/yaml}``` Enjoy :)