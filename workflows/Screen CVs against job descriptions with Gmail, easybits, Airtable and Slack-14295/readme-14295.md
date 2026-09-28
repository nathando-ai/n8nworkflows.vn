---
title: "🚀 Tự động sàng lọc CV với Gmail, Easybits, Airtable & Slack"
description: "Workflow n8n tự động so sánh CV với mô tả công việc, lưu trữ trên Airtable và gửi báo cáo qua Slack, giảm tới 80% thời gian tuyển dụng."
slug: "tu-dong-sang-loc-cv-gmail-easybits-airtable-slack"
tags: [n8n, automation, no-code, HR, AI]
keywords: [n8n workflow, tự động hóa tuyển dụng, sàng lọc CV, AI summarization, Airtable, Slack]
---

# 🚀 Tự động sàng lọc CV với Gmail, Easybits, Airtable & Slack

Bạn đã từng phải **đọc hàng chục, hàng trăm CV** trong hộp thư Gmail, rồi mới biết chúng có phù hợp hay không?  
Việc này không chỉ tốn thời gian mà còn dễ bỏ sót những tài năng tiềm năng.  

**Workflow này** sẽ tự động:

1. **Nhận CV** mới gửi tới Gmail.  
2. **Gửi nội dung CV** và mô tả công việc tới **Easybits AI** để phân tích và tính điểm phù hợp.  
3. **Lưu trữ** CV, kết quả đánh giá và trạng thái vào **Airtable**.  
4. **Thông báo** ngay trên **Slack** cho đội tuyển dụng biết ai là ứng viên “đáng chú ý”.  

Kết quả? **Tiết kiệm 80% thời gian** sàng lọc, giảm lỗi nhập liệu và luôn có dữ liệu cập nhật 24/7.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động xử lý CV ngay khi nhận được, không cần mở Gmail thủ công.  
- **Độ chính xác cao**: AI đánh giá dựa trên từ khóa và kỹ năng, giảm sai sót con người.  
- **Báo cáo tức thời**: Slack thông báo ngay, đội tuyển dụng có thể phản hồi ngay lập tức.  
- **Lưu trữ có hệ thống**: Airtable cung cấp view, filter, và báo cáo tùy chỉnh.  
- **Hoạt động 24/7**: Không cần nhân viên giám sát liên tục.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản Gmail** (được bật **Gmail API** và tạo **OAuth2 credentials**).  
- **API Key của Easybits** (hoặc bất kỳ dịch vụ AI summarization nào bạn dùng).  
- **Tài khoản Airtable** + **Base** với các bảng: `CVs`, `JobDescriptions`, `Results`.  
- **Workspace Slack** + **Incoming Webhook URL** hoặc **Slack Bot Token**.  
- **n8n** (cài đặt trên VPS hoặc Docker) với các credentials đã tạo ở trên.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập **n8n → Workflows → Import**.  
2. Tải file JSON từ link gốc: <https://n8n.io/workflows/14295> (hoặc nhấn **Export** → **Download JSON** từ giao diện n8n nếu bạn đã sao chép).  
3. Chọn **Import** và đặt tên cho workflow (mặc định: *Screen CVs against job descriptions*).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Mô tả | Cấu hình cần chỉnh |
|------|------|--------------------|
| **Gmail Trigger** | Lắng nghe email mới trong hộp thư Gmail. | - Chọn **Credential** (OAuth2 Gmail). <br> - Filter: `subject` chứa “CV” hoặc `to` là địa chỉ tuyển dụng. |
| **HTTP Request (Easybits)** | Gửi nội dung CV + mô tả công việc tới API AI. | - Method: `POST` <br> - URL: `https://api.easybits.ai/v1/summarize` <br> - Header: `Authorization: Bearer <API_KEY>` <br> - Body (JSON): `{ "cv": {{$json["body"]}}, "jobDescription": {{$node["Airtable – JobDesc"].json["description"]}} }` |
| **Code** (JavaScript) | Tính điểm phù hợp dựa trên kết quả AI. | - Sử dụng `items[0].json` để lấy `score` từ Easybits, sau đó đưa ra `match = score > 70 ? "YES" : "NO"`. |
| **IF** | Kiểm tra xem CV có đạt ngưỡng không. | - Condition: `{{$json["match"]}} === "YES"` |
| **Airtable** (Create/Update) | Lưu CV, điểm AI và trạng thái vào bảng `Results`. | - Chọn **Credential** Airtable. <br> - Base ID, Table Name (`Results`). <br> - Mapping: `CV URL`, `Score`, `Match`, `Timestamp`. |
| **Slack** | Gửi thông báo tới kênh tuyển dụng. | - Chọn **Credential** Slack (Webhook hoặc Bot Token). <br> - Channel: `#recruitment`. <br> - Message: `*New CV matched!* \n• Candidate: {{$json["candidateName"]}} \n• Score: {{$json["score"]}}%` |
| **Sticky Note** (optional) | Ghi chú mô tả luồng cho người dùng. | Không cần cấu hình, chỉ để tham khảo. |

> **Lưu ý:** Mỗi node **Credential** phải được tạo trước trong **n8n → Credentials**. Đừng quên bật **OAuth consent screen** cho Gmail và cấp quyền `https://www.googleapis.com/auth/gmail.readonly`.

#### 3. Kích hoạt ⚡️
1. **Test run**: Gửi một email thử nghiệm (đính kèm CV) tới Gmail đã cấu hình. Kiểm tra log của mỗi node để chắc chắn dữ liệu truyền đúng.  
2. Khi mọi thứ ổn, bật **Active** ở góc phải của workflow.  
3. Kiểm tra Slack: bạn sẽ nhận được tin nhắn “New CV matched!” nếu điểm AI vượt ngưỡng.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm Telegram**: Dùng node **Telegram** để gửi thông báo tới nhóm tuyển dụng trên Telegram.  
- **Lưu log chi tiết**: Kết nối **Google Sheets** hoặc **MongoDB** để lưu toàn bộ log raw của Easybits, tiện cho audit.  
- **Báo cáo định kỳ**: Dùng node **Cron** + **Airtable → Get All** → **Slack** để gửi báo cáo tổng hợp mỗi tuần.  
- **Tự động trả lời**: Thêm node **Gmail → Send Email** để gửi email cảm ơn tự động tới ứng viên không phù hợp.  

### 📌 Kết luận
Với workflow này, các sếp sẽ **không còn phải mở Gmail từng email một**, mà mọi CV đều được **đánh giá, lưu trữ và thông báo tự động**. Hãy triển khai ngay, giảm tải công việc HR và tập trung vào việc phỏng vấn những tài năng thực sự phù hợp! 🚀