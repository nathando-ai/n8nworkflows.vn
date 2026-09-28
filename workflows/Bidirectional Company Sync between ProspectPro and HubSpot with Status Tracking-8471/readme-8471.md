---
title: "🔄 Tự Động Hóa Đồng Bộ Hóa 2 Chiều ProspectPro ↔ HubSpot Với Theo Dõi Trạng Thái - N8n"
description: "Workflow tự động đồng bộ hóa thông tin doanh nghiệp từ ProspectPro sang HubSpot và ngược lại, đồng thời theo dõi trạng thái sync để tránh trùng lặp và tối ưu hóa quản lý khách hàng. Giúp các sếp tiết kiệm thời gian lên tới 15 giờ/tuần và giảm thiểu sai sót trong quản lý dữ liệu."
slug: "tieu-dong-bo-hoa-prospectpro-hubspot"
tags: [n8n, automation, prospectpro, hubspot, crm, no-code, sync-data]
keywords: [n8n workflow prospectpro hubspot, tự động hóa đồng bộ hóa 2 chiều, quản lý khách hàng tự động, theo dõi trạng thái sync, tiết kiệm thời gian CRM]
---

# 🔄 **Tự Động Hóa Đồng Bộ Hóa 2 Chiều ProspectPro ↔ HubSpot Với Theo Dõi Trạng Thái**

## **💡 Giải Pháp Cho Nỗi Đau Của Các Sếp**
Quản lý khách hàng và thông tin doanh nghiệp thủ công giữa **ProspectPro** và **HubSpot** là một công việc **mệt mỏi, tốn thời gian và dễ sai sót**. Các sếp thường phải:
- **Nhập liệu lặp đi lặp lại** giữa hai hệ thống, gây ra trùng lặp và mất mát dữ liệu.
- **Không theo dõi được trạng thái sync**, dẫn đến việc đồng bộ hóa không chính xác.
- **Tốn nhiều giờ mỗi tuần** để kiểm tra và điều chỉnh thủ công.
- **Không biết liệu dữ liệu đã được cập nhật đầy đủ** hay chưa.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tự động đồng bộ hóa 2 chiều** (ProspectPro → HubSpot **và** HubSpot → ProspectPro).
✅ **Theo dõi trạng thái sync** bằng cách gán **tags** (`HubspotSynced`/`HubspotSyncFailed`) để tránh trùng lặp.
✅ **Tối ưu hóa thời gian** bằng cách loại bỏ việc nhập liệu thủ công.
✅ **Cập nhật thông tin chính xác** từ cả hai hệ thống.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 15+ giờ/tuần** do loại bỏ việc nhập liệu thủ công.
- **Giảm thiểu sai sót** với đồng bộ hóa tự động và theo dõi trạng thái.
- **Cập nhật dữ liệu liên tục** (24/7) mà không cần can thiệp người dùng.
- **Tránh trùng lặp dữ liệu** nhờ hệ thống tag quản lý.
- **Cải thiện trải nghiệm khách hàng** với thông tin đồng bộ hóa chính xác.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần:
✔ **Tài khoản ProspectPro** (với **API Key** và quyền truy cập vào dữ liệu).
✔ **Tài khoản HubSpot** (với **OAuth 2.0 API Key** và quyền quản lý Company).
✔ **n8n Self-hosted** (để chạy workflow 24/7, không phụ thuộc vào phiên bản cloud).
✔ **Danh sách ProspectPro ID** (hoặc trigger từ ProspectPro như "New website visitor").

