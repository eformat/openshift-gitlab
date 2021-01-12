# openshift-gitlab

Project
```
oc new-project gitlab --display-name='Gitlab' --description='Gitlab'
oc adm policy add-scc-to-user anyuid -z gitlab-ce-user -n gitlab
oc adm policy add-scc-to-user privileged -z gitlab-ce-runner-user -n gitlab
```

No LDAP
```
oc new-app -f ./gitlab.yml \
  -p APPLICATION_HOSTNAME=gitlab.apps.foo.sandbox1543.opentlc.com \
  -p ETC_VOL_SIZE=1Gi \
  -p GITLAB_DATA_VOL_SIZE=1Gi \
  -p POSTGRESQL_VOL_SIZE=1Gi \
  -p REDIS_VOL_SIZE=1Gi
```

LDAP
```
oc new-app -f ./gitlab-ldap.yml \
  -p APPLICATION_HOSTNAME=gitlab.apps.dcp-apac-1.rht-labs.com \
  -p ETC_VOL_SIZE=100Mi \
  -p GITLAB_DATA_VOL_SIZE=20Gi \
  -p GITLAB_ROOT_PASSWORD=<password> \
  -p POSTGRESQL_VOL_SIZE=5Gi \
  -p REDIS_VOL_SIZE=5Gi \
  -p LDAP_HOST=idm.dcp-apac-1.rht-labs.com \
  -p LDAP_BIND_DN='uid=dcp-apac-1-sa,cn=users,cn=accounts,dc=dcp-apac-1,dc=rht-labs,dc=com' \
  -p LDAP_PASSWORD=<password>\
  -p LDAP_USER_FILTER='(memberOf=cn=ipausers,cn=groups,cn=accounts,dc=dcp-apac-1,dc=rht-labs,dc=com)' \
  -p LDAP_LABEL="DevOps Enablement Labs LDAP" \
  -p LDAP_PORT=389 \
  -p LDAP_ENCRYPTION=plain \
  -p LDAP_BASE='cn=users,cn=accounts,dc=dcp-apac-1,dc=rht-labs,dc=com' \
  -p NAMESPACE=ci-cd
```

Keycloak
```
oc new-app -f ./gitlab-keycloak.yml \
  -p APPLICATION_HOSTNAME=gitlab.apps.foo.sandbox1459.opentlc.com \
  -p ETC_VOL_SIZE=1Gi \
  -p GITLAB_DATA_VOL_SIZE=1Gi \
  -p POSTGRESQL_VOL_SIZE=1Gi \
  -p REDIS_VOL_SIZE=1Gi \
  -p KEYCLOAK_CLIENT_SECRET=7d77085d-8912-4394-ae62-fc97ca743778 \
  -p KEYCLOAK_URL=https://keycloak-keycloak.apps.foo.sandbox1459.opentlc.com \
  -p KEYCLOAK_REALM=OpenShift \
  -p KEYCLOAK_CLIENT_ID=gitlab
```
