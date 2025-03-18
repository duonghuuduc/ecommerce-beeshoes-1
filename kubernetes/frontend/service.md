apiVersion: v1
kind: Service
metadata:
  name: beeshoes1-frontend-service
  namespace: beeshoes1
spec:
  internalTrafficPolicy: Cluster
  ipFamilies:
    - IPv4
  ipFamilyPolicy: SingleStack
  ports:
    - name: tcp
      port: 80
      protocol: TCP
      targetPort: 80
  selector:
    app: beeshoes1-frontend
  sessionAffinity: None
  type: ClusterIP