# agriaf-kafka


helm install kafka --set externalAccess.enabled=true,externalAccess.service.type=LoadBalancer,externalAccess.service.port=19092,externalAccess.autoDiscovery.enabled=true,serviceAccount.create=true,rbac.create=true bitnami/kafka 


kubectl run kafka-client --restart='Never' --image docker.io/bitnami/kafka:3.2.0-debian-11-r3 --namespace default --command -- sleep infinity
kubectl exec --tty -i kafka-client --namespace default -- bash
    
    PRODUCER:
        kafka-console-producer.sh --broker-list kafka-0.kafka-headless.default.svc.cluster.local:9092 --topic test

    CONSUMER:
        kafka-console-consumer.sh  --bootstrap-server kafka.default.svc.cluster.local:9092 --topic test --from-beginning
