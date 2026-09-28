---
title: "📰 **Tự Động Hóa Báo Cáo Tin Tức Google Định Kì Với Gmail Phê Duyệt - Không Cần Code!**"
description: "Workflow tự động hóa lấy tin tức Google theo chủ đề, định dạng AI, gửi email phê duyệt và quản lý nội dung cho doanh nghiệp/ cá nhân. Giúp tiết kiệm thời gian lọc tin, tăng hiệu quả chia sẻ trên mạng xã hội hoặc blog."
slug: "tieu-dong-hoa-bao-cao-tin-tuc-google-voi-gmail"
tags: [n8n, automation, no-code, ai, google-news, gmail, airtable, openai]
keywords: [n8n workflow google news, tự động hóa tin tức, AI định dạng email, phê duyệt nội dung tự động, n8n + serpapi, n8n + openai]
---

# 🚀 **Tự Động Hóa Báo Cáo Tin Tức Google Định Kì Với Gmail Phê Duyệt**

### **Giải Pháp Cho Người Sử Dụng**
Bạn có bao giờ phải mất nhiều giờ mỗi ngày để lọc, đọc và chọn lọc tin tức từ Google News để chia sẻ trên blog, mạng xã hội hoặc báo cáo nội bộ? Hay bạn muốn **tự động hóa quá trình này** mà không cần viết một dòng code? Workflow này sẽ giúp bạn **lấy tin tức mới nhất, định dạng bằng AI, gửi email phê duyệt tự động** và quản lý nội dung một cách hiệu quả.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần phải thủ công lọc tin tức hàng ngày.
- **Nội dung cá nhân hóa**: AI định dạng tin tức theo phong cách riêng của bạn.
- **Phê duyệt tự động**: Gửi email cho bạn phê duyệt trước khi chia sẻ.
- **Quản lý hiệu quả**: Quản lý các batch tin tức bằng Airtable (hoặc Google Sheet).
- **Hoạt động liên tục**: Workflow chạy định kỳ (ví dụ: hàng ngày) mà không cần can thiệp.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản API**:
   - [SerpApi](https://serpapi.com/) (để lấy tin tức Google News).
   - [OpenAI API](https://openai.com/) (để sử dụng AI định dạng email).
   - [Airtable](https://airtable.com/) (để quản lý counter và batch tin tức).
   - [Gmail](https://mail.google.com/) (để phê duyệt email).
2. **Tham số cấu hình**:
   - **SerpApi Key**: Mã API từ SerpApi.
   - **OpenAI API Key**: Mã API từ OpenAI.
   - **Airtable API Key**: Mã API từ Airtable.
   - **Gmail OAuth2**: Thiết lập OAuth2 cho Gmail (xem hướng dẫn [đây](https://developers.google.com/gmail/api/quickstart/python)).
3. **Chủ đề tin tức**: Xác định chủ đề bạn muốn theo dõi (ví dụ: "Tin tức công nghệ Việt Nam").

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/8464](https://n8n.io/workflows/8464) hoặc copy/paste JSON vào **n8n Editor**.
- **Cách import**:
  1. Mở **n8n Editor** trên trang web hoặc máy chủ self-hosted.
  2. Nhấn **Import** và chọn file JSON đã tải.
  3. Chọn **Create Workflow** để tạo workflow mới từ file.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflows này bao gồm **11 node** quan trọng. Dưới đây là hướng dẫn chi tiết để cấu hình:

##### **A. Cấu Hình Credentials**
1. **SerpApi**:
   - Tạo **credentials** mới trong n8n với loại `serpApi`.
   - Điền **API Key** từ tài khoản SerpApi của bạn.
   - **Key Parameters**:
     - `operation`: `google_news`.
     - `q`: Chủ đề tin tức bạn muốn theo dõi (ví dụ: `"Tin tức công nghệ Việt Nam"`).
     - `num`: Số kết quả trả về (ví dụ: `100`).

2. **OpenAI**:
   - Tạo **credentials** mới với loại `openAiApi`.
   - Điền **API Key** từ OpenAI.
   - **Model**: Chọn `gpt-4o-mini` (hoặc model khác nếu muốn).

3. **Airtable**:
   - Tạo **credentials** mới với loại `airtableTokenApi`.
   - Điền **API Key** từ Airtable.
   - **Base ID**: ID của bảng Airtable bạn sử dụng (xem hướng dẫn [đây](https://airtable.com/api)).
   - **Table Name**: Tên bảng để quản lý counter (ví dụ: `NewsCounter`).

4. **Gmail**:
   - Tạo **credentials** mới với loại `gmailOAuth2`.
   - Thực hiện **OAuth2 setup** theo hướng dẫn của Google.
   - **Key Parameters**:
     - `to`: Email của bạn (để nhận email phê duyệt).
     - `subject`: Tiêu đề email (ví dụ: `"Phê duyệt tin tức hàng ngày"`).
     - `html`: Nội dung HTML từ AI (sẽ được tự động tạo).

##### **B. Cấu Hình Node Quản Lý Batch (Airtable)**
1. **Create Counter**:
   - Node này tạo một bản ghi mới trong Airtable để quản lý batch tin tức.
   - **Fields**:
     - `counter`: Giá trị bắt đầu từ `0` (sẽ tăng dần).

2. **Get Counter**:
   - Lấy giá trị hiện tại của counter từ Airtable.
   - **Key Parameters**:
     - `fields`: `counter`.

3. **Update Counter**:
   - Cập nhật counter sau khi xử lý xong một batch.
   - **Key Parameters**:
     - `fields`: `counter` (giá trị mới = giá trị cũ + 10).

4. **Delete Counter**:
   - Xóa bản ghi counter sau khi hoàn tất batch.

##### **C. Cấu Hình Node AI Định Dạng Email**
1. **Extract Details (Node Code)**:
   - Node này sử dụng **JavaScript** để trích xuất tiêu đề và chi tiết từ tin tức.
   - **Mã nguồn gợi ý**:
     ```javascript
     // Trích xuất tiêu đề và mô tả từ tin tức
     const newsHeaders = $input.all().map(item => ({
       title: item.title,
       description: item.description,
       link: item.link,
       date: item.date
     }));
     return { json: { newsHeaders } };
     ```

2. **Prepare Content Review Email (Node Agent)**:
   - Node này sử dụng **AI Agent** (OpenAI) để định dạng tin tức thành email HTML.
   - **Prompt gợi ý**:
     ```
     Tạo một email HTML với 10 tin tức mới nhất về chủ đề "{topic}".
     Cấu trúc:
     - Tiêu đề: "{title}"
     - Mô tả: "{description}"
     - Link: "{link}"
     - Ngày: "{date}"
     Sử dụng phong cách chuyên nghiệp và ngắn gọn.
     ```

##### **D. Cấu Hình Node Phê Duyệt Gmail**
1. **Gmail Approval News**:
   - Node này gửi email với nội dung HTML đã định dạng cho bạn phê duyệt.
   - **Key Parameters**:
     - `to`: Email của bạn.
     - `subject`: `"Phê duyệt tin tức hàng ngày"`.
     - `html`: Nội dung từ AI.
   - **Phê duyệt**:
     - Khi bạn mở email và **nhấn "Approve"**, workflow sẽ tiếp tục.
     - Nếu **nhấn "Decline"**, workflow sẽ lấy batch tin tức tiếp theo và gửi lại email phê duyệt.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Chạy workflow với **mode "Test"** để kiểm tra kết quả.
   - Kiểm tra email để xem nội dung đã định dạng như thế nào.
2. **Bật Active**:
   - Sau khi kiểm tra, chuyển workflow sang **mode "Active"**.
   - Cấu hình **Schedule Trigger** để chạy hàng ngày (ví dụ: `0 8 * * *` - 8h sáng hàng ngày).

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack/Telegram**:
   - Thay vì gửi email, bạn có thể gửi kết quả lên **Slack** hoặc **Telegram** bằng node `slack` hoặc `telegramBot`.
   - Cài đặt node `slack` và cấu hình credentials với token Slack.

2. **Lưu Log Hoạt Động**:
   - Sử dụng node `stickyNote` để lưu log các batch tin tức đã xử lý.
   - Giúp bạn theo dõi lịch sử và tránh trùng lặp.

3. **Gửi Báo Cáo Định Kỳ**:
   - Thêm node `gmail` hoặc `slack` để gửi **báo cáo tổng hợp** hàng tuần/month.
   - Ví dụ: "Tin tức được phê duyệt trong tuần này".

4. **Sử Dụng Model AI Khác**:
   - Thay `gpt-4o-mini` bằng model khác như `gpt-4` hoặc model từ Hugging Face (nếu self-hosted).

5. **Quản Lý Batch Lớn**:
   - Nếu muốn lấy nhiều hơn 10 tin tức/lần, tăng giá trị `num` trong SerpApi và điều chỉnh counter tương ứng.

---

### 📌 **Kết Luận**
Workflow này giúp bạn **tự động hóa hoàn toàn quá trình lấy tin tức, định dạng và phê duyệt**, tiết kiệm thời gian và tăng hiệu quả chia sẻ nội dung. **Không cần viết code**, chỉ cần cấu hình các credentials và chạy định kỳ.

:::success[**Hành Động Tiếp Theo**]
1. **Cài đặt n8n trên VPS** (nếu chưa có).
2. **Import workflow** và cấu hình credentials.
3. **Test run** và kiểm tra email phê duyệt.
4. **Bật Schedule Trigger** để chạy hàng ngày.
5. **Tận hưởng thời gian** mà trước đây bạn phải dành cho việc lọc tin tức!

**Bắt đầu ngay hôm nay và làm cho công việc của mình trở nên đơn giản hơn!** 🚀
:::

---
**🔗 [Tải workflow nguyên bản](https://n8n.io/workflows/8464)** | **📌 [Cài đặt n8n trên VPS](https://docs.n8n.io/hosting/self-hosting-on-a-vps/)**