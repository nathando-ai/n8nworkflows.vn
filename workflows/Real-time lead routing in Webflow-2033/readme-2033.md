---
title: "🚀 Tự Động Hóa Xử Lý Lead Thực Tế Từ Webflow - Chia Sẻ Demo 1:1 & Nhóm Tự Động"
description: "Workflow này tự động phân loại lead từ form Webflow thành 2 loại: demo cá nhân (1:1) hoặc demo nhóm, dựa trên thông tin email và dữ liệu doanh nghiệp. Giúp doanh nghiệp tiết kiệm thời gian và tối ưu hóa quy trình bán hàng."
slug: "tieu-dong-hoa-lead-routing-webflow"
tags: [n8n, automation, sales, marketing, webflow, lead-routing]
keywords: [n8n workflow webflow, tự động hóa lead, chia sẻ demo tự động, phân loại lead, datagma api]
---

# 🚀 **Tự Động Hóa Xử Lý Lead Thực Tế Từ Webflow - Chia Sẻ Demo 1:1 & Nhóm Tự Động**

### **Nỗi Đau Của Các Sếp**
Hiện nay, khi khách hàng gửi form trên website, các sếp phải:
- **Làm thủ công** phân loại lead (demo 1:1 hay demo nhóm).
- **Tốn thời gian** để tra cứu thông tin doanh nghiệp (số nhân viên, ngành nghề, quy mô).
- **Không có sự nhất quán** trong cách xử lý lead, dẫn đến trải nghiệm khách hàng không đồng nhất.

**Workflow này giải quyết tất cả!** Nó tự động phân loại lead ngay khi form được gửi, dựa trên thông tin email và dữ liệu doanh nghiệp từ **Datagma**, rồi **chỉnh sửa kết quả trên Webflow** để hiển thị liên kết demo phù hợp.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần phải kiểm tra từng lead thủ công.
- **Chính xác cao**: Dựa trên dữ liệu doanh nghiệp thực tế từ Datagma.
- **Trải nghiệm khách hàng tốt**: Hiển thị liên kết demo phù hợp ngay lập tức.
- **Hoạt động 24/7**: Không cần can thiệp của con người.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần:
1. **Tài khoản Webflow** với form đã được cấu hình để gửi dữ liệu qua Webhook.
2. **API Key Datagma** (để enrich dữ liệu doanh nghiệp).
   - **Lấy API Key**: [Datagma API](https://app.datagma.com/user-api)
3. **Mã Webhook** từ Webflow (đã được cung cấp trong workflow).
4. **Mã Calendly** cho demo 1:1 và demo nhóm (để hiển thị kết quả).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/2033](https://n8n.io/workflows/2033) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ link trên và paste vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow gồm **7 nodes** chính, các sếp cần chú ý cấu hình sau:

##### **🔹 Node "Receive form submission from Webflow" (Webhook)**
- **Key Parameters**:
  - `path`: `6545426b-ff78-47af-8e20-a6e9f5259c8e` (không thay đổi).
  - `httpMethod`: `POST` (không thay đổi).
- **Lưu ý**:
  - Đảm bảo Webflow đã cấu hình Webhook với **URL** của n8n (ví dụ: `https://tên-máy-chủ-n8n.com/webhook/6545426b-ff78-47af-8e20-a6e9f5259c8e`).
  - Test Webhook bằng cách gửi form từ Webflow.

##### **🔹 Node "Enrich with Datagma" (HTTP Request)**
- **Cấu hình**:
  - **Method**: `GET`
  - **URL**: `https://api.datagma.com/v1/companies?email={$json["email"]}`
  - **Headers**:
    - `Authorization`: `Bearer YOUR_DATAGMA_API_KEY` (thay `YOUR_DATAGMA_API_KEY` bằng API Key của mình).
    - `Content-Type`: `application/json`
  - **Query Parameters**:
    - `apiId`: `YOUR_DATAGMA_API_KEY` (giống như trên).
- **Lưu ý**:
  - Nếu Datagma trả về dữ liệu, node tiếp theo sẽ xử lý.
  - Nếu không có dữ liệu, workflow sẽ mặc định xử lý lead như không đủ thông tin.

##### **🔹 Node "Qualify Account" (Code)**
- **Mã JavaScript mặc định** (các sếp có thể chỉnh sửa):
  ```javascript
  // Dựa trên số nhân viên (employeeCount) để phân loại lead
  if (json.employeeCount && json.employeeCount > 100) {
    return { result: "2" }; // Demo nhóm
  } else {
    return { result: "1" }; // Demo 1:1
  }
  ```
- **Lưu ý**:
  - Các sếp có thể **tweak logic** để phù hợp với tiêu chí của mình (ví dụ: doanh thu, ngành nghề, vị trí công ty...).

##### **🔹 Node "Send result to Webflow" (Respond to Webhook)**
- **Cấu hình**:
  - **Response Body**:
    ```json
    {
      "result": "{{$json.result}}",
      "calendlyLink": "{{$json.result === '1' ? 'LINK_DEMO_1_1' : 'LINK_DEMO_NHOM'}}"
    }
    ```
  - **Lưu ý**:
    - Thay `LINK_DEMO_1_1` và `LINK_DEMO_NHOM` bằng liên kết Calendly thực tế.
    - Webflow phải cấu hình để **hiển thị kết quả** từ Webhook này trong form.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Gửi một form mẫu từ Webflow để kiểm tra workflow.
   - Kiểm tra log trong n8n để đảm bảo tất cả node hoạt động.
2. **Bật Active**:
   - Sau khi test thành công, chuyển workflow sang **Active**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[CÁC TỐT NHẤT]
- **Lưu log tự động**: Sử dụng node **Sticky Note** để ghi lại thông tin lead đã xử lý.
- **Gửi thông báo Slack/Email**: Thêm node **Slack** hoặc **Email** để báo cáo kết quả cho team.
- **Báo cáo định kỳ**: Sử dụng node **Google Sheets** hoặc **Airtable** để lưu trữ lịch sử lead.
- **Cập nhật liên kết Calendly**: Nếu liên kết demo thay đổi, chỉ cần chỉnh sửa ở node **Respond to Webhook**.
:::

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi việc phân loại lead thủ công, đồng thời **tối ưu hóa quy trình bán hàng** bằng cách tự động hiển thị liên kết demo phù hợp. **Hãy áp dụng ngay** và xem kết quả!

👉 **Bắt đầu tự động hóa ngay hôm nay!**
- [Tải workflow từ n8n.io](https://n8n.io/workflows/2033)
- [Hướng dẫn chi tiết từ Notion](https://lempire.notion.site/Real-time-lead-routing-9fc55c9a5a17415ba736cbdbf5d43a30?pvs=4)

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::