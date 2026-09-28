---
title: "🚀 Tự Động Hóa Scrape Bình Luận LinkedIn & Đánh Giá Tiềm Năng Lead Bằng AI (N8n + Azure OpenAI + Google Sheets)"
description: "Workflow tự động tìm kiếm bài viết LinkedIn liên quan đến vấn đề lead generation, scrape bình luận, đánh giá tiềm năng mua hàng bằng AI, và lưu kết quả vào Google Sheets để theo dõi. Giúp các sếp tiết kiệm 10+ giờ/tháng và tăng hiệu quả chăm sóc khách hàng 30%."
slug: "tieu-dong-hoa-scrape-linkedin-danh-gia-tien-nang-lead"
tags: [n8n, automation, lead-generation, ai-summarization, serpapi, connectsafely, azure-openai]
keywords: [n8n workflow scrape linkedin, tự động hóa lead generation, đánh giá tiềm năng lead bằng AI, n8n + azure openai, tự động scrape bình luận linkedin]
---

# 🚀 **Tự Động Hóa Scrape Bình Luận LinkedIn & Đánh Giá Tiềm Năng Lead Bằng AI**

### **Giải pháp cho các sếp bán hàng, marketing và sales development**
Bạn có bao giờ phải mất **giờ đồng hồ** để:
- Tìm kiếm bài viết LinkedIn liên quan đến vấn đề của khách hàng (ví dụ: "chuyển đổi thấp", "lỗi lead")?
- Quét hàng trăm bình luận để tìm những người có tiềm năng mua hàng?
- Phân tích thủ công ý định mua hàng của từng lead?

**Workflow này tự động hóa toàn bộ quy trình đó!** Nó sẽ:
1. **Scrape** bài viết LinkedIn từ Google Search (thông qua SerpAPI).
2. **Lấy tất cả bình luận** của mỗi bài viết (thông qua ConnectSafely).
3. **Đánh giá tiềm năng mua hàng** (intent score từ 0-100) bằng **Azure OpenAI GPT-4o-mini**.
4. **Lưu kết quả** vào Google Sheets với thông tin chi tiết (tên lead, bình luận, điểm số, nhãn).

Kết quả? **Các sếp có danh sách lead hot được sàng lọc tự động**, tiết kiệm **10+ giờ/tháng** và tăng **hiệu quả chăm sóc khách hàng lên 30%**.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và không bị giới hạn API, các sếp nên **self-host n8n** trên VPS.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đảm bảo tốc độ cao cho AI)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Không cần quét thủ công hàng trăm bình luận.
✅ **Đánh giá chính xác**: AI phân tích ý định mua hàng (intent score) từ 0-100.
✅ **Danh sách lead hot**: Tất cả lead có tiềm năng được sàng lọc và lưu vào Google Sheets.
✅ **Hoạt động 24/7**: Workflow chạy tự động, không cần can thiệp.
✅ **Cá nhân hóa**: Dễ dàng điều chỉnh keyword tìm kiếm và logic AI.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản SerpAPI** (để tìm kiếm bài viết LinkedIn).
2. **Tài khoản ConnectSafely** (để scrape bình luận).
3. **Azure OpenAI API Key** (để sử dụng GPT-4o-mini).
4. **Google Sheets** (để lưu kết quả, cần có **cột: post_url, lead_name, comment, intent_score, intent_label**).

