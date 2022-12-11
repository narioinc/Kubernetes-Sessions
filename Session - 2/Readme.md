# Install NGINX ingress:

``` $> kubectl apply -f nginx-ingress-controller.yaml ```

# Install the ingress rule

``` $> kubectl apply -f httpbin-ingress.yaml ```

# Access the service
* run minikube tunnel to create a artificial loadbalancer setup  ``` $> minikube tunnel ```
* now access the service on http://localhost:80
* curl on the same URL
* postman on the same URL    



