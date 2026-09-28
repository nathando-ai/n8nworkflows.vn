---
title: "🚀 Gửi Nhắc Nhở Follow‑up Ưu Tiên AI với GPT‑4.1‑mini, Gmail & Slack"
description: "Tự động phân loại độ khẩn cấp của công việc, gửi email, Slack, SMS và tổng hợp báo cáo hằng ngày chỉ bằng một workflow n8n."
slug: "gui-nhac-nho-followup-uu-tien-ai-gmail-slack"
tags: [n8n, automation, no-code, personal-productivity, ai, gmail, slack]
keywords: [n8n workflow, tự động hóa, GPT-4, Gmail, Slack, reminder]
---

# 🚀 Gửi Nhắc Nhở Follow‑up Ưu Tiên AI với GPT‑4.1‑mini, Gmail & Slack

Bạn đã bao giờ phải lướt qua hàng chục dòng email, tin nhắn Slack, hay bảng tính Google Sheets chỉ để tìm ra những công việc cần follow‑up gấp?  
Việc làm thủ công này không chỉ tốn thời gian mà còn dễ bỏ sót, ảnh hưởng tới năng suất và mối quan hệ với khách hàng.

**Workflow này** sẽ tự động:

1. **Nhận** mỗi khi có task mới được ghi vào Google Sheets.  
2. **Phân loại** độ khẩn cấp bằng GPT‑4.1‑mini (high, medium, low).  
3. **Gửi** email, tin Slack, hoặc SMS (Twilio) tùy mức độ.  
4. **Ghi lại** trạng thái và **tổng hợp** báo cáo hằng ngày gửi vào kênh Slack.  

Kết quả: **100 % tự động**, không cần viết code, giảm lỗi và tiết kiệm hàng giờ mỗi tuần.

:::info[Gợi ý hạ tầng cho n8n]  
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]  
- **Tiết kiệm thời gian**: Không còn mở nhiều công cụ để kiểm tra task.  
- **Độ chính xác cao**: AI phân loại dựa trên nội dung, giảm rủi ro bỏ sót.  
- **Cá nhân hoá**: Gửi kênh Slack, email hoặc SMS phù hợp với mức độ ưu tiên.  
- **Hoạt động liên tục**: Workflow chạy 24/7, báo cáo hằng ngày tự động.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]  
- **Google Account** với quyền truy cập Google Sheets (đọc/ghi).  
- **OpenAI API Key** (để gọi GPT‑4.1‑mini).  
- **Gmail Account** (hoặc Gmail API credentials) để gửi email.  
- **Slack Workspace** + **Slack Bot Token** + **Channel ID** cho thông báo.  
- **Twilio Account** (SID, Auth Token, số điện thoại) nếu muốn gửi SMS VIP.  
- **n8n** đã cài đặt (đề nghị chạy trên VPS).  
:::

## 📋 Danh sách các node trong workflow

