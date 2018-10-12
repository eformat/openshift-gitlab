# openshift-gitlab

No LDAP:

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

For LDAP:

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

### Work In Progress

OpenIDConnect support (so you can login using keycloak for example)

-- https://github.com/eformat/gitlab-ce-oidc
