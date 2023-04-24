---
title: Istio Traffic flow
author: Sanh Doan
date: 2022-07-05 07:25:00 +0700
categories: [Devops, Istio]
tags: [Devops, Istio]
---

![istio_traffic_flow](/assets/img/pages/istio_traffic_flow.jpg)

## English

1. User visit a website
2. Request come to Istio Gateway
3. Istio Gateway read VirtualService configuration to forward request to the corresponding service
4. Request go to Envoy proxy first
5. Then Envoy proxy pass the req/resp to service app
6. If service A need to communicate with other services (service B), Envoy proxy A will check VirtualService/DestRule to forward request/response to Envoy proxy B
7. Service B returns response to Envoy proxy B then Envoy proxy B returns back to Envoy proxy A <br>
   **Note: The Envoy proxy will gather metric and tracing info about the req/resp and send to Istio Control Plane**

## Vietnamese

1. Người dùng truy cập website
2. Request đi qua Istio Gateway
3. Istio Gateway sẽ đọc VirtualService configuration để forward request đến service tương ứng
4. Request đi đến Envoy proxy của service
5. Envoy proxy sẽ truyền data xuống cho service app
6. Nếu service A cần giao tiếp với service B thì Envoy proxy A sẽ kiểm tra VirtualService/DestRule để forward request/response đến Envoy proxy B
7. Service B sẽ trả dữ liệu cho Envoy proxy B, sau đó thì Envoy proxy B sẽ trả về lại cho Envoy proxy A<br/>
   **Note: Envoy proxy có nhiệm vụ thu thập các thông tin về metric và tracing của req/resp sau đó gửi về Istio Control Plane. Từ đó mình sẽ có thể monitor service**
