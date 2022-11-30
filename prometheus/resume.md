## ***Some userful metrics provided by spring:***

(Remmember0: You need to add this dependences before):

```
gradlle:
    implementation 'org.springframework.boot:spring-boot-starter-actuator'
maven:
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-actuator</artifactId>
    </dependency>

gradle:
    implementation 'io.micrometer:micrometer-registry-prometheus:1.5.1' -- you can search another version

maven:
    <dependency>
        <groupId>io.micrometer</groupId>
        <artifactId>micrometer-registry-prometheus</artifactId>
        <version>1.5.1</version>
    </dependency>
```

And enable prometheus metrics thought configuration:
```    
management.endpoints.web.exposure.include=metrics,prometheus
```


 - ***http_server_requests_seconds_count*** = counting the total number of requests your application received at this endpoint
 - ***http_server_requests_seconds_sum*** = counnting the sum of duration of each request your application received at this endpoint

If you want to know average duration inbound request for each status (200, 404, 422, for exemple), you can make this query:
```
    rate( http_server_requests_seconds_sum[1m]) / rate(http_server_requests_seconds_count[1m])
```
[rate](https://prometheus.io/docs/prometheus/latest/querying/functions/#rate)



 ### Referencees:
[Spring Actuator Metrics]( https://docs.spring.io/spring-boot/docs/current/reference/html/actuator.html#actuator.metrics.supported.logger)

[Spring Default Metrics](https://tomgregory.com/spring-boot-default-metrics/)

[Monitoring A Spring Boot Application - Part 1](https://tomgregory.com/monitoring-a-spring-boot-application-part-1-fundamentals/)

[Monitoring A Spring Boot Application - Part 2](https://tomgregory.com/monitoring-a-spring-boot-application-part-2-prometheus/)



https://prometheus.io/docs/concepts/metric_types/
https://tomgregory.com/the-four-types-of-prometheus-metrics/

https://prometheus.io/docs/prometheus/latest/querying/functions/#rate