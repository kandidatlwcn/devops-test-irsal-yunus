## Referensi
https://github.com/redis/redis/pull/1908

## build docker images
docker build -t redis:latest .

## docker run 
docker run --rm -d  -p 6379:6379/tcp redis:latest