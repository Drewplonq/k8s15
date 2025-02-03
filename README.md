# k8s15

1. необходимо сделать неймспейсы



2. деплой web должен стучаться к деплою auth-db этого не происходит, т.к. они в разных неймспейсах



3. для решения добавляем в конфиг сетевую политику

```
---
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: allow-web-consumer-to-auth-db
  namespace: data
spec:
  podSelector:
    matchLabels:
      app: auth-db
  ingress:
    - from:
        - namespaceSelector:
            matchLabels:
              name: web
      ports:
        - protocol: TCP
          port: 80
          
```          

