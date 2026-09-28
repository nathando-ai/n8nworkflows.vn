---
title: "🔄 **Cách Tự Động Làm Lại Thao Tác Nếu Thất Bại (Trừ Lỗi Đã Biết) - Building Block N8n Chuyên Nghiệp**"
description: "Giải pháp tự động hóa thông minh giúp các sếp xử lý lại yêu cầu thất bại tự động (trừ các lỗi đã biết) với tối đa 3 lần thử lại, tiết kiệm thời gian và tránh thủ công. Phù hợp cho API calls, web scraping, hoặc bất kỳ thao tác tự động nào cần độ bền cao."
slug: "cach-tu-dong-lam-lai-thao-tac-neu-that-bai-tru-loi-da-biet"
tags: [n8n, automation, retry-logic, error-handling, no-code]
keywords: [n8n retry workflow, tự động hóa làm lại thất bại, xử lý lỗi API n8n, building block n8n, tự động hóa không cần code]
---

# 🔄 **Tự Động Làm Lại Thao Tác Nếu Thất Bại (Trừ Lỗi Đã Biết) - Building Block N8n**

Hãy tưởng tượng một tình huống: Các sếp đang tự động hóa một quy trình quan trọng như **gửi yêu cầu API**, **trích xuất dữ liệu từ web**, hoặc **cập nhật thông tin trên CRM** – nhưng mỗi khi gặp lỗi mạng, server down, hoặc timeout, toàn bộ quy trình **ngừng lại và phải can thiệp thủ công**. Điều này không chỉ tốn thời gian mà còn làm gián đoạn toàn bộ workflow.

**Workflow này là giải pháp hoàn hảo!** Nó cho phép các sếp **tự động làm lại thao tác thất bại tối đa 3 lần** (cấu hình được) **trừ khi lỗi là lỗi đã biết** (ví dụ: lỗi 404, 500, hoặc message lỗi cụ thể). Sau khi hết số lần thử lại, hệ thống sẽ **dừng và báo lỗi** để các sếp xử lý, thay vì phải chạy thủ công từng bước.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng. Dưới đây là 2 lựa chọn VPS chất lượng với **mã giảm giá độc quyền** dành cho các sếp:
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (Đảm bảo tốc độ cao, phù hợp cho n8n)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Không phải can thiệp thủ công mỗi khi gặp lỗi nhỏ.
✅ **Độ bền cao**: Thao tác tự động hóa **không ngừng** ngay cả khi gặp lỗi tạm thời.
✅ **Xử lý lỗi thông minh**: **Bỏ qua lỗi đã biết** (ví dụ: lỗi 404) và chỉ làm lại khi lỗi là **tạm thời** (timeout, server down).
✅ **Cấu hình linh hoạt**: Đặt số lần thử lại (default: 3) và thời gian chờ giữa các lần thử lại (default: 5s).
✅ **Dễ dàng mở rộng**: Thay thế node **"Replace Me"** bằng bất kỳ node nào cần tự động hóa (API, webhook, database...).
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi sử dụng workflow này, các sếp cần chuẩn bị:
- **Môi trường n8n self-hosted** (không dùng phiên bản cloud để đảm bảo ổn định).
- **Node "Replace Me"** (node này sẽ được thay thế bằng node thực tế của các sếp, ví dụ: **HTTP Request**, **Google Sheets**, **Slack Webhook**...).
- **Thông tin cấu hình lỗi đã biết** (status code hoặc message lỗi cụ thể để workflow **bỏ qua**).
- **Credentials** (API key, token, hoặc thông tin xác thực) nếu node cần kết nối với bên thứ ba.

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể **import** workflow này bằng cách:
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/2719) và upload lên **n8n Editor**.
- **Copy/paste JSON** từ file vào **n8n Editor** (đảm bảo không có lỗi syntax).

:::note[Lưu ý]
- **Không sử dụng phiên bản n8n cloud** vì không đảm bảo độ ổn định 24/7.
- **Không thay đổi tên node** trừ khi các sếp biết rõ cấu trúc logic.
:::

---

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này bao gồm **10 node**, nhưng các sếp chỉ cần **cấu hình 3 node quan trọng** sau:

##### **A. Cấu hình "Set max tries" (Đặt số lần thử lại)**
- Node: **"Set tries"** (type: `set`)
  - **Tham số cần chỉnh**:
    ```json
    {
      "tries": 3  // Default, nhưng các sếp có thể tăng lên 5-10 nếu cần
    }
    ```
  - **Lưu ý**: Số lần này quyết định **số lần workflow sẽ làm lại thao tác thất bại**.

##### **B. Cấu hình "Set Wait" (Thời gian chờ giữa các lần thử lại)**
- Node: **"Wait"** (type: `wait`)
  - **Tham số cần chỉnh**:
    ```json
    {
      "time": "5000"  // 5 giây (default), các sếp có thể tăng lên 10s-30s nếu server chậm
    }
    ```
  - **Lưu ý**: Thời gian này giúp **tránh overloading server** khi làm lại nhiều lần.

