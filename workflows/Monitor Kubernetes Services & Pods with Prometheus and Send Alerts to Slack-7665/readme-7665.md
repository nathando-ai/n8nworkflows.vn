---
title: "🚀 Tự động giám sát Kubernetes Services & Pods bằng Prometheus và gửi cảnh báo Slack qua n8n"
description: "Xây dựng hệ thống DevOps tự động hóa 100%: Định kỳ quét metrics từ Prometheus, phân tích lỗi Pod/Endpoint và bắn cảnh báo thông minh trực tiếp lên Slack."
slug: "giam-sat-kubernetes-prometheus-slack-n8n"
tags: [n8n, automation, kubernetes, prometheus, devops, slack]
keywords: [n8n workflow, kubernetes monitoring, prometheus alerts, slack webhook, devops automation]
press: true
---

# 🚀 Tự động giám sát Kubernetes Services & Pods bằng Prometheus và gửi cảnh báo Slack

Trong môi trường hạ tầng hiện đại, việc theo dõi sức khỏe của các cụm Kubernetes (K8s) là nhiệm vụ sống còn của đội ngũ DevOps. Tuy nhiên, việc liên tục kiểm tra dashboard Grafana thủ công hay bỏ sót các lỗi chớp nhoáng như `CrashLoopBackOff`, Pod Pending, hay Service Endpoint sụt giảm có thể gây ra những sự cố nghiêm trọng cho hệ thống.

Bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n cực mạnh mẽ, tự động hóa toàn bộ quy trình: định kỳ truy vấn Prometheus, phân tích dữ liệu, gom nhóm thông minh và bắn cảnh báo chi tiết, trực quan trực tiếp lên kênh Slack của team.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow giám sát chạy ổn định 24/7 mà không lo gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Phát hiện sự cố tức thì:** Tự động quét cluster mỗi 5 phút, bắt trọn lỗi `CrashLoopBackOff`, Pod Restart Spike, Not Ready... trước khi khách hàng kịp kêu ca.
- **Giảm nhiễu (Noise Reduction):** Bộ lọc thông minh tự động loại bỏ các metric nhiễu, chỉ gửi cảnh báo thực sự có ý nghĩa (`> 0` cho các lỗi).
- **Cảnh báo trực quan trên Slack:** Tin nhắn được format đẹp mắt kèm emoji, phân cấp mức độ nghiêm trọng và tóm tắt theo namespace/service.
- **Hoạt động 24/7 không cần nghỉ ngơi:** Thay thế hoàn toàn việc canh trực thủ công của đội ngũ vận hành.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ TRƯỚC KHI "LÊN ĐỒ"]
- **Hệ thống Prometheus** đang chạy và có thể truy cập qua HTTP API.
- **Slack App / Incoming Webhook** hoặc tích hợp Bearer Token để gửi tin nhắn vào channel của team.
- **n8n Instance** (phiên bản Cloud hoặc Self-hosted).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow từ n8n (ID: `7665`).
- Vào n8n Editor, chọn **Add workflow** -> **Import from File** (hoặc paste trực tiếp mã JSON).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này bao gồm 16 nodes được sắp xếp logic từ việc lấy dữ liệu, xử lý đến khi bắn thông báo:

- **🕒 Every 5 Min Trigger:** Node khởi chạy định kỳ (mặc định 5 phút/lần). Có thể tinh chỉnh thời gian nếu muốn kiểmặt dày hơn.
- **Các HTTP Request Nodes (Prometheus):** 
  - *Current endpoints*, *Endpoints 5m ago*, *Pods Running State*, *Containers Not Ready*, *Pod Pending State*, *Pod Restart Spike*, *CrashLoopBackOff / Termination Reason*: Cần cấu hình lại URL kết nối đến Prometheus Server của các sếp trong phần cấu hình HTTP Request.
- **Các Code Nodes (Normalization & Mapping):** 
  - *Normalization*, *Slack formatter with summary*, *Map Prometheus results into namespace/service*... Các đoạn mã JavaScript có sẵn sẽ chuẩn hóa dữ liệu thô từ Prometheus thành cấu trúc JSON chuẩn (`namespace`, `service`, `pod_restart`, `pod_not_ready`...). Không cần sửa code trừ khi các sếp muốn đổi cấu trúc hiển thị.
- **Merge Nodes (*Merge (endpoints)* & *Merge All data collected*):** Gom nhóm toàn bộ các luồng metric thành một tập dữ liệu duy nhất trước khi chuyển sang bước định dạng tin nhắn.
- **📤 Send Alerts to Slack:** Node cuối cùng chịu trách nhiệm đẩy chuỗi tin nhắn đã format lên Slack. Cần cấu hình **Credentials** (`httpBearerAuth` hoặc Webhook URL) kết nối với workspace Slack của công ty.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để test thủ công xem dữ liệu từ Prometheus có trả về và format thành công hay không.
- Sau khi kiểm tra luồng chạy mượt mà, bật công tắc **Active** ở góc trên bên phải để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm Telegram / Microsoft Teams:** Ngoài Slack, các sếp có thể nhân bản node cuối để bắn song song cảnh báo sang group Telegram của bộ phận IT.
- **Lưu log vào Google Sheets / Database:** Thêm node Google Sheets để lưu lại lịch sử các lỗi Pod Restart, giúp kỹ sư dễ dàng thống kê và phân tích xu hướng lỗi theo tuần/tháng.
- **Phân loại mức độ nghiêm trọng (Severity):** Tùy chỉnh đoạn code trong *Slack formatter* để gắn tag `🔴 CRITICAL` cho lỗi CrashLoopBackOff và `🟡 WARNING` cho lỗi Pod Pending.

### 📌 Kết luận
Với workflow n8n giám sát Kubernetes qua Prometheus này, các sếp đã sở hữu một hệ thống DevOps tự động chuyên nghiệp chỉ trong vài nốt nhạc. Không còn nỗi lo "sập hệ thống mà sáng hôm sau mới biết", hãy cài đặt ngay để tối ưu hóa vận hành hệ thống của doanh nghiệp!