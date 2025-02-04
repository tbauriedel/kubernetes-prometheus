# Installation
```
helm repo add longhorn https://charts.longhorn.io
helm repo update
helm install longhorn longhorn/longhorn --namespace longhorn-system --create-namespace --version 1.7.2
```

# Basic Auth

Also documented inside the [ official longhorn docs](https://longhorn.io/docs/1.8.0/deploy/accessing-the-ui/longhorn-ingress/).

Create secret:  
```
USER=<USERNAME_HERE>; PASSWORD=<PASSWORD_HERE>; echo "${USER}:$(openssl passwd -stdin -apr1 <<< ${PASSWORD})" >> auth

kubectl -n longhorn-system create secret generic basic-auth --from-file=auth
```

Add these annotations to the Ingress:  
```
annotations:
    # type of authentication
    nginx.ingress.kubernetes.io/auth-type: basic
    # prevent the controller from redirecting (308) to HTTPS
    nginx.ingress.kubernetes.io/ssl-redirect: 'false'
    # name of the secret that contains the user/password definitions
    nginx.ingress.kubernetes.io/auth-secret: basic-auth
    # message to display with an appropriate context why the authentication is required
    nginx.ingress.kubernetes.io/auth-realm: 'Authentication Required '
```