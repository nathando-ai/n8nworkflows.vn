---
title: "🚀 Review GitHub Pull Requests tự động bằng Gemini – Gửi phản hồi, ghi log & thông báo Slack"
description: "Giải pháp tự động đánh giá PR trên GitHub bằng Gemini, tự động gửi review, lưu log vào Google Sheets và thông báo Slack – giảm thời gian review thủ công, tăng độ chính xác và minh bạch."
slug: "review-github-pr-gemini-automation"
tags: [n8n, automation, no-code, github, ai, slack, google-sheets, gemini]
keywords: [n8n workflow, tự động hóa, review PR, Gemini AI, GitHub, Slack, Google Sheets]
---

# 🚀 Review GitHub Pull Requests tự động bằng Gemini

Bạn đang phải dành hàng giờ để đọc, so sánh và đánh giá mã nguồn trong các Pull Request (PR) trên GitHub? Bạn muốn giảm thiểu sai sót, tăng tốc độ phản hồi và đồng thời lưu trữ lịch sử review một cách có hệ thống?  
Workflow này sẽ **đánh giá PR bằng Gemini AI, tự động gửi review lên GitHub, ghi log vào Google Sheets và thông báo ngay cho team qua Slack** – hoàn toàn không cần viết code.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

## 🎯 Kết quả các sếp nhận được

:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ vài phút cho tới vài giờ, workflow tự động thực hiện toàn bộ quy trình đánh giá.  
- **Độ chính xác cao**: Gemini AI phân tích diff, đưa ra nhận xét chi tiết, giảm sai sót do con người.  
- **Ghi log minh bạch**: Mọi review được lưu vào Google Sheets, dễ dàng tra cứu, báo cáo và audit.  
- **Thông báo tức thì**: Slack gửi tin nhắn ngay khi PR được đánh giá, giúp team luôn cập nhật.  
:::

## 🔧 Yêu cầu cần thiết

:::info[CHUẨN BỊ]
| Dịch vụ / API | Mô tả | Cách lấy |
|---|---|---|
| **GitHub Personal Access Token** | Dùng để lấy diff và gửi review. | Tạo token với quyền `repo` và `write:repo_hook`. |
| **Google Sheets API** | Lưu log vào bảng tính. | Tạo project, bật Sheets API, tạo OAuth2 client, lưu `client_id`, `client_secret`, `refresh_token`. |
| **Google Gemini API Key** | Truy cập mô hình Gemini. | Đăng ký tại Google Cloud, lấy API key. |
| **Slack Webhook URL** | Gửi thông báo. | Tạo Incoming Webhook trong Slack, copy URL. |
| **n8n Webhook URL** | Nhận sự kiện PR. | Được tạo khi bạn import workflow. |
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥
1. Tải file JSON từ trang gốc: <https://n8n.io/workflows/13563> hoặc copy toàn bộ JSON.  
2. Mở n8n Editor → **Import** → **Upload JSON** hoặc **Paste JSON**.  
3. Nhấn **Import**. Workflow sẽ xuất hiện trong danh sách.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Tên Node | Mô tả | Tham số cần cấu hình |
|---|---|---|---|
| Webhook | `GitHub PR webhook` | Nhận sự kiện `pull_request` từ GitHub. | `Webhook URL` (được tạo khi import). |
| Code | `Parse PR data` | Phân tích payload PR, lấy `pr_id`, `author`, `diff_url`. | Không cần cấu hình thêm. |
| HTTP Request | `Get PR diff` | Gọi `diff_url` để lấy diff. | `URL` = `{{$json["diff_url"]}}`, `Method` = `GET`. |
| Code | `Analyze diff` | Tách diff thành các file, line, comment. | Không cần cấu hình thêm. |
| Chain LLM | `Code review` | Chuẩn bị prompt cho Gemini. | `Prompt` = template (được viết trong node). |
| LM Chat Google Gemini | `Google Gemini AI` | Gửi prompt, nhận phản hồi. | `API Key` = Gemini key. |
| Code | `Format review` | Định dạng review thành JSON phù hợp với GitHub API. | Không cần cấu hình thêm. |
| HTTP Request | `Post GitHub review` | Gửi review lên GitHub. | `URL` = `https://api.github.com/repos/{{repo}}/pulls/{{pr_id}}/reviews`, `Method` = `POST`, `Body` = `{{$json["review_body"]}}`. |
| Google Sheets | `Log to Sheets` | Ghi log vào bảng tính. | `Spreadsheet ID`, `Sheet Name`, `Columns` (PR ID, Author, Review, Timestamp). |
| Slack | `Notify team` | Gửi tin nhắn Slack. | `Webhook URL`, `Message Text` = template. |
| Sticky Note | `Notes` | Ghi chú cho người dùng. | Không cần cấu hình. |

> **Lưu ý**: Đối với các node `Code`, bạn cần copy nội dung JavaScript đã được viết trong workflow gốc. Nếu muốn tùy chỉnh, hãy chỉnh sửa logic trong node.

### 3. Kích hoạt ⚡️
1. **Test run**: Chọn một PR mẫu, kích hoạt webhook bằng cách gửi payload từ GitHub (hoặc dùng công cụ Postman).  
2. Kiểm tra log trong Google Sheets và tin nhắn Slack.  
3. Khi mọi thứ hoạt động đúng, bật **Active** cho workflow.

## ✍️ Mẹo & gợi ý nâng cao
- **Thêm Slack/Telegram**: Sử dụng node `Telegram` để gửi thông báo tới kênh khác.  
- **Lưu log vào BigQuery**: Thay `googleSheets` bằng `bigquery` để lưu dữ liệu lớn hơn.  
- **Gửi báo cáo định kỳ**: Thêm node `Cron` + `Google Sheets` để tổng hợp review hàng ngày.  
- **Tùy chỉnh prompt**: Thêm các quy tắc coding style, kiểm tra unit test, hoặc yêu cầu kiểm tra bảo mật.  
- **Sử dụng `n8n-advanced`**: Để chạy workflow trên Kubernetes hoặc Docker Compose, giúp mở rộng quy mô.

## 📌 Kết luận
Workflow này giúp các sếp **đánh