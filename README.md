# openshift-gitlab

```
oc new-project gitlab --display-name='Gitlab' --description='Gitlab'
oc adm policy add-scc-to-user anyuid -z gitlab-ce-user -n gitlab

oc new-app -f ./gitlab.yml \
  -p APPLICATION_HOSTNAME=gitlab.apps.bar.com \
  -p ETC_VOL_SIZE=1Gi \
  -p GITLAB_DATA_VOL_SIZE=1Gi \
  -p POSTGRESQL_VOL_SIZE=1Gi \
  -p REDIS_VOL_SIZE=1Gi
```


