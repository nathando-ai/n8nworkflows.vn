---
title: "🚀 Tự Động Scrape Danh Sách Việc Làm & Gửi Cảnh Báo Thông Minh với Decodo + Google Gemini + Slack + Email"
description: "Workflow tự động hóa 100% không code giúp các sếp theo dõi việc làm mới từ nhiều trang tuyển dụng, lọc theo ngành nghề mục tiêu, và nhận cảnh báo ngay trên Slack/Email. Giảm thời gian tìm kiếm từ 10h/tháng xuống 0h, với độ chính xác cao nhờ AI Google Gemini."
slug: "tieu-dong-scrape-danh-sach-viec-lam"
tags: [n8n, automation, no-code, ai-summarization, market-research, google-gemini, decodo, slack-integration, gmail-automation]
keywords: [n8n workflow scrape việc làm, tự động hóa tìm việc, cảnh báo việc làm mới, google gemini n8n, decodo web scraping, alert việc làm slack email]
---

# 🚀 **Tự Động Scrape & Cảnh Báo Việc Làm Mới Nhất – Không Cần Code!**

### **Nỗi Đau Của Các Sếp Trong Tìm Việc Làm**
- **Thời gian tốn kha**: Phải tra cứu thủ công trên LinkedIn, Indeed, trang tuyển dụng của hàng chục công ty, mất từ 5-10h/tháng.
- **Thông tin rác**: Nhiều việc làm không phù hợp, hoặc bị lặp lại, khiến các sếp bỏ lỡ những cơ hội thực sự.
- **Không cập nhật kịp thời**: Các công ty thường cập nhật việc làm vào cuối tuần, nhưng các sếp chỉ check vào giữa tuần, dẫn đến bỏ lỡ.
- **Khó lọc theo ngành**: Muốn tìm việc làm trong ngành *Kỹ Thuật Phần Mềm* hay *Marketing Digital* nhưng phải lọc thủ công trên hàng trăm trang.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Scrape** danh sách việc làm mới từ trang tuyển dụng của các công ty.
✅ **Lọc** theo ngành nghề mục tiêu (VD: Kỹ Thuật, Marketing, Quản Trị).
✅ **Tóm tắt** thông tin việc làm bằng **Google Gemini AI** (chính xác hơn 90% so với cách thủ công).
✅ **Gửi cảnh báo** ngay trên **Slack** và **Email** khi có việc làm mới phù hợp.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động **24/7** mà không ngừng, các sếp nên **self-host** n8n trên VPS. Hệ thống này sẽ chạy ổn định, không bị giới hạn như phiên bản cloud.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** – giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (Đảm bảo tốc độ scrape nhanh)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10h/tháng**: Không cần tra cứu thủ công trên nhiều trang.
- **Độ chính xác cao**: Google Gemini AI **lọc bỏ** thông tin rác (quảng cáo, việc làm đã đóng), chỉ giữ lại việc làm **chính thức**.
- **Cảnh báo tức thời**: Nhận thông báo **ngay khi có việc làm mới** trên Slack/Email, không bỏ lỡ.
- **Tùy chỉnh ngành nghề**: Chỉ lấy việc làm trong **ngành Kỹ Thuật, Marketing, Quản Trị...** mà các sếp quan tâm.
- **Hoạt động liên tục**: Workflow chạy **mỗi ngày** (hoặc theo lịch tự động), không phụ thuộc vào thời gian của các sếp.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Airtable** (để lưu danh sách trang tuyển dụng của các công ty).
2. **API Key Decodo** (dùng để scrape trang web).
3. **Google Gemini API** (để tóm tắt và phân tích việc làm).
4. **Tài khoản Slack** (để gửi cảnh báo).
5. **Tài khoản Gmail** (để gửi email cảnh báo).
6. **Danh sách URL trang tuyển dụng** (các sếp cần nhập vào Airtable).

---
:::info[CHUẨN BỊ]
**Bước 1: Tạo bảng Airtable**
- Tạo một bảng mới trong Airtable với các cột:
  - `Company Name` (Tên công ty)
  - `Career Page URL` (Trang tuyển dụng)
  - `Department` (Ngành nghề, VD: Kỹ Thuật, Marketing)
- Nhập danh sách URL của các công ty các sếp quan tâm (VD: `https://careers.google.com/`, `https://jobs.microsoft.com/`).

