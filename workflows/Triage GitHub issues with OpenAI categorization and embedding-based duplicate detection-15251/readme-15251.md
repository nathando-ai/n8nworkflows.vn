---
title: "🚀 Tự động phân loại và xử lý Issue GitHub bằng AI - Giải phóng thời gian cho Dev Team"
description: "Workflow n8n tự động phân loại Issue GitHub bằng AI, phát hiện duplicate bằng embedding, giảm 80% thời gian xử lý thủ công cho Dev Team"
slug: "tu-dong-phan-loai-issue-github-bang-ai"
tags: [n8n, automation, no-code, github, ai]
keywords: [n8n workflow, tự động hóa github, phân loại issue, ai duplicate detection]
---

# 🚀 Tự động phân loại và xử lý Issue GitHub bằng AI - Giải phóng thời gian cho Dev Team

[Các sếp làm Dev Team] có biết không? Mỗi ngày phải xử lý hàng chục Issue trên GitHub là một công việc cực kỳ tốn thời gian và dễ gây mệt mỏi. Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình từ nhận Issue đến phân loại, xử lý và đóng Issue - chỉ trong vài phút cấu hình.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Giảm 80% thời gian xử lý thủ công**: Tự động phân loại và xử lý Issue trong vòng vài giây
- **Phát hiện duplicate chính xác**: Sử dụng embedding vector để tìm Issue trùng lặp với độ chính xác cao
- **Tự động hóa toàn bộ quy trình**: Từ nhận Issue đến đóng Issue hoàn toàn tự động
- **Tăng hiệu suất làm việc**: Dev Team tập trung vào các Issue quan trọng hơn
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản GitHub với Personal Access Token có quyền repo
- Tài khoản OpenAI với API key
- Google Sheet có tên "feature_roadmap" với các cột: date_added, issue_number, title, author, url, status
- Tài khoản Slack với quyền gửi tin nhắn vào channel
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/15251](https://n8n.io/workflows/15251)
2. Click vào nút "Import" ở góc trên bên phải
3. Copy toàn bộ JSON workflow và dán vào n8n Editor

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node GitHub Issue Webhook**:
   - Đảm bảo webhook đã được cấu hình trên repository của bạn
   - Path mặc định là "github-issue-triage" (có thể thay đổi)

2. **Node Set Configuration**:
   - Cập nhật các thông số:
     - `repo_owner`: Tên chủ sở hữu repository
     - `repo_name`: Tên repository
     - `sheet_id`: ID của Google Sheet "feature_roadmap"
     - `slack_channel`: Tên channel Slack để gửi thông báo
     - `faq_url`: URL của trang FAQ

3. **Node Fetch Recent Issues**:
   - Đảm bảo GitHub credentials đã được cấu hình
   - Thay đổi số lượng Issue lấy về nếu cần (mặc định là 30)

4. **Node Get Embeddings (Batch)**:
   - Đảm bảo OpenAI credentials đã được cấu hình
   - Kiểm tra API key còn hạn sử dụng

5. **Node Classify Issue**:
   - Đảm bảo OpenAI credentials đã được cấu hình
   - Có thể điều chỉnh prompt để phù hợp với dự án của bạn

6. **Node Add to Roadmap**:
   - Đảm bảo Google Sheets credentials đã được cấu hình
   - Kiểm tra cấu trúc của Google Sheet "feature_roadmap"

7. **Node Alert Dev Team**:
   - Đảm bảo Slack credentials đã được cấu hình
   - Kiểm tra quyền gửi tin nhắn vào channel đã chọn

#### 3. Kích hoạt ⚡️
1. Click vào nút "Test Workflow" để kiểm tra với dữ liệu mẫu
2. Sau khi kiểm tra thành công, click vào nút "Activate" để kích hoạt workflow

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp với Slack/Telegram**: Thêm node để gửi thông báo vào các kênh chat khác
- **Lưu log hoạt động**: Thêm node để lưu log các Issue đã xử lý vào Google Sheets
- **Gửi báo cáo định kỳ**: Thêm node để gửi báo cáo tổng hợp hàng tuần/tháng
- **Tích hợp với Jira**: Thêm node để tạo ticket trên Jira cho các Issue quan trọng

### 📌 Kết luận
Workflow này giúp các sếp Dev Team tự động hóa toàn bộ quy trình xử lý Issue GitHub, từ nhận Issue đến đóng Issue hoàn toàn tự động. Với việc phát hiện duplicate chính xác và phân loại Issue bằng AI, các sếp có thể tập trung vào các Issue quan trọng hơn và tăng hiệu suất làm việc đáng kể.

Hãy áp dụng ngay workflow này để giải phóng thời gian cho Dev Team và tập trung vào những việc quan trọng hơn!