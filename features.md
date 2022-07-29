# helm-demo

### Features in Demo:
- Charts availability as a helm repo
- Usage of dependent modules as subcharts
- Common template code for general or useful functions
- Each chart represented as a standalone chart
- Sharing variables between parent and child OR global values across charts
- Schema files for validation of data types
- Hooks for migrations, updates etc,.
- Post install notes and Post install validation messages
- Each component as a standalone helm chart and an independent release
- Auto Secrets injection into requires charts
- General idea on how to test a chart post install
- Favoring helm functions / new services rather than ansible
- Almost everything has a default value
- Upgrading few services
- Private repo overrides
- Fail on missing vars, fail on incompatible kubernetes version

### Future Features:
- Some sort of wrapper to run all the charts on new install and wrappers for each upgrade
- Github actions to auto update chart versions on helm repo on each commit / tag
- Chart testing using circle ci or helm github actions on full installtion along with functional test cases
- Operators for backup and restore and other operations
- Monitoring metrics and log parsing enabling / disabling with a flag
- End of install helm chart to get all values and store in a file to be stored in private repo

### Insallation Instructions
- Pre-requistes
  - Kubernetes cluster
  - If you are not on Kubernetes 1.23.x version, then update this file to match your version https://github.com/keshavprasadms/helm-auth/blob/master/kong-jwt-secrets/Chart.yaml#L25
  - For 1.24.3 Kubernetes version, you can update it as `~1.24.x` and so on
```
git clone https://github.com/keshavprasadms/helm-proxies.git
git clone https://github.com/keshavprasadms/helm-auth.git
git clone https://github.com/keshavprasadms/helm-db.git
helm repo add common https://keshavprasadms.github.io/helm-common
cd helm-db
helm upgrade --install postgresql postgresql
helm upgrade --install postgres-db-setup postgres-db-setup
helm upgrade --install postgres-user-setup postgres-user-setup
cd ../helm-auth
helm upgrade --install kong kong
helm upgrade --install kong-apis kong-apis
helm upgrade --install kong-consumer kong-consumer
helm upgrade --install kong-jwt-secrets kong-jwt-secrets -f override.yaml
cd ../helm-proxies
helm upgrade --install nginx nginx
helm upgrade --install echo echo
helm test echo
```
- Invoke the API using the nginx service at `NODE_IP:NODE_PORT`
- If you are using minikube, you can use the below commands and invoke the echo API
```
PORT=$(kubectl get svc nginx -ojsonpath='{.spec.ports[0].nodePort}')
IP=$(minikube ip)
curl http://$IP:$PORT/echoWithoutToken
curl http://$IP:$PORT/echoWithToken 
```
