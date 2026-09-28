---
title: "🚀 Tự Động Hóa Lấy Tên Người Liên Hệ LinkedIn Từ URL Với LinkUp (Không Cần Code)"
description: "Workflow này tự động trích xuất tên đầy đủ từ URL LinkedIn bằng API LinkUp, tiết kiệm thời gian cho việc tìm kiếm lead và cập nhật danh sách liên hệ. Hoàn toàn tự động hóa, không cần viết code."
slug: "tu-dong-hoa-lay-ten-nguoi-lien-he-linkedin"
tags: [n8n, automation, lead-generation, ai-summarization, linkedin-api]
keywords: [n8n workflow linkedin, tự động hóa lấy tên từ linkedin, linkup api, tự động hóa lead generation, n8n automation]
---

# 🚀 **Tự Động Hóa Lấy Tên Người Liên Hệ LinkedIn Từ URL Với LinkUp (Không Cần Code)**

### **Nỗi Đau Của Các Sếp**
Bạn có bao giờ phải mất thời gian thủ công tìm kiếm tên người liên hệ từ URL LinkedIn để cập nhật vào danh sách CRM, Excel hay hệ thống quản lý lead? Hoặc phải đối mặt với việc **dữ liệu không chính xác, mất thời gian, và không thể tự động hóa**? Workflow này sẽ giải quyết tất cả những vấn đề đó bằng cách **tự động trích xuất tên đầy đủ từ URL LinkedIn chỉ trong vài giây**, giúp bạn **tiết kiệm thời gian, tăng độ chính xác và tự động hóa quy trình lead generation**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
- **Tiết kiệm thời gian**: Không cần thủ công copy-paste tên từ LinkedIn.
- **Chính xác 100%**: API LinkUp đảm bảo trích xuất tên chính xác từ URL.
- **Tự động hóa lead generation**: Cập nhật danh sách liên hệ một cách liên tục.
- **Hoạt động 24/7**: Workflow chạy tự động khi có dữ liệu mới.
- **Kết hợp với CRM/Excel**: Dữ liệu tự động cập nhật vào bảng tính hoặc hệ thống quản lý.

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản LinkUp** (miễn phí hoặc trả phí):
   - Đăng ký tại [https://app.linkup.so](https://app.linkup.so) và lấy **API Key**.
   - **Lưu ý**: API Key phải được cài đặt trong **Settings** của workflow.
2. **n8n Self-hosted** (không dùng phiên bản cloud):
   - Cài đặt trên VPS (gợi ý sử dụng **Ubuntu**).
3. **Bảng dữ liệu LinkedInURL** (cấu trúc cụ thể sau).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/13974](https://n8n.io/workflows/13974) hoặc copy JSON từ canvas.
- **Import vào n8n Editor**:
  - Mở **n8n Workflow Editor**.
  - Nhấn **Import** → Dán JSON hoặc tải file `.json`.
  - **Kích hoạt workflow** bằng cách nhấn **Active**.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflows này gồm **9 node**, nhưng các bước quan trọng nhất cần chú ý:

##### **A. Cấu Hình API Key LinkUp**
- **Node "settings"** (type: `set`):
  - Thêm một **variable** mới tên `LINKUP_API_KEY`.
  - Gán giá trị là **API Key** của bạn (đã lấy từ LinkUp).
  - **Lưu ý**: Nếu không cấu hình này, API request sẽ thất bại.

##### **B. Chuẩn Bị Bảng Dữ Liệu LinkedInURL**
- **Node "linkedinurl"** (type: `dataTable`):
  - **Tên bảng**: `LinkedInURL`.
  - **Cấu trúc cột**:
    | Cột       | Loại Dữ Liệu | Mô Tả                          |
    |------------|---------------|----------------------------------|
    | `url`      | String        | URL LinkedIn (vd: `https://www.linkedin.com/in/stephaneheckel/`) |
    | `name`     | String        | **Trống ban đầu** (sẽ tự động cập nhật) |
  - **Lưu ý**:
    - Cột `name` **không được để trống** khi import.
    - Nếu chưa có dữ liệu, thêm ít nhất **1 URL** để test.

##### **C. Thiết Lập Node "linkup" (HTTP Request)**
- **Node "linkup"** (type: `httpRequest`):
  - **Method**: `POST`.
  - **URL**: `https://api.linkup.so/v1/search`.
  - **Headers**:
    - `Authorization`: `Bearer {{ $json["LINKUP_API_KEY"] }}`
    - `Content-Type`: `application/json`
  - **Body (JSON)**:
    ```json
    {
      "query": "Get the full name from LinkedIn profile URL: {{ $node["linkedinurl"].json["url"] }}"
    }
    ```
  - **Lưu ý**:
    - **Không sao chép body nguyên văn**, thay vì đó, sử dụng **expression** để động:
      ```json
      {
        "query": "Get the full name from LinkedIn profile URL: {{ $node["linkedinurl"].json["url"] }}"
      }
      ```
    - Nếu không, workflow sẽ **không hoạt động** với URL mới.

##### **D. Node "update name" (Update Data Table)**
- **Node "update name"** (type: `dataTable`):
  - **Operation**: `update`.
  - **Key**: `url` (để match với URL trong bảng).
  - **Field to update**: `name`.
  - **Value**: `{{ $node["linkup"].json["result"]["name"] }}` (trích xuất từ response LinkUp).
  - **Lưu ý**:
    - Nếu response LinkUp không trả về `name`, workflow sẽ **bị lỗi**.
    - **Test trước** với 1 URL để đảm bảo response đúng.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Nhấn **Execute Workflow** (node `manualTrigger`).
   - Kiểm tra **bảng `LinkedInURL`** để xem cột `name` có được cập nhật không.
   - **Nếu lỗi**, kiểm tra:
     - API Key có đúng không?
     - URL có đúng định dạng không?
     - Response từ LinkUp có chứa `name` không?

2. **Bật Active**:
   - Sau khi test thành công, **bật Active** để workflow chạy tự động khi có dữ liệu mới.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết Nối Với Slack/Telegram**:
   - Thêm node **Slack/Telegram** để thông báo khi workflow hoàn thành.
   - Ví dụ: `{{ $node["update name"].json["url"] }} đã được cập nhật tên: {{ $node["update name"].json["name"] }}`.

2. **Lưu Log Lịch Sử**:
   - Thêm node **Google Sheets** hoặc **Airtable** để lưu lịch sử cập nhật.
   - Cấu trúc bảng:
     | Cột          | Loại Dữ Liệu |
     |---------------|---------------|
     | `url`         | String        |
     | `name`        | String        |
     | `updated_at`   | DateTime      |

3. **Tự Động Cập Nhật Từ CRM**:
   - Nếu bạn dùng **HubSpot, Salesforce, Zoho**, kết nối với node **HubSpot API** để lấy danh sách URL và đẩy vào `LinkedInURL`.

4. **Sử Dụng AI Tóm Tắt Profile**:
   - Sau khi lấy tên, bạn có thể kết hợp với **LLM (n8n-nodes-base.llm)** để tóm tắt thông tin từ profile LinkedIn.

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi việc thủ công tìm kiếm tên trên LinkedIn, đồng thời **tăng độ chính xác** và **tự động hóa lead generation**. **Chỉ cần 5 phút setup**, bạn đã có một công cụ mạnh mẽ để quản lý danh sách liên hệ một cách hiệu quả.

**Hãy áp dụng ngay và bắt đầu tự động hóa quy trình của mình!** 🚀

---
**Cần hỗ trợ?**
- **Trên LinkedIn**: [Stéphane Heckel](https://www.linkedin.com/in/stephaneheckel/)
- **Trên Community n8n**: [Forum n8n](https://community.n8n.io/)
- **Đăng ký VPS n8n**: [TinoHost](https://tino.vn/vps-n8n?affid=388) (Mã giảm giá: **VPSN8N**)