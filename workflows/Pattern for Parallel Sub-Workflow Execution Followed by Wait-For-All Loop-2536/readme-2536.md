---
title: "🚀 Tự Động Hóa Xuất Xắc: Chạy Nhiều Sub-Workflow Song Song Và Đợi Tất Cả Hoàn Thành (N8n)"
description: "Giải pháp hoàn hảo để các sếp khởi động nhiều sub-workflow song song, theo dõi tiến trình và chờ tất cả hoàn thành trước khi tiếp tục quy trình chính - hoàn toàn không cần code!"
slug: "tieu-dong-hoa-song-song-va-doi-tat-ca-hoan-thanh"
tags: [n8n, automation, no-code, parallel-processing, workflow-orchestration, sub-workflow]
keywords: [n8n workflow song song, tự động hóa song song, chờ tất cả hoàn thành, sub-workflow n8n, orchestration n8n]
---

# 🚀 **Tự Động Hóa Xuất Xắc: Chạy Nhiều Sub-Workflow Song Song Và Đợi Tất Cả Hoàn Thành**

### **Giải pháp cho các sếp muốn chạy nhiều nhiệm vụ song song mà không lo mất kiểm soát tiến trình**

Hãy tưởng tượng một tình huống: Các sếp cần xử lý **nhiều nhiệm vụ độc lập** (ví dụ: gửi email, cập nhật database, gọi API) **tuy nhiên lại phải chờ tất cả hoàn thành trước khi tiếp tục bước tiếp theo**. Làm thủ công? **Tốn thời gian, dễ lỡ bước, và không thể mở rộng**. Với **workflow này**, các sếp có thể:
✅ **Khởi động nhiều sub-workflow song song** (song song thực sự, không phải giả mạo)
✅ **Theo dõi tiến trình** và chờ tất cả hoàn thành trước khi tiếp tục
✅ **Tự động hóa hoàn toàn** mà không cần viết một dòng code
✅ **Áp dụng cho mọi trường hợp**: Xử lý batch, tích hợp hệ thống, hoặc thậm chí là **AI + nhiều mô hình song song**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không phải chờ đợi tuần tự, mọi thứ chạy song song.
- **Tăng hiệu suất**: Xử lý nhiều nhiệm vụ đồng thời mà không tốn tài nguyên quá mức.
- **Đảm bảo tính nhất quán**: Chờ tất cả sub-workflow hoàn thành trước khi tiếp tục.
- **Dễ dàng mở rộng**: Thêm hoặc loại bỏ sub-workflow mà không cần thay đổi logic chính.
- **Hoàn toàn tự động hóa**: Không cần can thiệp thủ công giữa các bước.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Các sếp cần chuẩn bị:
1. **Một instance n8n self-hosted** (không thể chạy trên n8n.cloud vì yêu cầu webhook nội bộ).
2. **URL Base của n8n** (để cấu hình webhook nội bộ).
3. **Thời gian thử nghiệm**: Workflow này yêu cầu **test run** để đảm bảo sub-workflow hoạt động đúng.
4. **Các sub-workflow con** (cần tạo riêng và liên kết với workflow chính).

