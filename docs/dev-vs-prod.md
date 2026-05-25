# Dev vs Prod

1. **Выделяемые ресурсы**:
   - `dev`: по 1 реплике на сервис; requests: 100m CPU / 128Mi RAM; limits: 200m CPU / 256Mi RAM
   - `prod`: по 2 реплике на сервис; requests: 200m CPU / 256Mi RAM; limits: 500m CPU / 512Mi RAM

2. **Node Affinity**:
   - `dev`: без ограничений по узлам.
   - `prod`:
     - Сервисы *postgres* и *minio* на узлах `workload=system`.
     - Сервисы *frontend*, *bff*, *user-service*: на `workload=app`.
     - *message-service*: на `workload=app`, с предпочтением на `disk=fast`.

3. **Версии образов**:
   - `dev`: используется тег `latest`.
   - `prod`: используются последние хэши на момент 26.04.26.

4. **Namespaces**:
   - `dev`: `messager-dev`.
   - `prod`: `messager-prod`.