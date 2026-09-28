---
title: "📊 Tự Động Hóa Phân Tích Dữ Liệu Marketing: Gộp, Lọc & Tóm Tắt Bằng GPT-4o Trên Google Sheets"
description: "Workflow tự động hóa 100% không code giúp các sếp phân tích hiệu suất marketing từ Google Sheets, lọc dữ liệu theo tiêu chí chi tiêu và tương tác, sau đó sử dụng GPT-4o để tóm tắt và so sánh hiệu suất của các leader. Giúp tiết kiệm thời gian lên đến 80% trong việc báo cáo và phân tích."
slug: "tu-dong-hoa-phan-tich-du-lieu-marketing-google-sheets-gpt-4o"
tags: [n8n, automation, no-code, google-sheets, ai-summarization, gpt-4o, marketing-analytics]
keywords: [n8n workflow phân tích dữ liệu, tự động hóa báo cáo marketing, GPT-4o tóm tắt dữ liệu, Google Sheets tự động hóa, phân tích hiệu suất marketing]
---

# 🚀 **Tự Động Hóa Phân Tích Dữ Liệu Marketing: Gộp, Lọc & Tóm Tắt Bằng GPT-4o Trên Google Sheets**

### **Nỗi Đau Của Các Sếp**
Các sếp marketing thường phải mất **giờ đồng hồ** để:
- **Gộp dữ liệu** từ nhiều bảng Google Sheets (ví dụ: dữ liệu hiệu suất kênh và thông tin quản lý leader).
- **Lọc và phân loại** dữ liệu theo tiêu chí chi tiêu (ví dụ: chi tiêu ≥ $350 được đánh giá là "Great", còn lại là "Poor").
- **Tóm tắt và so sánh** hiệu suất của các leader một cách thủ công, dẫn đến **sai sót** và **tốn thời gian**.
- **Báo cáo định kỳ** cho ban lãnh đạo, nhưng lại không có **cách tự động hóa** để cập nhật liên tục.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tự động gộp dữ liệu** từ 2 bảng Google Sheets khác nhau.
✅ **Lọc và phân loại** dựa trên tiêu chí chi tiêu và tương tác.
✅ **Sử dụng GPT-4o** để tóm tắt và so sánh hiệu suất leader một cách **chính xác và cá nhân hóa**.
✅ **Cập nhật tự động** khi dữ liệu thay đổi, tiết kiệm **80% thời gian** so với cách làm thủ công.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần thủ công gộp, lọc và tóm tắt dữ liệu.
- **Chính xác cao**: GPT-4o phân tích và so sánh hiệu suất một cách **mạnh mẽ và logic**.
- **Báo cáo tự động**: Dữ liệu luôn cập nhật, không cần cập nhật thủ công.
- **Cá nhân hóa**: AI cung cấp **báo cáo chi tiết** về leader hiệu suất cao và thấp.
- **Hoạt động liên tục**: Workflow chạy 24/7, không phụ thuộc vào giờ làm việc.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google** và **Google Sheets OAuth2 API Key**:
   - Tạo một **Google Sheet mẫu** từ [đây](https://docs.google.com/spreadsheets/d/19aUQYZq02qHsCelO4eeV4sx_MTJJupC5qe0gDLQBtRA/copy).
   - Cấu hình **Google Sheets OAuth2** trong n8n (trong phần **Credentials**).
2. **API Key OpenAI**:
   - Đăng ký tài khoản [OpenAI](https://platform.openai.com/) và lấy **API Key**.
   - Thêm vào **OpenAI credential** trong n8n.
3. **n8n Self-hosted** (khuyến nghị) hoặc n8n.cloud (miễn phí cho các dự án nhỏ).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/6753](https://n8n.io/workflows/6753) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/6753) và dán vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này bao gồm **15 node** với các bước logic phức tạp. Dưới đây là **các node quan trọng cần cấu hình**:

##### **A. Cấu Hình Google Sheets**
- **Node "Google Sheets1" và "Sample Marketing Data"**:
  - Chọn **credentials**: `googleSheetsOAuth2Api`.
  - Điền **URL của Google Sheet** đã copy từ [đây](https://docs.google.com/spreadsheets/d/19aUQYZq02qHsCelO4eeV4sx_MTJJupC5qe0gDLQBtRA/copy).
  - Chọn **Sheet Name** tương ứng (ví dụ: `Marketing Data` và `Leader Assignment`).

##### **B. Cấu Hình OpenAI (GPT-4o)**
- **Node "OpenAI Chat Model"**:
  - Chọn **credentials**: `openAiApi`.
  - Đảm bảo **API Key** đã được thêm vào trong **OpenAI credential**.
  - Chọn **model**: `gpt-4o-mini` (mặc định trong workflow).

##### **C. Cấu Hình Logic Lọc & Phân Tích**
- **Node "Check if spend over $350" (If)**:
  - Đảm bảo **field "Spend"** trong dữ liệu được định dạng số (USD).
  - Cấu hình logic:
    - Nếu `Spend ≥ 350` → Nhánh **"Great"**.
    - Ngược lại → Nhánh **"Poor"**.

- **Node "Count bad days" và "Count good days" (Summarize)**:
  - Chọn **field "Leader"** để tính toán số ngày hiệu suất tốt/xấu cho mỗi leader.

##### **D. Cấu Hình AI Agent**
- **Node "AI Agent - Summarize Leader Performance"**:
  - Workflow tự động chuyển đổi dữ liệu thành **dạng text** để AI phân tích.
  - AI sẽ trả về **báo cáo tóm tắt** về:
    - Leader hiệu suất cao nhất.
    - Leader hiệu suất thấp nhất.
    - Lý do (ví dụ: chi tiêu thấp, tương tác ít).

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Chọn **Manual Trigger** và chạy thử với dữ liệu mẫu.
  - Kiểm tra kết quả ở **node "Structured Output Parser"** để đảm bảo AI hiểu đúng dữ liệu.
- **Bật Active**:
  - Sau khi kiểm tra thành công, bật **Active** để workflow chạy tự động khi có dữ liệu mới.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết Nối Slack/Telegram**:
   - Thêm **node Slack/Telegram** sau **AI Agent** để nhận báo cáo tự động qua chat.
   - Ví dụ: Khi workflow hoàn thành, gửi kết quả vào kênh Slack của team.

2. **Lưu Log Dữ Liệu**:
   - Thêm **node Google Sheets** mới để lưu **lịch sử phân tích** (ngày, leader, kết quả).
   - Giúp theo dõi **tiến bộ dài hạn** của các leader.

3. **Tự Động Cập Nhật Định Kỳ**:
   - Sử dụng **node Schedule** để chạy workflow hàng tuần/tháng.
   - Ví dụ: Chạy vào **thứ 7 hàng tuần** để cập nhật báo cáo cho ban lãnh đạo.

4. **Tùy Chỉnh Prompt AI**:
   - Nếu muốn AI **phân tích sâu hơn**, chỉnh sửa **prompt** trong **node OpenAI Chat Model**.
   - Ví dụ: Yêu cầu AI so sánh **trend tăng/giảm** của các leader trong tháng.

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp marketing muốn:
✔ **Tự động hóa phân tích dữ liệu** mà không cần viết code.
✔ **Tiết kiệm thời gian** lên đến 80% trong việc báo cáo.
✔ **Nhận báo cáo cá nhân hóa** từ AI về hiệu suất leader.

**Hành động ngay hôm nay:**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test với dữ liệu mẫu** để đảm bảo hoạt động chính xác.
3. **Bật Active** và **quên việc thủ công** phân tích dữ liệu!

**Nếu có vấn đề**, liên hệ với [Robert Breen](https://www.linkedin.com/in/robertbreen) hoặc comment bên dưới. Chúc các sếp thành công! 🚀