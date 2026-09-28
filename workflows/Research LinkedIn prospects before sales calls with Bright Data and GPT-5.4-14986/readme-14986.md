---
title: "🚀 Tự Động Hoá Nghiên Cứu Tiềm Năng LinkedIn Trước Cuộc Gọi Bán Hàng - Sử Dụng Bright Data & GPT-5.4"
description: "Workflow tự động hóa nghiên cứu tiềm năng LinkedIn trước cuộc gọi bán hàng bằng cách scrape dữ liệu, phân tích AI và lọc kết quả dựa trên độ tin cậy và điểm sẵn sàng. Giúp các sếp tiết kiệm thời gian lên tới 80% trong quá trình chuẩn bị cuộc gọi, đồng thời tăng tỷ lệ thành công với thông tin cá nhân hóa và chính xác."
slug: "tu-dong-hoa-nghien-cuu-tien-nang-linkedin-gpt-5-4"
tags: [n8n, automation, lead-generation, ai-summarization, bright-data, gpt-5-4, google-sheets, gmail]
keywords: [tự động hóa bán hàng, nghiên cứu tiềm năng LinkedIn, GPT-5.4, Bright Data API, tự động hóa no-code, workflow n8n, tự động hóa cuộc gọi bán hàng]
---

# 🚀 **Tự Động Hoá Nghiên Cứu Tiềm Năng LinkedIn Trước Cuộc Gọi Bán Hàng - Sử Dụng Bright Data & GPT-5.4**

### **🔍 Nỗi Đau Của Các Sếp Trong Quá Trình Bán Hàng**
Các sếp bán hàng thường phải mất **từ 2-4 giờ mỗi tuần** để nghiên cứu hồ sơ LinkedIn của khách hàng tiềm năng trước mỗi cuộc gọi. Quá trình này bao gồm:
- **Scrape dữ liệu** từ LinkedIn (thường gặp vấn đề với API bị chặn).
- **Tóm tắt thông tin** về chuyên môn, kinh nghiệm và điểm mạnh/điểm yếu của khách hàng.
- **Đánh giá độ phù hợp** của khách hàng với sản phẩm/dịch vụ của doanh nghiệp.
- **Chuẩn bị briefing** cho cuộc gọi, bao gồm các điểm nhấn quan trọng và câu hỏi phù hợp.

Kết quả? **Thời gian bị lãng phí, thông tin không đầy đủ hoặc không chính xác**, dẫn đến tỷ lệ thành công của cuộc gọi thấp hơn so với tiềm năng thực sự.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
Với workflow này, các sếp sẽ:
✅ **Tiết kiệm 80% thời gian** nghiên cứu trước cuộc gọi (từ 2-4 giờ xuống còn 5-10 phút).
✅ **Nhận thông tin cá nhân hóa** về khách hàng, bao gồm:
   - **Độ tin cậy** của dữ liệu (đánh giá từ AI).
   - **Điểm sẵn sàng** (Readiness Score) để đánh giá khả năng mua hàng.
   - **Các điểm nhấn** quan trọng để bắt đầu cuộc gọi hiệu quả.
✅ **Tự động lọc khách hàng** dựa trên tiêu chí độ tin cậy (Confidence ≥ 0.7) và điểm sẵn sàng (Readiness ≥ 70).
✅ **Nhận cảnh báo email tự động** cho các briefing cao độ tin cậy, giúp không bỏ lỡ cơ hội.
✅ **Lưu trữ tất cả dữ liệu** trong Google Sheets để theo dõi và phân tích sau này.

