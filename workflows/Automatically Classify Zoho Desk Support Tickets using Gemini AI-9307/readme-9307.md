---
title: "🤖 Tự Động Hóa Phân Loại Tickets Zoho Desk Bằng AI Gemini - Giảm Thời Gian Làm Việc 80%!"
description: "Workflow tự động phân loại tickets hỗ trợ Zoho Desk bằng AI Gemini, giảm thiểu công việc thủ công và tăng cường hiệu quả phản hồi cho khách hàng. Đảm bảo tất cả tickets mới được phân loại chính xác ngay từ đầu, tiết kiệm thời gian và giảm sai sót."
slug: "tu-dong-hoa-phan-loai-tickets-zoho-desk-bang-gemini"
tags: [n8n, automation, zoho-desk, ai-gemini, no-code, chatbot-ai]
keywords: [tự động hóa zoho desk, phân loại tickets bằng ai, gemini n8n, giảm thời gian phản hồi, workflow zoho desk, tự động hóa hỗ trợ khách hàng]
---

# 🚀 **Tự Động Hóa Phân Loại Tickets Zoho Desk Bằng AI Gemini – Giải Pháp Tiết Kiệm Thời Gian Cho Các Sếp**

### **Nỗi Đau Của Các Sếp Hiện Nay**
Các sếp quản lý bộ phận hỗ trợ khách hàng (CS) hay team IT thường phải mất **giờ đồng hồ** mỗi ngày để phân loại tickets mới từ Zoho Desk. Việc này không chỉ tốn thời gian mà còn dễ gây **sai sót** khi phân loại thủ công, dẫn đến:
- **Trễ phản hồi** cho khách hàng (giảm trải nghiệm và doanh số).
- **Sự mất tập trung** của team khi phải làm việc lặp đi lặp lại.
- **Không tối ưu hóa** công việc cho các vấn đề ưu tiên cao.

**Workflow này giải quyết tất cả đó!** Bằng cách sử dụng **AI Gemini** (mô hình chatbot tiên tiến của Google), workflow tự động phân loại **tất cả tickets chưa được phân loại** trong Zoho Desk, giúp các sếp **tiết kiệm 80% thời gian** và **tăng cường hiệu quả phản hồi**.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng. Điều này đảm bảo:
✅ **Tính bảo mật cao** (không phụ thuộc vào cloud miễn phí).
✅ **Tốc độ xử lý nhanh** (không bị giới hạn request).
✅ **Dễ dàng mở rộng** (thêm node, API, hoặc kết nối với nhiều dịch vụ khác).

👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** – giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đảm bảo ổn định cho AI)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian** phân loại tickets thủ công.
- **Phân loại chính xác** hơn nhờ AI Gemini (giảm sai sót đến **95%**).
- **Hỗ trợ khách hàng nhanh chóng** (tickets được phân loại ngay lập tức).
- **Tự động hóa liên tục** (không cần can thiệp thủ công).
- **Cá nhân hóa phản hồi** (AI phân loại dựa trên nội dung cụ thể).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Zoho Desk** (đã cấu hình OAuth2).
2. **API Key OpenRouter** (để kết nối với mô hình AI Gemini).
3. **Thông tin OAuth2 cho Zoho Desk** (xem hướng dẫn chi tiết [ở đây](https://gist.github.com/Julian194/7c0ef5abaa5e3850f2bcc0a51bcd4633)).
4. **N8n Self-hosted** (để chạy workflow 24/7).

---
:::note[LƯU Ý QUAN TRỌNG]
- **Không cần code** – workflow hoàn toàn **no-code**.
- **Hỗ trợ phân trang** (lấy tất cả tickets, không giới hạn).
- **Lọc tickets chưa phân loại** (tránh reprocessing).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có **2 cách** để import workflow:
- **Tải file JSON** từ [n8n.io/workflows/9307](https://n8n.io/workflows/9307) và import vào **n8n Editor**.
- **Copy/paste JSON** từ link trên vào **n8n Editor** (tab "Import").

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này gồm **9 node** chính, các sếp cần chú ý cấu hình sau:

##### **A. Cấu Hình OAuth2 Zoho Desk (Quá Trình Khó Khăn Nhất)**
- **Node "Get threads" & "Get first thread"**: Sử dụng **HTTP Request** để lấy tickets từ Zoho Desk.
- **Cần thiết**:
  - **Client ID & Client Secret** (từ OAuth2 Zoho Desk).
  - **Refresh Token** (để lấy access token mới).
  - **Base URL**: `https://desk.zoho.com/api/v1/`

🔹 **Hướng dẫn OAuth2 chi tiết**: [Tại đây](https://gist.github.com/Julian194/7c0ef5abaa5e3850f2bcc0a51bcd4633)

##### **B. Cấu Hình AI Gemini (OpenRouter)**
- **Node "OpenRouter Chat Model"**:
  - **Credentials**: Chọn `openRouterApi` (đã cấu hình trước).
  - **Model**: `google/gemini-2.5-flash-lite-preview-09-2025` (mô hình nhẹ nhưng hiệu quả).
  - **Prompt mặc định**:
    ```plaintext
    Classify the following Zoho Desk ticket into one of these categories:
    - Content
    - Contract
    - Invoice
    - Featured Products
    - Affiliate-Partner
    - Bug
    - Feature
    - Other

    Ticket Title: {{ $json["ticket"]["title"] }}
    Ticket Content: {{ $json["ticket"]["description"] }}
    ```
  - **Nếu muốn thay đổi danh mục**, chỉnh sửa **node "Filter classification = null"** (Code Node).

##### **C. Cấu Hình Phân Loại & Cập Nhật Ticket**
- **Node "Classify" (ChainLLM)**: AI sẽ trả về **danh mục phân loại** (ví dụ: "Bug").
- **Node "Update Ticket"**: Cập nhật **trường `classification`** trong Zoho Desk.
  - **Headers**: `Authorization: Bearer {{ $node["Get first thread"].json["access_token"] }}`
  - **Body**:
    ```json
    {
      "classification": "{{ $node["Classify"].json["response"] }}"
    }
    ```

##### **D. Pagination (Lấy Tất Cả Tickets)**
- **Node "Fetch All Tickets"**: Sử dụng **`from` parameter** để lấy **100 ticket/trang**.
- **Dừng khi**: `data.length === 0` hoặc `< 100` (tránh lỗi API).

---
#### **3. Kích Hoạt ⚡️**
1. **Test Run** với **1-2 ticket mẫu** để kiểm tra:
   - AI phân loại có chính xác không?
   - Cập nhật Zoho Desk thành công không?
2. **Bật Active** workflow sau khi kiểm tra thành công.

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Thêm Slack/Telegram Notifications**:
   - Sau khi phân loại, gửi thông báo **tickets mới** qua Slack/Telegram để team CS biết.
   - **Node thêm**: `n8n-nodes-base.slack` hoặc `n8n-nodes-base.telegram`.

2. **Lưu Log Phân Loại**:
   - Sử dụng **Google Sheets** hoặc **Notion** để lưu lịch sử phân loại.
   - **Node thêm**: `n8n-nodes-base.googleSheets`.

3. **Báo Cáo Định Kỳ**:
   - Tạo **báo cáo hàng tuần** về số lượng tickets phân loại, thời gian phản hồi trung bình.
   - **Node thêm**: `n8n-nodes-base.email` (gửi báo cáo tự động).

4. **Tối Ưu Hóa Prompt AI**:
   - Nếu muốn phân loại **ưu tiên cao** (ví dụ: "Urgent"), chỉnh sửa prompt:
     ```plaintext
     Classify as "Urgent" if the ticket contains keywords: "emergency", "critical", "urgent".
     ```

5. **Kết Nối Với CRM Khác**:
   - Nếu sử dụng **HubSpot, Salesforce**, có thể tự động chuyển **tickets phân loại** sang CRM tương ứng.

---
### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp và team CS, đồng thời **tăng cường hiệu quả phản hồi** cho khách hàng. Bằng cách **tự động hóa phân loại tickets bằng AI Gemini**, các sếp không chỉ **giảm thiểu sai sót** mà còn **tối ưu hóa công việc** một cách hoàn toàn tự động.

**Hành động ngay hôm nay!**
1. **Import workflow** và cấu hình OAuth2 Zoho Desk.
2. **Test với 1-2 ticket** để đảm bảo hoạt động.
3. **Bật Active** và **nghỉ ngơi** – AI sẽ làm việc thay các sếp!

👉 **[Tải workflow ngay](https://n8n.io/workflows/9307)** và **cài đặt VPS n8n** để bắt đầu tự động hóa!

---
**Cần hỗ trợ thêm?**
- **Đăng ký tư vấn miễn phí** với Julian Kaiser (tác giả workflow): [Book a call](https://calendly.com/julian-kaiser).
- **Hỏi đáp cộng đồng**: [n8n Community](https://community.n8n.io/).