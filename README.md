# Matrix
[Matrix](https://matrix.org/) server behind [Traefik](https://traefik.io/traefik/)

## Server

Setup your DNS records for `synapse.example.com` and `element.example.com` 

Ensure your proxy (Traefik) has set entrypoint at port 8448.

Clone repo and navigate to it.
```
git clone git@github.com:otasnovotny/matrix.git && \
cd matrix
```

Create .env
```
# with proper values!!!
cp .env.template .env
```

Generate a `homeserver.yaml` file
```
docker compose run --rm synapse generate
```

Make writable for $USER
```
sudo chmod -R a+rw ./synapse/
```

Create a new user
```
docker compose exec -it synapse register_new_matrix_user -c /data/homeserver.yaml http://localhost:8008
```

Run service
```
docker compose up -d
```

Check in browser your `synapse.example.com` and `element.example.com`

Check your `synapse.example.com` instance on `https://federationtester.matrix.org/`