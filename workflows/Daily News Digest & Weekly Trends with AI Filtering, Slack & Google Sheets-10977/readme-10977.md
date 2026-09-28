---
title: "📰 **Tự Động Hóa Báo Cáo Tin Tức Hàng Ngày & Báo Cáo Xu Hướng Tuần - Với AI Lọc Lọc & Slack**"
description: "Workflow tự động hóa lấy tin tức hàng ngày từ NewsAPI, lọc tin chất lượng bằng AI, tổng hợp vào Google Sheets và gửi báo cáo hàng ngày/tuần tới Slack (có dịch tiếng Nhật). Giúp các sếp tiết kiệm 10+ giờ/tháng theo dõi thị trường."
slug: "tieu-dong-hoa-bao-cao-tin-tuc-hang-ngay-va-tuan"
tags: [n8n, automation, ai-summarization, market-research, slack-integration, google-sheets, self-hosted]
keywords: [n8n workflow tin tức, tự động hóa báo cáo hàng ngày, ai lọc tin chất lượng, tổng hợp tin tức hàng tuần, slack + google sheets, openrouter ai]
---

# 🚀 **Tự Động Hóa Báo Cáo Tin Tức Hàng Ngày & Báo Cáo Xu Hướng Tuần - Với AI Lọc Lọc & Slack**

## **🔍 Nỗi Đau Của Các Sếp Hiện Nay**
Hàng ngày, các sếp phải:
- **Tìm kiếm và đọc** hàng chục bài tin từ nhiều nguồn khác nhau (TechCrunch, Bloomberg, Reuters...).
- **Lọc tin chất lượng** giữa những bài clickbait, tin cũ hoặc không liên quan.
- **Tổng hợp và gửi báo cáo** cho đội ngũ, mất thời gian và dễ bị bỏ sót.
- **Theo dõi xu hướng dài hạn** nhưng lại không có thời gian phân tích dữ liệu tích lũy.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Lấy tin tức** từ NewsAPI theo từ khóa của bạn (ví dụ: "Crypto", "AI", "SaaS").
✅ **Lọc tin chất lượng** bằng AI (OpenRouter) để loại bỏ tin clickbait.
✅ **Tổng hợp dữ liệu** vào Google Sheets với cấu trúc: **Tiêu đề, Tác giả, Tóm tắt, Link**.
✅ **Gửi báo cáo hàng ngày** tới Slack (có thể dịch sang tiếng Nhật bằng DeepL).
✅ **Tự động phân tích xu hướng tuần** vào thứ Hai sáng và gửi báo cáo chiến lược.

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm 10+ giờ/tháng** theo dõi tin tức thủ công.
- **Tin tức chất lượng cao** được AI lọc kỹ trước khi gửi.
- **Báo cáo tự động hóa** hàng ngày/tuần, không cần can thiệp.
- **Dữ liệu tích lũy** trong Google Sheets để phân tích dài hạn.
- **Cá nhân hóa** theo từ khóa và ngành nghề của bạn.
- **Dịch sang tiếng Nhật** (nếu cần) để chia sẻ với đội ngũ quốc tế.
:::

