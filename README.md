# OWASP MOD CORS RULES SET

## CREATE FOLDER AND PERMISSION

```sh
git clone https://github.com/wachira90/owasp-crs
cd owasp-crs

mkdir {logs/ssl}

touch logs/host-fs-auditlog.log
touch logs/host-fs-errorlog.log
```

## SSL

```
ssl/server.crt
ssl/server.key
```

## START COMMAND 

```sh
docker compose up -d
```

## STOP COMMAND 

```sh
docker compose down
```
