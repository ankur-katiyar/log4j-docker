# Log4j Vulnerability - Proof-of-concept

This repo has the docker and k8s YAMLs that are needed to recreate the log4j vulnerability (seel below).

Follow [this blog](https://medium.com/@ankurkatiyar/cve-2021-44228-proof-of-concept-on-kubernetes-34c7337e8a89) to understand how all of this is tied together.
#
## Build Docker Images

In case you need to customize the docker images

```bash
  cd <Git-Repo>/web-server
  make build push
```

```bash
  cd <Git-Repo>/marshalsec
  make build push
```

```bash
  cd <Git-Repo>/attack-server
  make build push
```
Make sure that you update the DockerHub to reflect your user-id before attempting to push.

For the POC, you don't need to customize the docker images.

#

## Deploy on Kubernetes

You can deploy the YAMLs under the k8s folder to any Kubernetes Cluster.

```bash
  cd <Git-Repo>/k8s
  kubectl create -f .
```

This will deploy 3 PODs on the cluster, each reprenting an "actor" playing it's part for us to understsand how the log4j vunerability works.

In addition to the YAMLs included here, you will need to deploy an Ingress on the Kubernetes cluster to allow testing the vunerable web app from public end-points.

Heres a sample that works for Ngnix-Ingress.

```YAML
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: log4j-ingress
  labels:
    app: log4j
    env: dev
  namespace: log4j
  annotations:
    nginx.ingress.kubernetes.io/affinity: "cookie"
    nginx.ingress.kubernetes.io/session-cookie-name: "route"
    nginx.ingress.kubernetes.io/session-cookie-expires: "172800"
    nginx.ingress.kubernetes.io/session-cookie-max-age: "172800"
    nginx.ingress.kubernetes.io/ssl-redirect: "false"
    nginx.ingress.kubernetes.io/force-ssl-redirect: "false"
    #nginx.ingress.kubernetes.io/rewrite-target: /
spec:
  tls:
  - hosts:
    - <YOUR-DOMAIN-NAME-HERE>
    #secretName: tls-java-secret
  rules:
  - host: <YOUR-DOMAIN-NAME-HERE>
    http:
      paths:
        - path: /
          backend:
            serviceName: log4j-webserver
            servicePort: 8080

```


#
## Authors
- [@ankur-katiyar](https://www.github.com/ankur-katiyar)

## Resources
 - [CVE-2021-44228](https://nvd.nist.gov/vuln/detail/CVE-2021-44228)


## License

[GNU General Public License v3.0](https://choosealicense.com/licenses/gpl-3.0/)