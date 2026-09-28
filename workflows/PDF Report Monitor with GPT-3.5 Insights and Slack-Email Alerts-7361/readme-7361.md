---
title: "🚀 Tự Động Hóa Theo Dõi Báo Cáo PDF với GPT-3.5 + Cảnh Báo Slack & Email (Không Cần Code)"
description: "Workflow tự động hóa theo dõi, phân tích nội dung báo cáo PDF bằng trí tuệ nhân tạo (GPT-3.5) và gửi cảnh báo tự động qua Slack và email. Giúp các sếp tiết kiệm thời gian theo dõi báo cáo hàng ngày, tránh bỏ lỡ thông tin quan trọng."
slug: "tu-dong-hoa-theo-doi-bao-cao-pdf-gpt-3-5-slack-email"
tags: [n8n, automation, ai-summarization, pdf-parsing, slack-alerts, email-automation, gpt-3.5, no-code]
keywords: [tự động hóa theo dõi báo cáo PDF, n8n workflow, cảnh báo Slack từ PDF, phân tích báo cáo bằng GPT-3.5, tự động hóa báo cáo doanh nghiệp, AI trong quản lý dữ liệu]
---

# 🚀 **Tự Động Hóa Theo Dõi Báo cáo PDF với GPT-3.5 + Cảnh Báo Slack & Email**

## **🔍 Nỗi Đau Của Các Sếp Khi Theo Dõi Báo Cáo PDF Thủ Công**
Hàng ngày, các sếp phải:
- **Quét qua hàng chục báo cáo PDF** để tìm thông tin quan trọng.
- **Bỏ lỡ thông tin nhạy cảm** vì quá tải công việc.
- **Tốn thời gian** để tóm tắt và chia sẻ kết quả với team.
- **Không biết cách phân tích hiệu quả** báo cáo dài dòng.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Quét và phân tích** tất cả báo cáo PDF mới trong thư mục FTP.
✅ **Tóm tắt nội dung chính** bằng GPT-3.5 (không cần viết code).
✅ **Gửi cảnh báo tự động** qua Slack và email khi có báo cáo mới.
✅ **Lưu lịch sử** để theo dõi đã xử lý những báo cáo nào.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm 5-10 giờ/tuần** theo dõi báo cáo thủ công.
- **Không bỏ lỡ bất kỳ thông tin quan trọng** nhờ cảnh báo tự động.
- **Nội dung báo cáo được tóm tắt chính xác** bằng trí tuệ nhân tạo.
- **Cảnh báo ngay lập tức** khi có báo cáo mới qua Slack và email.
- **Dữ liệu được lưu trữ an toàn** trong cơ sở dữ liệu PostgreSQL.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ TRƯỚC KHI SỬ DỤNG**]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản FTP** (để lưu trữ báo cáo PDF mới).
2. **API Key OpenAI** (để sử dụng GPT-3.5).
3. **Credentials Slack** (để gửi cảnh báo).
4. **Tài khoản email** (để gửi cảnh báo qua email).
5. **Cơ sở dữ liệu PostgreSQL** (để lưu lịch sử báo cáo đã xử lý).
6. **Tài khoản PDF Vector** (nếu muốn phân tích báo cáo chi tiết hơn).
7. **VPS n8n** (để chạy workflow 24/7).

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

## **🚀 Cách Import & Cấu Hình Workflow**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. **Tải file JSON** từ [link gốc](https://n8n.io/workflows/7361).
2. Trong **n8n Editor**, nhấn **Import** và chọn file JSON.
3. Hoặc **copy toàn bộ JSON** và dán vào **Import Workflow** trong n8n.

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflows này có **9 node chính**, các sếp cần cấu hình kỹ lưỡng:

#### **🔹 Node 1: Schedule Trigger (Check Every 15 Minutes)**
- **Cấu hình:** Chọn **15 phút** để workflow chạy tự động.
- **Lưu ý:** Đảm bảo n8n đang hoạt động 24/7 trên VPS.

#### **🔹 Node 2: Check Report Folder (FTP)**
- **Cấu hình:**
  - **Host:** Địa chỉ FTP của các sếp.
  - **Port:** Cổng FTP (thường là 21).
  - **Username & Password:** Tài khoản FTP.
  - **Path:** Thư mục chứa báo cáo PDF (ví dụ: `/reports/`).
- **Lưu ý:** Đảm bảo thư mục FTP có quyền đọc.

#### **🔹 Node 3: Filter New PDFs (If)**
- **Cấu hình:**
  - **Condition:** Kiểm tra file mới (tên file không tồn tại trong danh sách đã xử lý).
  - **Lưu ý:** Node này sẽ loại bỏ các file đã được xử lý trước đó.

