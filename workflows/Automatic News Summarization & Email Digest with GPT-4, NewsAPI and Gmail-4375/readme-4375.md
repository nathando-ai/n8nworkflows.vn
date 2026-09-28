---
title: "🚀 Tự Động Hóa Tóm Tắt Tin Tức AI + Email Digest Hàng Ngày Với GPT-4, NewsAPI & Gmail"
description: "Workflow tự động hóa lấy tin tức mới nhất từ NewsAPI, tóm tắt bằng GPT-4, và gửi email tổng hợp cá nhân hóa cho danh sách người nhận. Giúp tiết kiệm 10+ giờ/tháng cho các sếp làm newsletter, tổ chức hoặc content curator."
slug: "tieu-dong-hoa-tom-tat-tin-tuc-ai-email-digest"
tags: [n8n, automation, ai, marketing, email-digest]
keywords: [n8n workflow tự động hóa tin tức, GPT-4 tóm tắt tin tức, email digest tự động, NewsAPI + Gmail, tự động hóa newsletter]
---

# 🚀 **Tự Động Hóa Tóm Tắt Tin Tức AI + Email Digest Hàng Ngày**

### **Giải pháp cho các sếp bị "ngập" trong công việc thủ công:**
Làm sao để **tự động hóa việc tổng hợp tin tức hàng ngày**, **tóm tắt bằng trí tuệ nhân tạo**, và **gửi email cá nhân hóa** cho đội ngũ, khách hàng hoặc độc giả mà **không cần viết code**? Hãy tưởng tượng:
- **Tiết kiệm 10+ giờ/tháng** để tìm tin tức, tóm tắt và gửi email.
- **Cung cấp tin tức chính xác và tóm tắt** bằng GPT-4, thay vì phải đọc hàng chục bài viết.
- **Cá nhân hóa email** với tên người nhận, giúp tăng tỷ lệ mở và tương tác.
- **Hoạt động 24/7** mà không cần can thiệp thủ công.