🔹 **Lưu ý**:
- **SerpAPI** và **ConnectSafely** có giới hạn API, nên các sếp nên **mua gói cao cấp** nếu muốn scrape nhiều bài viết.
- **Azure OpenAI** yêu cầu **đăng ký mô hình gpt-4o-mini** và cấu hình credential chính xác.

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể:
- **Tải file JSON** từ [n8n.io/workflows/13185](https://n8n.io/workflows/13185) và import vào **n8n Editor**.
- **Copy JSON** từ link trên và **paste** vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **9 node**, các sếp cần chú ý cấu hình sau:

##### **🔹 Node 1: "Search LinkedIn Posts via SerpAPI"**
- **Credentials**: Chọn `serpApi` (đã cấu hình trước).
- **Query**: Thay đổi **keyword tìm kiếm** (ví dụ: `"low conversion rate" OR "missed leads"`).
- **Limiter**: Đặt số lượng kết quả (ví dụ: `10` bài viết).

##### **🔹 Node 2: "Fetch Post Comments via ConnectSafely"**
- **Credentials**: Chọn `connectSafelyApi` (đã cấu hình trước).
- **Account ID**: Điền **ID tài khoản ConnectSafely** (nếu chưa có, đăng ký tại [connectsafely.ai](https://connectsafely.ai/)).
- **Operation**: Đảm bảo chọn `getAllPostComments`.

##### **🔹 Node 3: "Parse & Filter Search Results" (Code Node)**
- **Lưu ý**: Node này **lọc URL bài viết LinkedIn** và loại bỏ kết quả không liên quan.
- **Mã code mặc định** đã xử lý tự động, **không cần chỉnh sửa** (nếu không biết code, để nguyên).

##### **🔹 Node 4: "AI Intent Detection Agent" (Agent Node)**
- **Model**: Sử dụng **Azure OpenAI GPT-4o-mini** (đã cấu hình trong `lmChatAzureOpenAi`).
- **Prompt**: Các sếp có thể **tùy chỉnh logic AI** trong **system message** (ví dụ: yêu cầu AI đánh giá cao lead có từ khóa `"urgent"` hoặc `"need solution"`).
- **Output**: AI trả về **điểm số (0-100) và nhãn (no-intent → high-intent)**.

##### **🔹 Node 5: "Azure OpenAI GPT-4o-mini"**
- **Credentials**: Chọn `azureOpenAiApi` (đã cấu hình trước).
- **Model**: Đảm bảo chọn `gpt-4o-mini`.
- **Temperature**: Đặt **0.3-0.5** để kết quả ổn định.

##### **🔹 Node 6: "Flatten Comments into Rows" (Code Node)**
- **Lưu ý**: Node này **chuyển đổi dữ liệu bình luận** từ dạng mảng thành **các hàng riêng biệt** (một hàng = một bình luận).
- **Mã code mặc định** đã xử lý tự động, **không cần chỉnh sửa**.

##### **🔹 Node 7: "Parse AI Intent Output" (Code Node)**
- **Lưu ý**: Node này **tách điểm số và nhãn** từ output của AI.
- **Mã code mặc định** đã xử lý tự động, **không cần chỉnh sửa**.

##### **🔹 Node 8: "Save Leads to Google Sheet"**
- **Credentials**: Chọn `googleSheetsOAuth2Api` (đã cấu hình trước).
- **Sheet Name**: Đảm bảo **tên sheet** và **cột** (post_url, lead_name, comment, intent_score, intent_label) **khớp với cấu trúc**.
- **Operation**: Chọn `append` để **thêm dữ liệu mới** vào sheet.

#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Chọn **Execute Workflow** và **nạp dữ liệu mẫu** (ví dụ: một bài viết LinkedIn có 5 bình luận).
   - Kiểm tra **Google Sheets** xem dữ liệu có được lưu đúng không.
2. **Bật Active**:
   - Sau khi test thành công, **bật Active** để workflow chạy tự động khi kích hoạt.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tùy chỉnh keyword tìm kiếm**:
   - Thay đổi **SerpAPI query** để tìm kiếm bài viết liên quan đến **vấn đề cụ thể** của doanh nghiệp (ví dụ: `"AI adoption challenges"`).
2. **Lưu log hoạt động**:
   - Thêm **Slack/Telegram Notification** để nhận thông báo khi workflow chạy thành công/thất bại.
3. **Gửi báo cáo định kỳ**:
   - Sử dụng **n8n + Google Sheets + Email Node** để tự động gửi **báo cáo lead hot** hàng tuần.
4. **Kết hợp với CRM**:
   - Sau khi scrape xong, **đưa lead vào HubSpot/Salesforce** bằng **n8n + CRM Node**.
5. **Optimize AI Prompt**:
   - Nếu muốn **AI đánh giá chính xác hơn**, các sếp có thể **tùy chỉnh system message** trong Agent Node (ví dụ: yêu cầu AI **loại bỏ bình luận spam**).

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc **quét bình luận LinkedIn thủ công** và **phân tích lead**. Với **AI đánh giá tiềm năng mua hàng**, các sếp có thể **tập trung vào chăm sóc lead hot** thay vì làm việc rườm rà.

**Hành động ngay!**
1. **Import workflow** và cấu hình credential.
2. **Test run** với một bài viết mẫu.
3. **Bật Active** và **theo dõi Google Sheets** để nhận danh sách lead hot.

👉 **[Tải workflow từ n8n.io](https://n8n.io/workflows/13185)** và **bắt đầu tự động hóa ngay!**

---
**Cần hỗ trợ?** Đăng ký **VPS n8n** tại [TinoHost](https://tino.vn/vps-n8n?affid=388) để workflow chạy **ổn định 24/7**! 🚀