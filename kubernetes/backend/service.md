apiVersion: v1
kind: Service
metadata:
  name: beeshoes1-backend-service
  namespace: beeshoes1
spec:
  internalTrafficPolicy: Cluster
  ipFamilies:
    - IPv4
  ipFamilyPolicy: SingleStack
  ports:
    - name: tcp
      port: 5214
      protocol: TCP
      targetPort: 5214
  selector:
    app: beeshoes1-backend
  sessionAffinity: None
  type: ClusterIP