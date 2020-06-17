## Database:

##### To get the password for "postgres" run:

    export POSTGRES_PASSWORD=$(kubectl get secret --namespace database postgresql-1590685458 -o jsonpath="{.data.postgresql-password}" | base64 --decode)

#### Local

    export POSTGRES_PASSWORD=$(kubectl get secret --namespace default postgresql-1591868440 -o jsonpath="{.data.postgresql-password}" | base64 --decode)

##### To connect to your database run the following command:

    kubectl run postgresql-1590685458-client --rm --tty -i --restart='Never' --namespace database --image docker.io/bitnami/postgresql:11.8.0-debian-10-r13 --env="PGPASSWORD=$POSTGRES_PASSWORD" --command -- psql --host postgresql-1590685458 -U postgres -d postgres -p 5432

##### To connect to your database from outside the cluster execute the following commands:

    kubectl port-forward --namespace database svc/postgresql-1590685458 5432:5432 &
    PGPASSWORD="$POSTGRES_PASSWORD" psql --host 127.0.0.1 -U postgres -d postgres -p 5432

## Hasura:

    http://klostra-backend.50109b3386884be38c0a.northeurope.aksapp.io
