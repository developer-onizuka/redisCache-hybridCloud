# redisCache-hybridCloud

# 1. Deploy the Function of rabbitmq-to-hybridCloud to AzureFunctions on Onprem-Kubernetes
> https://github.com/developer-onizuka/rabbitMQ_KEDA_Csharp#8-write-rabbitmqs-messages-to-mongodb
```
$ https://github.com/developer-onizuka/rabbitMQ_KEDA_Csharp
$ cd rabbitMQ_KEDA_Csharp/rabbitmq-to-hybridCloud
```
```
$ cat <<EOF > local.settings.json
{
    "IsEncrypted": false,
    "Values": {
        "AzureWebJobsStorage": "UseDevelopmentStorage=true",
        "FUNCTIONS_WORKER_RUNTIME": "dotnet",
        "RabbitMQConnection": "amqp://user:PASSWORD@rabbitmq.default.svc.cluster.local:5672",
        "MongoDBConnection": "mongodb://mongo-0:27017,mongo-1:27017,mongo-2:27017/?replicaSet=myReplicaSet",
        "CosmosDBConnection": "mongodb://myfirstcosmosdb:XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX"
    }
}
EOF
```
```
$ func kubernetes deploy --name rabbitmq-to-hybridcloud --registry 192.168.1.5:5000 --max-replicas 16 --polling-interval 5 --cooldown-period 30
```

# 2. Publish a large number of messages
There is a C# code which publish messages controlled with environment below in the rabbitMQ_KEDA_Csharp/send-to-rabbitmq directory.
Use it if you like.
```
export RABBITMQ_IPADDR="192.168.33.220"
export RABBITMQ_QUEUE="employee-queue"
export RABBITMQ_MESSAGECOUNT="10000"
```

# 3. Access to onprem.example.com

<img src="https://github.com/developer-onizuka/redisCache-hybridCloud/blob/main/redisCache-hybridCloud4.png" width="640"> <br>



# 4. Access to azure.example.com

First, you might see the following error. The reason is an index which needs to be created on the field being sorted. The default indexes can be dropped and custom indexes created.<br>

<img src="https://github.com/developer-onizuka/redisCache-hybridCloud/blob/main/redisCache-hybridCloud2.png" width="640"> <br>


> https://stackoverflow.com/questions/56988743/using-the-sort-cursor-method-without-the-default-indexing-policy-in-azure-cosm/60809868#60809868


Let's create the index for EmployeeID on Azure Portal below:<br>
<img src="https://github.com/developer-onizuka/redisCache-hybridCloud/blob/main/redisCache-hybridCloud1.png" width="640"> <br>

<img src="https://github.com/developer-onizuka/redisCache-hybridCloud/blob/main/redisCache-hybridCloud5.png" width="640"> <br>


# 5. Kiali's viewing

<img src="https://github.com/developer-onizuka/redisCache-hybridCloud/blob/main/redisCache-hybridCloud3.png" width="640"> <br>
