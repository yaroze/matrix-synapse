#A quick Synapse server with docker

Remember to generate and edit the homeserver.yaml file:


```bash
docker run -it --rm \
	-v $(pwd)/data:/data \
	-e SYNAPSE_SERVER_NAME=synapse.yaroze.org \
	-e SYNAPSE_REPORT_STATS=yes \
	matrixdotorg/synapse:latest generate

```

Example
```
server_name: "synapse.yaroze.org"
pid_file: /data/homeserver.pid
listeners:
  - port: 8008
    tls: false
    type: http
    x_forwarded: true
    resources:
      - names: [client, federation]
        compress: false

database:
  name: psycopg2
  args:
    user: synapse
    password: xxxxxxxx
    database: postgres
    host: postgres
    cp_min: 5
    cp_max: 10

log_config: "/data/synapse.yaroze.org.log.config"
media_store_path: /data/media_store
registration_shared_secret: "xxxxxxx"
report_stats: true
macaroon_secret_key: "xxxxxxxx"
form_secret: "xxxxxxx"
signing_key_path: "/data/synapse.yaroze.org.signing.key"
trusted_key_servers:
  - server_name: "matrix.org"


    #enable_registration: true
    #suppress_key_server_warning: true
# vim:ft=yaml


