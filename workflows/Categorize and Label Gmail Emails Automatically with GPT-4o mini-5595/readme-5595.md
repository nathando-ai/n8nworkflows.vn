---
title: "🤖 Tự Động Phân Loại & Nhãn Gmail với AI GPT-4o mini – Không Cần Code!"
description: "Workflow tự động hóa phân loại và gán nhãn cho email Gmail mới bằng AI GPT-4o mini, tiết kiệm thời gian quản lý hàng trăm tin nhắn hàng ngày. Hoạt động 24/7, chính xác và cá nhân hóa."
slug: "tieu-dong-phan-loai-nhan-gmail-voi-gpt-4o-mini"
tags: [n8n, automation, gmail, ai, gpt-4o-mini, no-code, ticket-management]
keywords: [tự động hóa gmail, phân loại email bằng ai, gpt-4o mini n8n, tự động gán nhãn email, workflow gmail ai, quản lý email hiệu quả]
---

# 🚀 **Tự Động Phân Loại & Nhãn Gmail với AI GPT-4o mini – Không Cần Code!**

### **Giải pháp cho những người nhận hàng trăm email mỗi ngày**
Làm thủ công phân loại email là một việc **tốn thời gian, dễ mắc lỗi** và không thể hoạt động liên tục. Với **workflow này**, các sếp sẽ tự động:
- **Phân loại email mới** vào các danh mục chính xác (Tài chính, Du lịch, Tin tức,...) bằng AI GPT-4o mini.
- **Gán nhãn tự động** cho từng email, giúp tìm kiếm và quản lý dễ dàng hơn.
- **Tiết kiệm 3-5 tiếng mỗi tuần** cho việc sắp xếp email thủ công.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không phải phân loại email thủ công hàng ngày.
- **Chính xác cao**: AI phân loại dựa trên nội dung, giảm sai sót.
- **Tự động hóa hoàn toàn**: Hoạt động 24/7, không cần can thiệp.
- **Quản lý dễ dàng**: Email được sắp xếp theo nhãn, tìm kiếm nhanh chóng.
- **Cá nhân hóa**: Thêm/loại bỏ danh mục tùy ý.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Gmail** đã kết nối với n8n (thông qua OAuth2).
2. **Nhãn Gmail** đã tạo sẵn với các tên:
   - `Work` (Làm việc)
   - `Personal` (Cá nhân)
   - `Finance` (Tài chính)
   - `Shopping` (Mua sắm)
   - `Travel` (Du lịch)
   - `Newsletters` (Tin tức)
   - `Others` (Khác)
