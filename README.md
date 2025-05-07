# megabank-postgres
Implementation of MegaBank that uses EDB PostgreSQL rather than Db2

This branch requires that the EDB PostgreSQL operator is already deployed on the OpenShift cluster.

 ## Deploy with EDB 

1. Create a new project:
    ```
    oc new-project megabank-pg
    ```

2. Give the `default` scc elevated privileges:

    ```
    oc -n megabank-pg adm policy add-scc-to-user anyuid -z default
    ```

3. Deploy the application.
    ```
    oc apply -f backend -f frontend -f database
    ```

    Alternatively, deploy it using GitOps tooling such as ArgoCD, FluxCD, or Red Hat Advanced Cluster Management.

4. Expose the `mbweb` service as a route.

    ```
    oc expose service/mbweb
    ```

5. Access MegaBank at the `MegaBank` endpoint:

    ```
    ROUTE=$(oc -n megabank-pg get route mbweb -o jsonpath='{.spec.host}')
    echo "http://${ROUTE}/MegaBank"
    ```
