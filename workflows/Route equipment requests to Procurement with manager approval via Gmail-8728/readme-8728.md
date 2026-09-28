---
title: "🚀 Tự Động Hóa Yêu Cầu Thiết Bị Cho Phòng Mua Hàng Với Phê Chuẩn Quản Lý - N8N"
description: "Workflow này tự động xử lý yêu cầu thiết bị từ nhân viên, kiểm tra phê chuẩn từ quản lý (nếu có) và chuyển giao trực tiếp đến phòng mua hàng - hoàn toàn không cần code. Giảm thiểu thời gian chờ đợi và tối ưu hóa quy trình mua sắm."
slug: "tu-dong-hoa-yeu-cau-thiet-bi-voi-phe-chuan-quan-ly"
tags: [n8n, automation, procurement, approval workflow, gmail, mysql, ai-chatbot]
keywords: [n8n workflow tự động hóa, yêu cầu thiết bị, phê chuẩn quản lý, phòng mua hàng, tự động hóa doanh nghiệp, n8n self-hosted]
---

# 🚀 **Tự Động Hóa Yêu Cầu Thiết Bị Cho Phòng Mua Hàng Với Phê Chuẩn Quản Lý**

## **🔥 Giới Thiệu: Giải Pháp Tự Động Hóa Quy Trình Mua Sắm Khó Khăn**
Hiện nay, nhiều doanh nghiệp vẫn phải phụ thuộc vào việc nhân viên gửi yêu cầu thiết bị qua email hoặc form thủ công, sau đó quản lý phải kiểm tra và phê duyệt từng đơn. Quá trình này không chỉ tốn thời gian mà còn dễ xảy ra lỗi, mất mát thông tin hoặc trễ hạn. **Workflow này giải quyết vấn đề này bằng cách:**
- **Tự động lấy thông tin nhân viên** từ cơ sở dữ liệu (MySQL) dựa trên mã số đăng ký.
- **Kiểm tra và yêu cầu phê chuẩn từ quản lý** (nếu nhân viên có quản lý).
- **Chuyển yêu cầu đã phê duyệt** đến phòng mua hàng một cách tự động.
- **Gửi thông báo kết quả** (được tối ưu hóa bởi AI) cho nhân viên và quản lý.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần phải theo dõi từng yêu cầu thủ công.
- **Chính xác và minh bạch**: Dữ liệu được lấy từ cơ sở dữ liệu, tránh sai sót.
- **Phê chuẩn tự động**: Quản lý chỉ cần phản hồi qua email, không cần vào hệ thống.
- **Tối ưu hóa quy trình mua hàng**: Yêu cầu được chuyển ngay đến phòng mua hàng khi được phê duyệt.
- **Trải nghiệm người dùng tốt**: Nhân viên nhận thông báo nhanh chóng và rõ ràng.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản n8n Self-hosted** (đã cài đặt và cấu hình).
2. **Cơ sở dữ liệu MySQL** với bảng `employees` có các cột:
   - `id`, `name`, `email`, `enrollment_number`, `manager` (nullable).
