---
title: "🚀 Tự Động Hóa Xử Lý Song Song (Parallel) & Bất Đồng Bộ (Async) với n8n"
description: "Hướng dẫn chi tiết cách xây dựng workflow n8n để chạy nhiều tác vụ dài hạn song song, không bị chặn (blocking), và tổng hợp kết quả tự động."
slug: "tu-dong-hoa-xu-ly-song-song-async-n8n"
tags: [n8n, automation, parallel-processing, asynchronous, workflow-design]
keywords: [n8n parallel workflow, n8n async processing, xử lý song song n8n, tự động hóa batch, n8n wait node]
---

# 🚀 Tự Động Hóa Xử Lý Song Song (Parallel) & Bất Đồng Bộ (Async) với n8n

Trong các quy trình tự động hóa phức tạp, các sếp thường gặp phải "nỗi đau" kinh điển: **Workflow bị treo (hang) hoặc chậm chạp** khi phải chờ đợi các tác vụ dài hạn như gọi API bên thứ ba, xử lý dữ liệu lớn, hoặc chờ phản hồi từ hệ thống khác. Nếu chạy tuần tự (sequential), thời gian tổng sẽ là tổng thời gian của từng bước. Nhưng nếu ta có thể chạy chúng **song song (parallel)** và **bất đồng bộ (asynchronous)**, hiệu suất sẽ tăng lên gấp bội.

Workflow này là một Proof-of-Concept (POC) hoàn chỉnh giúp các sếp nắm bắt cách n8n xử lý các tác vụ chạy nền (background tasks). Thay vì để workflow chính "ngồi chờ" (blocking), nó sẽ kích hoạt các sub-workflow, sau đó tạm dừng (Wait) cho đến khi các tác vụ con hoàn thành và gửi tín hiệu (Webhook) trở lại. Kết quả là một quy trình mượt mà, không nghẽn cổ chai, và có khả năng mở rộng cực tốt.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, đặc biệt là khi xử lý các tác vụ bất đồng bộ và webhook, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tăng tốc độ xử lý:** Chạy nhiều tác vụ độc lập cùng lúc, giảm tổng thời gian hoàn thành workflow xuống tối đa.
- **Không nghẽn tài nguyên:** Workflow chính không bị "đóng băng" (blocking) trong thời gian chờ, giúp n8n instance có thể xử lý các workflow khác song song.
- **Kiểm soát luồng dữ liệu chặt chẽ:** Sử dụng `Wait` node và `Merge` node để đảm bảo tất cả các kết quả từ các nhánh song song đều được thu thập và tổng hợp trước khi bước sang giai đoạn tiếp theo.
- **Mô hình kiến trúc mở rộng:** Dễ dàng nhân bản để chạy 10, 50 hoặc 100 tác vụ song song chỉ bằng cách thêm các nhánh `Execute Workflow` và `Wait`.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** Bản Community (Self-hosted) hoặc Cloud.
- **Hiểu biết cơ bản về n8n:** Biết cách import workflow, cấu hình credentials và hiểu khái niệm về Webhook.
- **Không cần API Key bên thứ ba:** Workflow này là POC (Proof of Concept) dùng các node cơ bản của n8n (`Wait`, `HTTP Request`, `Execute Workflow`) để mô phỏng, nên các sếp có thể chạy ngay mà không cần đăng ký dịch vụ bên ngoài.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Workflow này bao gồm **2 phần** (Main Orchestrator và Asynchronous Worker). Các sếp cần import cả 2 file JSON (hoặc copy 2 workflow) vào n8n.
1. Vào n8n Editor -> **Import from URL** hoặc **Import from File**.
2. Import workflow chính (Main Orchestrator).
3. Import workflow con (Asynchronous Worker).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

Đây là phần quan trọng nhất. Workflow hoạt động dựa trên cơ chế **Trigger -> Execute -> Wait -> Webhook Callback**.

**A. Cấu hình Workflow Con (Asynchronous Worker):**
1. Mở workflow con.
2. Node `Start` (Manual Trigger) hoặc `Call Entry Point` (Execute Workflow Trigger): Đảm bảo node này được cấu hình để nhận dữ liệu đầu vào.
3. Node `Request Webhook`: Đây là node `HTTP Request` dùng để gọi lại webhook của workflow chính khi hoàn thành.
   - **Lưu ý quan trọng:** Các sếp cần thay thế URL trong node này bằng **Webhook URL** của workflow chính (sẽ lấy ở bước B bên dưới).
   - Hoặc, nếu workflow chính có cấu hình `Wait for Webhook`, n8n sẽ tự động sinh ra URL webhook. Các sếp cần copy URL đó và dán vào node `Request Webhook` của workflow con.

