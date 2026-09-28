---
title: "🚀 Tự động đồng bộ Email từ Gmail có gắn nhãn vào Notion Database với n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động quét email Gmail theo nhãn chỉ định, tạo trang mới trên Notion Database và tự động gỡ nhãn khi hoàn thành công việc."
slug: "tu-dong-dong-bo-email-gmail-vao-notion-database-n8n"
tags: [n8n, automation, no-code, gmail, notion, productivity]
keywords: [n8n workflow, tự động hóa gmail notion, đồng bộ email vào notion, n8n gmail trigger, notion database integration]
---

# 🚀 Tự động đồng bộ Email từ Gmail có gắn nhãn vào Notion Database với n8n

Các sếp có bao giờ cảm thấy ngợp trước hàng tá email quan trọng cần xử lý, việc copy thủ công nội dung từng email sang Notion để theo dõi tiến độ vừa mất thời gian lại vừa dễ bỏ sót? Đừng để những thao tác thủ công này làm giảm hiệu suất làm việc của đội ngũ. 

Với workflow n8n này, mọi thứ sẽ được tự động hóa 100%. Khi các sếp gắn một nhãn (label) bất kỳ cho email trong Gmail (ví dụ: nhãn "Notion"), hệ thống sẽ tự động trích xuất nội dung, tạo một task mới trên Notion Database, và thậm chí tự động gỡ nhãn khi công việc trên Notion được hoàn tất!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Không cần copy/paste thủ công nội dung email sang Notion nữa.
- **Quản lý thông minh:** Tiêu đề email trở thành tiêu đề trang Notion, nội dung tóm tắt (snippet) làm thân bài, kèm theo đường dẫn trực tiếp tới email gốc.
- **Đồng bộ hai chiều:** Khi task trên Notion được đánh dấu hoàn thành (checked off), nhãn trên Gmail sẽ tự động bị xóa để làm sạch hộp thư.
- **Tránh trùng lặp:** Workflow thông minh kiểm tra xem email đã tồn tại trong database hay chưa trước khi tạo mới.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** Đã hoạt động (Cloud hoặc Self-hosted).
- **Gmail Account:** Cần cấu hình OAuth2 Credentials và tạo sẵn một nhãn (ví dụ: `Notion`).
- **Notion Account:** Đã tạo một Database với các trường (properties) tối thiểu:
  - `Title` (kiểu Title)
  - `Thread ID` (kiểu Text)
  - `Email thread` (kiểu URL)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tạo một workflow mới trong giao diện n8n Editor, sau đó copy toàn bộ mã JSON của workflow này và dán trực tiếp vào màn hình làm việc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình chính xác các node trọng điểm sau:

- **Node `Get emails from label and last request time` (Gmail):** 
  - Chọn Credentials tài khoản Gmail của các sếp.
  - Cấu hình lấy email dựa trên nhãn (label) đã tạo (ví dụ: `Notion`).
- **Node `Create database page` & `Try get database page` (Notion):**
  - Kết nối Notion API Credentials.
  - Chọn đúng Notion Database ID mà các sếp muốn lưu trữ dữ liệu.
  - Map các trường dữ liệu: Tiêu đề trang, Thread ID, và URL email.
- **Node `On updated database page` (Notion Trigger) & `Remove label from target email` (Gmail):**
  - Đảm bảo Notion Trigger kết nối đúng database để lắng nghe sự kiện khi task được chuyển trạng thái "checked off".
  - Node Gmail sẽ thực hiện hành động gỡ nhãn (`removeLabels`) tương ứng trên email gốc.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** chạy thử với dữ liệu mẫu để kiểm tra kết nối API.
- Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải để workflow tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo qua Telegram/Slack:** Thêm một node Telegram hoặc Slack ngay sau khi tạo page thành công trên Notion để bắn thông báo cho team cùng biết.
- **Gán nhãn tự động bằng AI:** Kết hợp thêm các node AI/LangChain để phân tích nội dung email và tự động gán nhãn, phân loại độ ưu tiên trước khi đẩy vào Notion.
- **Log lỗi:** Thiết lập Error Trigger để ghi nhận lại nếu có sự cố mất kết nối API từ Gmail hoặc Notion.

### 📌 Kết luận
Workflow này là một "vũ khí" đắc lực giúp tối ưu hóa quy trình xử lý email và quản lý công việc cá nhân cũng như đội ngũ. Hãy áp dụng ngay hôm nay để biến hộp thư Gmail thành một hệ thống quản lý task chuyên nghiệp trên Notion!