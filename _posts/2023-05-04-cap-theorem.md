---
title: CAP Theorem
author: Sanh Doan
date: 2023-05-04 23:300:00 +0700
categories: [Distributed system]
tags: [Distributed system]
---

Tiếng Việt phía dưới (Vietnamese below)

## English
The CAP theorem (Consistency, Availability, Partition Fault Tolerance) is a concept in distributed systems that defines the properties that a distributed system can achieve. This principle was coined by Eric Brewer, a computer scientist at the University of California, Berkeley in 2000.

There are 3 properties in CAP theorem:
1. Consistency: All nodes in the distributed system always see the same version of an object's data at any point of time
2. Availability: A request to the system is always served by at least one node in the system, whether an error occurs or not
3. Partition Fault Tolerance

When a network partition failure happens, it must be decided whether to do one of the following:

- cancel the operation and thus decrease the availability but ensure consistency
- proceed with the operation and thus provide availability but risk inconsistency.


## Vietnamese
Nguyên lý CAP (Consistency, Availability, Partition Fault Tolerance) là một khái niệm trong hệ thống phân tán, định nghĩa các tính chất mà một hệ thống phân tán có thể đạt được. Nguyên lý này được đặt ra bởi Eric Brewer, một nhà khoa học máy tính tại Đại học California, Berkeley vào năm 2000.

Trong CAP, chúng ta có 3 tính chất

1. Consistency (Tính nhất quán): Tất cả các nút trong hệ thống luôn nhìn thấy cùng một phiên bản dữ liệu của một đối tượng trong bất kỳ thời điểm nào.

2. Availability (Tính khả dụng): Một yêu cầu đến hệ thống luôn được đáp ứng bởi ít nhất một nút trong hệ thống, dù có xảy ra lỗi hay không.

3. Partition Fault Tolerance (Khả năng chống lỗi phân tán): Hệ thống vẫn hoạt động một cách chính xác khi một số phân vùng của nó bị lỗi.

Theo nguyên lý CAP, trong một hệ thống phân tán, khi yếu tố P (Partition Fault Tolerance) xảy ra thì ta phải ưu tiên (trade-off) 1 trong 2 yếu tố còn lại, và tùy vào mục đích sử dụng, ta sẽ lựa chọn các tính chất khác nhau. Ví dụ, một hệ thống ngân hàng trực tuyến có thể lựa chọn tính nhất quán và tính khả dụng, trong khi một hệ thống lưu trữ tệp có thể lựa chọn tính khả dụng và khả năng chống lỗi phân tán.

## Reference
- https://www.youtube.com/watch?v=P62lCiZKZgo