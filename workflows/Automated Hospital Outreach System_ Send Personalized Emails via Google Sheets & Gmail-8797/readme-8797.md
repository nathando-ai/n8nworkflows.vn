---
title: "🚀 Hệ Thống Tự Động Liên Hệ Bệnh Viện: Gửi Email Cá Nhân Hóa Từ Google Sheets & Gmail (N8n)"
description: "Tự động hóa việc gửi email cá nhân hóa đến hàng trăm bệnh viện chỉ với một tin nhắn chat. Workflow này giúp các sếp tiết kiệm thời gian lên đến 80% trong công việc liên hệ khách hàng, đồng thời đảm bảo tính chính xác và cá nhân hóa cao. Hỗ trợ 3 khu vực chính: Luzon, Visayas, Mindanao."
slug: "automated-hospital-outreach-system-n8n"
tags: [n8n, automation, no-code, google-sheets, gmail, chatbot, email-marketing]
keywords: [n8n tự động hóa, gửi email cá nhân hóa, liên hệ bệnh viện, google sheets n8n, chatbot n8n, workflow n8n cho doanh nghiệp y tế]
---

# 🚀 **Hệ Thống Tự Động Liên Hệ Bệnh Viện: Gửi Email Cá Nhân Hóa Từ Google Sheets & Gmail**

### **📌 Nỗi Đau Của Các Sếp Trong Công Việc Liên Hệ Bệnh Viện**
Gửi email liên hệ đến hàng trăm bệnh viện thủ công không chỉ tốn thời gian mà còn dễ gây lỗi nhân sự (nhân viên quên gửi, nội dung không đồng nhất, hoặc sai thông tin). Kết quả? **Tỷ lệ phản hồi thấp, mất thời gian đàm phán, và cơ hội kinh doanh bị bỏ lỡ**.

Với **Automated Hospital Outreach System**, các sếp có thể:
✅ **Gửi email cá nhân hóa** chỉ bằng một tin nhắn chat (không cần code).
✅ **Tự động tra cứu email** của bệnh viện từ Google Sheets.
✅ **Phân vùng theo khu vực** (Luzon, Visayas, Mindanao) để tối ưu hóa chiến dịch.
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **ổn định và an toàn**, các sếp nên **self-host n8n** trên VPS riêng:
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đảm bảo tốc độ cao cho email bulk)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian lên đến 80%** so với cách làm thủ công.
- **Tính chính xác 100%** (không sai email, không quên gửi).
- **Cá nhân hóa nội dung** cho từng bệnh viện (dễ dàng cập nhật template).
- **Hoạt động tự động** ngay cả khi các sếp nghỉ ngơi.
- **Phân vùng hiệu quả** (Luzon, Visayas, Mindanao) để tối ưu hóa chiến dịch.
- **Dễ dàng mở rộng** cho nhiều khu vực hoặc loại bệnh viện khác.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Google Sheets** (để lưu danh sách bệnh viện và email).
2. **Tài khoản Gmail** (để gửi email bulk, **không sử dụng Gmail cá nhân** vì có giới hạn gửi).
3. **API Key của Google Sheets** (để n8n có thể đọc/writing).
4. **Tin nhắn chat đầu tiên** (để kích hoạt workflow, định dạng như ví dụ dưới đây).

---
:::info[CHUẨN BỊ DỮ LIỆU]
**Cấu trúc Google Sheets bắt buộc:**
| **Region** | **Hospital Name** | **Email**          |
|------------|-------------------|--------------------|
| Luzon      | St. Luke's        | contact@stlukes.com|
| Luzon      | Makati Medical    | info@makati.com    |
| Visayas    | Cebu Doctors      | cebu@doctors.com   |

