# Docker Compose project for Kafka cluster

Create and start containers forming 3 node Kafka Raft cluster:

```bash
docker compose up -d --wait
```

Kafka brokers accessible from Docker host via localhost:

| Address        | Docker Compose service |
|----------------|------------------------|
| localhost:9192 | kafka1                 |
| localhost:9193 | kafka2                 |
| localhost:9194 | kafka3                 |

Sending messages with [kcat](https://github.com/edenhill/kcat):

```bash
kcat -P -b localhost:9192,localhost:9193,localhost:9194 -t example <<EOF
1:{"order_id":1,"order_ts":1534772501276,"total_amount":10.50,"customer_name":"Bob Smith"}
2:{"order_id":2,"order_ts":1534772605276,"total_amount":3.32,"customer_name":"Sarah Black"}
3:{"order_id":3,"order_ts":1534772742276,"total_amount":21.00,"customer_name":"Emma Turner"}
EOF
```
