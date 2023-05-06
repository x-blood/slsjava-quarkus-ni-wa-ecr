# Serverless Java17 Quarkus Web Adapter Container Example

| -                             | -                        |
|:------------------------------|--------------------------|
| Java version                  | Java17                   |
| Application Framework         | Quarkus 3.0.2.Final      |
| Deployment Framework          | AWS SAM CLI 1.82.0       |
| Development environment       | **Ubuntu Desktop 20.04** |
| » JDK for build               | Corretto-17.0.7.7.1      |
| » Container build environment | Docker Desktop 4.17.0    |

## Result of K6

```
```

**CloudWatch Logs Insights**
query-string:
```
filter @type="REPORT" and ispresent(@initDuration)
| stats count() as coldStarts, avg(@maxMemoryUsed), avg(@duration), avg(@initDuration), min(@initDuration), max(@initDuration) by bin(10m)
```
---

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
