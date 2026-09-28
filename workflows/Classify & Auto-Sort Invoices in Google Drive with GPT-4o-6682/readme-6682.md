---
title: "📄 **Tự Động Phân Loại & Sắp Xếp Hóa Đơn Google Drive Bằng GPT-4o - Giảm 90% Thời Gian Làm Thủ Công**"
description: "Workflow tự động hóa phân loại hóa đơn PDF từ Google Drive thành 3 danh mục chính (Retail, Manufacturing, EdTech) bằng AI GPT-4o, giảm thiểu sai sót và tiết kiệm thời gian cho bộ phận tài chính. Hoàn toàn không cần code!"
slug: "tu-dong-phan-loai-hoa-don-google-drive-gpt-4o"
tags: [n8n, automation, no-code, google-drive, ai-gpt-4o, invoice-processing, langchain]
keywords: [n8n workflow tự động hóa hóa đơn, phân loại hóa đơn bằng AI, GPT-4o tự động hóa, sắp xếp hóa đơn Google Drive, tự động hóa tài chính không code]
---

# 🚀 **Tự Động Phân Loại & Sắp Xếp Hóa Đơn Google Drive Bằng GPT-4o**

### **Giải pháp AI cho bộ phận tài chính: Phân loại hóa đơn PDF chỉ trong vài giây!**
Hóa đơn PDF từ các nhà cung cấp khác nhau thường rải rác trong Google Drive, khiến việc quản lý và phân loại trở nên phức tạp. Các sếp phải mất **giờ đồng hồ** để đọc từng hóa đơn, phân loại theo ngành nghề (Retail, Manufacturing, EdTech) và di chuyển chúng vào thư mục phù hợp. **Workflow này tự động hóa toàn bộ quy trình bằng AI GPT-4o**, giúp tiết kiệm **90% thời gian** và giảm thiểu sai sót nhân sự.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian**: Không cần đọc thủ công từng hóa đơn.
- **Chính xác 100%**: AI GPT-4o phân loại dựa trên nội dung, tránh sai sót của con người.
- **Sắp xếp tự động**: Hóa đơn được di chuyển vào thư mục phù hợp (Retail, Manufacturing, EdTech) ngay lập tức.
- **Hoạt động liên tục**: Workflow chạy 24/7, không cần can thiệp thủ công.
- **Kết nối Google Drive**: Tích hợp hoàn toàn với Google Drive, không cần chuyển đổi file.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Drive** với quyền truy cập vào thư mục chứa hóa đơn.
2. **API Key Azure OpenAI** (để kết nối với GPT-4o-mini).
3. **Thư mục phân loại sẵn** trong Google Drive với 3 tên:
   - `Retail`
   - `Manufacturing`
   - `EdTech`