**Lưu ý quan trọng**:
- Workflow này **không hoạt động trên n8n.cloud** vì cần webhook nội bộ.
- Các sub-workflow con **phải được tạo riêng** và kích hoạt trước khi workflow chính chạy.
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Tải file JSON từ [n8n.io/workflows/2536](https://n8n.io/workflows/2536).
2. Mở **n8n Editor** → Nhấn **Import** → Chọn file JSON.
3. **Hoặc** copy toàn bộ JSON và paste vào **Import Workflow** trong Editor.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **2 phần chính**:
- **Workflow chính (Parent Workflow)**: Khởi động và quản lý sub-workflow.
- **Sub-workflow con**: Cần tạo riêng và liên kết với workflow chính.

##### **A. Cấu hình Workflow Chính**
1. **Node `Webhook` (parallel-subworkflow-target)**
   - **Path**: `parallel-subworkflow-target` (không thay đổi).
   - **HTTP Method**: `POST`.
   - **Credentials**: Chọn **None** (n8n sẽ tự động xử lý).
   - **Lưu ý**: **URL Base của n8n** phải được cấu hình trong **Settings → Webhooks** (ví dụ: `http://localhost:5678`).

2. **Node `Initialize finishedSet` (Set)**
   - **Key**: `finishedSet` (không thay đổi).
   - **Value**: `[]` (mảng rỗng).
   - **Lưu ý**: Đây là **biến lưu trữ** để theo dõi sub-workflow đã hoàn thành.

3. **Node `Simulate Multi-Item for Parallel Processing` (Code)**
   - **JavaScript**:
     ```javascript
     // Đây là mã mô phỏng dữ liệu đầu vào cho sub-workflow.
     // Các sếp có thể thay đổi để phù hợp với yêu cầu thực tế.
     const items = [
       { id: "task-1", data: "Dữ liệu cho nhiệm vụ 1" },
       { id: "task-2", data: "Dữ liệu cho nhiệm vụ 2" },
       // Thêm nhiều item tùy ý
     ];
     return items;
     ```
   - **Lưu ý**: Thay đổi `items` để phù hợp với **sub-workflow** của các sếp.

4. **Node `Start Sub-Workflow via Webhook` (HTTP Request)**
   - **URL**: `{{ $json["url"] }}` (được truyền từ sub-workflow).
   - **HTTP Method**: `POST`.
   - **Headers**:
     - `Content-Type`: `application/json`.
   - **Body**:
     ```json
     {
       "id": "{{ $node["Loop Over Items"].json["$.id"] }}",
       "status": "started"
     }
     ```
   - **Lưu ý**: **URL này phải trỏ đến sub-workflow** (cần cấu hình trong sub-workflow).

5. **Node `If All Finished` (If)**
   - **Condition**: `{{ $json["finishedSet"].length === $node["Loop Over Items"].json["$.length"] }}`
   - **Lưu ý**: Kiểm tra xem tất cả sub-workflow đã hoàn thành chưa.

6. **Node `Call Resume on Parent Workflow` (HTTP Request)**
   - **URL**: `{{ $json["parentUrl"] }}` (được truyền từ sub-workflow).
   - **HTTP Method**: `POST`.
   - **Headers**:
     - `Content-Type`: `application/json`.
   - **Body**:
     ```json
     {
       "id": "{{ $node["Loop Over Items"].json["$.id"] }}",
       "status": "finished"
     }
     ```
   - **Lưu ý**: **URL này phải trỏ đến workflow chính** (cần cấu hình trong sub-workflow).

---

##### **B. Cấu hình Sub-Workflow Con**
Sub-workflow con **phải được tạo riêng** và kích hoạt trước khi workflow chính chạy.
1. **Node `Webhook` (trong sub-workflow)**
   - **Path**: `parallel-subworkflow` (không thay đổi).
   - **HTTP Method**: `POST`.
   - **Credentials**: **None**.
   - **Lưu ý**: **URL Base của n8n** phải được cấu hình trong **Settings → Webhooks**.

2. **Node `Start Sub-Workflow Logic` (Logic của sub-workflow)**
   - Các sếp có thể thêm **các node xử lý** (ví dụ: `HTTP Request`, `Google Sheets`, `Email`, `LLM`...) tùy thuộc vào yêu cầu.
   - **Lưu ý**: Sub-workflow **phải trả về 1 response** với:
     ```json
     {
       "url": "URL của workflow chính để báo cáo hoàn thành",
       "parentUrl": "URL của workflow chính để resume"
     }
     ```

3. **Node `Respond to Webhook` (trong sub-workflow)**
   - **Response**: Trả về JSON như trên.

---

#### **3. Kích hoạt ⚡️**
1. **Test run workflow chính**:
   - Nhấn **Test Workflow** → Chọn **Manual Trigger**.
   - Kiểm tra **sub-workflow** có chạy song song không.
2. **Kích hoạt workflow chính**:
   - Sau khi test thành công, **bật Active** cho workflow chính.
3. **Kích hoạt sub-workflow**:
   - Các sub-workflow **phải được kích hoạt riêng** trước khi workflow chính chạy.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Thêm Logs cho Debug**
   - Sử dụng **node `Set`** để lưu lịch sử vào **Google Sheets** hoặc **Slack**.
   - Ví dụ:
     ```javascript
     // Trong node Code (Update finishedSet)
     const finishedSet = $node["Initialize finishedSet"].json["finishedSet"];
     finishedSet.push({ id: $node["Loop Over Items"].json["$.id"], status: "finished" });
     $node["Update finishedSet"].json["finishedSet"] = finishedSet;
     ```

2. **Gửi Báo Cáo Định Kỳ**
   - Sử dụng **node `HTTP Request`** để gửi báo cáo kết quả qua **Email** hoặc **Slack**.
   - Ví dụ:
     ```json
     {
       "text": `Tất cả ${finishedSet.length} sub-workflow đã hoàn thành!`,
       "attachments": [
         {
           "title": "Danh sách sub-workflow",
           "fields": [
             { "title": "ID", "value": "Status", "short": true }
           ]
         }
       ]
     }
     ```

3. **Kết hợp với AI (LLM)**
   - Sử dụng **node `LLM`** để phân tích kết quả của sub-workflow.
   - Ví dụ: Gửi kết quả vào **ChatGPT** để tổng kết.

4. **Tối ưu Thời Gian Chờ**
   - Thay đổi **thời gian chờ** trong node `Wait` để phù hợp với tốc độ của sub-workflow.

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** để các sếp:
✔ **Chạy nhiều nhiệm vụ song song** mà không lo mất kiểm soát.
✔ **Chờ tất cả hoàn thành** trước khi tiếp tục quy trình chính.
✔ **Tự động hóa hoàn toàn** mà không cần viết code.

**Hành động ngay**:
1. **Tạo sub-workflow** và liên kết với workflow chính.
2. **Test run** và điều chỉnh logic nếu cần.
3. **Kích hoạt workflow** và bắt đầu tự động hóa!

👉 **Bắt đầu từ [n8n.io/workflows/2536](https://n8n.io/workflows/2536) ngay hôm nay!**