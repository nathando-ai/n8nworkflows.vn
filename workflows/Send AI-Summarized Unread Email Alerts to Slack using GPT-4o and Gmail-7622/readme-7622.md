---
title: "🚀 Gửi Thông Báo Email Chưa Đọc Tóm Tắt AI tới Slack bằng GPT‑4o & Gmail"
description: "Tự động thu thập email chưa đọc, tóm tắt nội dung bằng GPT‑4o và gửi nhanh chóng tới kênh Slack, giúp các sếp luôn nắm bắt thông tin quan trọng mà không mất thời gian."
slug: "gui-thong-bao-email-chua-doc-voi-gpt4o-vao-slack"
tags: [n8n, automation, no-code, AI, Gmail, Slack, OpenAI]
keywords: [n8n workflow, tự động hóa email, GPT-4o, Slack notification, AI summarization]
---

# 🚀 Gửi Thông Báo Email Chưa Đọc Tóm Tắt AI tới Slack bằng GPT‑4o & Gmail

Bạn đã bao giờ phải mở hòm thư, lướt qua hàng chục (hoặc hàng trăm) email chưa đọc, rồi mới kịp nhận ra có một tin quan trọng cần phản hồi ngay?  
Việc này không chỉ tốn thời gian mà còn dễ bỏ lỡ cơ hội hoặc gây trì hoãn trong quy trình làm việc.  

**Workflow này** sẽ tự động:
1. Kiểm tra Gmail mỗi vài phút để phát hiện email chưa đọc.  
2. Lấy nội dung email, đưa vào GPT‑4o‑mini để tóm tắt ngắn gọn (khoảng 250 ký tự).  
3. Gửi bản tóm tắt ngay vào kênh Slack mà bạn chỉ định.  

Kết quả: Các sếp luôn nhận được **thông báo nhanh, chính xác và có nội dung tóm tắt** mà không cần mở email thủ công.

:::info[Gợi ý hạ tầng cho n8n]  
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]  
- **Tiết kiệm thời gian:** Không cần mở Gmail để lọc email quan trọng.  
- **Độ chính xác cao:** Tóm tắt do GPT‑4o‑mini tạo, giảm rủi ro bỏ sót thông tin.  
- **Cá nhân hoá:** Thông báo được gửi ngay vào kênh Slack mà các sếp thường xuyên theo dõi.  
- **Hoạt động liên tục:** Workflow chạy tự động 24/7, luôn cập nhật email mới.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]  
- **Tài khoản Gmail** (có quyền truy cập API).  
- **Tài khoản Slack** và **Webhook/Token** cho kênh muốn nhận thông báo.  
- **API Key OpenAI** (để sử dụng GPT‑4o‑mini).  
- **n8n** đã cài đặt và có quyền **Connect Credentials** cho ba dịch vụ trên.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n Editor.  
2. Click **Import** → **From File** và tải file JSON của workflow (hoặc **Copy/Paste** JSON vào ô nhập).  
3. Nhấn **Import**, workflow sẽ xuất hiện trên canvas.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Hành động cần cấu hình | Ghi chú |
|------|------------------------|---------|
| **Trigger on Unread Email** (gmailTrigger) | - Chọn **Credential** Gmail đã kết nối.<br>- Đặt **Label** (nếu muốn) và **Polling Frequency** (mặc định 5 phút). | Bạn có thể giảm/ tăng tần suất tùy nhu cầu. |
| **Get Email** (gmail) | - Operation: **Get** (đã mặc định).<br>- **Message ID**: lấy từ `Trigger on Unread Email` → `{{$json["id"]}}`. | Đảm bảo truyền đúng ID để lấy nội dung email. |
| **AI Agent** (agent) | - **Prompt**: `"Summarize the following email in 250 characters, highlight any action items and urgency."` (có thể tùy chỉnh).<br>- **Input**: nội dung email (`{{$node["Get Email"].json["body"]}}`). | Thay đổi prompt để điều chỉnh phong cách tóm tắt. |
| **OpenAI Chat Model** (lmChatOpenAi) | - Chọn **Credential** OpenAI.<br>- Model: **gpt-4o-mini** (đã được chọn).<br>- **Temperature**: 0.7 (hoặc tùy chỉnh). | Đảm bảo model và key đúng. |
| **Structured Output Parser** (outputParserStructured) | - **Schema**: `{ "summary": "string" }` (được tạo tự động).<br>- **Input**: kết quả từ **AI Agent**. | Parser sẽ trích xuất trường `summary` để gửi Slack. |
| **Send Notification to Slack** (slack) | - Chọn **Credential** Slack.<br>- **Channel**: nhập ID hoặc tên kênh (ví dụ: `#general`).<br>- **Message Text**: `"📬 *New Unread Email* \n*From:* {{$json["from"]}}\n*Subject:* {{$json["subject"]}}\n*Summary:* {{$node["Structured Output Parser"].json["summary"]}}"`. | Có thể thêm emoji, prefix hoặc routing dựa trên người gửi. |

> **⚠️ Lưu ý:** Đừng quên bật **“Connect Credentials First”** (xem note trên canvas) để các node có thể truy cập Gmail, Slack và OpenAI.

#### 3. Kích hoạt ⚡️
1. Nhấn **Execute Workflow** lần đầu để kiểm tra với email chưa đọc mẫu.  
2. Kiểm tra Slack: bạn sẽ nhận được tin nhắn tóm tắt.  
3. Nếu mọi thứ ổn, bật **Active** (nút chuyển đổi ở góc trên bên phải) để workflow chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp Telegram:** Thêm node Telegram để gửi bản sao tin nhắn tới nhóm Telegram.  
- **Lưu log vào Google Sheets:** Dùng node Google Sheets để ghi lại ngày‑giờ, người gửi, tiêu đề và bản tóm tắt, tiện cho báo cáo định kỳ.  
- **Báo cáo hàng ngày:** Sử dụng node **Cron** + **Slack** để gửi tổng hợp các email đã tóm tắt trong ngày.  
- **Tùy chỉnh độ dài:** Thay đổi `250 characters` trong prompt nếu muốn bản tóm tắt chi tiết hơn hoặc ngắn gọn hơn.

### 📌 Kết luận
Với workflow này, các sếp sẽ **không còn phải mở Gmail để dò tìm email quan trọng** nữa – mọi thông tin đã được tóm tắt nhanh gọn và đẩy thẳng vào Slack, giúp quyết định nhanh hơn, công việc suôn sẻ hơn. Hãy triển khai ngay, trải nghiệm tự động hoá thông minh và tập trung vào những việc thực sự quan trọng! 🚀