# Matrix
This is a guide how to run dockerized [Matrix server](https://matrix.org/) behind [Traefik](https://traefik.io/traefik/)

## Server

Setup your DNS records for Synapse `matrix.example.com` and Element `element.example.com`. 

Ensure your proxy (Traefik) has set entrypoint at port 8448.

Clone repo and navigate to it.
```
git clone git@github.com:otasnovotny/matrix.git && \
cd matrix
```

### Configuration

Create .env
```
# with proper values!!!
cp .env.template .env
```

Create `nginx.conf`
```
# replace example.com!!!
cp nginx.conf.template nginx.conf
```

Create well-known files
```
# replace example.com!!!
cp ./nginx/well-known/matrix/server.template ./nginx/well-known/matrix/server
cp ./nginx/well-known/identity/server.template ./nginx/well-known/identity/server
```

Run service
```
docker compose up -d
```

Generate a `homeserver.yaml` file
```
docker compose run --rm synapse generate
```

Make writable for $USER if necessary
```
sudo chmod -R a+rw ./synapse/
sudo chmod -R a+rw ./nginx/
```

Create a new user
```
docker compose exec -it synapse register_new_matrix_user -c /data/homeserver.yaml http://localhost:8008
```

Check in browser your `matrix.example.com` and `element.example.com`

Check your `matrix.example.com` instance on `https://federationtester.matrix.org/`

Clients

Install one of [clients](https://matrix.org/ecosystem/clients/). 