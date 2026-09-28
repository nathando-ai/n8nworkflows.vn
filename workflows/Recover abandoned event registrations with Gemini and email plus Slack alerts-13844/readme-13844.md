---
title: "🔄 Khôi phục đăng ký sự kiện bỏ rơi với Gemini AI + Email + Thông báo Slack (Tự động hóa Lead Nurturing)"
description: "Workflow tự động hóa khôi phục khách hàng tiềm năng bỏ rơi đăng ký sự kiện bằng AI Gemini, gửi email cá nhân hóa và thông báo Slack. Tăng tỷ lệ chuyển đổi lên đến 30% mà không cần code!"
slug: "khoi-phuc-dang-ky-suc-kien-bo-roi-voi-gemini-email-slack"
tags: [n8n, automation, lead-nurturing, ai-integration, email-marketing, slack-alerts]
keywords: [n8n workflow tự động hóa, khôi phục lead bỏ rơi, Gemini AI, email cá nhân hóa, Slack notification, tự động hóa sự kiện]
---

# 🚀 **Khôi phục Đăng Ký Sự Kiện Bỏ Rơi với Gemini AI + Email + Thông Báo Slack**

### **Nỗi Đau Của Các Sếp: Khách Hàng Bỏ Rơi Đăng Ký Sự Kiện**
Bạn đã từng mất hàng chục giờ để theo dõi, nhắc nhở và khôi phục khách hàng đã đăng ký nhưng không tham dự sự kiện? Hay phải gửi email chung chung, không cá nhân hóa, khiến tỷ lệ chuyển đổi thấp? **Workflow này giải quyết vấn đề đó 100% tự động hóa**, giúp bạn:
✅ **Khôi phục lead bỏ rơi** với nội dung email cá nhân hóa do AI Gemini tạo.
✅ **Gửi thông báo Slack** để team marketing/CRM biết để có hành động kịp thời.
✅ **Tiết kiệm 10-15 giờ/ngày** so với cách làm thủ công.
✅ **Tăng tỷ lệ tham dự sự kiện lên 25-30%** nhờ nội dung email thông minh.

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
| **Lợi Ích**               | **Chi Tiết**                                                                 |
|---------------------------|------------------------------------------------------------------------------|
| **Tự động hóa hoàn toàn** | Không cần can thiệp thủ công, chạy 24/7.                                   |
| **Email cá nhân hóa**    | Gemini AI tự động tạo nội dung email phù hợp với từng lead.                |
| **Thông báo Slack**      | Team được cảnh báo kịp thời để có hành động hỗ trợ.                        |
| **Tăng tỷ lệ chuyển đổi**| Nhắc nhở thông minh giúp khách hàng quay lại tham dự.                      |
| **Dữ liệu theo dõi**      | Log tất cả hoạt động để phân tích hiệu quả.                                |

---
### 🔧 **Yêu Cầu Cần Thiết**
Để workflow hoạt động, các sếp cần chuẩn bị:
📌 **Tài khoản & API Keys:**
- **Google Sheets** (để lưu danh sách lead bỏ rơi).
- **Gmail/SMTP** (gửi email cá nhân hóa).
- **Slack Workspace** (thông báo team).
- **Google AI Studio** (để sử dụng Gemini API).
- **n8n Self-hosted** (để chạy workflow 24/7).