**Lưu ý:**
- **Cột "Region"** phải có giá trị: `LUZON`, `VISAYAS`, hoặc `MINDANAO`.
- **Cột "Email"** phải có email chính xác của bệnh viện.
- **Tên Sheet** trong Google Sheets phải **không có dấu cách** (ví dụ: `Hospital_List`).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Tải file JSON từ [đây](https://n8n.io/workflows/8797) (hoặc copy JSON từ link trên).
2. Mở **n8n Editor** → Nhấn **Import Workflow** → Dán JSON và nhấn **Import**.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Sau khi import, các sếp cần **cấu hình lại các node quan trọng** như sau:

##### **🔹 Node "MINDANAO", "VISAYAS FILES", "LUZON FILES" (Google Sheets)**
- **Thao tác:**
  - Nhấn vào mỗi node → Tab **Credentials** → Chọn **Google Sheets**.
  - Điền:
    - **Sheet ID**: ID của Google Sheet chứa danh sách bệnh viện (tham khảo cách lấy [đây](https://support.google.com/docs/answer/10701260)).
    - **Sheet Name**: Tên của tab trong Google Sheet (ví dụ: `Hospital_List`).
    - **Range**: `A2:B` (giả sử dữ liệu bắt đầu từ hàng 2, cột A là Region, cột B là Hospital Name).
  - **Lưu ý:** Các node này **không cần credentials** vì sẽ được kết nối chung với node `Region Switcher`.

##### **🔹 Node "When chat message received" (ChatTrigger)**
- **Thao tác:**
  - Nhấn vào node → Tab **Configuration** → Chọn **Webhook** (nếu muốn kích hoạt bằng API) hoặc **Chat** (nếu muốn kích hoạt bằng tin nhắn).
  - **Lưu ý:** Nếu sử dụng **Slack/Telegram**, các sếp cần cài đặt **Webhook** tương ứng và điền URL vào node này.

##### **🔹 Node "Hospital Parser" (Code)**
- **Thao tác:**
  - Mở node → Nhấn **Edit** → Sửa code để **trích xuất thông tin từ tin nhắn chat**:
    ```javascript
    // Dữ liệu đầu vào từ tin nhắn chat (ví dụ: "LUZON\nSt. Luke's\nMakati Medical")
    const input = $input.all();

    // Tách vùng và danh sách bệnh viện
    const region = input[0].chatMessage.split('\n')[0].trim().toUpperCase();
    const hospitals = input[0].chatMessage.split('\n').slice(1).map(h => h.trim());

    // Trả về kết quả
    return {
      json: {
        region: region,
        hospitals: hospitals
      }
    };
    ```
  - **Lưu ý:** Đảm bảo **tin nhắn chat có định dạng chính xác** (ví dụ: `LUZON\nSt. Luke's\nMakati Medical`).

##### **🔹 Node "Region Switcher" (Switch)**
- **Thao tác:**
  - Nhấn vào node → Tab **Configuration** → Chọn **Region** (trong trường hợp này là `$node["Hospital Parser"].json.region`).
  - **Cấu hình các case:**
    - **Case 1:** `LUZON` → Chọn node `LUZON FILES`.
    - **Case 2:** `VISAYAS` → Chọn node `VISAYAS FILES`.
    - **Case 3:** `MINDANAO` → Chọn node `MINDANAO`.
    - **Case Default:** Nếu không khớp, hiển thị lỗi (ví dụ: `Không tìm thấy vùng`).

##### **🔹 Node "Batch Sender" (SplitInBatches)**
- **Thao tác:**
  - Nhấn vào node → Tab **Configuration** → Đặt:
    - **Batch Size:** `5` (gửi tối đa 5 email/lần để tránh bị chặn bởi Gmail).
    - **Field:** `$node["Region Switcher"].json.hospitals` (danh sách bệnh viện).

##### **🔹 Node "Send Gmail Message" (Gmail)**
- **Thao tác:**
  - Nhấn vào node → Tab **Credentials** → Chọn **Gmail**.
  - Điền:
    - **From Email:** Email chính của tài khoản Gmail (ví dụ: `contact@yourcompany.com`).
    - **Subject:** `Cá nhân hóa: [Tên Bệnh Viện] - [Tên Công Ty]`.
    - **Body:** Nội dung email cá nhân hóa (sử dụng **template HTML** hoặc **Markdown**):
      ```html
      <p>Chào <strong>{{ $node["Batch Sender"].json.email }}</strong>,</p>
      <p>Tôi là [Tên Bạn] từ [Tên Công Ty]. Chúng tôi rất vui khi liên hệ với quý vị về [Dịch vụ/Công Ty].</p>
      <p>Xin vui lòng liên hệ với tôi tại: <a href="mailto:contact@yourcompany.com">contact@yourcompany.com</a> để biết thêm chi tiết.</p>
      ```
  - **Lưu ý:**
    - **Không sử dụng Gmail cá nhân** (sử dụng tài khoản doanh nghiệp).
    - **Cài đặt 2FA** cho tài khoản Gmail để bảo mật.
    - **Không gửi quá 50 email/ngày** để tránh bị chặn.

---

#### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run** với dữ liệu mẫu:
   - Gửi tin nhắn chat: `LUZON\nSt. Luke's\nMakati Medical`.
   - Kiểm tra **log** trong n8n để đảm bảo email được gửi đúng.
2. **Bật Active workflow**:
   - Nhấn **Active** ở góc trên bên phải của canvas.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack/Telegram**:
   - Thay vì sử dụng **Webhook**, các sếp có thể **gửi tin nhắn qua Slack/Telegram** để kích hoạt workflow.
   - **Cách làm:** Cài đặt **Slack App** hoặc **Telegram Bot** và kết nối với node `When chat message received`.

2. **Lưu Log Email Đã Gửi**:
   - Thêm node **Google Sheets** mới để ghi lại lịch sử email đã gửi (giúp theo dõi và phân tích hiệu quả).
   - **Cấu trúc log:**
     | **Date**       | **Hospital**      | **Email Sent** | **Status** |
     |----------------|-------------------|----------------|------------|
     | 2024-05-20     | St. Luke's        | Yes            | Success    |

3. **Gửi Báo Cáo Định Kỳ**:
   - Sử dụng **n8n + Google Sheets** để tự động tạo báo cáo hàng tuần về số email đã gửi và tỷ lệ phản hồi.
   - **Cách làm:** Thêm node **Google Sheets** sau `Send Gmail Message` để cập nhật thống kê.

4. **Cá Nhân Hóa Nội Dung Email**:
   - Sử dụng **AI (LangChain)** trong node `Hospital Parser` để tự động tạo nội dung email dựa trên loại bệnh viện.
   - **Ví dụ:** Nếu bệnh viện là **bệnh viện đa khoa**, nội dung email sẽ khác với **bệnh viện chuyên khoa**.

---

### 📌 **Kết Luận**
**Automated Hospital Outreach System** là **giải pháp hoàn hảo** để các sếp tiết kiệm thời gian, tăng hiệu quả liên hệ và **tự động hóa 100% công việc email bulk**. Với **cấu hình đơn giản** và **không cần code**, workflow này giúp các doanh nghiệp y tế hoặc dịch vụ liên quan **tối ưu hóa chiến dịch marketing** một cách hiệu quả.

**🚀 Hãy áp dụng ngay và bắt đầu tự động hóa công việc của mình!**
Nếu có vấn đề, các sếp có thể tham khảo **video tutorial** từ tác giả [đây](https://www.youtube.com/embed/5u9W-Iegq6k).

---
**🔹 Cần hỗ trợ thêm?**
- **Diễn đàn n8n**: [https://community.n8n.io/](https://community.n8n.io/)
- **TinoHost (VPS n8n)**: [https://tino.vn/vps-n8n?affid=388](https://tino.vn/vps-n8n?affid=388)