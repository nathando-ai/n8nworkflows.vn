---
title: "🚀 Tự động tạo bài blog với GPT‑4 và đăng lên Ghost CMS"
description: "Workflow n8n tự động tạo nội dung blog bằng GPT‑4, chuẩn SEO và đăng ngay lên Ghost CMS mỗi 12 giờ, không cần viết mã."
slug: "tu-dong-tao-bai-blog-voi-gpt4-ghost-cms"
tags: [n8n, automation, no-code, content-creation, ghost-cms]
keywords: [n8n workflow, tự động hóa, GPT-4, Ghost CMS, tạo nội dung]
---

# 🚀 Tự động tạo bài blog với GPT‑4 và đăng lên Ghost CMS

Việc viết bài blog chất lượng, chuẩn SEO và đăng tải đều đặn luôn là “cơn ác mộng” cho các sếp marketing: phải lên ý tưởng, viết, chỉnh sửa, tạo meta‑data, rồi mới cuối cùng mới đăng lên nền tảng CMS.  
**Workflow này** giải quyết toàn bộ quy trình chỉ trong vài giây, chạy tự động mỗi 12 giờ, không cần một dòng code nào. Bạn chỉ cần cung cấp API key của OpenAI và Ghost, mọi thứ sẽ được thực hiện tự động:  
- **AI** tạo tiêu đề, nội dung, thẻ, mô tả meta.  
- **Code node** định dạng dữ liệu cho Ghost.  
- **HTTP Request** gửi bài viết lên Ghost CMS.  

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không còn viết tay, chỉ cần thiết lập một lần.  
- **Độ chính xác cao**: AI tạo nội dung dựa trên prompt chuẩn SEO, giảm lỗi ngữ pháp.  
- **Đăng tự động**: Bài viết được xuất bản ngay lập tức lên Ghost mà không cần thao tác thủ công.  
- **Hoạt động liên tục**: Chạy mỗi 12 giờ, luôn có nội dung mới cho blog.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản OpenAI** với **API Key** (để sử dụng node `OpenAI`).  
- **Ghost CMS**: URL của site và **Admin API Key** (để cấu hình node `HTTP Request1`).  
- **n8n** đã được cài đặt (Self‑hosted hoặc Cloud).  
- Quyền **Schedule Trigger** để workflow có thể chạy định kỳ.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Tải file JSON của workflow (được cung cấp trong mục **Export** của n8n).  
2. Vào n8n → **Workflows** → **Import** → Chọn file JSON hoặc **Paste JSON** → **Import**.  
3. Workflow sẽ xuất hiện trên canvas với 5 node: `Schedule Trigger`, `OpenAI`, `HTTP Request1`, `Code`, `Code1`.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Cấu hình quan trọng | Hướng dẫn |
|------|--------------------|-----------|
| **Schedule Trigger** | **Cron** | Đặt `Every 12 hours` (hoặc tùy chỉnh thời gian chạy). |
| **OpenAI** | **Credentials** → `openAiApi` | Dán **API Key** của OpenAI. <br>**Prompt** (được lưu trong node Code) sẽ yêu cầu AI tạo: <br>• Tiêu đề <br>• Nội dung chính <br>• Thẻ (tags) <br>• Meta description. |
| **Code** | **JavaScript** | Chuyển đổi output của OpenAI thành đối tượng JSON phù hợp với Ghost API (ví dụ: `{title, html, tags, meta_description}`). Không cần thay đổi logic nếu bạn dùng prompt mặc định. |
| **Code1** | **JavaScript** | Thêm bước **format** nếu muốn chèn hình ảnh, excerpt hoặc custom fields. Có thể bỏ qua nếu không cần. |
| **HTTP Request1** | **Credentials** → `ghostAdminApi` | Điền **API URL** (ví dụ: `https://your-ghost-site.com/ghost/api/v3/admin/posts/`) và **Admin API Key**. <br>**Method**: `POST` <br>**Body**: `JSON` → chọn **Expression** để truyền dữ liệu từ node `Code` (hoặc `Code1`). |
| **Sticky Note** (nếu có) | Thông tin mô tả | Không cần cấu hình, chỉ để tham khảo. |

> **Lưu ý:** Đảm bảo **CORS** và **IP whitelist** trên Ghost cho phép gọi API từ server n8n của bạn.

#### 3. Kích hoạt ⚡️
1. Nhấn **Execute Workflow** → chọn **Run Once** để kiểm tra với dữ liệu mẫu.  
2. Kiểm tra Ghost CMS: một bài viết mới sẽ xuất hiện.  
3. Nếu mọi thứ ổn, bật **Active** (nút chuyển đổi ở góc phải) để workflow chạy tự động theo lịch đã đặt.

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo Slack/Telegram**: Thêm node `Slack` hoặc `Telegram` sau `HTTP Request1` để gửi tin nhắn báo cáo thành công/kết quả lỗi.  
- **Lưu log vào Google Sheets**: Dùng node `Google Sheets` để ghi lại tiêu đề, thời gian đăng, URL bài viết.  
- **Tạo hình ảnh kèm**: Kết hợp node `OpenAI DALL·E` hoặc `Stable Diffusion` để tự động sinh ảnh bìa, sau đó đính kèm trong payload gửi tới Ghost.  
- **Đa ngôn ngữ**: Thêm một node `Code` để gọi OpenAI dịch nội dung sang các ngôn ngữ khác và đăng từng phiên bản trên các sub‑domain.  
- **Tối ưu thời gian đăng**: Thay `Schedule Trigger` bằng node `Cron` dựa trên phân tích thời gian tương tác cao (có thể lấy dữ liệu từ Google Analytics).  

### 📌 Kết luận
Với workflow **Automated Blog Post Generation with GPT‑4 and Publishing to Ghost CMS**, các sếp có thể “đặt và quên” việc tạo nội dung, tập trung vào chiến lược và phân tích hiệu quả. Hãy import ngay, cấu hình API, bật chạy và để AI làm việc cho bạn! 🚀