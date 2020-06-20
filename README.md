# oauthhydra

## startup

```
git submodule update --recursive --init

docker-compose -f development/docker-compose.yml up
```

## create client
```sh
docker-compose -f development/docker-compose.yml exec hydra \
    hydra clients create \
    --endpoint http://127.0.0.1:4445/ \
    --id my-client \
    --secret secret \
    -g client_credentials

docker-compose -f development/docker-compose.yml exec hydra \
    hydra token client \
    --endpoint http://127.0.0.1:4444/ \
    --client-id my-client \
    --client-secret secret

docker-compose -f development/docker-compose.yml exec hydra \
    hydra token introspect \
    --endpoint http://127.0.0.1:4445/ \
    --client-id my-client \
    --client-secret secret \
    Roal12t-8T6MtIbl4Hu7GOuPmWppf69atMMBMddDcPI.TbLHuReykPPboCt_fjHblMdxKke-MhmVFp9fhgyYC-w

docker-compose -f development/docker-compose.yml exec hydra \
    hydra clients create \
    --endpoint http://127.0.0.1:4445 \
    --id auth-code-client \
    --secret secret \
    --grant-types authorization_code,refresh_token \
    --response-types code,id_token \
    --scope openid,offline \
    --callbacks http://127.0.0.1:5555/callback

docker-compose -f development/docker-compose.yml exec hydra \
    hydra token user \
    --client-id auth-code-client \
    --client-secret secret \
    --endpoint http://127.0.0.1:4444/ \
    --port 5555 \
    --scope openid,offline
```
