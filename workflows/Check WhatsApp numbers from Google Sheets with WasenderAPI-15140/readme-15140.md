---
title: "📱 **Tự Động Kiểm Tra Số Điện Thoại WhatsApp Từ Google Sheets Với WasenderAPI - Giúp Các Sếp Tiết Kiệm Thời Gian & Tăng Tỷ Lệ Thành Công Lead**"
description: "Workflow này tự động kiểm tra danh sách số điện thoại trong Google Sheets để xác định số nào đã đăng ký WhatsApp, giúp các sếp loại bỏ số không hiệu quả trước khi gửi tin nhắn, tiết kiệm chi phí và tăng tỷ lệ phản hồi. Kết quả được cập nhật tự động vào bảng tính, sẵn sàng cho chiến dịch tiếp thị."
slug: "tieu-dong-kiem-tra-so-whatsapp-tu-google-sheets"
tags: [n8n, automation, lead-generation, wasenderapi, google-sheets, no-code]
keywords: [n8n workflow tự động hóa, kiểm tra số WhatsApp, lead generation, tự động hóa marketing, google sheets api, wasender api]
---

# 🚀 **Tự Động Kiểm Tra Số WhatsApp Từ Google Sheets - Giải Pháp Tối Ưu Hóa Chiến Dịch Tiếp Thị**

### **Nỗi Đau Của Các Sếp Khi Làm Thủ Công**
Các sếp thường phải:
- **Nhập danh sách số điện thoại** vào Google Sheets hoặc Excel.
- **Kiểm tra từng số** trên WhatsApp thủ công để xác định số nào đã đăng ký (tránh bị block).
- **Loại bỏ số không hiệu quả** trước khi gửi tin nhắn, nhưng quá trình này **tốn thời gian, dễ sai sót** và không thể thực hiện 24/7.
- **Mất chi phí** vì gửi tin nhắn đến số chưa đăng ký WhatsApp (WhatsApp có chính sách nghiêm ngặt với số không hoạt động).

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Kiểm tra số WhatsApp** trong danh sách từ Google Sheets.
✅ **Loại bỏ số không hiệu quả** (đã block hoặc chưa đăng ký).
✅ **Cập nhật kết quả tự động** vào bảng tính.
✅ **Gửi báo cáo** khi hoàn thành (để các sếp biết số nào sẵn sàng tiếp thị).

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đảm bảo tốc độ cao, không lag)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần kiểm tra thủ công, workflow chạy tự động trong vài phút.
- **Tăng tỷ lệ thành công**: Chỉ tiếp cận số WhatsApp **đã đăng ký**, giảm nguy cơ bị block.
- **Dữ liệu chính xác**: Kết quả được cập nhật **tự động** vào Google Sheets, sẵn sàng cho chiến dịch tiếp thị.
- **Hoạt động liên tục**: Workflow có thể **bật 24/7** và xử lý danh sách mới mỗi khi cập nhật.
- **Giảm chi phí**: Tránh mất tiền gửi tin nhắn đến số không hoạt động.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
✔ **Tài khoản Google Sheets** (để lưu danh sách số điện thoại).
✔ **Danh sách số điện thoại** (đã được nhập vào Google Sheets theo **mẫu template** dưới đây).
✔ **Tài khoản WasenderAPI** (để kiểm tra số WhatsApp).
✔ **Node `n8n-nodes-wasenderapi`** (cần cài đặt từ **n8n Community Nodes**).
✔ **Credentials**:
   - **Google Sheets OAuth2** (để đọc/giữi dữ liệu).
   - **WasenderAPI Account** (để gọi API kiểm tra số).