3. **API Key OpenAI** với quyền truy cập vào mô hình **GPT-4o mini**.
4. **n8n Workflow Editor** (cài đặt [n8n Community](https://n8n.io/) hoặc [n8n Cloud](https://n8n.io/cloud/)).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/5595) hoặc copy/paste JSON vào **n8n Editor**.
- **Cách import**:
  1. Mở **n8n Workflow Editor**.
  2. Nhấn **Import** (icon "↗️" ở góc trên bên phải).
  3. Chọn file JSON hoặc dán JSON vào ô **Paste JSON**.
  4. Nhấn **Import**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflows này bao gồm **13 node**, các sếp cần chú ý cấu hình sau:

##### **📬 Gmail Trigger (Node 1)**
- **Cấu hình**:
  - Chọn **credentials**: `gmailOAuth2` (đã cấu hình trước khi import).
  - **Interval**: Đặt thời gian kiểm tra email mới (ví dụ: **mỗi 5 phút** để không quá tải API).
  - **Filter**: Chỉ kích hoạt khi email **không có nhãn nào**.

##### **🤖 AI Agent (GPT-4o mini) + Structured Output Parser (Node 2-4)**
- **Node "OpenAI Chat Model2"**:
  - Chọn **credentials**: `openAiApi` (đã cấu hình API Key OpenAI).
  - **Model**: Đảm bảo chọn `gpt-4o-mini` (không thay đổi).
- **Node "Give a Label AI Agent"**:
  - **Prompt**: Cần **tùy chỉnh** để phù hợp với danh mục của các sếp. Ví dụ:
    ```plaintext
    Bạn là một trợ lý AI phân loại email. Dựa trên nội dung email, hãy trả về một nhãn trong danh sách sau:
    - Work (Làm việc)
    - Personal (Cá nhân)
    - Finance (Tài chính)
    - Shopping (Mua sắm)
    - Travel (Du lịch)
    - Newsletters (Tin tức)
    - Others (Khác)

    Trả về kết quả dưới dạng JSON:
    { "email_label": "Tên nhãn phù hợp" }
    ```
- **Node "Structured Output Parser1"**:
  - Đảm bảo **format output** là JSON như trên để Switch Node hoạt động.

##### **🔀 Switch Node (Node 5)**
- **Cấu hình**:
  - **Key**: Chọn `$.email_label` (lấy từ output của AI).
  - **Conditions**:
    - `Work`: Nếu `email_label` = "Work".
    - `Personal`: Nếu `email_label` = "Personal".
    - `Finance`: Nếu `email_label` = "Finance".
    - `Shopping`: Nếu `email_label` = "Shopping".
    - `Travel`: Nếu `email_label` = "Travel".
    - `Newsletters`: Nếu `email_label` = "Newsletters".
    - `Others`: Nếu `email_label` = "Others".

##### **🏷️ Gmail Label Nodes (Node 6-12)**
- **Mỗi node** (`Work`, `Personal`, `Finance`,...) đều tương ứng với một nhãn Gmail.
- **Cấu hình**:
  - Chọn **credentials**: `gmailOAuth2`.
  - **Operation**: `addLabels`.
  - **Label Name**: Điền **tên nhãn chính xác** (không có khoảng trắng hoặc ký tự đặc biệt).

#### **3. Kích hoạt ⚡️**
- **Test Run**:
  - Gửi một email mẫu (không có nhãn) vào Gmail.
  - Chạy **Manual Execution** trên node **Gmail Trigger** để kiểm tra.
  - Kiểm tra email đã được gán nhãn đúng không.
- **Bật Active**:
  - Sau khi test thành công, nhấn **Active** trên workflow.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tùy chỉnh danh mục**:
   - Thêm/loại bỏ nhãn trong **AI Agent** và **Switch Node** theo nhu cầu.
   - Ví dụ: Thêm `Support` (Hỗ trợ) hoặc `Urgent` (Khẩn cấp).

2. **Lưu log hoạt động**:
   - Thêm **Sticky Note** hoặc **Google Sheets** để ghi lại lịch sử phân loại.
   - Cài đặt **node `n8n-nodes-base.googleSheets`** để lưu dữ liệu phân loại.

3. **Gửi báo cáo định kỳ**:
   - Kết hợp với **Slack/Telegram** để thông báo khi có email mới được phân loại.
   - Sử dụng **node `n8n-nodes-base.slack`** hoặc `n8n-nodes-base.telegram`.

4. **Optimize API Call**:
   - Nếu nhận nhiều email, giảm **interval** của Gmail Trigger xuống **10-15 phút** để tránh bị giới hạn API.

5. **Sử dụng mô hình AI khác**:
   - Thay thế `gpt-4o-mini` bằng `gpt-3.5-turbo` (rẻ hơn) nếu không cần độ chính xác cao.

---

### 📌 **Kết luận**
Workflows này **giải phóng thời gian** cho các sếp khỏi việc phân loại email thủ công, đồng thời **tăng cường hiệu suất quản lý** với sự hỗ trợ của AI. **Chỉ cần import, cấu hình và bật hoạt động** – không cần code!

👉 **Hãy áp dụng ngay** và tự động hóa quản lý email của mình! Nếu cần hỗ trợ tùy chỉnh, liên hệ với **Arlin Perez** qua [LinkedIn](https://www.linkedin.com/in/arlin-perez/) để được hỗ trợ chi tiết.

---
**Chúc các sếp thành công!** 🚀