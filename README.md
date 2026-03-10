# redis
* crie a pasta onde ficará os arquivos do Redis, volumes, etc
  ```bash
  mkdir -p ~/projects/redis
  ```

  * Se usar com senha, acrescente ao serviço a seguinte linha e defina a variável $NEXTCLOUD_REDIS_PASSWORD:
  - `command: ["redis-server", "--requirepass", "$NEXTCLOUD_REDIS_PASSWORD"]`
* Levante o container:
  ```bash
  docker compose up -d
  ```
  Talvez precise criar a network mas o Docker dirá como fazer.

* Verificar se está funcionando (irá aparecer as entradas em tempo real)
  ```
  docker exec -it redis-redis-1 redis-cli MONITOR
  ```
# Troubleshooting
- Erro: `redis-1  | 1:M 02 Dec 2025 14:34:52.704 # Bad file format reading the append only file appendonly.aof.80.incr.aof: make a backup of your AOF file, then use ./redis-check-aof --fix <filename.manifest>`
- Solução: `docker compose run --rm redis redis-check-aof --fix /data/appendonlydir/appendonly.aof.80.incr.aof`