👉 **🎁 Đăng ký VPS TinoHost (Mã giảm giá: VPSN8N - 39%)** để tự host n8n:
🔗 [https://tino.vn/vps-n8n?affid=388](https://tino.vn/vps-n8n?affid=388)
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/8471](https://n8n.io/workflows/8471).
- **Nhấn "Import"** trong n8n Editor và chọn file.
- **Hoặc copy/paste JSON** từ file vào Editor và nhấn **"Import"**.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này **không tự động hóa hoàn toàn** mà cần **cấu hình một số node quan trọng**:

##### **A. Cấu Hình Credentials**
- **ProspectPro API**:
  - Đăng nhập vào [ProspectPro](https://www.prospectpro.nl/) → **API Settings** → Lấy **API Key**.
  - Trong n8n, tạo **credentials mới** với tên `prospectproApi` và điền **API Key**.
- **HubSpot OAuth 2.0**:
  - Tạo **OAuth App** trong HubSpot (Settings → Integrations → OAuth Apps).
  - Đăng ký **credentials mới** trong n8n với tên `hubspotOAuth2Api` và điền:
    - **Client ID**
    - **Client Secret**
    - **Redirect URI** (đặt là `http://localhost:5678/oauth/callback`)

##### **B. Cấu Hình Node "Continue?" (Nếu Có Điều Kiện)**
- Node này **kiểm tra xem có nên tiếp tục sync** hay không.
- **Mặc định**, workflow sẽ **bắt đầu từ ProspectPro ID**, nhưng các sếp có thể **thêm điều kiện** (ví dụ: chỉ sync khi trạng thái = "New Lead").

##### **C. Cấu Hình Node "Search Companies by Bedrijfsdata ID" & "Search Companies by Domain"**
- N8n **không hỗ trợ sync logic trực tiếp** với HubSpot, nên phải dùng **HTTP Request** để tìm kiếm.
- **Cần điền tham số chính xác** trong `keyParameters`:
  ```json
  {
    "url": "https://api.hubapi.com/crm/v3/objects/companies/search",
    "method": "POST",
    "body": {
      "properties": ["hs_company_domain", "name"],
      "filterGroups": [
        {
          "propertyName": "hs_company_domain",
          "operator": "equals",
          "value": "$node["Get prospect"].json()$.domain"
        }
      ]
    }
  }
  ```

##### **D. Cấu Hình Node "Create a company" & "Update a company"**
- **Node HubSpot** sẽ tự động tạo hoặc cập nhật **Company** trong HubSpot.
- **Đảm bảo điền đầy đủ trường cần sync** (ví dụ: `name`, `domain`, `hs_company_domain`).

##### **E. Cấu Hình Node "Set Tag: HubspotSynced" & "Set Tag: HubspotSyncFailed"**
- **Node Code** này sẽ **gán tags** cho ProspectPro để theo dõi trạng thái sync.
- **Mẫu code mặc định**:
  ```javascript
  // Set Tag: HubspotSynced
  return {
    tags: ["HubspotSynced"]
  };
  ```
  ```javascript
  // Set Tag: HubspotSyncFailed
  return {
    tags: ["HubspotSyncFailed"]
  };
  ```

##### **F. Cấu Hình Node "ProspectPro Trigger Example" (Nếu Sử Dụng Trigger)**
- Nếu muốn **kích hoạt workflow khi có sự kiện mới** (ví dụ: "New website visitor"), cần:
  - **Kết nối với node `prospectproTrigger`**.
  - **Cấu hình Webhook URL** trong ProspectPro để gửi dữ liệu đến n8n.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run** với **dữ liệu mẫu** (ví dụ: một ProspectPro ID).
2. **Kiểm tra logs** để đảm bảo:
   - Dữ liệu được sync chính xác.
   - Tags được gán đúng (`HubspotSynced`/`HubspotSyncFailed`).
3. **Bật Active** workflow.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
- **Kết nối với Slack/Telegram** để thông báo khi sync thành công/thất bại:
  ```javascript
  // Trong node Code, thêm:
  return {
    message: `Sync ${status} for Prospect ID: ${prospectId}`
  };
  ```
- **Lưu log sync** vào **Google Sheets/Notion** để theo dõi lịch sử.
- **Tự động gửi báo cáo định kỳ** (ví dụ: hàng tuần) về số lượng sync thành công/thất bại.
- **Sử dụng node `executeWorkflowTrigger`** để kích hoạt workflow từ một workflow khác (ví dụ: khi có email mới).
:::

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp bằng cách **tự động đồng bộ hóa ProspectPro ↔ HubSpot** và **theo dõi trạng thái sync** một cách hiệu quả. **Không cần code**, chỉ cần **cấu hình đúng credentials** và **điều chỉnh node "Continue?"** theo nhu cầu.

**🚀 Hãy áp dụng ngay để:**
✔ **Tiết kiệm thời gian** và **giảm sai sót**.
✔ **Cập nhật dữ liệu liên tục** mà không cần can thiệp.
✔ **Tối ưu hóa quản lý khách hàng** với thông tin đồng bộ hóa chính xác.

**🔗 [Tải workflow JSON](https://n8n.io/workflows/8471) và bắt đầu tự động hóa ngay!** 🚀