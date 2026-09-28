---
title: "🚀 Tạo bản tin công nghệ AI được tổng hợp bằng GPT‑4.1 Mini và Notion Database"
description: "Tự động lấy, phân loại, tóm tắt và lưu trữ tin tức công nghệ vào Notion một cách nhanh chóng và chính xác."
slug: "tao-ban-tin-cong-nghe-ai-gpt-4-1-mini-notion"
tags: [n8n, automation, no-code, AI, Notion, GPT]
keywords: [n8n workflow, tự động hóa, AI summarization, Notion integration, GPT-4.1 Mini]
---

# 🚀 Tạo bản tin công nghệ AI được tổng hợp bằng GPT‑4.1 Mini và Notion Database

Bạn đang phải mất hàng giờ để lọc, đọc và viết lại tin tức công nghệ?  
Workflow này sẽ giúp bạn **tự động** lấy dữ liệu từ Notion, phân loại, tóm tắt bằng GPT‑4.1 Mini và **đăng** bản tin mới vào Notion – **không cần viết một dòng code**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Từ vài giờ → vài phút.  
- **Chính xác & nhất quán**: Mọi bản tin đều được GPT‑4.1 Mini kiểm duyệt.  
- **Cá nhân hóa**: Thêm tiêu đề, ngày tháng, tag tự động.  
- **Hoạt động liên tục**: Lên lịch hàng ngày, không cần can thiệp thủ công.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản Notion**: Cần quyền đọc/ghi vào database chứa tin tức.  
- **API Key OpenAI**: Để gọi GPT‑4.1 Mini.  
- **ID Database Notion**: Định danh nơi lưu trữ bản tin.  
- **VPS hoặc máy chủ n8n**: Để chạy workflow 24/7.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Tải file JSON từ link gốc: <https://n8n.io/workflows/8665>.  
2. Mở n8n Editor → **Import** → **Upload JSON**.  
3. Hoặc copy toàn bộ JSON và dán vào **Import from clipboard**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Tên thực tế | Cấu hình cần chỉnh | Ghi chú |
|------|-------------|---------------------|---------|
| `When clicking ‘Execute workflow’` | `manualTrigger` | Không cần thay đổi | Dùng để test thủ công. |
| `Schedule Trigger` | `scheduleTrigger` | **Thời gian** (ví dụ: 00:00 mỗi ngày) | Đặt lịch hàng ngày. |
| `Get many database pages` | `notion` | **Database ID** (đã có trong credentials) | Lấy danh sách tin tức. |
| `Code in JavaScript` (1) | `code` | **Date filter** (định dạng `YYYY-MM-DD`) | Lọc bài viết theo ngày. |
| `Text Classifier` | `textClassifier` | **Model**: GPT‑4.1 Mini | Phân loại “Tech” và “Startup”. |
| `OpenAI Chat Model` (1) | `lmChatOpenAi` | **Model**: gpt‑4.1‑mini | Tóm tắt từng bài. |
| `Code in JavaScript` (2) | `code` | **Combine articles** | Tạo object chứa tất cả bài. |
| `AI Agent` | `agent` | **Prompt**: “Generate a single article with raw Notion page format.” | Tạo bản tin duy nhất. |
| `OpenAI Chat Model` (2) | `lmChatOpenAi` | **Model**: gpt‑4.1‑mini | Tạo nội dung cuối cùng. |
| `Code in JavaScript` (3) | `code` | **Format JSON**: Định dạng Notion page | Chuẩn bị payload cho HTTP. |
| `HTTP Request` | `httpRequest` | **URL**: `https://api.notion.com/v1/pages` <br>**Method**: POST <br>**Headers**: `Authorization: Bearer <NOTION_TOKEN>` <br>**Body**: JSON từ node trước | Tạo trang Notion mới. |

> **Lưu ý**: Mỗi node `Code in JavaScript` có thể cần chỉnh tham số `dateFilter`, `tags`, `pageTitle` tùy theo nhu cầu.

#### 3. Kích hoạt ⚡️
1. **Test run**: Chạy workflow thủ công bằng nút **Execute workflow**. Kiểm tra log, đảm bảo không có lỗi.  
2. **Bật Active**: Sau khi xác nhận, chuyển workflow sang trạng thái **Active**.  
3. Workflow sẽ tự động chạy theo lịch đã đặt.

### ✍️ Mẹo & gợi ý nâng cao
- **Slack/Telegram Notification**: Thêm node `Slack` hoặc `Telegram` sau `HTTP Request` để nhận thông báo khi bản tin được đăng.  
- **Lưu Log vào Google Sheets**: Dùng node `Google Sheets` để ghi lại tiêu đề, ngày, link.  
- **Bản tin hàng tuần**: Thay `Schedule Trigger` thành “Every Monday 08:00” và điều chỉnh `dateFilter` để lấy tuần trước.  
- **Tùy chỉnh Prompt**: Thêm phần “Include key takeaways” vào prompt của AI Agent để làm nổi bật những điểm quan trọng.  

### 📌 Kết luận
Workflow này giúp các sếp **đưa tin tức công nghệ** vào Notion một cách nhanh, chính xác và không cần viết code.  
Hãy thử ngay, điều chỉnh theo nhu cầu và chia sẻ kết quả! 🚀