**Bước 2: Cấu hình API**
- **Decodo**: Tạo API key tại [Decodo](https://decodo.com/) và thêm vào n8n.
- **Google Gemini**: Tạo API key tại [Google AI Studio](https://makersuite.google.com/) và chọn credential `googlePalmApi`.
- **Slack**: Tạo App Slack và lấy `OAuth Token` (credential `slackOAuth2Api`).
- **Gmail**: Cấu hình OAuth2 cho Gmail (credential `gmailOAuth2`).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể:
- **Tải file JSON** từ [n8n.io/workflows/13187](https://n8n.io/workflows/13187) và import vào n8n Editor.
- **Copy JSON** từ trang trên và dán vào n8n Editor (tab `Import`).

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflows này có **13 node**, nhưng chỉ cần chú ý đến các node sau:

##### **A. Schedule Trigger (Lịch chạy tự động)**
- **Node**: `Run Daily`
- **Cấu hình**:
  - Chọn `Daily` và thời gian phù hợp (VD: 8h sáng để scrape vào đầu ngày).
  - **Không cần chỉnh** nếu muốn chạy hàng ngày.

##### **B. Airtable Search Records (Lấy URL trang tuyển dụng)**
- **Node**: `Search records`
- **Cấu hình**:
  - Chọn `airtableOAuth2Api` (credential đã cấu hình).
  - **Filter**: Chỉ lấy các URL có `valid: true` (để bỏ những trang không hoạt động).
  - **Không cần chỉnh** nếu đã nhập dữ liệu vào Airtable đúng định dạng.

##### **C. Decodo + Google Gemini (Scrape & Tóm Tắt Việc Làm)**
- **Node**: `Decodo` + `Job extractor` (AI Agent)
- **Cấu hình**:
  - **Decodo**:
    - Chọn `decodo` credential.
    - **URLs**: Sẽ tự động lấy từ Airtable.
    - **Rate Limit**: Node `Wait 5 seconds` giúp tránh bị chặn.
  - **Google Gemini**:
    - Chọn `googlePalmApi`.
    - **Prompt**: AI sẽ tự động phân tích và tóm tắt việc làm (không cần chỉnh).

##### **D. Lọc Theo Ngành Nghề (Edit Fields)**
- **Node**: `Job Name` (type: `set`)
- **Cấu hình**:
  - **Thêm cột `department`** (VD: `Engineering`, `Marketing`).
  - **Chỉnh `filter`** để lấy việc làm trong ngành mục tiêu (VD: `{{ $json["department"] }} === "Engineering"`).

##### **E. Gửi Cảnh Báo (Slack + Email)**
- **Node**: `Send a message1` (Slack) + `Send a message` (Gmail)
- **Cấu hình**:
  - **Slack**:
    - Chọn `slackOAuth2Api`.
    - **Message Format**: Sử dụng template đã có (có thể chỉnh nội dung).
  - **Gmail**:
    - Chọn `gmailOAuth2`.
    - **Subject**: `🚀 Cảnh báo việc làm mới: {{ $json["title"] }}`
    - **Body**: Nội dung tóm tắt từ Google Gemini.

##### **F. Code JavaScript (Lọc Bỏ Thông Tin Rác)**
- **Node**: `Code in JavaScript`
- **Lưu ý**:
  - **Không cần chỉnh** nếu muốn giữ mặc định (loại bỏ việc làm trống, không hợp lệ).
  - Nếu cần **tùy chỉnh**, các sếp có thể mở node này và chỉnh logic.

---

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Chạy **manual test** với 1-2 URL mẫu để kiểm tra.
  - Kiểm tra:
    - AI có scrape được thông tin việc làm không?
    - Slack/Email có nhận được cảnh báo không?
- **Bật Active**:
  - Sau khi test thành công, **bật Active** workflow.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Thêm Log Lịch Sử**:
   - Sử dụng **Airtable** hoặc **Google Sheets** để lưu lịch sử việc làm đã cảnh báo (để tránh lặp lại).
   - **Cách làm**: Thêm node `airtable.createRecord` sau khi gửi cảnh báo.

2. **Kết Nối với Telegram**:
   - Thay vì Slack, các sếp có thể gửi cảnh báo qua **Telegram Bot** (cài node `@n8n/n8n-nodes-telegram`).
   - **Ưu điểm**: Nhận được thông báo ngay cả khi không mở Slack.

3. **Báo Cáo Định Kỳ**:
   - Sử dụng **Google Sheets** hoặc **Airtable** để tạo báo cáo tuần/month về số lượng việc làm mới.
   - **Cách làm**: Thêm node `googleSheets.createRow` sau khi scrape xong.

4. **Tùy Chỉnh AI Gemini**:
   - Nếu muốn **AI tóm tắt chi tiết hơn**, chỉnh prompt trong node `Google Gemini Chat Model`:
     ```json
     {
       "prompt": "Tóm tắt việc làm này một cách chi tiết, bao gồm: tiêu đề, mô tả công việc, yêu cầu kỹ năng, mức lương (nếu có), và liên kết ứng tuyển. Loại bỏ tất cả thông tin không liên quan đến việc làm."
     }
     ```

5. **Quản Lý Nhiều Ngành Nghề**:
   - Nếu muốn **lọc nhiều ngành** (VD: Kỹ Thuật + Marketing), chỉnh node `Edit Fields` thành:
     ```json
     {
       "filter": "{{ $json["department"] }} === 'Engineering' || $json['department'] === 'Marketing'"
     }
     ```

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn:
✔ **Tiết kiệm thời gian** trong việc tìm việc làm.
✔ **Nhận cảnh báo tức thời** khi có việc làm mới phù hợp.
✔ **Không cần code** hoặc kiến thức kỹ thuật.

**Hành động ngay!**
1. **Import workflow** vào n8n.
2. **Cấu hình Airtable + API** theo hướng dẫn.
3. **Bật Active** và bắt đầu nhận cảnh báo việc làm **mỗi ngày**!

**🚀 Cảm ơn các sếp đã thử nghiệm!** Nếu có vấn đề, hãy để lại comment dưới đây, mình sẽ hỗ trợ ngay. 😊

---