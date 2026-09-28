---
title: "🚀 Tự động tóm tắt bình luận Notion bằng AI (Google Gemini & n8n)"
description: "Hướng dẫn xây dựng workflow n8n tự động quét bình luận trên Notion database, sử dụng AI Google Gemini để tóm tắt và cập nhật ngược lại trang Notion mỗi giờ."
slug: "tu-dong-tom-tat-binh-luan-notion-bang-ai"
tags: [n8n, automation, notion, ai, google-gemini, productivity]
keywords: [n8n workflow, tóm tắt notion, notion automation, google gemini n8n, tự động hóa notion]
---

# 🚀 Tự động tóm tắt bình luận Notion bằng AI

Các sếp có đang gặp tình trạng quản lý dự án trên Notion nhưng các trang (pages) có quá nhiều bình luận (comments) thảo luận dài dằng dặc? Việc đọc lại toàn bộ từng dòng thảo luận để nắm ý chính mất rất nhiều thời gian, đặc biệt khi các thành viên liên tục cập nhật ý kiến.

Đừng lo, bài viết này sẽ hướng dẫn các sếp thiết lập một workflow n8n cực kỳ thông minh: tự động quét bình luận mới trên Notion, dùng AI (Google Gemini) để tóm tắt ngắn gọn và ghi trực tiếp bản tóm tắt đó lên trang Notion một cách hoàn toàn tự động!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian tối đa:** Không cần đọc hàng chục bình luận dài dòng, AI sẽ cô đọng lại thành các ý chính cần hành động (action items).
- **Cập nhật liên tục:** Tự động quét định kỳ mỗi giờ để bắt trọn mọi thảo luận mới phát sinh.
- **Tập trung cao độ:** Giúp quản lý và các thành viên nắm bắt tiến độ dự án nhanh chóng ngay trực tiếp tại trang Notion liên quan.
- **Vận hành 100% tự động:** Không cần can thiệp thủ công, loại bỏ hoàn toàn việc quên tổng hợp thông tin.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và API sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản Notion** và quyền tạo Internal Integration (để lấy Notion API Key).
- **Notion Database** có chứa các trang cần theo dõi bình luận, kèm theo 2 trường (properties) phụ:
  - Một property kiểu **Text** (để chứa nội dung AI tóm tắt).
  - Một property kiểu **Date** (để lưu mốc thời gian chạy gần nhất).
- **Google Gemini API Key** (hoặc các LLM khác tùy chọn như OpenAI, Claude).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này từ n8n template (ID: 5048) và dán trực tiếp vào giao diện n8n Editor của mình, hoặc sử dụng tính năng import file JSON.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động trơn tru với dữ liệu của các sếp, hãy cấu hình kỹ các node sau:

- **Node `Define your Notion Database` (Set):** 
  - Khai báo chính xác các biến số bao gồm: ID của Notion Database, tên trường (property) chứa bản tóm tắt AI, và tên trường lưu ngày chạy cuối cùng (last execution date).
- **Node `List database pages` & `Add summary to Notion page and update last execution date` (Notion):**
  - Cần kết nối tài khoản thông qua **Notion API** credentials (Notion Internal Integration). Đảm bảo integration của các sếp đã được cấp quyền truy cập (Share) vào Database mục tiêu.
- **Node `List comments` (HTTP Request):**
  - Sử dụng Notion API để gọi danh sách bình luận của trang. Cần sử dụng chung Notion credentials ở bước trên.
- **Node `Google Gemini Chat Model` & `Summarize conversation` (Agent):**
  - Kết nối credentials của Google Gemini (Google Palm API). 
  - Tại đây, các sếp có thể tùy chỉnh prompt trong Agent để AI viết ngắn gọn, tập trung vào hành động (action-oriented) hoặc định dạng theo ý muốn.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để test thủ công một lượt xem dữ liệu từ Notion có đổ về AI và ghi ngược lại thành công hay không.
- Sau khi test xanh mượt, bật công tắc **Active** ở góc trên cùng bên phải để workflow tự động chạy theo lịch (mặc định mỗi giờ một lần từ node `Run every hour`).

### ✍️ Mẹo & gợi ý nâng cao
- **Tối ưu trigger:** Thay vì dùng lịch chạy định kỳ hàng giờ (`Run every hour`), các sếp có thể thay thế bằng **Notion Webhooks** (nếu dùng n8n Cloud) để workflow kích hoạt tức thì ngay khi có bình luận mới được thêm vào.
- **Tùy chỉnh Prompt:** Biến tấu câu lệnh (prompt) trong Agent AI để ép nó trả về kết quả theo định dạng Bullet points, phân rõ ai cần làm gì (Assignee) cho chuyên nghiệp.
- **Cắt giảm token:** Nếu bình luận quá dài, hãy tinh chỉnh dữ liệu truyền vào AI (chỉ lấy phần nội dung text thuần túy) để tiết kiệm lượng token tiêu thụ.
- **Mở rộng thông báo:** Kết hợp thêm node gửi thông báo về **Telegram** hoặc **Slack** cho quản lý mỗi khi có một bản tóm tắt quan trọng được cập nhật lên Notion.

### 📌 Kết luận
Workflow tự động tóm tắt bình luận Notion bằng AI là trợ thủ đắc lực giúp tối ưu hóa luồng giao tiếp và quản lý công việc trong team. Hãy áp dụng ngay để biến Notion thành một "bộ não" thông minh và tự động hóa thực thụ!