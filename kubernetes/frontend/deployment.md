apiVersion: apps/v1
kind: Deployment
metadata:
  labels:
    app: beeshoes1-frontend
  name: beeshoes1-frontend-deployment
  namespace: beeshoes1
spec:
  replicas: 1
  revisionHistoryLimit: 11
  selector:
    matchLabels:
      app: beeshoes1-frontend
  strategy:
    rollingUpdate:
      maxSurge: 25%
      maxUnavailable: 25%
    type: RollingUpdate
  template:
    metadata:
      labels:
        app: beeshoes1-frontend
      namespace: beeshoes
    spec:
      containers:
        - image: harbor.duchdbank.online/beeshoes/beeshoes1-frontend:v1
          imagePullPolicy: Always
          name: beeshoes1-frontend
          ports:
            - containerPort: 80
              name: tcp
              protocol: TCP
      imagePullSecrets:
      - name: beeshoes1-registry-secret