---
### **🔧 Yêu Cầu Cần Thiết**
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Bright Data** (để scrape LinkedIn):
   - API Key (Bearer Token) để kết nối với Bright Data.
   - [Đăng ký tài khoản Bright Data](https://brightdata.com/) (mã giảm giá: **BRIGHTDATA** - giảm 10%).
2. **Tài khoản OpenAI** (để sử dụng GPT-5.4):
   - API Key từ [OpenAI](https://platform.openai.com/).
3. **Google Sheets** (để lưu danh sách URL và kết quả):
   - Một bảng Google Sheets với **tab "upcoming_calls"** và cột **"url"** (để nhập danh sách LinkedIn).
   - [Hướng dẫn kết nối Google Sheets với n8n](https://docs.n8n.io/integrations/built-in/nodes/n8n-nodes-base.googleSheets.html).
4. **Tài khoản Gmail** (để gửi cảnh báo email):
   - [Cấu hình OAuth cho Gmail](https://docs.n8n.io/integrations/built-in/nodes/n8n-nodes-base.gmail.html).
5. **VPS Self-hosted n8n** (để workflow chạy 24/7):
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).

---
### **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải workflow từ n8n.io**:
  - Truy cập [link workflow gốc](https://n8n.io/workflows/14986) và nhấn **"Import"** (hoặc tải file JSON).
- **Hoặc import từ file JSON**:
  - Tải file JSON từ [đây](https://n8n.io/workflows/14986/download) và nhấn **"Import"** trong n8n Editor.
- **Hoặc copy/paste JSON**:
  - Mở n8n Editor → **"Import"** → **"Paste JSON"** và dán nội dung từ file JSON.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Sau khi import, các sếp cần **cấu hình chi tiết** các node quan trọng như sau:

##### **A. Node "Daily Prospect Research" (ScheduleTrigger)**
- **Cấu hình lịch chạy**:
  - Chọn **"Daily"** và thời gian phù hợp (ví dụ: 8h sáng để có đủ thời gian phân tích).
  - **Lưu ý**: Nếu chạy trên VPS, đảm bảo thời gian đồng bộ với giờ Việt Nam.

##### **B. Node "Read Upcoming Calls Sheet" (GoogleSheets)**
- **Chọn credentials**:
  - Chọn tài khoản Google đã kết nối với n8n.
- **Cấu hình sheet**:
  - **Sheet Name**: `"upcoming_calls"` (phải trùng với tab trong Google Sheets).
  - **Range**: `"url!A:A"` (cột chứa danh sách URL LinkedIn).
  - **Lưu ý**: Đảm bảo cột **"url"** không có tiêu đề (hoặc chọn **"Header"** nếu có).

##### **C. Node "Scrape LinkedIn Profile" (HTTPRequest)**
- **Thêm Header Auth**:
  - Trong **"Headers"**, thêm:
    ```
    Authorization: Bearer {BRIGHT_DATA_API_KEY}
    ```
  - Thay `{BRIGHT_DATA_API_KEY}` bằng API Key của Bright Data.
- **URL Template**:
  - Sử dụng template:
    ```
    https://linkedin-scraper-api.brightdata.com/v1/scrape?url={{$json["url"]}}
    ```
  - **Lưu ý**: Bright Data có giới hạn request, nên không nên scrape quá 100 URL/ngày (tránh bị block).

##### **D. Node "GPT-5.4 Model" (lmChatOpenAi)**
- **Thêm API Key**:
  - Trong **"Credentials"**, chọn tài khoản OpenAI đã kết nối.
- **Cấu hình Prompt**:
  - Prompt mặc định đã được tối ưu hóa để phân tích hồ sơ LinkedIn. **Không cần chỉnh sửa** trừ khi muốn thay đổi logic phân tích.
- **Model**: Đảm bảo chọn **"gpt-5.4"** (hoặc model tương đương nếu không có).

##### **E. Node "IF Confidence >= 0.7" & "IF Readiness Score >= 70" (If)**
- **Không cần chỉnh sửa** logic mặc định, vì nó đã được tối ưu hóa để:
  - **Lọc kết quả có độ tin cậy cao** (Confidence ≥ 0.7).
  - **Chỉ gửi briefing cho khách hàng có Readiness ≥ 70**.

##### **F. Node "Email Full Brief" & "Email Short Brief" (Gmail)**
- **Chọn credentials**:
  - Chọn tài khoản Gmail đã kết nối.
- **Cấu hình email**:
  - **Subject**: Đã được tự động hóa (ví dụ: *"Briefing cho cuộc gọi với [Tên Khách Hàng]"*).
  - **Body**: Sử dụng template mặc định (có thể chỉnh sửa để thêm logo hoặc thông tin doanh nghiệp).

##### **G. Node "Append Call Briefs" (GoogleSheets)**
- **Chọn sheet đích**:
  - **Sheet Name**: `"call_briefs"` (phải tạo trước trong Google Sheets).
  - **Range**: `"A1"` (nơi dữ liệu sẽ được append).
  - **Lưu ý**: Đảm bảo sheet này có **các cột phù hợp** (ví dụ: `url`, `name`, `confidence`, `readiness`, `briefing`).

---
#### **3. Kích Hoạt ⚡️**
1. **Test Run với dữ liệu mẫu**:
   - Thêm **1-2 URL LinkedIn** vào cột `"url"` trong sheet `"upcoming_calls"`.
   - Chạy **"Test"** trong n8n Editor để kiểm tra workflow.
   - Kiểm tra:
     - Dữ liệu scrape có chính xác không?
     - AI phân tích có logic hợp lý không?
     - Email briefing có được gửi không?
2. **Bật Active**:
   - Sau khi test thành công, chuyển **"Active"** sang **"ON"**.

---
### **✍️ Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram Bot** để nhận cảnh báo tức thời khi có briefing mới.
   - **Cách làm**:
     - Sử dụng node **HTTPRequest** để gửi thông báo đến Slack/Telegram.
     - Ví dụ: `https://api.slack.com/messaging/composing` (Slack) hoặc `https://api.telegram.org/bot<BOT_TOKEN>/sendMessage` (Telegram).

2. **Lưu Log Dữ Liệu**:
   - Thêm node **Google Sheets** hoặc **Airtable** để lưu **tất cả log hoạt động** (bao gồm lỗi, thành công, thời gian chạy).
   - **Lợi ích**: Theo dõi hiệu suất và phát hiện vấn đề nhanh chóng.

3. **Tự Động Cập Nhật Sheet "upcoming_calls"**:
   - Sử dụng **Google Apps Script** để tự động thêm URL mới từ một nguồn khác (ví dụ: CRM như HubSpot, Salesforce).
   - **Cách làm**:
     - Tạo một script Google Apps Script để lấy dữ liệu từ CRM và append vào sheet `"upcoming_calls"`.

4. **Tối Ưu Hóa Chi Phí**:
   - **Bright Data**: Sử dụng **Proxy Residential** để giảm nguy cơ bị block.
   - **OpenAI**: Nếu chi phí GPT-5.4 cao, thử **GPT-4** hoặc **GPT-3.5** với prompt được tối ưu hóa.
   - **Lưu ý**: Chi phí ước tính:
     - **Bright Data**: ~$0.01-0.03/URL.
     - **GPT-5.4**: ~$0.005/phân tích.

5. **Tạo Báo Cáo Định Kỳ**:
   - Sử dụng **Google Data Studio** hoặc **Power BI** để tạo báo cáo về:
     - Số lượng briefing được tạo.
     - Độ tin cậy trung bình.
     - Tỷ lệ thành công của cuộc gọi (nếu có dữ liệu theo dõi).

---
### **📌 Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp bán hàng muốn **tự động hóa 100% quá trình nghiên cứu tiềm năng LinkedIn** trước cuộc gọi. Với **AI phân tích GPT-5.4** và **lọc tự động dựa trên độ tin cậy**, các sếp sẽ:
✔ **Tiết kiệm thời gian** để tập trung vào cuộc gọi thực sự.
✔ **Tăng tỷ lệ thành công** nhờ thông tin cá nhân hóa và chính xác.
✔ **Hoạt động 24/7** mà không cần can thiệp thủ công.

**🚀 Hành động ngay!**
1. **Chuẩn bị tài khoản** (Bright Data, OpenAI, Google Sheets, Gmail).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Test và bật Active** để bắt đầu tự động hóa ngay hôm nay!

---
**🔗 Tài Liệu Tham Khảo**:
- [Workflow gốc trên n8n.io](https://n8n.io/workflows/14986)
- [Hướng dẫn Bright Data API](https://brightdata.com/docs/scraping-api)
- [Hướng dẫn OpenAI API](https://platform.openai.com/docs/api-reference)
- [Hướng dẫn Google Sheets n8n](https://docs.n8n.io/integrations/built-in/nodes/n8n-nodes-base.googleSheets.html)

---
**💬 Có thắc mắc?**
- **Yaron Been** (tác giả workflow) chia sẻ trên LinkedIn: [@YaronBeen](https://www.linkedin.com/in/yaronbeen/).
- **Cộng đồng n8n Việt Nam**: [Facebook Group](https://www.facebook.com/groups/n8nvietnam/) | [Discord](https://discord.gg/n8n).