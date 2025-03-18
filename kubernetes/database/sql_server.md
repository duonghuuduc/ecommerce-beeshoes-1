apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: sqlserver
  namespace: beeshoes
spec:
  serviceName: sqlserver-service
  replicas: 1
  selector:
    matchLabels:
      app: sqlserver
  template:
    metadata:
      labels:
        app: sqlserver
    spec:
      securityContext:
        fsGroup: 65534 
      containers:
      - name: sqlserver
        image: mcr.microsoft.com/mssql/server:2019-latest
        env:
        - name: ACCEPT_EULA 
          value: "Y"
        - name: SA_PASSWORD 
          value: "Duckissyou368" 
        - name: MSSQL_PID  
          value: "Express"
        ports:
        - containerPort: 1433  
          name: mssql
        volumeMounts:
        - name: sqlserver-storage
          mountPath: /var/opt/mssql 
      volumes:
      - name: sqlserver-storage
        persistentVolumeClaim:
          claimName: nfs-pvc  


apiVersion: v1
kind: Service
metadata:
  name: sqlserver-service
  namespace: beeshoes1
spec:
  selector:
    app: sqlserver
  ports:
  - port: 1433
    targetPort: 1433
    protocol: TCP
  type: ClusterIP


apiVersion: v1
kind: Secret
metadata:
  name: database-connection-secret
  namespace: beeshoes1
stringData:
  ConnectionStrings_UserAppCon: "Server=sqlserver-service,1433;Database=beeshoes1;User Id=sa;Password=Duckissyou368"


------ Them vao Deployment
envFrom:
- secretRef:
    name: database-connection-secret