---
:::note[Mẫu Google Sheets]
Các sếp **phải sử dụng template này** để lưu danh sách số điện thoại:
🔗 **[Mẫu Google Sheets](https://docs.google.com/spreadsheets/d/1K0ps-y9OVJ5L15dnOekIxxTwxvTa0zOQNwGDEFSrYYY/edit?usp=sharing)**
- **Cột "Mobile Number"** chứa danh sách số cần kiểm tra.
- **Cột "Status"** sẽ tự động cập nhật kết quả (OK/Invalid/Blocked).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có **2 cách** để import workflow:
- **Tải file JSON** từ [n8n.io/workflows/15140](https://n8n.io/workflows/15140) và import vào **n8n Editor**.
- **Copy JSON** từ trang trên và **paste** vào **Create New Workflow** trong n8n.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **12 node**, các sếp cần **cấu hình kỹ** các phần sau:

##### **A. Cấu Hình Google Sheets**
- **Node "Load phone numbers from Google Sheets"**:
  - Chọn **credentials**: `googleSheetsOAuth2Api`.
  - **Sheet Name**: Đặt tên là **"Mobile Numbers"** (phù hợp với template).
  - **Range**: `Sheet1!A2:B` (để lấy cột "Mobile Number" và "Status").
  - **Operation**: `Read`.

- **Node "Update result in Google Sheets" & "write Invalid format"**:
  - Chọn **credentials**: `googleSheetsOAuth2Api`.
  - **Range**: `Sheet1!B2:B` (để cập nhật cột "Status").
  - **Operation**: `Append or Update`.

##### **B. Cấu Hình WasenderAPI**
- **Node "Check WhatsApp registration with WasenderAPI"**:
  - Chọn **credentials**: `wasenderAccountApi`.
  - **API Key**: Điền vào **Credentials** của WasenderAPI.
  - **Parameters**:
    - `operation`: `checkOnWhatsApp`.
    - `resource`: `contact`.
    - **Input Data**: `$node["Load phone numbers from Google Sheets"]["json"][0]["Mobile Number"]`.

- **Node "Notify error" & "Notify check complete"**:
  - Chọn **credentials**: `wasenderAccountApi`.
  - **API Key**: Điền vào **Credentials**.
  - **Parameters**:
    - **Target Number**: Điền số WhatsApp của các sếp để nhận thông báo.
    - **Message**: Tùy chỉnh nội dung (ví dụ: `"Kiểm tra số WhatsApp hoàn tất!"`).

##### **C. Cấu Hình Node Code (Normalize & Validate Phone)**
- **Node "Normalize phone number"**:
  - Sử dụng **JavaScript** để chuẩn hóa số điện thoại (ví dụ: `+84123456789` → `+84123456789`).
  - **Code mẫu**:
    ```javascript
    $input.all().map(item => {
      const phone = item.json["Mobile Number"];
      // Sử dụng thư viện `libphonenumber` (nếu cần) hoặc logic tự định nghĩa
      return {
        json: {
          "Mobile Number": phone.replace(/\D/g, ''),
          "Status": "Pending"
        }
      };
    });
    ```

- **Node "Validate international phone format"**:
  - Kiểm tra định dạng số có hợp lệ không (ví dụ: bắt buộc bắt đầu bằng `+`).
  - **Code mẫu**:
    ```javascript
    $input.all().map(item => {
      const phone = item.json["Mobile Number"];
      if (!phone.startsWith('+')) {
        return {
          json: {
            "Mobile Number": phone,
            "Status": "Invalid format"
          }
        };
      }
      return {
        json: {
          "Mobile Number": phone,
          "Status": "Pending"
        }
      };
    });
    ```

##### **D. Cấu Hình Node Wait (Tránh Rate Limit)**
- **Node "Wait"**:
  - Thời gian chờ mặc định: **10 giây** (để tránh bị WasenderAPI chặn).
  - **Lưu ý**: Nếu danh sách số nhiều, các sếp có thể **tăng thời gian chờ** (ví dụ: 15-30 giây) để tránh bị block.

##### **E. Cấu Hình Node Split In Batches**
- **Node "process one by one"**:
  - **Batch Size**: Đặt **1** để xử lý từng số một (tránh quá tải API).
  - **Delay Between Batches**: Đặt **10 giây** (để tránh rate limit).

---

#### **3. Kích Hoạt ⚡️ Workflow**
- **Bước 1**: **Test Run** với **dữ liệu mẫu** (đảm bảo không có lỗi).
- **Bước 2**: **Bật Active** workflow.
- **Bước 3**: **Chạy thủ công** bằng **Manual Trigger** hoặc **lên lịch tự động** (nếu cần).

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm **node Slack/Telegram** để thông báo kết quả khi workflow hoàn tất.
   - **Cách làm**:
     - Sử dụng **node `n8n-nodes-slack`** hoặc **`n8n-nodes-telegram`**.
     - Gửi tin nhắn tự động khi workflow kết thúc.

2. **Lưu Log Kết Quả**:
   - Thêm **node `n8n-nodes-base.ftp`** hoặc **`n8n-nodes-base.httpRequest`** để lưu log vào **Google Drive** hoặc **database** để theo dõi lịch sử.

3. **Tự Động Cập Nhật Danh Sách Số Mới**:
   - Kết nối với **CRM** (HubSpot, Zoho, Salesforce) để **tự động lấy danh sách số mới** vào Google Sheets.
   - **Cách làm**:
     - Sử dụng **node `n8n-nodes-hubspot`** hoặc **`n8n-nodes-zoho`** để lấy dữ liệu.
     - Sau đó, **chuyển dữ liệu** vào Google Sheets trước khi chạy workflow.

4. **Báo Cáo Định Kỳ**:
   - Sử dụng **node `n8n-nodes-base.email`** để gửi **báo cáo tuần/Tháng** về tỷ lệ số WhatsApp hiệu quả.
   - **Cách làm**:
     - Thêm **node `n8n-nodes-base.dateTime`** để kiểm tra ngày tháng.
     - Nếu ngày là cuối tháng, gửi email báo cáo.

---
### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** để các sếp:
✔ **Tiết kiệm thời gian** bằng tự động hóa.
✔ **Tăng tỷ lệ thành công** trong chiến dịch WhatsApp.
✔ **Tránh bị block** và **giảm chi phí** không cần thiết.

**Hành động ngay!**
1. **Import workflow** vào n8n.
2. **Cấu hình Google Sheets & WasenderAPI**.
3. **Chạy thử** và **bật tự động** để tiết kiệm thời gian hàng ngày.

**Cần hỗ trợ?** Các sếp có thể liên hệ với tác giả **Razvan Bara** qua [website](https://www.razvanbara.com/) để tối ưu hóa workflow thêm hiệu quả!

---
**🚀 Chúc các sếp thành công với chiến dịch tiếp thị WhatsApp hiệu quả!**