---
title: "🤖 **Tự Động Hóa Phân Loại Giao Dịch Revolut Bằng GPT-4 + Supabase – Không Cần Code!**"
description: "Workflow này tự động phân loại giao dịch Revolut thành danh mục chi tiêu (thuê nhà, ăn uống, học tập...) bằng trí tuệ nhân tạo GPT-4, đồng thời lưu trữ kết quả vào Supabase. Giúp các sếp tiết kiệm **10+ giờ/tháng** quản lý tài chính cá nhân hoặc doanh nghiệp."
slug: "tu-dong-hoa-phan-loai-giao-dich-revolut-gpt-4-supabase"
tags: [n8n, automation, no-code, GPT-4, Supabase, tài chính cá nhân, AI phân loại]
keywords: [n8n workflow Revolut, tự động hóa phân loại giao dịch, GPT-4 phân loại chi tiêu, Supabase tự động hóa tài chính, lưu trữ giao dịch Revolut]
---

# 🚀 **Tự Động Hóa Phân Loại Giao Dịch Revolut Bằng GPT-4 + Supabase**

### **Giải pháp cho ai?**
Các sếp đang **mệt mỏi** với việc:
- **Làm thủ công** phân loại hàng trăm giao dịch Revolut hàng tháng (thuê nhà, ăn uống, học tập, giải trí...).
- **Không biết** giao dịch nào là **đăng ký tự động** (subscription) hay **chuyển nội bộ** (internal transfer).
- **Không có hệ thống** để theo dõi chi tiêu theo danh mục, dẫn đến **quên chi tiêu** hoặc **tính sai ngân sách**.
- **Không muốn code** nhưng muốn tự động hóa quy trình này.

**Workflow này sẽ:**
✅ **Tự động tải** file CSV từ Google Drive (được export từ Revolut).
✅ **Phân loại giao dịch** thành danh mục chi tiêu chính xác bằng **GPT-4** (không cần viết code).
✅ **Lưu trữ kết quả** vào **Supabase** (hoặc cơ sở dữ liệu khác) để **theo dõi dài hạn**.
✅ **Loại bỏ giao dịch trùng lặp** bằng thuật toán hash.
✅ **Tích hợp với các công cụ BI** (Google Sheets, Tableau) để **báo cáo chi tiêu** một cách chuyên nghiệp.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài **n8n trên VPS riêng** (Self-hosted) để tránh giới hạn của phiên bản cloud.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**).
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đủ sức mạnh cho workflow này).
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tháng** so với cách làm thủ công.
- **Chính xác 95%+** trong phân loại giao dịch (so với cách phân loại bằng mắt).
- **Loại bỏ giao dịch trùng lặp** (như chuyển khoản nội bộ) tự động.
- **Nhận báo cáo chi tiêu** theo danh mục (thuê nhà, ăn uống, học tập...) chỉ với **1 click**.
- **Kết hợp với Slack/Telegram** để **cảnh báo chi tiêu quá mức**.
- **Mở rộng** cho **doanh nghiệp** (phân loại chi tiêu cho team).
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Revolut** (để export file CSV giao dịch).
2. **Google Drive** (để lưu file CSV từ Revolut).
3. **Supabase** (để lưu trữ giao dịch và danh mục phân loại).
   - **Bảng `transactions`** (để lưu giao dịch).
   - **Bảng `categories`** (để lưu danh mục chi tiêu).
4. **API Key OpenAI** (để sử dụng **GPT-4.1-mini**).
5. **Tài khoản n8n** (cài đặt trên VPS hoặc dùng phiên bản cloud).

---
:::note[CHUẨN BỊ SUPABASE]
Các sếp cần tạo **2 bảng cơ bản** trong Supabase:
- **`transactions`** (cột: `id`, `amount`, `description`, `category`, `is_subscription`, `is_internal`).
- **`categories`** (cột: `id`, `name`, `description`).
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có **2 cách** để import workflow này:
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/8807) và import vào **n8n Editor**.
- **Copy JSON** từ link trên và **paste** vào **n8n Editor** (tab `Import`).

👉 **Lưu ý:** Workflow này **không hoạt động ngay** sau khi import. Các sếp cần **cấu hình các node** như hướng dẫn dưới đây.

---

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

