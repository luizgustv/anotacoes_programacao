<h1>Micronaut AWS</h1>

<p>O micronaut oferece certos recursos para serem utilizados com a Amazon Web Services (AWS).</p>

<p>Possui surpote para a dependência <a href="https://github.com/aws/aws-sdk-java-v2"> AWS SDK v2. </a>Para adiciona-la use a seguinte dependência:</p>

```
implementation("io.micronaut.aws:micronaut-aws-sdk-v2")
```

É possível configurar as credenciais da AWS em uma arquivo yml:
```
aws:
  accessKeyId: your_access_key_id_here
  secretKey: your_secret_key_id_here
  sessionToken: your_session_token_here
```

E a partir daí é necessário também adicionar a dependência do serviço quer se quer utilizar:

<h2>DynamoDb</h2>

Dependência:
```
implementation("software.amazon.awssdk:dynamodb")
```

<h2>Java annotations for DynamoDb</h2>
https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/DynamoDBMapper.Annotations.html

