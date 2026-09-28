---
title: "🎨 Tự Động Hoá Vẽ Biểu Đồ Topology Mạng Layer-2 Từ CDP/LLDP Sang Lucidchart Với AI Gemini & AWX (N8N)"
description: "Workflow này tự động thu thập dữ liệu mạng Layer-2 từ thiết bị (CDP/LLDP) qua AWX, xử lý bằng AI Gemini và tạo ra prompt chuẩn cho Lucidchart vẽ biểu đồ tự động. Giúp kỹ sư mạng tiết kiệm 80% thời gian vẽ đồ thị thủ công."
slug: "tieu-dong-hoa-ve-bieu-do-topology-mang-lucidchart"
tags: [n8n, automation, engineering, ai, lucidchart, awx, google-gemini, network-automation]
keywords: [n8n workflow mạng, tự động hóa vẽ biểu đồ mạng, lucidchart ai, awx n8n, gemini api, cdp lldp parser]
---

# 🚀 **Tự Động Hoá Vẽ Biểu Đồ Topology Mạng Layer-2 Từ CDP/LLDP Sang Lucidchart Với AI Gemini & AWX**

## **🔥 Nỗi Đau Của Kỹ Sư Mạng**
Hàng ngày, các kỹ sư mạng phải:
- **Thủ công thu thập** thông tin CDP/LLDP từ hàng trăm thiết bị switch/router qua CLI.
- **Tìm kiếm và ghi chép** thông tin neighbor, interface, VLAN, và relationship giữa thiết bị.
- **Vẽ đồ thị** trên Lucidchart/Excalidraw bằng tay, dễ bị lỗi và mất nhiều thời gian.
- **Không thể cập nhật tự động** khi mạng thay đổi (thêm thiết bị, thay đổi VLAN, failover).

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Thu thập** dữ liệu CDP/LLDP từ mạng qua AWX.
✅ **Xử lý bằng AI Gemini** để tách cắt và cấu trúc dữ liệu thành format chuẩn.
✅ **Tạo prompt** sẵn sàng cho Lucidchart vẽ biểu đồ tự động.
✅ **Cập nhật liên tục** khi mạng thay đổi.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian** so với cách thủ công.
- **Chính xác 100%** (không sai sót như khi ghi chép tay).
- **Cập nhật tự động** khi mạng thay đổi (không cần làm lại từ đầu).
- **Sẵn sàng cho AI vẽ** (chỉ copy-paste prompt vào Lucidchart là xong).
- **Dễ mở rộng** (thêm Slack/Email báo cáo, lưu log, hoặc vẽ bằng Kroki).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **AWX (Ansible Tower)**:
   - Một **Job Template** đã cấu hình để chạy lệnh `show cdp neighbors detail` hoặc `show lldp neighbors detail`.
   - **Token API** hoặc **tài khoản AWX** để n8n gọi API.
   - **URL API AWX** (ví dụ: `http://<IP_AWX>:80/api/v2/job_templates/<ID_TEMPLATE>/launch/`).