##### **A. Node `Download extract` (Google Drive)**
- **Cấu hình:**
  - **Credentials:** Chọn `googleDriveOAuth2Api` (đã cấu hình trước khi import).
  - **File ID:** Đặt vào **ID của file CSV từ Revolut** (được export từ [Revolut Dashboard](https://www.revolut.com/dashboard/)).
  - **Folder ID:** Nếu lưu trong thư mục cụ thể, điền **Folder ID** của thư mục đó.

👉 **Lấy File ID & Folder ID:**
1. Mở file CSV trên Google Drive.
2. **Chia sẻ** file (đặt quyền là "Ai có liên kết").
3. **Sao chép link** và **tách phần `id=`** (ví dụ: `https://drive.google.com/file/d/FILE_ID/view?usp=sharing` → `FILE_ID`).

##### **B. Node `Create a row` (Supabase - Insert Transactions)**
- **Cấu hình:**
  - **Credentials:** Chọn `supabaseApi`.
  - **Table:** Chọn `transactions`.
  - **Columns to insert:**
    - `amount` (số tiền giao dịch).
    - `description` (mô tả giao dịch).
    - `category` (danh mục sẽ được AI phân loại sau).
    - `is_subscription` (flag cho giao dịch đăng ký tự động).
    - `is_internal` (flag cho chuyển khoản nội bộ).

##### **C. Node `gpt-4.1-mini` (OpenAI LLM)**
- **Cấu hình:**
  - **Credentials:** Chọn `openAiApi` (đã cấu hình API Key OpenAI).
  - **Model:** Đặt là `gpt-4.1-mini` (rẻ hơn GPT-4 nhưng vẫn hiệu quả).
  - **Prompt:** Workflow đã **sẵn sàng** với prompt phân loại giao dịch. **Không cần chỉnh sửa** (nếu muốn tối ưu, các sếp có thể **thêm/loại danh mục** trong bảng `categories` ở Supabase).

##### **D. Node `Extract merchant` (Code Node)**
- **Lưu ý:** Node này **tự động trích xuất tên merchant** từ mô tả giao dịch (ví dụ: "Starbucks Coffee" → "Starbucks").
- **Không cần chỉnh sửa** (nếu muốn cải tiến, các sếp có thể mở node này và **sửa logic** bằng JavaScript).

##### **E. Node `Uniq Hash` (Crypto Node)**
- **Lưu ý:** Node này **tạo hash duy nhất** cho mỗi giao dịch để **tránh trùng lặp** khi insert vào Supabase.
- **Không cần chỉnh sửa** (nếu muốn thay đổi thuật toán, các sếp có thể **sửa code** trong node này).

##### **F. Node `Manual Trigger` (Bắt đầu workflow)**
- **Lưu ý:** Workflow này **bắt đầu bằng nút "Execute workflow"** (manual trigger).
- **Các sếp có thể thay thế** bằng:
  - **Schedule Node** (để chạy tự động hàng ngày).
  - **Webhook Node** (để gọi từ ứng dụng khác).

---
#### **3. Kích hoạt ⚡️**
1. **Test run** với **1 giao dịch mẫu** (ví dụ: "Starbucks Coffee - 5.99 EUR").
2. **Kiểm tra kết quả** trong Supabase:
   - Bảng `transactions` nên có **danh mục phân loại** (ví dụ: "Eating Out").
   - Bảng `categories` nên có **danh mục mới** (nếu giao dịch không thuộc danh mục cũ).
3. **Bật Active** workflow.

---
### ✍️ **Mẹo & gợi ý nâng cao**
#### **1. Tích hợp với Slack/Telegram để báo cáo chi tiêu**
- **Sử dụng node `slack` hoặc `telegram`** để gửi **báo cáo chi tiêu hàng tháng**.
- **Ví dụ:**
  ```json
  {
    "text": "📊 Báo cáo chi tiêu tháng {{ $date.format('MM-YYYY') }}:\n- Thuê nhà: {{ $sum.amount }} EUR\n- Ăn uống: {{ $sum2.amount }} EUR\n- Học tập: {{ $sum3.amount }} EUR"
  }
  ```
  (Sử dụng **node `aggregate`** để tính tổng chi tiêu theo danh mục).

#### **2. Lưu log vào Google Sheets**
- **Sử dụng node `googleSheets`** để lưu **lịch sử phân loại** (giúp theo dõi sai sót của AI).
- **Cấu hình:**
  - **Sheet Name:** `Revolut_Transactions_Log`.
  - **Columns:** `Date`, `Transaction`, `Category`, `Confidence_Score`.

#### **3. Xây dựng dashboard theo dõi chi tiêu**
- **Kết nối Supabase với:**
  - **Google Data Studio** (báo cáo chi tiêu).
  - **Tableau/Power BI** (tối ưu hóa chi tiêu doanh nghiệp).
- **Ví dụ:**
  - **Biểu đồ chi tiêu theo tháng**.
  - **Báo cáo chi tiêu cao nhất** (cảnh báo chi tiêu quá mức).

#### **4. Cải tiến prompt cho GPT-4**
- Nếu **GPT-4 phân loại sai**, các sếp có thể:
  - **Thêm/loại danh mục** trong bảng `categories` ở Supabase.
  - **Sửa prompt** trong node `chainLlm` (mở node và chỉnh sửa **JavaScript**).

#### **5. Chạy tự động hàng ngày**
- Thay thế **Manual Trigger** bằng **Schedule Node**:
  - **Cron:** `0 0 * * *` (chạy hàng ngày lúc 00:00).
  - **Timezone:** Chọn **Việt Nam (Asia/Ho_Chi_Minh)**.

---
### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi việc **phân loại giao dịch Revolut thủ công**, đồng thời **tối ưu hóa quản lý tài chính** bằng trí tuệ nhân tạo **GPT-4** và cơ sở dữ liệu **Supabase**.

👉 **Bắt đầu ngay!**
1. **Import workflow** từ [đây](https://n8n.io/workflows/8807).
2. **Cấu hình Google Drive, Supabase, OpenAI**.
3. **Chạy test** và **bắt đầu tự động hóa**!

**Nếu có vấn đề**, các sếp có thể:
- **Đăng câu hỏi** trên [Community n8n](https://community.n8n.io/).
- **Mở issue** trên [GitHub](https://github.com/n8n-io/n8n/issues).

---
**🚀 Hãy tự động hóa tài chính của mình ngay hôm nay!** 🚀