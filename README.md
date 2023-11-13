### docker swarm の開始

```
docker swarm init
```

### docker swarm の終了

```
docker swarm leave --force
```

### docker swarm へ stack の追加

```
docker stack deploy -c bb.yaml demo
```

### docker secret

あくまでも読み取って利用する。環境変数で _FILE をつけることで DB 等ではパスワードの取得先パスとして利用することも可能。ファイルで保管することの方が推奨はされているものの、例えばディレクトリトラバーサルが実現してしまった場合には読み出されてしまうリスクも存在する。

```
echo "myPlainSecret" | docker secret create mysecret -
docker service create --name redis --secret mysecret redis:alpine
docker service ps redis
docker exec -it $(docker ps --filter name=redis -q) cat /run/secrets/mysecret.txt
```

### docker service の scale 

AutoScaling 機能は標準では提供されない

```
docker service ls
docker service scale name=10
```

### CronJob

標準では提供されないが、コンテナが提供されている
https://crazymax.dev/swarm-cronjob/usage/get-started/