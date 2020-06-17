### Prerequisites

Things you need to install.

- Install [docker](https://docs.docker.com/install/)

- Install [kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)

- Enable kubernetes in docker setting (Kubernetes fan)

- Install [helm](https://helm.sh/docs/intro/install/)

## Database

- Install database [postgresql](https://hub.helm.sh/charts/bitnami/postgresql)

```
    helm repo add bitnami https://charts.bitnami.com/bitnami
    helm install postgres bitnami/postgresql
```

- Get postgresql password:

```
export POSTGRES_PASSWORD=$(kubectl get secret --namespace default postgres-postgresql -o jsonpath="{.data.postgresql-password}" | base64 --decode)

echo $POSTGRES_PASSWORD
```

## Hasura:

Let's deploy [Hasura](./k8s/Hasura) in kubernetes.

Update [deployment.yaml](./k8s/Hasura/deployment.yml) hasura deployment file - locally - with your postgres password.

```
env:
- name: HASURA_GRAPHQL_DATABASE_URL
    value: "postgresql://postgres:<YourPostgresPassword>@postgresql:5432/postgres"
```

Finally run:

`kubectl apply -f ./k8s/hasura`

Expose hasura from cluster to localhost:

`kubectl port-forward svc/hasura-service 9001`

Now Hasura i availibale at: http://localhost:9001
