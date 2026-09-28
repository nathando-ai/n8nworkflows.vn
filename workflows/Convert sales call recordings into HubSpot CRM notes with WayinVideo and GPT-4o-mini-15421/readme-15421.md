---
title: "🤖 Tự Động Chuyển Góp Ý Cuộc Gọi Bán Hàng Sang Ghi Chú HubSpot Với WayinVideo + GPT-4o-mini (Không Cần Code)"
description: "Giải pháp tự động hóa hoàn toàn cho các đội bán hàng tự động hóa ghi chú CRM từ cuộc gọi Zoom/Teams/Meet sang HubSpot với AI tóm tắt thông minh, tiết kiệm 10+ giờ/tháng cho các sếp."
slug: "tieu-dong-hoa-chuyen-gop-y-cuoc-ghi-ban-hang-sang-ghi-chu-hubspot"
tags: [n8n, automation, crm, ai-summarization, hubspot, wayinvideo, gpt-4o-mini]
keywords: [tự động hóa bán hàng, ghi chú hubspot tự động, wayinvideo n8n, gpt-4o-mini cho crm, tự động hóa cuộc gọi zoom, ai tóm tắt cuộc gọi]
---

# 🚀 **Tự Động Chuyển Góp Ý Cuộc Gọi Bán Hàng Sang HubSpot Với AI (Không Cần Code)**

### **Nỗi Đau Của Các Sếp Bán Hàng**
Các sếp bán hàng và quản lý CRM thường phải:
- **Ghi chép thủ công** tất cả ghi chú sau mỗi cuộc gọi (tốn 10-15 phút/cuộc gọi).
- **Mất thời gian** tìm kiếm thông tin quan trọng trong cuộc gọi (điểm yếu, lời khuyên, kế hoạch tiếp theo).
- **Không có hệ thống** để đánh giá cảm xúc khách hàng hoặc đánh giá giai đoạn giao dịch.
- **Lặp lại công việc** khi phải nhập liệu vào HubSpot sau khi gọi.

**Giải pháp này tự động hóa toàn bộ quy trình** bằng cách:
✅ **Chuyển tự động** ghi chú cuộc gọi từ Zoom/Teams/Meet sang HubSpot.
✅ **Tóm tắt thông minh** với GPT-4o-mini, trích xuất **9 trường dữ liệu quan trọng** (tóm tắt cuộc gọi, điểm yếu, kế hoạch tiếp theo, cảm xúc, giai đoạn giao dịch...).
✅ **Tạo ghi chú và nhiệm vụ** tự động trên HubSpot, đồng thời **ghi log chi tiết** vào Google Sheets.
✅ **Hoạt động 24/7** mà không cần can thiệp của con người.

---

## 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tháng** cho đội bán hàng (không phải ghi chép thủ công).
- **Chính xác 100%** với AI tóm tắt thông minh, không bỏ sót chi tiết.
- **Cá nhân hóa ghi chú** cho từng khách hàng với cảm xúc và giai đoạn giao dịch.
- **Hoạt động liên tục** (24/7) ngay cả khi các sếp nghỉ ngơi.
- **Dữ liệu thống kê** được lưu vào Google Sheets để phân tích sau này.
- **Tạo nhiệm vụ tự động** trên HubSpot để không quên kế hoạch tiếp theo.
:::

---

