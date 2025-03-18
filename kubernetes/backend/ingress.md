apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: beeshoes1-backend-ingress
  namespace: beeshoes1
spec:
  ingressClassName: nginx
  rules:
    - host: api-beeshoes1.duc.com
      http:
        paths:
          - backend:
              service:
                name: beeshoes1-backend-service
                port:
                  number: 5214
            path: /
            pathType: Prefix