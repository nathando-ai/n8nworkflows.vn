---
title: "🚀 Theo dõi hiệu suất mô hình AI với LangFuse - Tự động hóa 100% không cần code"
description: "Hướng dẫn chi tiết cách tự động theo dõi và phân tích hiệu suất mô hình AI trong n8n bằng LangFuse để tối ưu hóa chi phí và hiệu suất"
slug: "theo-doi-hieu-suat-ai-langfuse-n8n"
tags: [n8n, automation, no-code, AI, observability]
keywords: [n8n workflow, tự động hóa AI, LangFuse, observability, AI performance]
---

# 🚀 Theo dõi hiệu suất mô hình AI với LangFuse - Tự động hóa 100% không cần code

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp khi quản lý hiệu suất mô hình AI. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp có thể đã gặp phải tình trạng này: Mô hình AI của bạn đang chạy nhưng không biết nó hoạt động như thế nào thực sự. Bạn không thể theo dõi chi phí token, thời gian xử lý hay hiệu suất của từng bước trong workflow. Điều này khiến việc tối ưu hóa trở nên khó khăn và tốn kém.

Với workflow này, các sếp có thể tự động theo dõi và phân tích hiệu suất mô hình AI trong n8n bằng LangFuse, một công cụ quan sát hiệu suất mạnh mẽ cho các ứng dụng AI.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tự động thu thập và phân tích dữ liệu hiệu suất mô hình AI
- Theo dõi chi phí token và thời gian xử lý thực tế
- Tối ưu hóa hiệu suất workflow AI một cách khoa học
- Tích hợp liền mạch với LangFuse cho báo cáo và phân tích nâng cao
- Giảm thời gian xử lý và chi phí vận hành mô hình AI
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản LangFuse Cloud và API keys
- Instance n8n với node HTTP
- Credentials n8n API và HTTP Basic Auth
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor
2. Nhấn vào "Import from URL" và dán link: [https://n8n.io/workflows/9971](https://n8n.io/workflows/9971)
3. Hoặc copy nội dung JSON từ file workflow và paste vào n8n Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

**Node "When Executed by Another Workflow"**
- Không cần cấu hình gì thêm

**Node "n8n"**
- Chọn credentials: `n8nApi`
- Đảm bảo API key của bạn có quyền truy cập vào các execution

**Node "Split Out"**
- Không cần cấu hình gì thêm

**Node "Loop Over Items"**
- Không cần cấu hình gì thêm

**Node "HTTP Request"**
- Chọn credentials: `httpBasicAuth`
- URL: `https://cloud.langfuse.com/api/public/ingestion`
- Method: `POST`
- Headers: `Content-Type: application/json`
- Body: `{{$node["Code: prepare JSON for LF"].json}}`

**Node "Wait1"**
- Thời gian chờ: 1000ms (1 giây)

**Node "Remove Duplicates"**
- Chọn trường để loại bỏ trùng lặp: `execution_id`

**Node "Wait to get an execution data"**
- Thời gian chờ: 60000ms (60 giây)

**Node "Code: structure execution data"**
- Không cần cấu hình gì thêm

**Node "Code: prepare JSON for LF"**
- Không cần cấu hình gì thêm

#### 3. Kích hoạt ⚡️
1. Test run workflow với dữ liệu mẫu
2. Kiểm tra kết quả trên LangFuse Dashboard
3. Bật Active workflow để chạy tự động

### ✍️ Mẹo & gợi ý nâng cao
- Thêm node để gửi báo cáo hàng ngày qua email hoặc Slack
- Tích hợp với các công cụ khác như Prometheus để giám sát thời gian thực
- Tạo các dashboard tùy chỉnh trong LangFuse để theo dõi các chỉ số quan trọng
- Thêm các bước để tự động tối ưu hóa mô hình dựa trên dữ liệu phân tích

### 📌 Kết luận
Workflow này cung cấp giải pháp toàn diện để theo dõi và phân tích hiệu suất mô hình AI trong n8n. Bằng cách tích hợp với LangFuse, các sếp có thể lấy được những thông tin quan trọng để tối ưu hóa chi phí và hiệu suất của mô hình AI một cách khoa học. Hãy áp dụng ngay để nâng cao hiệu quả hoạt động của hệ thống AI của bạn!