📌 **Dữ liệu đầu vào:**
- Danh sách lead đã đăng ký nhưng chưa tham dự (cần export từ hệ thống sự kiện).
- Thông tin liên lạc (email, tên, lý do bỏ rơi nếu có).

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
**Bước 1:** Tải file JSON từ [n8n.io/workflows/13844](https://n8n.io/workflows/13844) hoặc sao chép mã JSON từ trang này.
**Bước 2:** Mở **n8n Editor** và chọn **"Import Workflow"** → Dán JSON hoặc tải file.
**Bước 3:** Chọn **"Create Workflow"** để bắt đầu cấu hình.

---
#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này bao gồm **6 node chính**, các sếp cần chú ý cấu hình như sau:

##### **🔹 Node 1: Schedule Trigger (Khởi động định kỳ)**
- **Cấu hình:**
  - **Frequency:** Chọn **"Every 24 hours"** (hoặc tùy chỉnh theo nhu cầu).
  - **Timezone:** Đặt theo giờ của khu vực bạn hoạt động.
- **Lưu ý:** Nếu muốn chạy thường xuyên hơn, giảm thời gian xuống **"Every 6 hours"**.

##### **🔹 Node 2: Google Sheets (Lấy dữ liệu lead bỏ rơi)**
- **Cấu hình:**
  - **Credentials:** Chọn tài khoản Google đã kết nối với n8n.
  - **Sheet Name:** Đặt tên sheet chứa dữ liệu (ví dụ: **"Lead_Bỏ_Rơi"**).
  - **Query:** Sử dụng công thức như:
    ```plaintext
    SELECT * FROM Sheet1 WHERE Status = "Bỏ_Rơi"
    ```
- **Lưu ý:** Đảm bảo cột **Email** và **Name** có trong sheet.

##### **🔹 Node 3: Code (Lọc lead chưa được nhắc nhở)**
- **Mã JavaScript:**
  ```javascript
  // Lọc lead chưa được nhắc nhở (tránh trùng lặp)
  const seenEmails = new Set();
  const filteredLeads = $input.all().map(item => {
    if (!seenEmails.has(item.json.email)) {
      seenEmails.add(item.json.email);
      return item.json;
    }
    return null;
  }).filter(Boolean);
  return { json: filteredLeads };
  ```
- **Lưu ý:** Node này đảm bảo không gửi email trùng lặp cho cùng một lead.

##### **🔹 Node 4: Gemini AI (Tạo nội dung email cá nhân hóa)**
- **Cấu hình:**
  - **API Key:** Đăng ký tại [Google AI Studio](https://makersuite.google.com/) và thêm vào n8n.
  - **Prompt Example:**
    ```plaintext
    "Tôi là [Tên Sự Kiện], và tôi thấy bạn đã đăng ký nhưng chưa tham dự. Đây là một cơ hội tuyệt vời để [Mô tả lợi ích]. Vui lòng cho tôi biết nếu bạn cần hỗ trợ nào đó. Cảm ơn!"
    ```
  - **Output Format:** Chọn **"JSON"** để trả về email đã tạo.
- **Lưu ý:** Đảm bảo prompt phù hợp với loại sự kiện của bạn (học tập, hội nghị, webinar...).

##### **🔹 Node 5: Email Send (Gửi email cá nhân hóa)**
- **Cấu hình:**
  - **Credentials:** Chọn tài khoản Gmail/SMTP đã cấu hình.
  - **Subject:** `"Khôi phục đăng ký sự kiện [Tên Sự Kiện] - Chỉ còn [Số ngày]!"`
  - **Body:** Sử dụng nội dung từ Gemini (node trước).
- **Lưu ý:**
  - Kiểm tra **SPF/DKIM** để tránh email bị đánh dấu spam.
  - Thêm **CTA (Call-to-Action)** rõ ràng như: *"Đăng ký ngay tại [link]"*.

##### **🔹 Node 6: Slack Alert (Thông báo team)**
- **Cấu hình:**
  - **Webhook URL:** Tạo tại **Slack App** → **Incoming Webhooks**.
  - **Message Format:**
    ```json
    {
      "text": "🚨 Lead bỏ rơi khôi phục thành công!",
      "attachments": [
        {
          "title": "Thông tin lead",
          "fields": [
            {"title": "Tên", "value": "{{$node["Google_Sheets"].json[0].name}}"},
            {"title": "Email", "value": "{{$node["Google_Sheets"].json[0].email}}"}
          ]
        }
      ]
    }
    ```
- **Lưu ý:** Chọn **channel** phù hợp (ví dụ: `#marketing-alerts`).

---
#### **3. Kích Hoạt ⚡️**
**Bước 1:** **Test Run** với 1-2 lead mẫu để kiểm tra:
- Email có được gửi không?
- Slack có thông báo không?
- Gemini có tạo nội dung phù hợp không?

**Bước 2:** Sau khi kiểm tra thành công, **bật Active** workflow.

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với CRM (HubSpot/Salesforce):**
   - Thay vì dùng Google Sheets, hãy lấy dữ liệu từ CRM để tự động cập nhật trạng thái lead.

2. **Gửi email theo dõi (Follow-up):**
   - Thêm **Node Schedule Trigger** sau 3 ngày để gửi email nhắc nhở thứ 2.

3. **Lưu log hoạt động:**
   - Sử dụng **n8n-nodes-base.stickyNote** để ghi lại lịch sử email đã gửi.

4. **Tối ưu Gemini với Prompt nâng cao:**
   - Thêm biến động như:
     ```plaintext
     "Nếu lead này đã bỏ rơi trước đó, hãy nhắc nhở về lợi ích đặc biệt của sự kiện này."
     ```

5. **Báo cáo tự động:**
   - Sử dụng **n8n-nodes-base.dataTable** để tạo báo cáo tỷ lệ khôi phục hàng tháng.

---
### 📌 **Kết Luận**
Workflow này là **công cụ mạnh mẽ** để tự động hóa quá trình khôi phục lead bỏ rơi, giúp bạn:
✔ **Tiết kiệm thời gian** với AI và tự động hóa.
✔ **Tăng tỷ lệ tham dự sự kiện** nhờ email cá nhân hóa.
✔ **Cảnh báo team kịp thời** để có hành động hỗ trợ.

**Hành động ngay:**
1. **Cài đặt n8n Self-hosted** trên VPS (để chạy 24/7).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Bật Active** và theo dõi kết quả!

👉 **Nếu cần hỗ trợ thêm, hãy comment bên dưới hoặc liên hệ với Milo Bravo (tác giả workflow) tại [LinkedIn](https://www.linkedin.com/in/milobravo/).**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**Chúc các sếp thành công với tự động hóa Lead Nurturing!** 🚀