---
title: AWS CloudFront
author: Sanh Doan
date: 2023-04-24 19:25:00 +0700
categories: [Devops, AWS]
tags: [Devops, AWS, CloudFront]
---

# Định nghĩa

AWS CloudFront là một dịch vụ phân phối nội dung (CDN) được cung cấp bởi Amazon Web Services (AWS). Nó cho phép bạn phân phối nội dung đến người dùng trên toàn thế giới với tốc độ cao hơn bằng cách sử dụng mạng CDN của AWS, bao gồm hàng trăm trạm phân phối được đặt tại các vị trí khác nhau trên thế giới.

CloudFront có thể được sử dụng để phân phối các loại nội dung như trang web tĩnh, trang web động, video, âm thanh, hình ảnh và tài liệu truyền thông. Nó sử dụng các máy chủ cực gần người dùng để tải nội dung, giúp giảm thiểu thời gian đợi và tăng tốc độ tải trang.

Bạn có thể liên kết với nó để phân phối nội dung từ các nguồn như Amazon S3, Elastic Load Balancing, hoặc các máy chủ web tùy chỉnh. Bạn cũng có thể cấu hình tùy chọn bảo mật như bảo vệ chống sao chép và mã hóa HTTPS để bảo vệ nội dung trên đường truyền.

CloudFront cung cấp nhiều tính năng, bao gồm:
- Tính năng giảm thiểu độ trễ (latency) với định tuyến thông minh
- Tính năng bảo mật cho phép kiểm soát quyền truy cập và bảo vệ dữ liệu
- Tính năng theo dõi và báo cáo hiệu suất
- Hỗ trợ nhiều định dạng nội dung như HTTP, HTTPS, RTMP và RTMPS
- Tích hợp với nhiều dịch vụ AWS khác để cung cấp khả năng mở rộng và tăng cường tính khả dụng

# Terraform

```bash
# Khai báo nhà cung cấp "aws" và chỉ định khu vực là "us-west-2"
provider "aws" {
  region = "us-west-2"
}

# Khai báo tài nguyên S3 với tên là "my-bucket"
resource "aws_s3_bucket" "bucket" {
  bucket = "my-bucket"
}

# Khai báo tài nguyên CloudFront distribution với tên là "distribution"
resource "aws_cloudfront_distribution" "distribution" {
  # Khối origin được sử dụng để chỉ định nguồn nội dung của distribution từ bucket S3 đã được tạo trước đó
  origin {
    domain_name = "${aws_s3_bucket.bucket.bucket_regional_domain_name}"
    origin_id   = "my-bucket-origin"
  }

  enabled             = true
  # Cho phép IPv6
  is_ipv6_enabled     = true
  # Ghi chú
  comment             = "My CloudFront distribution"
  # Tên tệp mặc định
  default_root_object = "index.html"

  # Hành vi lưu trữ cache mặc định
  default_cache_behavior {
    # Danh sách các phương thức HTTP được phép cho các yêu cầu được lưu trữ cache
    allowed_methods  = ["GET", "HEAD"]
    # Danh sách các phương thức HTTP được lưu trữ cache
    cached_methods   = ["GET", "HEAD"]
    # ID của nguồn lưu trữ đích
    target_origin_id = "my-bucket-origin"

    # Cấu hình cho phép truyền các giá trị từ yêu cầu gốc đến yêu cầu phục vụ bởi CloudFront, ví dụ như query string và cookies. Trong ví dụ này, query string không được chuyển tiếp, trong khi cookie được chuyển tiếp với tùy chọn "none"
    forwarded_values {
      query_string = false

      cookies {
        forward = "none"
      }
    }

    # Cấu hình cho phép phương thức truy cập của khách hàng đến nội dung được phục vụ bởi CloudFront. Trong ví dụ này, nó được thiết lập thành "redirect-to-https" để chuyển tiếp khách hàng từ HTTP sang HTTPS.
    viewer_protocol_policy = "redirect-to-https"
  }

  # Loại giá cả
  price_class = "PriceClass_All"

  # Giới hạn truy cập
  restrictions {
    geo_restriction {
      restriction_type = "whitelist"
      locations        = ["US", "CA"]
    }
  }

  # Chứng chỉ SSL cho người dùng xem nội dung
  viewer_certificate {
    acm_certificate_arn = "arn:aws:acm:us-west-2:123456789012:certificate/xxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
    ssl_support_method  = "sni-only"
  }
}

```