**B. Cấu hình Workflow Chính (Main Orchestrator):**
1. **Node `Call 1` và `Call 2` (Execute Workflow):**
   - Chọn workflow con (Asynchronous Worker) từ dropdown.
   - **Quan trọng:** Trong cài đặt của node `Execute Workflow`, các sếp cần bật tùy chọn **"Wait for Sub-workflow Completion"**? 
     - *Sửa lại:* Thực tế, trong pattern Async này, ta **KHÔNG** bật "Wait for Sub-workflow Completion" ở node Execute Workflow nếu muốn nó chạy nền ngay lập tức. Thay vào đó, ta dùng node `Wait` để chờ tín hiệu webhook.
     - Tuy nhiên, template này sử dụng cơ chế: `Execute Workflow` (chạy nền) -> `Wait` (chờ webhook).
     - Hãy đảm bảo node `Execute Workflow` được cấu hình để **không** blocking.
2. **Node `Wait for Webhook 1` và `Wait for Webhook 2`:**
   - Đây là các node `Wait` với chế độ **"Wait for Webhook"**.
   - Mỗi node này sẽ tạo ra một **Webhook URL** duy nhất.
   - **Bước bắt buộc:** Copy Webhook URL của `Wait for Webhook 1` và dán vào node `Request Webhook` (trong workflow con) cho lần gọi thứ 1.
   - Copy Webhook URL của `Wait for Webhook 2` và dán vào node `Request Webhook` (trong workflow con) cho lần gọi thứ 2.
   - *Mẹo:* Nếu các sếp muốn tái sử dụng workflow con cho nhiều lần gọi, hãy truyền Webhook URL như một tham số (input) từ workflow chính sang workflow con, thay vì hardcode.
3. **Node `Merge`:**
   - Đảm bảo cấu hình Merge node nhận input từ cả `Wait for Webhook 1` và `Wait for Webhook 2`.
   - Chế độ Merge: Chọn **"Append"** hoặc **"Combine by Position"** tùy thuộc vào cấu trúc dữ liệu trả về.
4. **Node `Sum` (Summarize):**
   - Node này sẽ tổng hợp dữ liệu từ Merge node. Các sếp có thể chỉnh sửa prompt hoặc logic summarize nếu cần.

**C. Kiểm tra liên kết:**
- Đảm bảo rằng khi workflow con chạy xong, nó gọi đúng Webhook URL của workflow chính.
- Workflow chính sẽ "thức dậy" từ trạng thái `Wait` khi nhận được webhook.

#### 3. Kích hoạt ⚡️
1. **Test Run:**
   - Chạy workflow chính bằng nút **Execute Workflow**.
   - Quan sát: Workflow sẽ chạy nhanh qua `Call 1` và `Call 2`, sau đó dừng lại tại các node `Wait`.
   - Các workflow con sẽ chạy nền. Khi chúng hoàn thành và gọi webhook, workflow chính sẽ tiếp tục.
   - Kiểm tra output cuối cùng tại node `Sum`.
2. **Bật Active:**
   - Sau khi test thành công, bật **Active** cho cả 2 workflow.
   - Lưu ý: Workflow con cần Active để có thể được gọi bởi workflow chính.

### ✍️ Mẹo & gợi ý nâng cao
- **Động hóa số lượng tác vụ:** Thay vì hardcode 2 nhánh `Call 1` và `Call 2`, các sếp có thể sử dụng node `Split In Batches` hoặc `Loop Over Items` để tạo ra N nhánh song song dựa trên dữ liệu đầu vào (ví dụ: xử lý 100 email cùng lúc).
- **Xử lý lỗi (Error Handling):** Thêm node `Error Trigger` vào workflow con để gửi thông báo (Slack/Email) nếu một tác vụ con thất bại, thay vì để workflow chính chờ mãi.
- **Timeout:** Cấu hình thời gian chờ tối đa cho node `Wait`. Nếu webhook không đến sau 5 phút, workflow nên tự động bỏ qua hoặc báo lỗi để tránh treo.
- **Ghi log:** Thêm node `Write to Google Sheets` hoặc `Postgres` sau node `Sum` để lưu lại lịch sử các lần chạy song song, giúp theo dõi hiệu suất và debug.

### 📌 Kết luận
Việc nắm vững pattern **Asynchronous Parallel Processing** trong n8n sẽ giúp các sếp nâng cấp hệ thống tự động hóa từ mức "chạy được" lên mức "chạy nhanh và ổn định". Workflow này là nền tảng vững chắc để xây dựng các hệ thống batch processing, data pipeline phức tạp, hoặc bất kỳ quy trình nào yêu cầu hiệu suất cao. Hãy import, thử nghiệm và tùy biến theo nhu cầu thực tế của doanh nghiệp!