#### **🔹 Node 4: PDF Vector - Parse Report (PDF Vector)**
- **Cấu hình:**
  - **API Key:** Điền API Key từ [PDF Vector](https://pdfvector.com/).
  - **Operation:** Chọn **Parse**.
  - **Resource:** Chọn **Document**.
  - **File:** Chọn file PDF từ node FTP.
- **Lưu ý:** Nếu không có tài khoản PDF Vector, có thể thay thế bằng **OpenAI GPT-3.5** để tóm tắt trực tiếp.

#### **🔹 Node 5: Extract Key Insights (OpenAI)**
- **Cấu hình:**
  - **Model:** Chọn **gpt-3.5-turbo**.
  - **Prompt:** Sử dụng template mặc định (hoặc tùy chỉnh):
    ```
    Tóm tắt nội dung chính của báo cáo PDF này trong 3 điểm quan trọng nhất.
    ```
  - **API Key:** Điền API Key OpenAI.
- **Lưu ý:** Nếu không có API Key, có thể sử dụng **node Code** để viết logic tóm tắt đơn giản.

#### **🔹 Node 6: Format Alerts (Code)**
- **Cấu hình:**
  - **JavaScript Code:** Sử dụng template dưới đây để định dạng cảnh báo:
    ```javascript
    // Format cảnh báo cho Slack và Email
    const insights = $input.all().map(item => item.json.output.text).join("\n\n");

    return {
      slackMessage: `📄 **Báo cáo mới được phân tích:**\n\n${insights}`,
      emailSubject: "🔍 Cảnh báo: Báo cáo mới đã được phân tích",
      emailBody: `Dưới đây là nội dung chính của báo cáo:\n\n${insights}`
    };
    ```
- **Lưu ý:** Đảm bảo code đúng cú pháp để tránh lỗi.

#### **🔹 Node 7: Send Slack Alert (Slack)**
- **Cấu hình:**
  - **Workspace URL:** `https://slack.com/api/chat.postMessage`.
  - **Credentials:** Chọn **Slack App Token** (cần tạo trong Slack).
  - **Channel:** Chọn kênh cần gửi cảnh báo (ví dụ: `#báo-cáo`).
  - **Message:** Sử dụng biến `$node["Format Alerts"].json()`.
- **Lưu ý:** Cần tạo **Slack App** và cấp quyền `chat:write` cho bot.

#### **🔹 Node 8: Send Email Alert (Email Send)**
- **Cấu hình:**
  - **From:** Email của các sếp (ví dụ: `admin@doanhnghiep.com`).
  - **To:** Email nhận cảnh báo (ví dụ: `team@doanhnghiep.com`).
  - **Subject:** `$node["Format Alerts"].json().emailSubject`.
  - **Body:** `$node["Format Alerts"].json().emailBody`.
- **Lưu ý:** Nếu dùng Gmail, cần **mã hóa mật khẩu** trong n8n.

#### **🔹 Node 9: Log Processed Report (PostgreSQL)**
- **Cấu hình:**
  - **Host:** Địa chỉ PostgreSQL (ví dụ: `localhost`).
  - **Port:** Cổng PostgreSQL (thường là `5432`).
  - **Database:** Tên cơ sở dữ liệu.
  - **Table:** Tạo bảng `processed_reports` với các cột:
    ```sql
    CREATE TABLE processed_reports (
      id SERIAL PRIMARY KEY,
      file_name VARCHAR(255),
      processed_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
    );
    ```
  - **Operation:** Chọn **Insert**.
  - **Data:** Sử dụng `$node["Check Report Folder"].json().file.name`.
- **Lưu ý:** Đảm bảo PostgreSQL đang hoạt động và có quyền write.

---

### **3. Kích Hoạt Workflow ⚡️**
1. **Test Run** với một file PDF mẫu:
   - Nhấn **Run Workflow** và kiểm tra các node có hoạt động không.
   - Kiểm tra **Slack** và **email** có nhận cảnh báo không.
2. **Bật Active** khi đã kiểm tra xong.

---

## **✍️ Mẹo & Gợi Ý Nâng Cao**
:::tip[**CÁCH LÀM NÀY ĐỂ TĂNG HIỆU QUẢ**]
1. **Thêm Log Lịch Sử** vào Slack:
   - Sử dụng **node StickyNote** để lưu thông tin báo cáo đã xử lý.
   - Gửi thông báo: `📄 **Báo cáo [FILE_NAME] đã được xử lý tại [THỜI GIAN]`.`

2. **Tùy Chỉnh Prompt GPT-3.5**:
   - Thay đổi prompt để phù hợp với loại báo cáo (ví dụ: báo cáo tài chính, báo cáo marketing).
   - Ví dụ:
     ```
     Tóm tắt báo cáo tài chính này với 3 điểm:
     1. Doanh thu tăng/giảm bao nhiêu?
     2. Chi phí lớn nhất là gì?
     3. Dự báo tương lai của doanh nghiệp.
     ```

3. **Kết Nối với Trello/Notion**:
   - Sử dụng **node Webhook** để tự động tạo task trong Trello khi có báo cáo mới.
   - Ví dụ: Tạo task `📄 Xem báo cáo [TÊN_FILE]` trong Trello.

4. **Báo Cáo Định Kỳ**:
   - Sử dụng **node ScheduleTrigger** để gửi báo cáo tổng hợp hàng tuần qua email.
   - Ví dụ: Gửi email tổng hợp tất cả báo cáo đã xử lý trong tuần.

5. **Sử Dụng PDF Vector** (nếu có):
   - Nếu có tài khoản PDF Vector, node này sẽ **phân tích cấu trúc** báo cáo chi tiết hơn (ví dụ: bảng biểu, danh sách).
   - Kết quả sẽ được gửi cùng với GPT-3.5.

---

## **📌 Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi việc theo dõi báo cáo PDF thủ công, đồng thời **tăng cường hiệu quả** bằng trí tuệ nhân tạo. Bằng cách tự động:
✔ **Phân tích** báo cáo bằng GPT-3.5.
✔ **Gửi cảnh báo** qua Slack và email.
✔ **Lưu lịch sử** để theo dõi.

**Hãy áp dụng ngay để bắt đầu tự động hóa báo cáo của mình!** 🚀

---
**🔹 Cần hỗ trợ thêm?**
- **Join Cộng Đồng n8n Việt Nam** tại [Facebook](https://facebook.com/groups/n8nvietnam).
- **Đăng ký VPS n8n** với mã giảm giá **VPSN8N** tại [TinoHost](https://tino.vn/vps-n8n?affid=388).