---
title: "🚀 Phát hiện vi phạm bản quyền tự động với ScrapeGraphAI & phản hồi pháp lý"
description: "Giải pháp n8n tự động quét web, so sánh nội dung và gửi cảnh báo pháp lý ngay lập tức khi phát hiện vi phạm bản quyền."
slug: "phat-hien-vi-pham-ban-quyen-tu-dong-scrapegraphai"
tags: [n8n, automation, no-code, AI, legal-tech]
keywords: [n8n workflow, tự động hóa, phát hiện vi phạm bản quyền, ScrapeGraphAI, phản hồi pháp lý]
---

# 🚀 Phát hiện vi phạm bản quyền tự động với ScrapeGraphAI & phản hồi pháp lý

Doanh nghiệp ngày càng phải đối mặt với hàng ngàn nội dung trái phép lan truyền trên internet: bài viết sao chép, hình ảnh, video hay thậm chí là slogan thương hiệu. Việc **giám sát thủ công** không chỉ tốn thời gian, mà còn dễ bỏ sót, khiến thương hiệu bị tổn hại và mất cơ hội thực thi quyền sở hữu trí tuệ.

**Workflow n8n** này sẽ **tự động**:
1. **Tìm kiếm** trên web các dấu hiệu vi phạm bằng ScrapeGraphAI.  
2. **So sánh** nội dung thu thập được với kho dữ liệu bản quyền của bạn.  
3. **Xác định mức độ rủi ro** và **kích hoạt hành động pháp lý** (cảnh báo, thu thập chứng cứ, gửi cease‑and‑desist).  
4. **Gửi thông báo tức thời** qua Telegram tới đội ngũ pháp lý.

Kết quả: **giảm 80 % thời gian giám sát**, **tăng độ chính xác** trong việc phát hiện vi phạm và **đảm bảo phản hồi nhanh chóng** trước các mối đe dọa.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động quét và phân tích hàng trăm trang mỗi ngày.  
- **Độ chính xác cao**: AI so sánh nội dung, giảm false positive xuống <5 %.  
- **Phản hồi nhanh**: Cảnh báo ngay lập tức qua Telegram, giảm thời gian phản hồi pháp lý.  
- **Hoạt động liên tục**: Chạy 24/7 trên VPS, không cần can thiệp thủ công.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản ScrapeGraphAI** + API Key.  
- **Bot Telegram** và **Token** (để nhận thông báo).  
- **Telegram Chat ID** của nhóm pháp lý hoặc cá nhân.  
- **n8n** (cài đặt trên VPS hoặc Docker).  
- **Schedule Trigger**: cấu hình thời gian chạy (ví dụ: mỗi 6 giờ).  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. **Tải file JSON** của workflow (từ link gốc: https://n8n.io/workflows/6642).  
2. Vào **n8n Editor → Import → From File** và chọn file JSON.  
3. Hoặc **Copy/Paste** toàn bộ JSON vào **Import → Paste JSON**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Công việc | Cấu hình cần chỉnh |
|------|-----------|--------------------|
| **Schedule Trigger** | Đặt lịch chạy tự động | Chọn **Cron** hoặc **Interval** (ví dụ: `0 */6 * * *` – mỗi 6 giờ). |
| **ScrapeGraphAI Web Search** | Tìm kiếm vi phạm trên web | <ul><li>**API Key**: chọn credential ScrapeGraphAI.</li><li>**Search Query**: nhập các cụm từ bản quyền, tên thương hiệu, slogan.</li><li>**Search Options**: bật “Include images & videos” nếu cần.</li></ul> |
| **Content Comparer** (Code) | So sánh nội dung thu thập được với dữ liệu gốc | <ul><li>Thêm **protectedContent** (đoạn văn bản, slogan) vào biến `protectedContent` trong code.</li><li>Điều chỉnh **similarityThreshold** (mặc định 0.8) tùy mức nhạy cảm.</li></ul> |
| **Infringement Detector** (Code) | Xác định mức độ rủi ro và đề xuất hành động | <ul><li>Kiểm tra **riskScore** trả về từ Content Comparer.</li><li>Định nghĩa **riskLevels** (high, medium, low) trong code.</li></ul> |
| **Legal Action Trigger** (If) | Phân luồng dựa trên mức độ rủi ro | <ul><li>Điều kiện **high** → đi tới **Brand Protection Alert**.</li><li>Điều kiện **medium** → đi tới **Monitoring Alert**.</li><li>Luôn tạo **Evidence Collection** (có thể thêm node email/ticket). </li></ul> |
| **Brand Protection Alert** (Telegram) | Gửi cảnh báo khẩn cấp | <ul><li>Chọn **Credential**: Telegram Bot Token.</li><li>Nhập **Chat ID** của nhóm pháp lý.</li><li>Nội dung tin: `🚨 *Vi phạm bản quyền HIGH* – Case ID: {{ $json["caseId"] }}`.</li></ul> |
| **Monitoring Alert** (Telegram) | Gửi thông báo giám sát mức trung bình | <ul><li>Chat ID: kênh/nhóm giám sát.</li><li>Nội dung: `🔎 *Vi phạm trung bình* – Case ID: {{ $json["caseId"] }}`.</li></ul> |

> **Lưu ý:** Sau khi cấu hình xong, **đừng quên lưu** workflow (`Ctrl+S`) và **đóng** cửa sổ cấu hình.

#### 3. Kích hoạt ⚡️
1. **Test run** một lần với dữ liệu mẫu (có thể tạo một “dummy” protected phrase).  
2. Kiểm tra log của các node **Code** để xác nhận `riskScore` và `caseId`.  
3. Khi mọi thứ ổn, bật **Active** ở góc trên bên phải. Workflow sẽ tự động chạy theo lịch đã định.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết nối Slack**: Thêm node Slack để đồng thời gửi cảnh báo tới kênh Slack của bộ phận pháp lý.  
- **Lưu log vào Google Sheets**: Dùng node Google Sheets để ghi lại mọi case, giúp tạo báo cáo hàng tháng.  
- **Tự động tạo ticket**: Kết hợp với Jira/Asana API để tạo ticket ngay khi phát hiện vi phạm high‑risk.  
- **Phân tích hình ảnh**: Nếu cần kiểm tra hình ảnh, tích hợp thêm node **Computer Vision** (Google Vision hoặc Azure) để so sánh watermark.

### 📌 Kết luận
Với workflow **“Copyright Infringement Detector with ScrapeGraphAI and Automated Legal Response”**, các sếp có thể **giảm thiểu rủi ro bản quyền**, **tăng tốc độ phản hồi** và **đảm bảo thương hiệu luôn được bảo vệ** mà không tốn công sức lập trình. Hãy **import ngay**, **cấu hình các credentials** và **đặt lịch chạy** – bảo vệ tài sản trí tuệ của bạn chỉ trong vài phút! 🚀