## 1. Docker exec command only access file inside container

```bash
docker exec -it dev-postgres pg_restore -U postgres -d dvdrental /dvdrental.tar
```

- dvdrental.tar is backup file that contain database schema and data.
- dvdrental.tar must be exist inside container, then we have to copy this file into container.
- `docker cp <local_file> <container_name>:<file's_full_path_inside_container>`