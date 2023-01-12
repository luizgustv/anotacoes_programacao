## Prometheus metric types

- [Counter](https://prometheus.io/docs/concepts/metric_types/#counter)
- [Gauge](https://prometheus.io/docs/concepts/metric_types/#gauge)
- [Histograms](https://prometheus.io/docs/concepts/metric_types/#histogram)
- [Summary](https://prometheus.io/docs/concepts/metric_types/#summary)



https://www.robustperception.io/understanding-machine-cpu-usage/


## Some userful metrics provided by spring:

(Remmember): You need to add this dependences before):

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
[But, what is rate in prometheus?](https://prometheus.io/docs/prometheus/latest/querying/functions/#rate)

For outbound request  time:
```
    rate(http_client_requests_seconds_sum[1m]) / rate(http_client_requests_seconds_count[1m])
```

 ### Referencees:
[Spring Actuator Metrics]( https://docs.spring.io/spring-boot/docs/current/reference/html/actuator.html#actuator.metrics.supported.logger)

[Spring Default Metrics](https://tomgregory.com/spring-boot-default-metrics/)

[Monitoring A Spring Boot Application - Part 1](https://tomgregory.com/monitoring-a-spring-boot-application-part-1-fundamentals/)

[Monitoring A Spring Boot Application - Part 2](https://tomgregory.com/monitoring-a-spring-boot-application-part-2-prometheus/)

[Prometheus Metric Types](https://prometheus.io/docs/concepts/metric_types/)

[The four types of prometheus metrics](https://tomgregory.com/the-four-types-of-prometheus-metrics/)

[About prometheus rate](https://prometheus.io/docs/prometheus/latest/querying/functions/#rate)


- Create new panel in grafana in order to show errors;
- Ajusting endpoint getNote() in order to return a http status 404 when the note was not found, maybe showing other errors too;
- Search for other panels
- Custom  metric

sum(rate(http_server_requests_seconds_sum{application="$application", instance="$instance", status!~"5.."}[1m]))/sum(rate(http_server_requests_seconds_count{application="$application", instance="$instance", status!~"5.."}[1m]))

max(http_server_requests_seconds_max{application="$application", instance="$instance", status!~"5.."})

