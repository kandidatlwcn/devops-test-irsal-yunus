## Referensi 
https://stackoverflow.com/questions/25920029/setting-up-mysql-and-importing-dump-within-dockerfile

## docker build
docker build -t mysql:latest .

## docker run
docker run --rm -d  -p 3306:3306/tcp -p 33060:33060/tcp mysql-latest:latestq