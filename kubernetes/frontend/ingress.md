zapiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: beeshoes1-frontend-ingress
  namespace: beeshoes1
spec:
  ingressClassName: nginx
  rules:
    - host: beeshoes1.duc.com
      http:
        paths:
          - backend:
              service:
                name: beeshoes1-frontend-service
                port:
                  number: 80
            path: /
            pathType: Prefix