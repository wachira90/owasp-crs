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

## CUSTOM

```yml
services:

  modsecurity:
    image: owasp/modsecurity-crs:4.11.0-nginx-202502270602
    ports:
      - "80:8080"
      - "443:8443"
    volumes:
      - /tmp/host-fs-auditlog.log:/var/log/modsec_audit.log
      - /tmp/host-fs-errorlog.log:/var/log/modsec_error.log
    environment:
      TZ: "Asia/Bangkok"
      MODSEC_AUDIT_ENGINE: "on"
      MODSEC_AUDIT_LOG: "/var/log/modsec_audit.log"
      LOGLEVEL: "warn"
      ERRORLOG: "/var/log/modsec_error.log"
      BLOCKING_PARANOIA: "2"
      DETECTION_PARANOIA: "2"
      ENFORCE_BODYPROC_URLENCODED: "1"
      ANOMALY_INBOUND: "10"
      ANOMALY_OUTBOUND: "5"
      ALLOWED_METHODS: "GET POST PUT DELETE HEAD"
      ALLOWED_REQUEST_CONTENT_TYPE: "text/xml|application/xml|text/plain"
      ALLOWED_REQUEST_CONTENT_TYPE_CHARSET: "utf-8|iso-8859-1"
      ALLOWED_HTTP_VERSIONS: "HTTP/1.1 HTTP/2 HTTP/2.0"
      RESTRICTED_EXTENSIONS: ".cmd/ .com/ .config/ .dll/"
      RESTRICTED_HEADERS: "/proxy/ /if/"
      STATIC_EXTENSIONS: "/.jpg/ /.jpeg/ /.png/ /.gif/"
      MAX_NUM_ARGS: "128"
      ARG_NAME_LENGTH: "50"
      ARG_LENGTH: "200"
      TOTAL_ARG_LENGTH: "6400"
      MAX_FILE_SIZE: "100000"
      COMBINED_FILE_SIZES: "1000000"
      TIMEOUT: "60"
      SERVER_ADMIN: "root@localhost"
      SERVER_NAME: "localhost"
      PORT: "8080"
      MODSEC_RULE_ENGINE: "on"
      MODSEC_REQ_BODY_ACCESS: "on"
      MODSEC_REQ_BODY_LIMIT: "13107200"
      MODSEC_REQ_BODY_NOFILES_LIMIT: "131072"
      MODSEC_RESP_BODY_ACCESS: "on"
      MODSEC_RESP_BODY_LIMIT: "524288"
      MODSEC_PCRE_MATCH_LIMIT: "1000"
      MODSEC_PCRE_MATCH_LIMIT_RECURSION: "1000"
      VALIDATE_UTF8_ENCODING: "1"
      CRS_ENABLE_TEST_MARKER: "1"
      BACKEND: "http://192.168.1.11:4044"
    stdin_open: true
    tty: true
    restart: "unless-stopped"
```




