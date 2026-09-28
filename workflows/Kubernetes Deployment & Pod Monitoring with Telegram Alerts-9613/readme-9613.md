---
title: "🚀 Tự động giám sát Kubernetes Deployment & Pods, cảnh báo qua Telegram bằng n8n"
description: "Hướng dẫn xây dựng hệ thống tự động kiểm tra Kubernetes cluster, phát hiện workload lỗi và gửi cảnh báo trực tiếp qua Telegram, đồng thời lưu báo cáo markdown định kỳ."
slug: "giam-sat-kubernetes-va-canh-bao-telegram-bang-n8n"
tags: [n8n, automation, kubernetes, devops, telegram, monitoring]
keywords: [n8n workflow, giám sát kubernetes, k8s monitoring, cảnh báo telegram, devops automation]
---

# 🚀 Tự động giám sát Kubernetes Deployment & Pods, cảnh báo qua Telegram bằng n8n

Việc thủ công kiểm tra trạng thái các Pods và Deployments trên cụm Kubernetes (K8s) mỗi ngày là một nỗi đau đầu của các DevOps Engineer. Khi hệ thống gặp sự cố sập Pod hay lỗi Deployment mà không phát hiện kịp thời, dịch vụ sẽ bị gián đoạn gây thiệt hại lớn. 

Giải pháp? Workflow n8n tự động hóa 100% này sẽ thay các sếp kiểm tra cluster K8s định kỳ, tự động tải `kubectl` khi chạy, quét toàn bộ namespace, lọc ra các workload đang lỗi (0 ready pods), bắn ngay cảnh báo qua Telegram và lưu lại báo cáo chi tiết dưới dạng file Markdown. Không cần code phức tạp, setup một lần chạy mượt mà mãi mãi!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Phát hiện sự cố tức thì:** Tự động cảnh báo ngay qua Telegram khi có Pod/Deployment không sẵn sàng (0 ready pods).
- **Báo cáo định kỳ minh bạch:** Tự động tạo và lưu trữ báo cáo Markdown (`k8s-report-YYYY-MM-DD-HHmmss.md`) cho mọi lần chạy.
- **Tự động hóa toàn diện:** Tự động tải và cấu hình `kubectl` trong quá trình chạy, không cần cài đặt phức tạp trên server n8n.
- **Hoạt động 24/7:** Chạy ngầm liên tục theo lịch trình (Schedule Trigger) giúp DevOps an tâm ngủ ngon giấc.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n (Self-hosted được khuyến nghị để có quyền thực thi lệnh hệ thống).
- Tài khoản Telegram và một Bot Token được tạo từ **@BotFather** kèm Chat ID nhận thông tin.
- Nội dung tệp cấu hình **kubeconfig** để kết nối tới cụm Kubernetes của các sếp.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Copy toàn bộ mã JSON của workflow hoặc import file JSON trực tiếp vào giao diện n8n Editor của các sếp. Workflow bao gồm 8 nodes chính: *Schedule Trigger, Kubeconfig Setup, Get Pods, Get Deployments, Process & Generate Report, Has Alerts?, Send Telegram Alert, Save Report*.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống hoạt động chính xác, các sếp cần cấu hình kỹ các điểm sau:
- **Kubeconfig Setup (Node Code):** Dán nội dung file `kubeconfig` của cụm Kubernetes vào node này và cấu hình `namespace` mục tiêu (mặc định là `production`).
- **Get Pods & Get Deployments (Node Execute Command):** Hai node này chạy song song để lấy danh sách Pods và Deployments từ namespace đã chỉ định. Node sẽ tự động tải `kubectl` nếu chưa có trên môi trường chạy.
- **Send Telegram Alert (Node Telegram):** 
  - Kết nối tài khoản Telegram thông qua `telegramApi` credentials (sử dụng Bot Token từ `@BotFather`).
  - Thay thế `YOUR_TELEGRAM_CHAT_ID` bằng Chat ID thực tế của các sếp. (Mẹo lấy Chat ID: Nhắn tin cho bot của các sếp, sau đó truy cập `https://api.telegram.org/bot<TOKEN>/getUpdates`).
- **Save Report (Node Write Binary File):** Cấu hình đường dẫn thư mục lưu trữ file báo cáo Markdown trên server n8n của các sếp với định dạng tên tệp: `k8s-report-YYYY-MM-DD-HHmmss.md`.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để test run thủ công, kiểm tra xem dữ liệu Pod/Deployment có được lấy về chính xác không và tin nhắn Telegram có gửi thành công hay không.
- Sau khi test ngon lành, gạt công tắc sang **Active** để workflow tự động chạy theo lịch trình.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thêm kênh chat:** Ngoài Telegram, các sếp có thể nối thêm node Slack hoặc Discord để bắn cảnh báo đa kênh cho đội ngũ kỹ thuật.
- **Lưu log vào Database:** Kết hợp thêm node PostgreSQL hoặc Supabase để lưu trữ lịch sử sức khỏe cluster theo thời gian thực, phục vụ việc vẽ biểu đồ Grafana.
- **Mở rộng phạm vi quét:** Thay vì chỉ định một namespace cố định, các sếp có thể cấu hình node quét toàn bộ cluster (`--all-namespaces`) để giám sát toàn diện hơn.

### 📌 Kết luận
Hệ thống giám sát Kubernetes tự động với n8n và Telegram là trợ thủ đắc lực giúp đội ngũ DevOps nắm bắt tình trạng cluster ngay lập tức mà không cần tốn thời gian kiểm tra thủ công. Triển khai ngay hôm nay để tối ưu hóa vận hành hệ thống của các sếp nhé!