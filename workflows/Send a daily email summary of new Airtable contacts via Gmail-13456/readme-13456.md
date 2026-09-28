---
title: "📧 Tự Động Hóa Email Tổng Kết Liên Hệ Khách Hàng Mới Airtable Hàng Ngày - Gmail"
description: "Giải pháp tự động hóa hoàn toàn không code giúp các sếp nhận được email tổng kết tất cả liên hệ mới được thêm vào Airtable mỗi ngày vào buổi tối, với định dạng bảng HTML sạch sẽ và chính xác. Tiết kiệm thời gian lên đến 30% cho công việc quản lý CRM."
slug: "tieu-dong-hoa-email-tong-ket-airtable-gmail"
tags: [n8n, automation, crm, airtable, gmail, no-code]
keywords: [tự động hóa email airtable, gửi email tổng kết hàng ngày, n8n workflow crm, tự động hóa quản lý khách hàng, tự động hóa gmail airtable]
---

# 🚀 Tự Động Hóa Email Tổng Kết Liên Hệ Khách Hàng Mới Airtable Hàng Ngày

### 🔍 **Nỗi Đau Của Các Sếp**
Quản lý liên hệ khách hàng thủ công trên Airtable là một công việc tốn thời gian và dễ bị bỏ qua. Các sếp phải:
- **Lặp đi lặp lại** mỗi ngày để kiểm tra và tổng kết mới liên hệ.
- **Mất thời gian** chuyển đổi dữ liệu từ Airtable sang email định dạng chuyên nghiệp.
- **Rủi ro sai sót** khi nhập liệu thủ công, dẫn đến thông tin không chính xác.

Workflow này **giải quyết hoàn toàn** vấn đề trên bằng cách tự động:
✅ **Lấy dữ liệu mới** từ Airtable mỗi ngày.
✅ **Chuyển đổi sang email HTML** sạch sẽ, dễ đọc.
✅ **Gửi tự động** vào buổi tối, giúp các sếp **tập trung vào công việc chiến lược** thay vì công việc thủ công.

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần kiểm tra Airtable hàng ngày.
- **Chính xác 100%**: Dữ liệu lấy trực tiếp từ Airtable, không sai sót.
- **Định dạng chuyên nghiệp**: Email với bảng HTML sạch sẽ, dễ đọc.
- **Hoạt động liên tục**: Gửi email tự động vào thời gian đã thiết lập.
- **Tích hợp hoàn toàn**: Không cần code, chỉ cần cấu hình đơn giản.
:::

