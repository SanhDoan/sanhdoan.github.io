---
title: K8s Liveness and Readiness
author: Sanh Doan
date: 2023-05-01 20:50:00 +0700
categories: [Devops, K8s]
tags: [Devops, K8s]
---

Tiếng Việt phía dưới (Vietnamese below)

# English
## Liveness
Liveness is used to check if a pod is working or not. If the pod does not work, K8s will delete that pod and recreate another pod.

## Readiness
Readiness is used to check if a pod is ready so that K8s will start sending request to the pod. If Readiness probe failed, it will stop sending request until it is ready.

## Probes
### HTTP probe
This is the most common probe. K8s ping to the route (api) periodically. If the response is 200-300 status code, the pod is marked as healthy
```yaml
apiVersion: apps/v1
kind: Deployment
spec:
  containers:
      readinessProbe:
        httpGet:
          path: /health
          port: 8080
          scheme: HTTP
        # Options ...
      livenessProbe:
        httpGet:
          path: /health
          port: 8080
          scheme: HTTP
        # Options ...
```

### Command probe
K8s execute a command in your container periodically. If the result is 0 (zero), container is marked as healthy. In contrast, it is marked as unhealthy.
```yaml
livenessProbe:
  exec:
    command:
      - bash
      - ./healthy-check.sh
```

### TCP probe
K8s try to create a TCP connection on configured port. If connection is success, a pod is marked as healthy.
```yaml
livenessProbe:
  tcpSocket:
    port: 8080
```

## Configuration options
```yaml
readiness:
  initialDelaySeconds: 5
  # Periodical time that K8s will ping the pod to check. Default is 10s. Minimum is 1s.
  periodSeconds: 10
  # If probe time exceed the timeout, pod is marked as failed. Default is 1s. Minimum is 1s.
  timeoutSeconds: 3
  # When a probe is failed, K8s will try failureThreshold times before quit.
  # Liveness: delete current pod and create a new pod - Readiness: mark a pod is unhealthy)
  # Default is 3. Minimum is 1.
  failureThreshold: 3
  # When a probe is failed, a pod need to satify minumum successThreshold times to marked as healthy
  # Default is 1. Minimum is 1. Liveness must be 1
  successThreshold: 1
```

##############################################

# Vietnamese
## Liveness
Liveness dùng để kiểm tra 1 pod có đang hoạt động hay không. Nếu pod không hoạt động thì K8s sẽ xóa pod đó và tạo 1 pod mới

## Readiness
Readiness dùng để kiểm tra 1 pod đã sẵn sàng chưa để gửi lưu lượng truy cập đến pod đó. Nếu Readiness kiểm tra không thành công thì sẽ tạm ngưng gửi request đến pod đến khi pod đó sẵn sàng

## Các loại probe
### HTTP probe
Đây là loại probe phổ biến nhất. K8s sẽ định kì ping đến đường dẫn được chỉ định, nếu response trong phạm vi 200 - 300 thì pod sẽ được xem là đang healthy
```yaml
apiVersion: apps/v1
kind: Deployment
spec:
  containers:
      readinessProbe:
        httpGet:
          path: /health
          port: 8080
          scheme: HTTP
        # Options...
      livenessProbe:
        httpGet:
          path: /health
          port: 8080
          scheme: HTTP
        # Options...
```

### Command probe
K8s sẽ chạy 1 command bên trong container. Nếu response của command bằng 0, container sẽ được đánh dấu là success (healthy). Ngược lại là unhealthy
```yaml
livenessProbe:
  exec:
    command:
      - bash
      - ./healthy-check.sh
```

### TCP probe
K8s sẽ cố gắng thiết lập một kết nối TCP trên port được chỉ định. Nếu nó có thể thiết lập kết nối, thì Pod được coi là healthy, ngược lại sẽ là một pod unhealthy.
```yaml
livenessProbe:
  tcpSocket:
    port: 8080
```

## Configuration options
```yaml
readiness:
  initialDelaySeconds: 5
  # Khoảng thời gian định kì K8s sẽ ping đến pod để kiểm tra. Mặc định là 10s. Tối thiểu là 1s.
  periodSeconds: 10
  # Thời gian timeout cho 1 lần check, nếu vượt quá timeout mà không nhận được response thì pod sẽ được xem là failed. Mặc định là 1s. Tối thiểu là 1s.
  timeoutSeconds: 3
  # Khi probe failed thì K8s sẽ thử lại 1 số lần trước khi bỏ cuộc.
  # Liveness: delete pod cũ và tạo pod mới - Readiness: đánh dấu là unhealthy)
  # Mặc định là 3. Giá trị tối thiểu là 1.
  failureThreshold: 3
  # Khi 1 probe bị failed thì pod phải đạt được tối thiểu số lần successThreshold mới được đánh dấu là success.
  # Mặc định là 1. Phải là 1 cho liveness. Giá trị tối thiểu là 1.
  successThreshold: 1
```