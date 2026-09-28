---
title: "📊 Tính Trung Tâm (Centroid) Của Bộ Vectors Tự Động - Không Cần Code!"
description: "Workflow n8n này tự động tính toán trung tâm của bộ vectors (mảng số) từ yêu cầu HTTP GET, đảm bảo tính chính xác và hiệu quả cao cho các ứng dụng AI, dữ liệu lớn hoặc phân tích toán học. Giúp các sếp tiết kiệm thời gian và tránh lỗi tính toán thủ công."
slug: "tinh-trung-tam-centroid-cua-bo-vectors"
tags: [n8n, automation, no-code, math, data-processing, api-integration]
keywords: [n8n tính centroid, tự động hóa toán học, tính trung tâm vectors, workflow n8n cho AI, tính toán dữ liệu không code]
---

# 🚀 **Tính Trung Tâm (Centroid) Của Bộ Vectors Tự Động - Không Cần Code!**

### **Giải pháp nào cho các sếp khi phải tính trung tâm của hàng trăm, nghìn vectors thủ công?**
Thời gian của các sếp quá quý giá để phải tính toán trung tâm (centroid) của bộ vectors bằng tay, đặc biệt khi dữ liệu lớn và phức tạp. **Workflow này tự động hóa toàn bộ quá trình** bằng cách nhận dữ liệu từ yêu cầu HTTP GET, kiểm tra tính hợp lệ của vectors, tính toán trung tâm chính xác, và trả về kết quả ngay lập tức – **không cần viết một dòng code nào!**

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần tính toán thủ công cho bộ vectors lớn.
- **Tính chính xác cao**: Kiểm tra và tính toán tự động, tránh sai sót.
- **Hoạt động liên tục**: Chạy 24/7 trên VPS, không phụ thuộc vào thời gian làm việc.
- **Kết quả ngay lập tức**: Trả về centroid trong thời gian thực qua API.
- **Dễ dàng mở rộng**: Kết hợp với các workflow khác (ví dụ: gửi kết quả qua Slack/Email).
:::

---