---
### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Airtable**:
   - Một **Personal Access Token** với các scope sau:
     - `data.records:read`
     - `schema.bases:read`
   - [Tạo Token tại đây](https://airtable.com/create/tokens).
2. **Tài khoản Gmail**:
   - Tài khoản Gmail chính thức (không dùng tài khoản Google Workspace nếu không cần thiết).
3. **Workflow n8n**:
   - Cài đặt n8n trên **VPS riêng** (Self-hosted) để hoạt động 24/7.
   - [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).
4. **Bảng Airtable**:
   - Một **bảng liên hệ (Contacts)** đã được tạo sẵn trong Airtable.
:::

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. **Tải file JSON** từ [n8n.io/workflows/13456](https://n8n.io/workflows/13456).
2. Trong **n8n Editor**, chọn **Import Workflow** và chọn file JSON tải xuống.
   *Hoặc* copy toàn bộ JSON và paste vào **Import Workflow** từ menu.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này bao gồm **4 node chính**, các sếp cần chú ý cấu hình sau:

##### **Node 1: Daily Evening Schedule (Trigger)**
- **Cấu hình thời gian**:
  - Mặc định là **11h tối hàng ngày**. Các sếp có thể thay đổi thời gian phù hợp (ví dụ: 8h sáng).
  - **Cách chỉnh**:
    - Nhấp vào node **Daily Evening Schedule** → **Edit**.
    - Chọn **Schedule Trigger** → **Edit**.
    - Thay đổi **Time** và **Time Zone** theo mong muốn.

##### **Node 2: Search Airtable Contacts**
- **Cấu hình Airtable**:
  - **Credentials**: Chọn **airtableTokenApi** (đã cấu hình trước khi import).
  - **Base ID & Table Name**:
    - Tìm **Base ID** của bảng Airtable trong URL: `https://airtable.com/<Base ID>/<Table Name>`.
    - Điền vào **Base ID** và **Table Name** trong node.
  - **Lọc dữ liệu mới**:
    - Thêm điều kiện lọc để lấy **chỉ mới liên hệ mới** (ví dụ: `createdTime > "2023-10-01T00:00:00.000Z"`).
    - **Gợi ý**:
      ```json
      {
        "filterByFormula": "AND({createdTime} > \"2023-10-01T00:00:00.000Z\")"
      }
      ```
    - Thay đổi ngày tháng theo ngày bắt đầu lấy dữ liệu.

##### **Node 3: Convert to HTML Table**
- **Cấu hình định dạng**:
  - Node này tự động chuyển đổi dữ liệu từ Airtable sang **HTML Table**.
  - Các sếp có thể **tùy chỉnh cột hiển thị** bằng cách chỉnh **Output Fields** trong node **Search Airtable Contacts** (ví dụ: chỉ hiển thị `Name`, `Email`, `Phone`).

##### **Node 4: Send Daily Contacts Email (Gmail)**
- **Cấu hình Gmail**:
  - **Credentials**: Chọn **gmailOAuth2** (đã cấu hình OAuth2 trong n8n).
  - **Người nhận (Recipient)**: Thay đổi địa chỉ email thành **email cá nhân** của các sếp.
  - **Tiêu đề email (Subject)**: Có thể chỉnh thành `"Tổng Kết Liên Hệ Mới Hôm Nay - [Ngày]"`.
  - **Nội dung email (Body)**:
    - Sử dụng **HTML Table** từ node trước để hiển thị dữ liệu.
    - **Gợi ý nội dung**:
      ```html
      <h2>Tổng Kết Liên Hệ Mới Hôm Nay</h2>
      <p>Dưới đây là danh sách liên hệ mới được thêm vào Airtable:</p>
      {{ $json["html"] }}
      <p>Trân trọng,<br>Hệ thống Tự Động Hóa</p>
      ```

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Chọn **Run Workflow** để kiểm tra dữ liệu mẫu.
   - Kiểm tra email đã được gửi đúng không.
2. **Bật Active**:
   - Sau khi kiểm tra thành công, **bật Active** để workflow hoạt động tự động hàng ngày.

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Gửi Email Định Kỳ Khác**:
   - Thay đổi thời gian trong **Schedule Trigger** để gửi email vào **sáng sớm** hoặc **buổi trưa**.

2. **Tích Hợp Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram Bot** để thông báo khi có liên hệ mới.
   - **Cách làm**:
     - Thêm node **Slack Webhook** sau node **Convert to HTML Table**.
     - Chỉnh **Message** để hiển thị thông báo ngắn gọn.

3. **Lưu Log Dữ Liệu**:
   - Thêm node **Google Sheets** hoặc **Airtable** để lưu lịch sử email đã gửi.
   - **Cách làm**:
     - Thêm node **Google Sheets** sau node **Send Email**.
     - Ghi dữ liệu như `Ngày`, `Số lượng liên hệ`, `Email đã gửi`.

4. **Tùy Chỉnh Nội Dung Email**:
   - Thêm **câu chào** hoặc **báo cáo tổng hợp** bằng cách sử dụng **LLM Node** (n8n-nodes-base.llm) để tự động sinh nội dung.
   - **Ví dụ**:
     ```json
     {
       "prompt": "Tóm tắt ngắn gọn về {{ $json["newContacts"].length }} liên hệ mới được thêm vào Airtable hôm nay."
     }
     ```

5. **Xử Lý Trùng Lặp**:
   - Thêm điều kiện lọc để **tránh gửi trùng lặp** nếu workflow bị ngắt.
   - **Cách làm**:
     - Thêm node **Set** trước node **Send Email** để lưu trạng thái đã gửi.
     - Sử dụng **If Condition** để kiểm tra trước khi gửi.

---
### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn **tự động hóa quản lý CRM** mà không cần code. Với chỉ **vài bước cấu hình**, các sếp sẽ:
✔ **Tiết kiệm thời gian** lên đến 30% cho công việc quản lý liên hệ.
✔ **Nhận email tổng kết** hàng ngày với định dạng chuyên nghiệp.
✔ **Hoạt động 24/7** mà không cần can thiệp thủ công.

**Hành động ngay hôm nay**:
1. **Cài đặt n8n trên VPS** (nếu chưa có).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Bật Active** và bắt đầu tự động hóa!

👉 [Xem Video Walkthrough](https://youtu.be/lQh1fuIrBN8) để hiểu rõ hơn về cách cấu hình.

---
:::note[CHÚ Ý]
- **Không sử dụng tài khoản Gmail cá nhân** cho mục đích thương mại (nếu có nhiều email gửi).
- **Kiểm tra spam** nếu email không đến được inbox.
- **Cập nhật token Airtable** nếu hết hạn (thường sau 1 năm).
:::