4. **n8n Self-hosted** (không dùng phiên bản cloud để đảm bảo bảo mật dữ liệu).
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Bước 1**: Tải file JSON của workflow từ [đây](https://n8n.io/workflows/6682) (hoặc copy JSON từ canvas).
- **Bước 2**: Mở **n8n Editor** → Nhấn **"Import"** → Dán JSON và chọn **"Import"**.
- **Bước 3**: Workflow sẽ xuất hiện trên canvas với 11 node.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflows này **không hoạt động ngay** sau khi import. Các sếp cần cấu hình các node quan trọng sau:

##### **A. Cấu hình Google Drive**
- **Node "Search files and folders"**:
  - Điền **ID thư mục** chứa hóa đơn (tham khảo cách lấy ID [tại đây](https://support.google.com/docs/answer/3093493?hl=vi)).
  - Chọn **OAuth2 Credential**: `googleDriveOAuth2Api` (cần tạo trước trong **Credentials** của n8n).

- **Node "Download File"**:
  - Sử dụng **file ID** từ node trước (`={{ $json.id }}`).
  - Đảm bảo **operation = "download"**.

- **Node "Manufacturing", "Retail", "EdTech"**:
  - Điền **ID thư mục đích** tương ứng (ví dụ: `folder_id_retail`, `folder_id_manufacturing`, `folder_id_edtech`).
  - Chọn **OAuth2 Credential**: `googleDriveOAuth2Api` (giống node trước).

##### **B. Cấu hình AI GPT-4o**
- **Node "Azure OpenAI Chat Model"**:
  - Điền **API Key Azure OpenAI** vào **Credentials** (`azureOpenAiApi`).
  - Chọn **Model**: `gpt-4o-mini` (đã cấu hình sẵn trong workflow).
  - **System Prompt** (nếu cần chỉnh sửa):
    ```json
    "You are an invoice classifier. Classify the following invoice into one of these categories: Retail, Manufacturing, or EdTech. Return ONLY the category name."
    ```

- **Node "AI Agent"**:
  - Kết nối với node **Azure OpenAI Chat Model**.
  - Đảm bảo **Loop Over Items** (`Split in Batches`) được cấu hình để xử lý từng hóa đơn một.

##### **C. Cấu hình Switch (Logic điều kiện)**
- **Node "Switch"**:
  - Cấu hình **3 branch** với điều kiện:
    - `Retail` → Route đến node `Retail`.
    - `Manufacturing` → Route đến node `Manufacturing`.
    - `EdTech` → Route đến node `EdTech`.
  - **Lưu ý**: Nếu AI phân loại sai, các sếp có thể chỉnh sửa **System Prompt** trong node Azure OpenAI.

#### **3. Kích hoạt ⚡️**
- **Bước 1**: Nhấn **"Execute workflow"** (node `manualTrigger`).
- **Bước 2**: Chọn **Test Run** với 1-2 hóa đơn mẫu để kiểm tra.
- **Bước 3**: Nếu hoạt động ổn, bật **Active** để workflow chạy tự động khi có file mới.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Lưu log hoạt động**:
   - Thêm node **n8n-nodes-base.httpRequest** sau node `Switch` để gửi thông báo về **Slack/Telegram** khi có hóa đơn mới được phân loại.
   - Ví dụ: Gửi tin nhắn `"Hóa đơn [Tên File] đã được phân loại vào [Danh mục]"` vào kênh Slack.

2. **Tự động xử lý hàng tuần**:
   - Sử dụng **n8n-nodes-base.cron** để chạy workflow **tự động hàng tuần** (ví dụ: Chủ nhật 8h sáng) để phân loại tất cả hóa đơn mới trong Google Drive.

3. **Kết hợp với Google Sheets**:
   - Thêm node **Google Sheets** sau node `Switch` để ghi kết quả phân loại vào bảng tính, giúp theo dõi dễ dàng.

4. **Chỉnh sửa System Prompt**:
   - Nếu AI phân loại không chính xác, cập nhật **System Prompt** trong node Azure OpenAI để rõ ràng hơn về yêu cầu phân loại.

---

### 📌 **Kết luận**
Workflow **Classify & Auto-Sort Invoices in Google Drive with GPT-4o** là giải pháp **tự động hóa hoàn toàn** cho bộ phận tài chính, giúp các sếp:
✅ **Tiết kiệm 90% thời gian** so với làm thủ công.
✅ **Tránh sai sót** nhờ AI GPT-4o phân loại chính xác.
✅ **Sắp xếp hóa đơn tự động** vào thư mục phù hợp.

**Hành động ngay!**
- **Import workflow** và cấu hình theo hướng dẫn trên.
- **Test với 1-2 hóa đơn** trước khi áp dụng toàn bộ.
- **Tích hợp với Slack/Telegram** để nhận báo cáo tự động.

**Nếu có vấn đề**, các sếp có thể tham khảo [câu hỏi thường gặp](https://docs.n8n.io/) hoặc liên hệ cộng đồng n8n trên [Discord](https://n8n.io/community). **Chúc các sếp thành công!** 🚀