apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: beeshoes1-backend
  name: beeshoes1-backend-deployment
  namespace: beeshoes1
spec:
  replicas: 1
  revisionHistoryLimit: 11
  selector:
    matchLabels:
      app: beeshoes1-backend
  strategy:
    rollingUpdate:
      maxSurge: 25%
      maxUnavailable: 25%
    type: RollingUpdate
  template:
    metadata:
      labels:
        app: beeshoes1-backend
      namespace: beeshoes1
    spec:
      containers:
      - image: harbor.duchdbank.online/beeshoes/beeshoes1-backend:v1
        imagePullPolicy: Always
        name: beeshoes1-backend
        ports:
          - containerPort: 5214
            name: tcp
            protocol: TCP
      imagePullSecrets:
      - name: beeshoes1-registry-secret