---
## **🔧 Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ TRƯỚC KHI LẮP ĐẶT**]
Để workflow hoạt động, các sếp cần chuẩn bị:
✔ **Tài khoản n8n** (Self-hosted hoặc Cloud - **khuyến nghị self-hosted** để ổn định 24/7).
✔ **API Key NewsAPI** (Free tier có giới hạn 100 request/ngày - [Đăng ký miễn phí](https://newsapi.org/)).
✔ **API Key OpenRouter** (hoặc OpenAI/GPT-4) - [Đăng ký OpenRouter](https://openrouter.ai/) (giá rẻ hơn OpenAI).
✔ **API Key DeepL** (để dịch tin tức sang tiếng Nhật - [Đăng ký DeepL](https://www.deepl.com/pro-api)).
✔ **Tài khoản Google Sheets** và một **bảng tính mới** với các cột: `title`, `author`, `summary`, `url`.
✔ **Slack Workspace** và **channel** để gửi báo cáo.
✔ **VPS** (nếu self-hosted) - **👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) với mã giảm giá **VPSN8N** (giảm 39%) hoặc [VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)**.
:::

---
## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/10977](https://n8n.io/workflows/10977).
2. **Nhấn vào "Export"** (icon ba chấm) và chọn **JSON**.
3. **Trên n8n Editor**, nhấn **"Import"** và dán JSON vào.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Mở n8n Editor** và tạo một **workflow mới**.
2. **Nhấn "Import"** và chọn **Paste JSON**.
3. **Dán toàn bộ mã JSON** từ [n8n.io/workflows/10977](https://n8n.io/workflows/10977) (có thể tải từ link trên).

---
### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này có **2 phần chính**:
- **Phần hàng ngày** (lấy tin, lọc AI, gửi Slack, lưu Sheets).
- **Phần tuần** (phân tích xu hướng từ dữ liệu tích lũy).

#### **🔹 Cấu Hình Credentials (Bắt buộc)**
| **Node**               | **Tham Số Cần Điền**                          | **Lưu Ý**                                                                 |
|------------------------|-----------------------------------------------|---------------------------------------------------------------------------|
| **NewsAPI**            | `apiKey` trong `Get News` node.              | Đăng ký tại [NewsAPI](https://newsapi.org/) và điền key vào.              |
| **OpenRouter**         | Chọn trong `OpenRouter Chat Model`, `OpenRouter Weekly`. | Chọn model phù hợp (ví dụ: `mistralai/mixtral-8x7b`).                  |
| **DeepL**              | `apiKey` trong `Translate to Japanese`.      | Đăng ký tại [DeepL Pro](https://www.deepl.com/pro-api).                  |
| **Google Sheets**      | `googleSheetsOAuth2Api` trong `Append row` và `Read sheet`. | Chọn file Sheets đã tạo trước.                                            |
| **Slack**              | Chọn `channel` trong `Send English Message` và `Send Japanese Message`. | Chọn channel muốn gửi báo cáo.                                           |

#### **🔹 Cấu Hình Cụ Thể Các Node Quan Trọng**
##### **A. Phần Hàng Ngày (Daily Digest)**
1. **"Set Keyword" (Node `set`)**
   - **Thay đổi `chatInput`** từ `"technology"` thành từ khóa của bạn (ví dụ: `"Crypto"`, `"AI"`, `"SaaS"`).
   - **Ví dụ:**
     ```json
     {
       "chatInput": "Crypto"
     }
     ```

2. **"Get News" (Node `httpRequest`)**
   - **Không cần chỉnh** (sử dụng API NewsAPI mặc định).

3. **"AI Agent (Filter)" & "AI Agent (Structure)"**
   - **Không cần chỉnh** (AI sẽ tự động lọc tin và tạo tóm tắt).
   - **Nếu muốn điều chỉnh AI**, mở node `agent` và chỉnh `prompt` trong `OpenRouter Chat Model`.

4. **"Append row in sheet" (Node `googleSheets`)**
   - **Chọn file Sheets** đã tạo trước (cột: `title`, `author`, `summary`, `url`).
   - **Không cần chỉnh tab** (sử dụng mặc định).

5. **"Send English Message" & "Send Japanese Message" (Node `slack`)**
   - **Chọn channel** muốn gửi báo cáo.
   - **Kiểm tra `message`** để đảm bảo nội dung hiển thị rõ ràng.

##### **B. Phần Tuần (Weekly Report)**
1. **"Read sheet (weekly)" (Node `googleSheets`)**
   - **Chọn cùng file Sheets** như phần `Append row in sheet`.
   - **Không cần chỉnh tab** (sử dụng mặc định).

2. **"AI Agent Weekly Report"**
   - **Không cần chỉnh** (AI sẽ tự động phân tích xu hướng từ dữ liệu tuần trước).
   - **Nếu muốn điều chỉnh**, mở node `agent` và chỉnh `prompt` trong `OpenRouter Weekly`.

3. **"Send Weekly Summary" (Node `slack`)**
   - **Chọn channel** muốn gửi báo cáo tuần.
   - **Kiểm tra `message`** để đảm bảo báo cáo đầy đủ.

4. **"Cron Weekly Report" (Node `cron`)**
   - **Mặc định chạy thứ Hai lúc 9:00 AM**.
   - **Nếu muốn thay đổi**, chỉnh `cronExpression` (ví dụ: `0 0 9 * * 1` để chạy thứ Hai 9h sáng).

---
### **3. Kích Hoạt Workflow ⚡️**
1. **Test Run với dữ liệu mẫu**
   - Nhấn **"Run Workflow"** và chọn **Webhook** (node đầu tiên).
   - **Gửi một request test** (ví dụ: `POST https://tên-n8n.com/webhook/iphone-news` với body rỗng).
   - **Kiểm tra**:
     - Tin tức có được lấy không?
     - AI có lọc tin chất lượng không?
     - Slack có nhận được báo cáo không?
     - Google Sheets có cập nhật dữ liệu không?

2. **Bật Active Workflow**
   - Sau khi test thành công, **bật toggle `Active`** để workflow chạy tự động hàng ngày/tuần.

---
## **✍️ Mẹo & Gợi Ý Nâng Cao**
:::info[**CÁCH TIẾP CẬN THÊM**]
1. **Thêm Notion hoặc Airtable**
   - Thay vì Google Sheets, có thể lưu dữ liệu vào **Notion** hoặc **Airtable** để dễ dàng chia sẻ với team.

2. **Gửi Email Báo Cáo**
   - Thêm node `n8n-nodes-base.email` để gửi báo cáo hàng ngày/tuần qua email.

3. **Lưu Log Lịch Sử**
   - Thêm node `n8n-nodes-base.stickyNote` để lưu lịch sử tin tức đã xử lý.

4. **Tự động Cập Nhật Từ Khóa**
   - Sử dụng **Webhook** để cho phép team cập nhật từ khóa mới mà không cần chỉnh workflow.

5. **Báo Cáo Xu Hướng Chi Tiết**
   - Chỉnh `prompt` trong `AI Agent Weekly Report` để AI phân tích sâu hơn (ví dụ: so sánh xu hướng giữa các tuần).

6. **Dịch Sang Nhiều Ngôn Ngữ**
   - Thay vì chỉ dịch sang tiếng Nhật, có thể thêm node DeepL khác để dịch sang **Tiếng Trung, Tiếng Hàn**...

7. **Kết Nối với Trello/Notion**
   - Sử dụng node `n8n-nodes-base.trello` hoặc `n8n-nodes-base.notion` để tự động tạo task từ tin tức quan trọng.
:::

---
## **📌 Kết Luận**
Workflow này **giải phóng thời gian** của các sếp để tập trung vào chiến lược thay vì việc theo dõi tin tức thủ công. Với **AI lọc tin chất lượng**, **báo cáo tự động hóa** và **dữ liệu tích lũy**, nó trở thành **công cụ không thể thiếu** cho các doanh nghiệp theo dõi thị trường.

**🚀 Hãy áp dụng ngay và tiết kiệm 10+ giờ/tháng!**
- **Self-hosted** để ổn định 24/7.
- **Chỉnh từ khóa** theo ngành nghề của bạn.
- **Dịch sang nhiều ngôn ngữ** nếu cần.

**👉 [Tải workflow ngay](https://n8n.io/workflows/10977) và bắt đầu tự động hóa!**