| # | Tên node | Loại |
|---|----------|------|
| 1 | New Task Entry Trigger | googleSheetsTrigger |
| 2 | Workflow Configuration | set |
| 3 | Normalize Task Data | set |
| 4 | Classify Follow‑up Urgency | agent |
| 5 | OpenAI Chat Model | lmChatOpenAi |
| 6 | Structured Output Parser | outputParserStructured |
| 7 | Route by Urgency | switch |
| 8 | Send High Urgency Email | gmail |
| 9 | Send High Urgency Slack Alert | slack |
|10 | Send Medium Urgency Email | gmail |
|11 | Add to Weekly Summary | set |
|12 | Send VIP SMS Reminder | twilio |
|13 | Log Follow‑up Status | googleSheets |
|14 | Daily Summary Schedule | scheduleTrigger |
|15 | Fetch Daily Follow‑ups | googleSheets |
|16 | Send Daily Summary to Slack | slack |
|17 | Error Handler Trigger | errorTrigger |
|18 | Alert Admin on Error | slack |

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. **Tải file JSON** của workflow (từ link gốc hoặc file đính kèm).  
2. Vào **n8n → Workflows → Import** → Chọn file JSON → **Import**.  
3. Hoặc **Copy/Paste** toàn bộ JSON vào **Editor → Import from Clipboard**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Cấu hình cần chỉnh | Ghi chú |
|------|-------------------|---------|
| **New Task Entry Trigger** | *Spreadsheet ID*, *Sheet Name*, *Range* | Đảm bảo sheet chứa cột: `Task`, `Due Date`, `Owner`, `Priority (optional)` |
| **Workflow Configuration** | Các biến môi trường: `OPENAI_API_KEY`, `SLACK_CHANNEL_ID`, `TWILIO_SID`, `TWILIO_AUTH_TOKEN` | Dùng **Credentials** → **Add New** → chọn loại tương ứng |
| **Classify Follow‑up Urgency (agent)** | Chọn **OpenAI Agent** → nhập **Prompt**: “Phân loại độ khẩn cấp của task dựa trên nội dung, trả về ‘high’, ‘medium’ hoặc ‘low’.” | Prompt có thể tùy chỉnh để phù hợp ngôn ngữ doanh nghiệp |
| **OpenAI Chat Model** | Model: `gpt-4.1-mini`, **API Key** | Đặt **Temperature** = 0.2 để giảm độ ngẫu nhiên |
| **Structured Output Parser** | Schema: `{ "urgency": "string" }` | Đảm bảo output luôn là `high`, `medium`, `low`. |
| **Route by Urgency (switch)** | Thiết lập 3 case: `high`, `medium`, `low` | Mỗi case dẫn tới node gửi tương ứng. |
| **Send High Urgency Email** | *From*, *To (Owner email)*, *Subject*, *HTML Body* | Nội dung email có thể chèn biến `{{ $json["Task"] }}`. |
| **Send High Urgency Slack Alert** | *Channel ID*, *Message* | Sử dụng **Blocks** để làm nổi bật task. |
| **Send Medium Urgency Email** | Tương tự node email high nhưng nội dung nhẹ hơn. |
| **Send VIP SMS Reminder** | *To (phone number)*, *Body* | Chỉ chạy khi `urgency = high` **và** `Owner` thuộc danh sách VIP (cấu hình trong **Workflow Configuration**). |
| **Log Follow‑up Status** | *Spreadsheet ID*, *Sheet Name* | Ghi lại `Task`, `Urgency`, `Sent At`, `Channel`. |
| **Daily Summary Schedule** | Cron: `0 9 * * 1-5` (9h sáng các ngày làm việc) | Điều chỉnh thời gian phù hợp. |
| **Fetch Daily Follow‑ups** | Truy vấn Google Sheets để lấy các task đã gửi trong ngày. |
| **Send Daily Summary to Slack** | *Channel ID*, *Message* | Tổng hợp số task high/medium, link tới sheet. |
| **Error Handler Trigger** | Không cần cấu hình, tự động kích hoạt khi có lỗi. |
| **Alert Admin on Error** | *Channel ID*, *Message* | Thông báo chi tiết lỗi để nhanh chóng xử lý. |

#### 3. Kích hoạt ⚡️
1. **Test run**: Nhập một task mẫu vào Google Sheet → Kiểm tra các node chạy đúng (email, Slack, SMS).  
2. Khi mọi thứ ổn, bật **Active** ở góc phải của workflow.  
3. Kiểm tra **Execution Log** để chắc chắn không có lỗi.

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp Zapier/Make**: Nếu muốn đồng bộ task từ Asana hoặc Trello, thêm webhook trước node `New Task Entry Trigger`.  
- **Lưu log chi tiết**: Dùng node **HTTP Request** để gửi log tới Elastic/Kibana hoặc Google Cloud Logging.  
- **Báo cáo tuần**: Thêm schedule `weekly` để tổng hợp số task high/medium trong tuần và gửi PDF qua Gmail.  
- **Phân quyền**: Sử dụng **n8n Access Control** để chỉ admin mới chỉnh sửa workflow, người dùng chỉ xem báo cáo.  

### 📌 Kết luận
Với workflow này, các sếp sẽ không còn lo lắng về việc quên follow‑up hay mất thời gian lọc email. AI sẽ tự động phân loại, gửi kênh phù hợp và cung cấp báo cáo hằng ngày, giúp tăng năng suất và duy trì mối quan hệ khách hàng chuyên nghiệp.  
**Hãy triển khai ngay** để trải nghiệm tự động hoá thông minh trong công việc hàng ngày!