3. **Tài khoản Gmail OAuth2** (để gửi email phê chuẩn và thông báo).
4. **API Key OpenAI** (để sử dụng mô hình GPT-4.1-nano để tạo nội dung email tự động).
5. **Địa chỉ email phòng mua hàng** (ví dụ: `procurement@doanhnghiep.com`).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/8728](https://n8n.io/workflows/8728) hoặc copy toàn bộ JSON từ trang này.
- Mở **n8n Editor** → Nhấn **Import** → Dán JSON và nhấn **Import**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này có **30 node** và cần cấu hình chi tiết như sau:

##### **A. Cấu hình cơ sở dữ liệu MySQL**
- **Node "Get Employee"** và **"Get Manager"** cần kết nối đến bảng `employees` với cấu hình:
  ```json
  {
    "host": "your-mysql-host",
    "port": 3306,
    "database": "your-database",
    "user": "your-username",
    "password": "your-password"
  }
  ```
- **Query cho "Get Employee"**:
  ```sql
  SELECT id, name, email, enrollment_number, manager FROM employees WHERE enrollment_number = '{{$node["Question form"].json["enrollment_number"]}}'
  ```
- **Query cho "Get Manager"**:
  ```sql
  SELECT id, name, email FROM employees WHERE id = '{{$node["Get Employee"].json["manager"]}}'
  ```

##### **B. Cấu hình Gmail OAuth2**
- Tạo **credentials mới** trong n8n với loại `gmailOAuth2`.
- Cấu hình trong node **"Send request to approve"**, **"Notify approved request"**, và **"Notify denied request"**:
  - **To**: Địa chỉ email của quản lý hoặc phòng mua hàng.
  - **Subject**: Tùy chỉnh (ví dụ: *"Phê duyệt yêu cầu thiết bị: {{$node["Get Employee"].json["name"]}}"*).

##### **C. Cấu hình OpenAI API**
- Tạo **credentials mới** với loại `openAiApi` và điền `API Key`.
- Các node sử dụng mô hình `gpt-4.1-nano` (đã được cấu hình sẵn trong workflow).

##### **D. Cấu hình Form và Email Tự Động**
- **Node "Question form"**: Thêm trường nhập `enrollment_number` (mã số đăng ký) và trường mô tả yêu cầu.
- **Node "Approval request message"**: Cấu hình LLM để tạo email phê chuẩn với nội dung:
  ```json
  {
    "role": "system",
    "content": "Bạn là một quản lý chuyên nghiệp. Hãy tạo một email phê duyệt yêu cầu thiết bị cho nhân viên, bao gồm thông tin sau:\n- Tên nhân viên: {{employee.name}}\n- Yêu cầu: {{sanitized_request}}\n- Email phải ngắn gọn, chuyên nghiệp và yêu cầu phản hồi trong 24 giờ."
  }
  ```
- **Node "Create request message"**: Tương tự, nhưng nội dung email gửi đến phòng mua hàng (không đề cập đến phê chuẩn).

##### **E. Cấu hình Node "noOp"**
- Node này được sử dụng để **chuyển tiếp yêu cầu** đến phòng mua hàng. Các sếp có thể thay thế bằng:
  - **Gmail node** (gửi email trực tiếp).
  - **API node** (gửi yêu cầu đến hệ thống ERP).
  - **Slack/Teams node** (thông báo trên kênh).

---

#### **3. Kích hoạt ⚡️**
1. **Test run** với dữ liệu mẫu:
   - Nhập `enrollment_number` của một nhân viên có quản lý.
   - Kiểm tra email phê chuẩn được gửi đến quản lý.
   - Sau khi quản lý phản hồi (gửi email phê duyệt/từ chối), kiểm tra thông báo cho nhân viên và yêu cầu chuyển đến phòng mua hàng.
2. **Bật Active workflow** khi đã kiểm tra hoàn chỉnh.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Thêm Slack/Telegram Notifications**:
   - Sử dụng node **Slack** hoặc **Telegram Bot** để thông báo kết quả phê chuẩn ngay khi có phản hồi từ quản lý.

2. **Lưu log yêu cầu**:
   - Thêm node **MySQL** hoặc **Google Sheets** để ghi lại lịch sử yêu cầu, trạng thái phê duyệt và thời gian xử lý.

3. **Báo cáo định kỳ**:
   - Sử dụng node **Google Sheets** hoặc **Excel** để tạo báo cáo tổng hợp yêu cầu đã phê duyệt/từ chối hàng tháng.

4. **Tối ưu hóa LLM**:
   - Thay đổi mô hình OpenAI thành `gpt-4` (nếu có budget) để nội dung email được sinh ra chuyên nghiệp hơn.

5. **Thêm trường xác minh**:
   - Sử dụng node **Form** để yêu cầu nhân viên nhập mã xác minh (OTP) trước khi gửi yêu cầu, giảm thiểu yêu cầu giả.

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho quản lý và phòng mua hàng bằng cách tự động hóa quy trình phê duyệt yêu cầu thiết bị. **Không cần code**, chỉ cần cấu hình cơ sở dữ liệu và email, bạn đã có một hệ thống tự động hóa hoàn chỉnh. **Áp dụng ngay để tối ưu hóa quy trình mua sắm của doanh nghiệp!**

---
**💡 Lưu ý cuối cùng:**
- **Không lưu trữ dữ liệu nhạy cảm** (PII) trong logs n8n. Sử dụng node **Set** để chỉ lưu thông tin cần thiết.
- **Test workflow với dữ liệu mẫu** trước khi chuyển sang sản xuất.
- **Cập nhật thường xuyên** để đảm bảo tính nhất quán với cơ sở dữ liệu và quy trình mới.

**Bắt đầu tự động hóa ngay hôm nay!** 🚀