2. **Google Gemini API**:
   - **API Key** từ [Google AI Studio](https://aistudio.google.com/).
   - **Credentials** trong n8n với tên `googlePalmApi`.

3. **Google Drive OAuth**:
   - **Credentials OAuth2** để lưu prompt vào Google Docs (nếu muốn lưu trữ).

4. **Lucidchart API (tùy chọn)**:
   - Nếu muốn tự động vẽ đồ thị, cần **API Key Lucidchart** (không bắt buộc trong workflow này).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/11537](https://n8n.io/workflows/11537) hoặc copy JSON từ canvas.
- **Import vào n8n Editor**:
  - Mở n8n → **Workflow** → **Import** → Dán JSON hoặc tải file `.json`.
  - **Kích hoạt workflow** (Active).

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow được chia thành **3 phần chính**, các sếp cần cấu hình kỹ:

##### **📌 Phần 1: Gọi Playbook AWX & Lấy Job ID**
- **Node "HTTP Request-Launch Job"**:
  - **Method**: `POST`
  - **URL**: `http://<IP_AWX>:<PORT>/api/v2/job_templates/<ID_TEMPLATE>/launch/`
    *Ví dụ*: `http://10.1.1.1:80/api/v2/job_templates/1/launch/`
  - **Headers**:
    ```json
    {
      "Content-Type": "application/json"
    }
    ```
  - **Body (JSON)**:
    ```json
    {
      "extra_vars": {
        "command": "show cdp neighbors detail"
      }
    }
    ```
  - **Credentials**: Chọn `httpBasicAuth` (đã tạo trước trong n8n).

- **Node "Edit Fields Parametros Basicos" (Set)**:
  - Lưu **Job ID** từ response của node trên vào biến `jobId` để dùng sau.

##### **📌 Phần 2: Theo Dõi Trạng Thái Job & Xử Lý Output**
- **Node "HTTP Request - Get JobStatus"**:
  - **Method**: `GET`
  - **URL**: `http://<IP_AWX>:<PORT>/api/v2/jobs/<jobId>/`
  - **Credentials**: `httpBasicAuth`.
  - **Lưu ý**: Cần **wait** cho job hoàn thành trước khi lấy stdout.

- **Node "HTTP Request - Get JobStdout"**:
  - **Method**: `GET`
  - **URL**: `http://<IP_AWX>:<PORT>/api/v2/jobs/<jobId>/stdout/`
  - **Credentials**: `httpBasicAuth`.
  - **Kết quả**: Lấy được **stdout** chứa dữ liệu CDP/LLDP.

- **Node "Wait"**:
  - Thiết lập **thời gian chờ** (ví dụ: 30 giây) để AWX hoàn thành job.

- **Node "Aggregate Devices" (Code)**:
  - **Mã JavaScript** trong node này **tách cắt** stdout thành các đối tượng device, neighbor, và interface.
  - *Lưu ý*: Nếu dữ liệu mạng khác thường, cần **sửa logic parser** trong node này.

##### **📌 Phần 3: Tạo Prompt Lucidchart & Lưu Trữ**
- **Node "Generate L2 Topology" (Google Gemini)**:
  - **Prompt mẫu** (cần tùy chỉnh theo yêu cầu):
    ```
    Tôi có dữ liệu CDP/LLDP sau:
    [Dữ liệu từ node "Aggregate Devices"]
    Hãy tạo một prompt chuẩn cho Lucidchart với:
    1. Danh sách thiết bị (Switch, Router, Firewall).
    2. Các liên kết (interface) giữa thiết bị.
    3. Màu sắc và style cho từng loại thiết bị.
    4. Format JSON sẵn sàng copy-paste vào Lucidchart AI.
    ```
  - **Credentials**: Chọn `googlePalmApi`.

- **Node "Prompt for Lucid" (Google Gemini - Lần 2)**:
  - **Sử dụng kết quả** từ node trước để **tạo prompt cuối cùng** (nếu cần điều chỉnh thêm).

- **Node "Create a document" / "Update a document" (Google Docs)**:
  - **Tạo hoặc cập nhật** một Google Doc để lưu prompt.
  - **Credentials**: `googleDocsOAuth2Api`.
  - *Lưu ý*: Nếu muốn lưu vào Google Drive thay vì Docs, cần thay node này bằng **Google Drive**.

---

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Chọn **Manual Trigger** → **Execute**.
   - Kiểm tra **stdout** từ AWX có đúng không?
   - Kiểm tra **prompt Lucidchart** có hợp lý không?

2. **Bật Active**:
   - Sau khi test thành công, **bật Active** workflow.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Thêm Báo Cáo Slack/Email**:
   - Sau khi tạo prompt, thêm node **Slack Webhook** hoặc **Send Email** để thông báo kết quả.

2. **Lưu Log vào Google Sheets**:
   - Thêm node **Google Sheets** để ghi lại lịch sử các lần chạy.

3. **Tự Động Vẽ Biểu Đồ**:
   - Nếu có **API Key Lucidchart**, thêm node **HTTP Request** để gọi API vẽ đồ thị tự động.

4. **Tùy Chỉnh Parser**:
   - Nếu mạng có **naming convention** đặc biệt (ví dụ: prefix `SW-` cho switch), sửa node **Aggregate Devices** để phù hợp.

5. **Dùng Kroki thay Lucidchart**:
   - Thay vì Lucidchart, có thể tạo **Mermaid.js** và render bằng **Kroki** (node `httpRequest` gọi API Kroki).

---

### 📌 **Kết Luận**
Workflow này **giải phóng kỹ sư mạng** khỏi công việc vẽ đồ thị thủ công, thay vào đó chỉ cần **click một nút** là có prompt sẵn sàng cho AI vẽ. **Tiết kiệm thời gian, giảm lỗi, và cập nhật tự động** khi mạng thay đổi.

**Hành động ngay!**
1. **Import workflow** vào n8n.
2. **Cấu hình AWX và Google Gemini**.
3. **Test và bật Active**.
4. **Copy-paste prompt vào Lucidchart** và xem kết quả!

---
**💡 Cần hỗ trợ?**
- **AWX Playbook**: Liên hệ tác giả [Gustavo Dorantes](https://n8n.io/workflows/11537) để lấy playbook.
- **Sửa parser**: Nếu dữ liệu mạng khác thường, chia sẻ stdout cho tôi, tôi giúp sửa logic!