##### **C. Cấu hình "Catch known error" (Lọc lỗi đã biết)**
- Node: **"Catch known error"** (type: `if`)
  - **Cấu hình điều kiện**:
    - **Condition**: `$node["Replace Me"].json["statusCode"] == 404`** (hoặc `$node["Replace Me"].json["error"] == "Lỗi cụ thể"`).
    - **Lưu ý**:
      - **Thay thế `404` hoặc `Lỗi cụ thể`** bằng lỗi mà các sếp **không muốn làm lại** (ví dụ: lỗi 404, 403, hoặc message lỗi từ API).
      - **Nếu node trả về lỗi khác**, workflow sẽ **tiếp tục làm lại** (nếu còn tries left).

##### **D. Thay thế node "Replace Me"**
- Node: **"Replace Me"** (type: `noOp`)
  - **Cách thay thế**:
    1. **Xóa node này** và **thêm node thực tế** (ví dụ: **HTTP Request**, **Google Sheets**, **Slack**...).
    2. **Bật "Enable error branch"** trong **Node Settings** của node mới.
    3. **Kết nối output** như trong hình minh họa của workflow gốc.
  - **Ví dụ thực tế**:
    - Nếu các sếp muốn tự động hóa **gửi yêu cầu API**, thay thế bằng **HTTP Request**.
    - Nếu muốn **trích xuất dữ liệu từ website**, thay thế bằng **Browser Node** (n8n-nodes-base.browser).

##### **E. Kết nối output của node mới**
- Sau khi thay thế node, các sếp cần:
  1. **Kết nối output "Success"** của node mới đến node **"Success"** (noOp).
  2. **Kết nối output "Error"** của node mới đến node **"If tries left"** (if).

---

#### **3. Kích hoạt ⚡️**
Sau khi cấu hình xong:
1. **Test run** với dữ liệu mẫu (ví dụ: gửi yêu cầu API giả).
2. **Bật Active workflow** và **chạy thử** để kiểm tra:
   - Nếu thao tác thành công → **Dừng ở node "Success"**.
   - Nếu thao tác thất bại → **Workflow tự động làm lại** (nếu còn tries left).
   - Nếu hết tries và lỗi **không phải lỗi đã biết** → **Dừng và báo lỗi** (node "Retry limit reached").

---

### ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CÁCH DÙNG HIỆU QUẢ HƠN]
1. **Kết hợp với Slack/Telegram để báo lỗi**:
   - Thêm node **Slack Webhook** hoặc **Telegram Bot** vào **output "Error"** để nhận thông báo khi thất bại.
   - **Cấu hình message**:
     ```json
     {
       "text": "Lỗi tại thao tác: $node["Replace Me"].json["error"]\nLần thử lại thứ: $node["Set tries"].json["tries"]"
     }
     ```

2. **Lưu log vào Google Sheets/Notion**:
   - Thêm node **Google Sheets** hoặc **Notion** vào **output "Success"** và **"Error"** để theo dõi lịch sử.
   - **Cấu hình sheet**:
     ```json
     {
       "sheetName": "Log tự động hóa",
       "columns": ["Thời gian", "Status", "Lỗi (nếu có)", "Lần thử lại"]
     }
     ```

3. **Tăng số lần thử lại cho thao tác quan trọng**:
   - Đặt `tries: 5` hoặc `tries: 10` trong node **"Set tries"** nếu thao tác cần độ bền cao (ví dụ: API chậm phản hồi).

4. **Sử dụng Sticky Note để ghi chú**:
   - Node **"StickyNote"** có thể dùng để **ghi chú** về lỗi thường gặp hoặc hướng dẫn sửa chữa.
   - **Ví dụ**:
     ```json
     {
       "content": "Lỗi 503 thường xảy ra vào giờ cao điểm, thử lại sau 10s."
     }
     ```

5. **Tự động gửi báo cáo định kỳ**:
   - Kết hợp với **n8n Cron Trigger** để **gửi báo cáo tổng hợp** về thành công/thất bại hàng ngày.
:::

---

### 📌 **Kết luận**
Workflow **"Retry on fail except for known error"** là **building block không thể thiếu** cho các sếp muốn tự động hóa quy trình **không ngừng** mà không lo bị gián đoạn bởi lỗi tạm thời. Với **cấu hình đơn giản** và **logic thông minh**, nó giúp:
✔ **Tiết kiệm thời gian** bằng việc loại bỏ việc can thiệp thủ công.
✔ **Tăng độ tin cậy** của hệ thống tự động hóa.
✔ **Xử lý lỗi một cách thông minh** (bỏ qua lỗi đã biết, làm lại lỗi tạm thời).

**Hãy áp dụng ngay workflow này vào dự án của các sếp và trải nghiệm sự **tiện lợi và hiệu quả** mà nó mang lại!** 🚀

---
**🔹 Cần hỗ trợ cấu hình chi tiết?** Liên hệ với **Mario (Software Architect)** qua [đây](https://n8n.io/workflows/2719) để được tư vấn **các workflow tùy chỉnh** cho doanh nghiệp!