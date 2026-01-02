## Khởi động & dừng hệ thống

### Chạy services

```bash
docker compose up -d
```

### Kiểm tra container

```bash
docker ps
```

### Xem log

```bash
docker logs mongodb-container
docker logs redis-container
```

### Dừng services

```bash
docker compose down
```

### Dừng & xóa dữ liệu (cẩn thận)

```bash
docker compose down -v
```

---

## Kết nối MongoDB (chi tiết)

### Kết nối từ **máy host**

* Host: `localhost`
* Port: `27017`
* Username: `admin`
* Password: `admin123`
* Auth DB: `admin`

Connection string:

```text
mongodb://admin:admin123@localhost:27017/?authSource=admin
```

### Kết nối bằng Mongo Shell

```bash
docker exec -it mongodb-container mongosh \
  -u admin -p admin123 --authenticationDatabase admin
```

### Kết nối từ **container khác trong cùng compose**

```text
mongodb://admin:admin123@mongodb:27017/?authSource=admin
```

### Kết nối MongoDB Compass

* Hostname: `localhost`
* Port: `27017`
* Authentication: Username / Password
* Username: `admin`
* Password: `admin123`
* Authentication Database: `admin`

---

## Kết nối Redis (chi tiết)

### Kết nối từ **máy host**

* Host: `localhost`
* Port: `6379`
* Password: `admin123`

Connection string:

```text
redis://:admin123@localhost:6379
```

### Redis CLI trong container

```bash
docker exec -it redis-container redis-cli -a admin123
```

### Kết nối từ **container khác trong compose**

```text
redis://:admin123@redis:6379
```

---

## Sử dụng trong Backend

### Spring Boot – MongoDB

```yaml
spring:
  data:
    mongodb:
      uri: mongodb://admin:admin123@localhost:27017/appdb?authSource=admin
```

### Spring Boot – Redis

```yaml
spring:
  data:
    redis:
      host: localhost
      port: 6379
      password: admin123
```