Workflow này **không chỉ dành cho newsletter**, mà còn phù hợp cho:
✔ **Doanh nghiệp** muốn cập nhật tin tức cho nhân viên.
✔ **Tổ chức** cần tổng hợp thông tin cho các cuộc họp.
✔ **Content curator** muốn chuyển đổi tin tức thành nội dung dễ tiêu thụ.

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Thay vì tóm tắt 50 bài tin mỗi ngày, AI làm việc đó cho bạn.
- **Tin tức chính xác và tóm tắt**: GPT-4 tạo ra **5 điểm chính** từ mỗi bài tin, giúp đọc nhanh hơn 300%.
- **Email cá nhân hóa**: Gửi với tên người nhận (ví dụ: *"Chào [Tên], đây là tin tức mới nhất..."*), tăng tỷ lệ mở lên **20-30%**.
- **Hoạt động tự động**: Chỉ cần bật workflow, nó sẽ **lấy tin tức, tóm tắt và gửi email** theo lịch trình.
- **Dễ dàng mở rộng**: Thêm nhiều nguồn tin, thay đổi lịch trình hoặc kết nối với Mailchimp.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản NewsAPI** (miễn phí):
   - Đăng ký tại [newsapi.org](https://newsapi.org/) và lấy **API Key**.
   - Lưu ý: Đăng ký tài khoản **miễn phí** chỉ cho phép lấy **100 request/ngày**. Nếu cần nhiều hơn, nâng cấp lên **Pro** (~$50/năm).
   - *Gợi ý*: Sử dụng **API Key** cho **US news** (mặc định trong workflow).

2. **Tài khoản OpenAI** (miễn phí):
   - Đăng ký tại [openai.com](https://openai.com/) và lấy **API Key**.
   - Chọn mô hình **GPT-4o-mini** (rẻ và hiệu quả cho tóm tắt tin tức).
   - *Lưu ý*: Nếu vượt quá hạn mức miễn phí, có thể chuyển sang **GPT-4 Turbo** (tùy chọn trong workflow).

3. **Google Sheets** (quản lý danh sách email):
   - Tạo một **Google Sheet** với **2 cột**:
     - **Name** (tên người nhận, để cá nhân hóa email).
     - **Email** (địa chỉ email của người nhận).
   - *Ví dụ*:
     | Name       | Email               |
     |------------|---------------------|
     | Nguyễn Văn A | a@example.com       |
     | Trần Thị B  | b@example.com       |

4. **Tài khoản Gmail** (gửi email):
   - Đăng nhập vào **Gmail** và cấp quyền cho n8n thông qua **OAuth2**.
   - *Lưu ý*: Email này sẽ là **nguồn gửi** cho tất cả người nhận. Nếu muốn gửi từ nhiều địa chỉ, cần thêm **các tài khoản Gmail khác** và cấu hình trong workflow.

5. **n8n Self-hosted** (khuyến nghị):
   :::info[Gợi ý hạ tầng cho n8n]
   Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng** (Self-hosted).
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
   :::
---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có **2 cách** để import workflow này:

**Cách 1: Từ file JSON**
1. Tải workflow từ [n8n.io/workflows/4375](https://n8n.io/workflows/4375) (ấn **Export**).
2. Trên **n8n Editor**, nhấn **Import** và chọn file JSON vừa tải.
3. Chọn **Self-hosted** (nếu cài trên VPS) hoặc **n8n.cloud** (nếu dùng miễn phí).

**Cách 2: Copy/Paste JSON**
1. Mở **n8n Editor** và chọn **Create new workflow**.
2. Nhấn **Import** → **Paste JSON** và dán nội dung từ [n8n.io/workflows/4375](https://n8n.io/workflows/4375) (ấn **Export** → **Copy JSON**).
3. Chọn **Self-hosted** và nhấn **Import**.

---

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Sau khi import, các sếp **phải cấu hình** các node sau để workflow hoạt động:

##### **A. Schedule Trigger (Lịch trình)**
- **Thời gian chạy mặc định**: **Mỗi 10 phút** (có thể thay đổi).
- **Lưu ý**:
  - Nếu muốn **chạy hàng ngày vào 8h sáng**, chỉnh thành:
    ```
    0 8 * * *
    ```
  - *Cú pháp*: `Phút Giây Ngày Tháng Tuần`.

##### **B. Pull News (Lấy tin tức từ NewsAPI)**
- **Node loại**: `httpRequest`
- **Cấu hình bắt buộc**:
  - **URL**:
    ```
    https://newsapi.org/v2/top-headlines?country=us&apiKey={{$node["NewsAPI Key"].json()["apiKey"]}}
    ```
    - Thay `us` bằng **mã quốc gia** cần lấy tin (ví dụ: `vn` cho Việt Nam, `uk` cho Anh).
  - **Headers**:
    - `Content-Type`: `application/json`
  - **Credentials**:
    - Tạo **1 credential mới** trong n8n với tên **"NewsAPI Key"**.
    - Điền **API Key** từ [newsapi.org](https://newsapi.org/).

##### **C. OpenAI Chat Model (Tóm tắt tin tức)**
- **Node loại**: `lmChatOpenAi`
- **Cấu hình bắt buộc**:
  - **Model**: `gpt-4o-mini` (mặc định).
  - **Prompt**:
    ```
    Tóm tắt bài tin này thành 5 điểm chính, ngắn gọn và rõ ràng. Đảm bảo không có thông tin sai lệch.
    ```
  - **Credentials**:
    - Tạo **1 credential mới** với tên **"OpenAI API Key"**.
    - Điền **API Key** từ OpenAI.

##### **D. Email list (Danh sách email từ Google Sheets)**
- **Node loại**: `googleSheets`
- **Cấu hình bắt buộc**:
  - **Spreadsheet ID**: Lấy từ liên kết Google Sheets (ví dụ: `https://docs.google.com/spreadsheets/d/1AbCdEfGhIjKlMnOpQrStUvWxYz/` → phần `1AbCdEfGhIjKlMnOpQrStUvWxYz`).
  - **Sheet Name**: Tên tab trong Google Sheets (ví dụ: `Subscriber List`).
  - **Range**: `A1:B` (lấy cả cột Name và Email).
  - **Credentials**:
    - Tạo **1 credential mới** với tên **"Google Sheets OAuth2"**.
    - Cấp quyền cho n8n truy cập vào Google Sheets.

##### **E. Send Mail (Gửi email)**
- **Node loại**: `gmail`
- **Cấu hình bắt buộc**:
  - **To**: `{{$node["Email list"].json()["email"]}}` (lấy email từ Google Sheets).
  - **Subject**: `Tin tức mới nhất - {{ $node["Pull News"].json()["title"] }}`.
  - **Body**:
    ```
    Chào {{ $node["Email list"].json()["name"] }},

    Đây là tin tức mới nhất được tổng hợp tự động:

    {{ $node["OpenAI Chat Model"].json()["content"] }}

    Trân trọng,
    [Tên của bạn/doanh nghiệp]
    ```
  - **Credentials**:
    - Tạo **1 credential mới** với tên **"Gmail OAuth2"**.
    - Đăng nhập vào Gmail và cấp quyền cho n8n.

---

#### **3. Kích hoạt ⚡️**
1. **Test Run** (kiểm tra trước khi bật):
   - Nhấn **Run Workflow** và chọn **Test Run**.
   - Kiểm tra:
     - Tin tức có được lấy không?
     - Tóm tắt có logic không?
     - Email có gửi được không?

2. **Bật Active**:
   - Sau khi test thành công, nhấn **Active** để workflow chạy tự động.

---

### ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Thêm nhiều nguồn tin tức**:
   - Sử dụng **NewsAPI** cho nhiều quốc gia (ví dụ: `country=vn&category=technology`).
   - Kết hợp với **RSS Feed** bằng node `httpRequest` để lấy tin từ các trang web khác.

2. **Cá nhân hóa email hơn**:
   - Thêm **đoạn giới thiệu cá nhân** vào email (ví dụ: *"Chào [Tên], đây là tin tức quan trọng nhất trong ngày..."*).
   - Sử dụng **node `template`** để định dạng email đẹp hơn.

3. **Lưu log hoạt động**:
   - Thêm **node `stickyNote`** để ghi lại lỗi hoặc kết quả.
   - Kết nối với **Google Sheets** để theo dõi lịch sử gửi email.

4. **Gửi báo cáo định kỳ**:
   - Thêm **node `scheduleTrigger`** khác để gửi **báo cáo tuần/Tháng** tổng hợp.
   - Ví dụ: *"Tin tức quan trọng nhất trong tuần"*.

5. **Kết nối với Mailchimp/ConvertKit**:
   - Thay vì gửi qua Gmail, kết nối với **Mailchimp** để quản lý danh sách và phân tích mở email.

6. **Thêm tính năng unsubscribe**:
   - Thêm **link unsubscribe** vào email và kết nối với **Google Sheets** để xóa email không muốn nhận.

7. **Tùy chỉnh lịch trình**:
   - Chạy workflow **hàng ngày vào 8h sáng** thay vì mỗi 10 phút.
   - Sử dụng **node `scheduleTrigger`** với `0 8 * * *` (8h sáng hàng ngày).
:::

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc thủ công tóm tắt tin tức và gửi email. Với **GPT-4, NewsAPI và Gmail**, bạn có thể:
✅ **Tự động hóa 100%** việc tổng hợp tin tức.
✅ **Tóm tắt bằng trí tuệ nhân tạo** chính xác và ngắn gọn.
✅ **Gửi email cá nhân hóa** với tỷ lệ mở cao.
✅ **Hoạt động 24/7** mà không cần can thiệp.

**Hành động ngay!**
1. **Cài đặt n8n trên VPS** (nếu chưa có).
2. **Import workflow** và cấu hình các credential.
3. **Test Run** và bật **Active**.
4. **Mở rộng** với các tính năng nâng cao như trên.

👉 **[Tải workflow ngay](https://n8n.io/workflows/4375)** và bắt đầu tự động hóa tin tức của mình!

---
**Chia sẻ & phản hồi**:
Nếu có **vấn đề** khi cấu hình, hãy để lại **comment** bên dưới hoặc liên hệ qua [TinoHost](https://tino.vn) để hỗ trợ kỹ thuật. Chúc các sếp thành công! 🚀