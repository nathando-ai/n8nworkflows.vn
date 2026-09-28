---
title: "🔒 Gọi API Google Cloud Run An Toàn Với Service Account (N8N) - Hướng Dẫn Chi Tiết"
description: "Tự động hóa gọi API Google Cloud Run một cách an toàn bằng Service Account trong n8n, không cần viết code. Giải pháp hoàn hảo cho DevOps, AI Multimodal và tự động hóa quy trình doanh nghiệp."
slug: "goi-api-google-cloud-run-an-toan-voi-service-account"
tags: [n8n, automation, devops, google-cloud-run, api-security]
keywords: [n8n gọi api cloud run, tự động hóa api google, service account n8n, an toàn api cloud run, tự động hóa devops]
---

# 🚀 Gọi API Google Cloud Run An Toàn Với Service Account (N8N)

## 💡 Bạn đang gặp vấn đề gì?
Cần gọi API của Google Cloud Run một cách an toàn, nhưng lo lắng về vấn đề **xác thực**, **bảo mật** và **quyền hạn**? Hoặc đang phải viết code phức tạp để xử lý token JWT và gọi API? **Workflow này giải quyết tất cả!**

Với **n8n**, bạn có thể tự động hóa việc gọi API Google Cloud Run **một cách an toàn**, sử dụng **Service Account** để xác thực, **không cần viết một dòng code nào**. Workflow này sẽ tự động:
- **Tạo token ID** (ID token) từ Service Account.
- **Gọi API Cloud Run** với header `Authorization: Bearer <id_token>`.
- **Trả về kết quả** từ API một cách tự động.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **An toàn tuyệt đối**: Sử dụng **Service Account** thay vì API Key, giảm thiểu rủi ro bị lộ.
- **Tự động hóa hoàn toàn**: Không cần viết code, chỉ cần cấu hình.
- **Chuẩn hóa quy trình**: Gọi API một cách **liên tục và chính xác**.
- **Kiểm soát quyền hạn**: Chỉ cấp quyền cho Service Account cần thiết.
- **Hoạt động 24/7**: Workflow chạy tự động trên n8n self-hosted.
:::

