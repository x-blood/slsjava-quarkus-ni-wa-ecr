# Serverless Java17 Quarkus Web Adapter Container Example

| -                       | -                     |
|:------------------------|-----------------------|
| Java version            | Java17                |
| Application Framework   | Quarkus 3.0.2.Final   |
| Deployment Framework    | AWS SAM CLI 1.82.0    |
| Development environment | Ubuntu Desktop 20.04  |
| » JDK for local build   | Corretto-17.0.7.7.1   |
| » Container build       | Docker Desktop 4.17.0 |

## Result of K6

```

          /\      |‾‾| /‾‾/   /‾‾/   
     /\  /  \     |  |/  /   /  /    
    /  \/    \    |     (   /   ‾‾\  
   /          \   |  |\  \ |  (‾)  | 
  / __________ \  |__| \__\ \_____/ .io

  execution: local
     script: slsjava_quarkus_ni_wa_ecr.js
     output: -

  scenarios: (100.00%) 1 scenario, 200 max VUs, 31s max duration (incl. graceful stop):
           * default: 200 looping VUs for 1s (gracefulStop: 30s)


     data_received..................: 1.2 MB 489 kB/s
     data_sent......................: 137 kB 57 kB/s
     http_req_blocked...............: avg=594.31ms min=342.27ms med=553.46ms max=1.23s    p(90)=856.34ms p(95)=923.25ms
     http_req_connecting............: avg=79.2ms   min=59.84ms  med=73.58ms  max=130.7ms  p(90)=109.01ms p(95)=117.36ms
     http_req_duration..............: avg=440.43ms min=25.76ms  med=445.43ms max=832.1ms  p(90)=773.68ms p(95)=799.42ms
       { expected_response:true }...: avg=440.43ms min=25.76ms  med=445.43ms max=832.1ms  p(90)=773.68ms p(95)=799.42ms
     http_req_failed................: 0.00%  ✓ 0         ✗ 200  
     http_req_receiving.............: avg=213.51µs min=7µs      med=20µs     max=11.77ms  p(90)=94.9µs   p(95)=849.09µs
     http_req_sending...............: avg=72.25µs  min=25µs     med=49µs     max=1.28ms   p(90)=115.4µs  p(95)=140.14µs
     http_req_tls_handshaking.......: avg=490.31ms min=252.97ms med=430.38ms max=1.15s    p(90)=748.62ms p(95)=826.12ms
     http_req_waiting...............: avg=440.14ms min=25.71ms  med=445.34ms max=831.96ms p(90)=773.47ms p(95)=798.22ms
     http_reqs......................: 200    83.679242/s
     iteration_duration.............: avg=2.03s    min=1.79s    med=2.02s    max=2.38s    p(90)=2.2s     p(95)=2.24s   
     iterations.....................: 200    83.679242/s
     vus............................: 106    min=106     max=200
     vus_max........................: 200    min=200     max=200


running (02.4s), 000/200 VUs, 200 complete and 0 interrupted iterations
default ✓ [======================================] 200 VUs  1s
```

**CloudWatch Logs Insights**
query-string:
```
filter @type="REPORT" and ispresent(@initDuration)
| stats count() as coldStarts, avg(@maxMemoryUsed), avg(@duration), avg(@initDuration), min(@initDuration), max(@initDuration) by bin(10m)
```
---
| coldStarts | avg(@maxMemoryUsed) | avg(@duration) | avg(@initDuration) | min(@initDuration) | max(@initDuration) |
|------------|---------------------|----------------|--------------------|--------------------|--------------------|
| 142        | 57007042.2535       | 3.6455         | 330.0665           | 127.09             | 566.46             |
---

## Getting Started

### Build
```make
make build-remote-docker
make sam-build
```

### Deploy (Initial)
```make
make sam-deploy-guided
```

### Deploy
```
make sam-deploy
```
