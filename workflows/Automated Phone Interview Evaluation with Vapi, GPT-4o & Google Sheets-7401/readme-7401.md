---
title: "🚀 Tự Động Đánh Giá Phỏng Vấn Điện Thoại với Vapi, GPT‑4o & Google Sheets"
description: "Giải pháp không code tự động thu thập, phân tích và lưu trữ kết quả phỏng vấn qua điện thoại, giúp HR tiết kiệm thời gian và tăng độ chính xác."
slug: "tu-dong-hoa-phong-van-dien-thoai-vapi-gpt4o-google-sheets"
tags: [n8n, automation, no-code, HR, AI, GoogleSheets]
keywords: [n8n workflow, tự động hóa phỏng vấn, Vapi, GPT‑4o, Google Sheets, AI evaluation]
---

# 🚀 Tự Động Đánh Giá Phỏng Vấn Điện Thoại với Vapi, GPT‑4o & Google Sheets

Bạn đã từng phải **nghe lại hàng chục bản ghi âm phỏng vấn**, ghi chú thủ công, rồi mới đưa ra quyết định tuyển dụng?  
Quá trình này không chỉ tốn thời gian mà còn dễ gây sai sót và thiếu tính nhất quán.  

**Workflow này** sẽ tự động nhận transcript từ Vapi.ai, dùng **GPT‑4o-mini** phân tích và đánh giá ứng viên dựa trên tiêu chí bạn định nghĩa, sau đó **lưu kết quả vào Google Sheets** để bạn và đội ngũ HR có thể xem ngay lập tức – **không cần viết một dòng code nào**.

:::info[Gợi ý hạ tầng cho n8n]  
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]  
- **Tiết kiệm 80% thời gian** so với việc nghe lại và ghi chú thủ công.  
- **Đánh giá nhất quán** nhờ AI phân tích dựa trên tiêu chí chuẩn hoá.  
- **Kết quả ngay lập tức** trong Google Sheets, dễ chia sẻ và báo cáo.  
- **Tích hợp liền mạch** với hệ thống gọi điện Vapi.ai và các công cụ HR khác.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]  
- **n8n Instance** (self‑hosted hoặc cloud).  
- **OpenAI API Key** (để sử dụng GPT‑4o‑mini).  
- **Google Account** và **Google Sheets OAuth2 credentials**.  
- **Vapi.ai (hoặc hệ thống gọi điện khác)** có khả năng gửi webhook POST tới n8n.  
- **Google Sheet** (có cấu trúc cột phù hợp – dùng mẫu có sẵn hoặc tự tạo).  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập **Workflows → Import from JSON** trong n8n.  
2. Dán **JSON** của workflow (bạn có thể tải từ trang gốc: https://n8n.io/workflows/7401).  
3. Nhấn **Import** và workflow sẽ xuất hiện trên canvas.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Công việc cần cấu hình | Hướng dẫn chi tiết |
|------|-----------------------|--------------------|
| **Webhook** | Đặt **Path** và **Method** | - Path đã được thiết lập sẵn: `351ffe7c-69f2-4657-b593-c848d59205c0` <br> - Method: `POST` <br> Sau import, n8n sẽ tạo URL dạng `https://<your-n8n-domain>/webhook/351ffe7c-69f2-4657-b593-c848d59205c0`. Cập nhật URL này trong **Vapi.ai** để gửi transcript. |
| **Edit Fields2** (Set) | Chuẩn hoá dữ liệu đầu vào | - Thêm/đổi tên các trường nếu Vapi gửi khác (ví dụ: `transcript`, `candidateId`). <br> - Đảm bảo output có các key: `transcript`, `candidateId`, `jobTitle` (hoặc tùy chỉnh). |
| **OpenAI Chat Model** & **OpenAI Chat Model2** | Chọn model & credentials | - Chọn **Credentials → OpenAI API** và dán **API Key** của bạn. <br> - Model: `gpt-4o-mini` (đã được set sẵn). <br> - Đối với Node thứ 2, mục đích là **tách câu trả lời thành JSON** – không cần thay đổi nếu bạn dùng tiêu chí mặc định. |
| **Structured Output Parser** | Định dạng JSON đầu ra | - Trong **Schema**, định nghĩa các trường bạn muốn nhận (ví dụ: `score`, `strengths`, `weaknesses`, `recommendation`). <br> - Sử dụng **JSON Schema** mẫu có trong tài liệu workflow hoặc tạo mới dựa trên tiêu chí HR của bạn. |
| **Evaluate Candidate** (Agent) | Thiết lập tiêu chí đánh giá | - Mở node, chỉnh **System Message** để đưa vào yêu cầu đánh giá (ví dụ: “Đánh giá ứng viên cho vị trí lái xe tại Massachusetts”). <br> - Cập nhật **Checklist** (các tiêu chí) phù hợp với công việc của bạn. |
| **Convert to JSON** (Agent) | Chuyển kết quả sang JSON chuẩn | - Thường không cần thay đổi, chỉ đảm bảo **Output Format** là `JSON`. |
| **Save to Google Sheets** | Kết nối Google Sheet & mapping cột | - Chọn **Credentials → Google Sheets OAuth2** và ủy quyền. <br> - Chọn **Spreadsheet ID** (URL của sheet). <br> - Chọn **Sheet Name** (mặc định `Sheet1`). <br> - Map các trường JSON (`candidateId`, `score`, `strengths`, …) tới các cột trong sheet. |
| **Sticky Note** (nếu có) | Ghi chú hướng dẫn nội bộ | - Bạn có thể để lại ghi chú cho các thành viên khác về cách cập nhật webhook URL hoặc thay đổi tiêu chí. |

#### 3. Kích hoạt ⚡️
1. **Test run**: Gửi một payload mẫu từ Vapi (hoặc dùng Postman) tới webhook URL. Kiểm tra log từng node, đặc biệt là output của **Structured Output Parser**.  
2. Nếu mọi thứ trả về **JSON hợp lệ**, mở **Toggle** “Active” ở góc trên bên phải để workflow chạy liên tục.  

### ✍️ Mẹo & gợi ý nâng cao
- **Kết nối Slack/Telegram**: Thêm node **Slack** hoặc **Telegram** sau node “Save to Google Sheets” để gửi thông báo ngay khi có ứng viên mới.  
- **Lưu log chi tiết**: Dùng node **Google Drive** hoặc **S3** để lưu bản transcript gốc và kết quả AI, phục vụ audit.  
- **Báo cáo định kỳ**: Thêm **Cron** node (hàng ngày/tuần) để tổng hợp dữ liệu từ Sheet và gửi báo cáo PDF qua email.  
- **Đa ngôn ngữ**: Thay model thành `gpt-4o` (phiên bản đầy đủ) và thêm **Prompt** để AI dịch và đánh giá ứng viên không nói tiếng Anh.  

### 📌 Kết luận
Với workflow **Automated Phone Interview Evaluation**, các sếp có thể **tự động hoá toàn bộ quy trình phỏng vấn điện thoại**, từ nhận transcript, phân tích AI, tới lưu trữ kết quả trong Google Sheets – giảm thiểu công sức, tăng độ chính xác và cho phép tập trung vào quyết định chiến lược.  
Hãy **import ngay**, cấu hình các credentials và bắt đầu trải nghiệm tự động hoá thông minh cho bộ phận HR của bạn! 🚀

---  

**Liên hệ hỗ trợ**  
📧 [robert@ynteractive.com](mailto:robert@ynteractive.com)  
🔗 [LinkedIn của Robert Breen](https://www.linkedin.com/in/robert-breen-29429625/)