---

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Google Cloud Account** và **Google Cloud Project** đã được tạo.
2. **Google Service Account** với quyền **Cloud Run Invoker**.
3. **Google Cloud Run Service** đã được cấu hình yêu cầu **xác thực**.
4. **Private Key JSON** của Service Account (tải từ [Google Cloud Console](https://console.cloud.google.com/iam-admin/serviceaccounts)).
5. **API Key** hoặc **Credentials** cho n8n để gọi Google Cloud Run.
6. **n8n self-hosted** (không dùng phiên bản cloud).
7. **Dữ liệu mẫu** (nếu cần gọi API với tham số).
:::

---

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- **Tải file JSON** của workflow từ [n8n.io/workflows/7568](https://n8n.io/workflows/7568).
- **Mở n8n Editor** và chọn **Import Workflow** từ menu.
- **Chọn file JSON** đã tải và nhấn **Import**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

##### **A. Cấu hình Google Credentials (Service Account)**
1. **Tạo Credential mới** trong n8n:
   - Mở **Google** node → Chọn **Create New Credential**.
   - **Authentication:** Chọn **Service Account**.
   - **Service account email:** Copy từ file `.json` (thường là `client_email`).
   - **Private key:** Copy **toàn bộ block** từ file `.json` (bao gồm `-----BEGIN PRIVATE KEY-----` và `-----END PRIVATE KEY-----`).
   - **Save** credential.

2. **Bật API cần thiết** trong [Google Cloud Console](https://console.cloud.google.com/apis/library):
   - Ví dụ: **Sheets API**, **Drive API**, hoặc API khác bạn sử dụng.
   - **Chia sẻ tài nguyên** với email của Service Account (ví dụ: chia sẻ Sheet/Folder cho `client_email`).

##### **B. Cấu hình Node `Set Example Context Fields`**
- **Thêm biến `service_url`**: Điền **URL base** của Cloud Run service (ví dụ: `https://your-service-url.a.run.app`).
- **Thêm biến `service_path` (nếu có)**: Nếu API có đường dẫn cụ thể (ví dụ: `/api/v1/data`).

##### **C. Cấu hình Node `Merge`**
- **Mode:** Chọn **Combine**.
- **Combine By:** Chọn **All Possible Combinations**.
- **Lưu ý**: Node này sẽ **gộp dữ liệu** từ các node trước đó (ví dụ: `id_token` từ `Get Auth` và dữ liệu từ `Set Example Context Fields`).

##### **D. Cấu hình Node `Split Out`**
- **Operation:** Chọn **Split Out Items**.
- **Field to split:** Chọn trường **mảng** bạn muốn phân tách (ví dụ: `items` nếu có).
- **Include:** Chọn **All other fields** để **giữ nguyên `id_token` và `service_url`**.
- **Kết quả**: Mỗi phần tử trong mảng sẽ được xử lý riêng.

##### **E. Cấu hình Node `Cloud Run Request`**
- **Method:** Chọn **POST** (hoặc **GET** tùy API).
- **URL:** `{service_url}{service_path}` (nếu `service_path` có giá trị).
- **Headers:**
  - `Authorization: Bearer ${{$json["id_token"]}}` (đảm bảo lấy token từ `Get Auth`).
  - **Thêm headers khác** nếu API yêu cầu (ví dụ: `Content-Type: application/json`).
- **Body:** Nếu API cần dữ liệu, điền vào **Request Body** (có thể là JSON hoặc form-data).
- **Credentials:** Chọn **httpBearerAuth** (đã cấu hình ở bước A).

##### **F. Cấu hình Node `Get Auth` (sub-workflow)**
- **Chạy sub-workflow** này trước để lấy `id_token`.
- **Lưu ý**: Sub-workflow này sẽ **tạo token JWT** từ Service Account và trả về `id_token`.

##### **G. Kích hoạt Workflow**
1. **Test Run** với dữ liệu mẫu:
   - Nhấn **Execute** trên node **Execute**.
   - Kiểm tra kết quả ở **Cloud Run Request** và **Get Auth**.
2. **Bật Active** workflow nếu test thành công.

---

### ✍️ Mẹo & gợi ý nâng cao
1. **Lưu log hoạt động**:
   - Sử dụng **Slack/Telegram Webhook** để báo cáo kết quả gọi API.
   - Ví dụ: Nếu API thành công → gửi tin nhắn Slack; nếu lỗi → gửi email cảnh báo.

2. **Gọi API định kỳ**:
   - Sử dụng **n8n Cron Trigger** để gọi API theo lịch (ví dụ: hàng ngày).

3. **Xử lý lỗi tự động**:
   - Thêm **If** node để kiểm tra `statusCode` từ API.
   - Nếu lỗi → gọi lại API sau một thời gian (retry logic).

4. **Kết hợp với Google Sheets/Drive**:
   - Sau khi gọi API thành công, lưu kết quả vào **Google Sheets** hoặc **Google Drive** tự động.

5. **Mở rộng với AI Multimodal**:
   - Nếu API trả về dữ liệu cần xử lý (ví dụ: text, image), kết hợp với **n8n-nodes-ai** để phân tích tự động.

---

### 📌 Kết luận
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn gọi API Google Cloud Run **an toàn, tự động hóa và không cần code**. Bằng cách sử dụng **Service Account**, bạn đảm bảo quyền hạn được kiểm soát chặt chẽ, trong khi **n8n** đảm bảo quy trình hoạt động liên tục.

**Hành động ngay!**
1. **Cài đặt n8n self-hosted** trên VPS (để workflow chạy 24/7).
2. **Cấu hình Google Service Account** và Cloud Run.
3. **Import workflow** và chạy thử.
4. **Tích hợp với Slack/Email** để theo dõi kết quả.

👉 [Xem hướng dẫn chi tiết trên Medium](https://medium.com/@marcocodes/build-a-secure-google-cloud-run-api-then-call-it-from-n8n-88c03291a95f) để biết cách cấu hình Google Cloud Run từ đầu!

---
**Chia sẻ và phản hồi** nếu có bất kỳ thắc mắc nào! 🚀