### 🔧 **Yêu cầu cần thiết**
Để workflow hoạt động, các sếp cần:
1. **Một instance n8n self-hosted** (đã cài đặt và chạy trên VPS).
2. **URL Webhook** để nhận yêu cầu từ bên ngoài (sẽ được tạo tự động khi import workflow).
3. **Dữ liệu đầu vào** là một mảng vectors trong tham số `vectors` của yêu cầu GET (ví dụ: `vectors=[[2,3,4],[4,5,6]]`).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Mở **n8n Workflow Editor**.
2. Nhấn **Import** và chọn file JSON (hoặc paste JSON từ [đây](https://n8n.io/workflows/2839)).
3. Chọn **Create Workflow** để tạo mới.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **4 node chính**, các sếp cần chú ý cấu hình như sau:

##### **Node 1: Receive Vectors (Webhook)**
- **Chức năng**: Nhận yêu cầu GET từ bên ngoài với tham số `vectors`.
- **Cấu hình**:
  - **Path**: Đặt thành `centroid` (không cần thay đổi).
  - **Method**: Chọn `GET`.
  - **Credentials**: Chọn `None` (hoặc tùy chọn nếu cần xác thực).
- **Lưu ý**:
  - URL webhook sẽ tự động tạo sau khi lưu workflow (ví dụ: `https://<tên-domain>/webhook-test/centroid`).
  - **Dữ liệu đầu vào phải có tham số `vectors`** (ví dụ: `?vectors=[[2,3,4],[4,5,6]]`).

##### **Node 2: Extract & Parse Vectors (Set)**
- **Chức năng**: Trích xuất và định dạng lại mảng vectors từ dữ liệu đầu vào.
- **Cấu hình**:
  - **Operation**: Chọn `Set`.
  - **JSON Path**: Đặt thành `$.vectors` (trích xuất tham số `vectors` từ yêu cầu).
  - **Output**: Kiểm tra kết quả có dạng `[ [2,3,4], [4,5,6], ... ]` (mảng 2D).
- **Lưu ý**:
  - Nếu tham số `vectors` **không tồn tại**, workflow sẽ **báo lỗi** và dừng lại.
  - **Kiểm tra dữ liệu đầu vào** trước khi chạy test.

##### **Node 3: Validate & Compute Centroid (Code)**
- **Chức năng**: Kiểm tra tính hợp lệ của vectors và tính trung tâm.
- **Cấu hình**:
  - **Code (JavaScript)**:
    ```javascript
    // Kiểm tra vectors có phải là mảng 2D không?
    if (!Array.isArray($input.vectors) || $input.vectors.length === 0) {
      throw new Error("Vectors must be a non-empty array.");
    }

    // Kiểm tra tất cả vectors có cùng số chiều không?
    const dimensions = $input.vectors[0].length;
    for (const vector of $input.vectors) {
      if (!Array.isArray(vector) || vector.length !== dimensions) {
        throw new Error("Vectors have inconsistent dimensions.");
      }
    }

    // Tính trung tâm (centroid) bằng cách lấy trung bình mỗi chiều
    const centroid = $input.vectors[0].map((_, index) => {
      const sum = $input.vectors.reduce((acc, vector) => acc + vector[index], 0);
      return sum / $input.vectors.length;
    });

    return { centroid };
    ```
  - **Lưu ý**:
    - Nếu vectors **không hợp lệ** (ví dụ: số chiều khác nhau), workflow sẽ trả về lỗi:
      ```json
      { "error": "Vectors have inconsistent dimensions." }
      ```
    - Nếu vectors **hợp lệ**, sẽ tính toán và trả về centroid:
      ```json
      { "centroid": [4, 5, 6] }
      ```

##### **Node 4: Return Centroid Response (Respond To Webhook)**
- **Chức năng**: Trả về kết quả (centroid hoặc lỗi) cho yêu cầu HTTP.
- **Cấu hình**:
  - **Response Format**: Chọn `JSON`.
  - **Status Code**: Đặt thành `200` (thành công) hoặc `400` (lỗi).
- **Lưu ý**:
  - Nếu tính toán thành công, trả về:
    ```json
    { "centroid": [4, 5, 6] }
    ```
  - Nếu có lỗi, trả về:
    ```json
    { "error": "Vectors have inconsistent dimensions." }
    ```

#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Gửi yêu cầu GET đến URL webhook với tham số `vectors` (ví dụ: `https://<tên-domain>/webhook-test/centroid?vectors=[[2,3,4],[4,5,6]]`).
   - Kiểm tra kết quả trả về trong **n8n Editor** (tab "Executions").
2. **Bật Active**:
   - Đảm bảo workflow **Active** và **Running** trong danh sách workflows.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết hợp với Slack/Telegram**:
   - Sau khi tính toán xong, gửi kết quả centroid qua Slack/Telegram để các sếp theo dõi dễ dàng.
   - **Cách làm**: Thêm node `n8n-nodes-base.slack` hoặc `n8n-nodes-base.telegram` sau node `Respond To Webhook`.

2. **Lưu log kết quả**:
   - Sử dụng node `n8n-nodes-base.googleSheets` hoặc `n8n-nodes-base.database` để lưu lịch sử tính toán vào bảng Excel hoặc cơ sở dữ liệu.

3. **Tự động hóa từ dữ liệu CSV/JSON**:
   - Nếu vectors được lưu trong file CSV/JSON, sử dụng node `n8n-nodes-base.httpRequest` để tải dữ liệu trước khi gửi vào workflow.

4. **Cập nhật API Key (nếu cần)**:
   - Nếu workflow tương tác với các dịch vụ bên ngoài (ví dụ: Google Sheets), các sếp cần thêm **credentials** trong **n8n Settings**.

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp cần tính toán trung tâm của bộ vectors một cách **tự động, chính xác và không cần code**. Bằng cách import và cấu hình đơn giản, các sếp có thể **tiết kiệm thời gian, tránh sai sót** và mở rộng ứng dụng cho các dự án AI, phân tích dữ liệu hoặc toán học.

**Hãy áp dụng ngay và tự động hóa tính toán centroid cho dự án của mình!** 🚀
Nếu có bất kỳ câu hỏi hoặc cần hỗ trợ, các sếp có thể liên hệ với **Mauricio Perera** (tác giả workflow) qua [LinkedIn](https://www.linkedin.com/in/mauricioperera/) để thảo luận về các workflow tùy chỉnh!