## 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản WayinVideo** (để transcribe cuộc gọi):
   - [Đăng ký WayinVideo](https://wayin.video/) (miễn phí cho 100 phút/tháng).
   - **API Key** từ Dashboard → API Keys.
2. **Tài khoản OpenAI** (để sử dụng GPT-4o-mini):
   - [Đăng ký OpenAI](https://platform.openai.com/) (cần thẻ tín dụng).
   - **API Key** từ Dashboard → API Keys.
3. **Tài khoản HubSpot** (để tạo ghi chú và nhiệm vụ):
   - [Đăng ký HubSpot](https://app.hubspot.com/) (miễn phí cho 1000 liên hệ).
   - **Private App Token** (tạo tại: **Settings → Integrations → Private Apps**).
   - **Scopes cần thiết**:
     - `crm.objects.contacts.read`
     - `crm.objects.contacts.write`
     - `crm.objects.notes.write`
     - `crm.objects.tasks.write`
4. **Tài khoản Google Sheets** (để lưu log):
   - [Đăng ký Google Workspace](https://workspace.google.com/) (nếu chưa có).
   - **OAuth2 Credential** trong n8n (cài đặt tại: **Credentials → Add → Google Sheets**).
   - **ID Sheet** của bảng tính (định dạng: `1AbCdEfGhIjKlMnOpQrStUvWxYz`).
5. **Bảng tính Google Sheets** với tab tên **"CRM Call Log"** và các cột sau:
   | Cột Tên                          | Loại Dữ liệu |
   |-----------------------------------|--------------|
   | Contact Email                     | Text         |
   | Contact Name                      | Text         |
   | Company Name                      | Text         |
   | Call Purpose                      | Text         |
   | Call Date                         | Date         |
   | Sales Rep                         | Text         |
   | Call Duration (min)               | Number       |
   | HubSpot Contact ID                | Text         |
   | HubSpot Note ID                   | Text         |
   | HubSpot Task ID                   | Text         |
   | Deal Stage                        | Text         |
   | Sentiment                         | Text         |
   | Confidence Score                  | Number       |
   | Follow-up Date                    | Date         |
   | Recording URL                     | Text         |
   | Created On                        | DateTime     |

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. **Tải file JSON** từ [link gốc](https://n8n.io/workflows/15421).
2. Trong **n8n Editor**, nhấn **Import Workflow** và chọn file JSON.
   **Hoặc**:
   - Copy toàn bộ JSON từ file và dán vào **Import Workflow** trong n8n.

:::note[LƯU Ý]
- **Không chạy workflow ngay** sau khi import, vì cần cấu hình các node quan trọng.
- **Không xóa node nào** trong workflow, chỉ chỉnh sửa thông tin cần thiết.
:::

---

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**

#### **🔹 Node 2 & 4: WayinVideo — Submit & Get Transcript**
- **Thay thế `YOUR_WAYINVIDEO_API_KEY`** bằng API Key của WayinVideo (từ Dashboard → API Keys).
- **URL API**:
  - **Submit Transcription**: `https://api.wayin.video/v1/transcription`
  - **Get Transcript Results**: `https://api.wayin.video/v1/transcription/{taskId}`

#### **🔹 Node 9: OpenAI — GPT-4o-mini Model**
- **Kết nối credential OpenAI**:
  1. Trong n8n, đi đến **Credentials → Add → OpenAI**.
  2. Nhập **API Key** từ OpenAI.
  3. Chọn **model = gpt-4o-mini** (đã được cấu hình sẵn trong workflow).

#### **🔹 Node 11, 13, 14: HTTP — HubSpot API**
- **Thay thế `YOUR_HUBSPOT_PRIVATE_APP_TOKEN`** bằng **Private App Token** từ HubSpot.
- **URL API**:
  - **Search Contact**: `https://api.hubapi.com/crm/v3/objects/contacts/search`
  - **Create Note**: `https://api.hubapi.com/crm/v3/objects/notes`
  - **Create Task**: `https://api.hubapi.com/crm/v3/objects/tasks`
- **Headers cần thiết**:
  ```json
  {
    "Authorization": "Bearer YOUR_HUBSPOT_PRIVATE_APP_TOKEN",
    "Content-Type": "application/json"
  }
  ```

#### **🔹 Node 15: Google Sheets — Log CRM Entry**
- **Kết nối credential Google Sheets**:
  1. Trong n8n, đi đến **Credentials → Add → Google Sheets**.
  2. Nhập **OAuth2 Client ID** và **Client Secret** từ Google Cloud Console.
  3. **Thay thế `YOUR_GOOGLE_SHEET_ID`** bằng ID của bảng tính (định dạng: `1AbCdEfGhIjKlMnOpQrStUvWxYz`).
  4. **Chọn tab "CRM Call Log"** trong Google Sheets.

#### **🔹 Node 7 & 10: Code — Format & Parse CRM Output**
- **Không cần chỉnh sửa** nếu các sếp đã cấu hình các node khác đúng.
- **Node 7** định dạng transcript với speaker labels và timestamps.
- **Node 10** trích xuất 9 trường dữ liệu từ AI và xây dựng nội dung ghi chú HubSpot.

---

### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run với dữ liệu mẫu**:
   - Nhập một **URL cuộc gọi** (Zoom/Teams/Meet) vào form.
   - Kiểm tra các node:
     - **WayinVideo** có transcribe thành công không?
     - **GPT-4o-mini** có trích xuất 9 trường dữ liệu không?
     - **HubSpot** có tạo ghi chú và nhiệm vụ không?
     - **Google Sheets** có ghi log không?
2. **Bật Active workflow**:
   - Sau khi test thành công, chuyển workflow từ **Inactive → Active**.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[CÁCH TIẾP CẬN THÊM]
1. **Gửi thông báo Slack/Telegram khi hoàn thành**:
   - Thêm **Node Slack/Telegram** sau node **15 (Google Sheets)** để thông báo khi ghi chú được tạo.
   - **Cấu hình**:
     ```json
     {
       "text": `📝 Ghi chú cuộc gọi cho {{$node["15"].json["Contact Name"]}} đã được tạo thành công!\n📅 Ngày gọi: {{$node["1"].json["Call Date"]}}\n🔗 Link cuộc gọi: {{$node["1"].json["Recording URL"]}}`
     }
     ```
2. **Lưu log vào Google Drive**:
   - Thay vì Google Sheets, các sếp có thể lưu file Excel/PDF vào Google Drive.
   - **Cách làm**:
     - Thêm **Node Google Drive** sau node **15**.
     - Cấu hình để tạo file mới với tên `CRM_Log_{{$node["1"].json["Call Date"]}}.xlsx`.
3. **Tự động gửi email báo cáo hàng tuần**:
   - Sử dụng **Node Email** (Gmail/SMTP) để gửi báo cáo tổng hợp từ Google Sheets.
   - **Cấu hình**:
     - **Subject**: `Báo cáo cuộc gọi bán hàng tuần (Từ {{startDate}} đến {{endDate}})`
     - **Nội dung**: Trích xuất dữ liệu từ Google Sheets (đối tượng, giai đoạn giao dịch, cảm xúc...).
4. **Kết hợp với Zoom API**:
   - Nếu các sếp sử dụng **Zoom**, có thể tự động lấy danh sách cuộc gọi mới từ Zoom và gửi vào form.
   - **Cách làm**:
     - Thêm **Node Zoom API** trước node **1 (Form)**.
     - Lấy danh sách cuộc gọi mới và tự động nhập vào form.
5. **Cập nhật sentiment score**:
   - Sử dụng **Node LangChain** để phân tích cảm xúc chi tiết hơn (ví dụ: "vui", "bực bội", "lưỡng lự").
   - **Cách làm**:
     - Thêm **Node Agent** mới sau node **8** để phân tích sentiment sâu hơn.
     - Cấu hình prompt:
       ```json
       "prompt": "Analyze the following transcript and provide a detailed sentiment score (1-10) for each speaker segment. Include reasons for the score."
       ```

---

## 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp bán hàng, giúp họ tập trung vào **quan hệ khách hàng** thay vì **ghi chép thủ công**. Với **AI tóm tắt thông minh** và **tự động hóa hoàn toàn**, các sếp sẽ:
✔ **Tiết kiệm 10+ giờ/tháng**.
✔ **Không bỏ sót chi tiết** trong cuộc gọi.
✔ **Cải thiện chất lượng ghi chú** với cảm xúc và giai đoạn giao dịch.
✔ **Hoạt động 24/7** mà không cần can thiệp.

**Hành động ngay hôm nay!**
1. **Chuẩn bị các credential** (WayinVideo, OpenAI, HubSpot, Google Sheets).
2. **Import workflow** và cấu hình các node.
3. **Test với một cuộc gọi mẫu** và bật **Active workflow**.
4. **Tận hưởng sự tự động hóa hoàn toàn** cho đội bán hàng!

---
:::note[CHÚ Ý CUỐI CUNG]
- **Giám sát workflow** thường xuyên trong **n8n Dashboard** để phát hiện lỗi.
- **Cập nhật API Key** nếu hết hạn.
- **Mở rộng** với các tính năng nâng cao như Slack/Telegram notification hoặc báo cáo tự động.
:::

---
**🎁 Đăng ký VPS TinoHost để chạy n8n ổn định 24/7:**
👉 [VPS N8N - Giảm 39%](https://tino.vn/vps-n8n?affid=388) (Mã giảm giá: **VPSN8N**)
👉 [VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)