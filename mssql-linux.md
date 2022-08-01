# Instll mssql on docker
[mssql docker image](https://hub.docker.com/_/microsoft-mssql-server)

## Express
```sh
docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=Chinese!520" -e "MSSQL_PID=Standard" \
   -p 1401:1433 --name sqlstandard-2019 --hostname sqlstandard-2019 \
   -d \
   mcr.microsoft.com/mssql/server:2019-latest
```

## Standard
```sh
docker run -e "ACCEPT_EULA=Y" -e "SA_PASSWORD=Chinese!520" -e "MSSQL_PID=Express" \
   -p 1401:1433 --name sqlexpress-2019 --hostname sqlexpress-2019 \
   -d \
   mcr.microsoft.com/mssql/server:2019-latest
```

---
---
