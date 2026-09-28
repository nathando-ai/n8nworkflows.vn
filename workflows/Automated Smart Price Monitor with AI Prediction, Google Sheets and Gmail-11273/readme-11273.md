---
title: "📈 **Hệ Thống Theo Dõi Giá Thông Minh Tự Động với AI + Google Sheets + Email (N8N)**"
description: "Tự động theo dõi giá sản phẩm trên Amazon (hoặc các website khác), dự đoán xu hướng giá bằng AI GPT-4o-mini, và gửi cảnh báo mua hàng qua email. Giúp các sếp tiết kiệm thời gian và tối ưu hóa quyết định mua bán."
slug: "automated-smart-price-monitor-n8n"
tags: [n8n, automation, market-research, ai-summarization, google-sheets, gmail, openai]
keywords: [tự động hóa theo dõi giá amazon, ai dự đoán xu hướng giá, n8n workflow, google sheets automation, cảnh báo mua hàng tự động]
---

# 🚀 **Hệ Thống Theo Dõi Giá Thông Minh Tự Động với AI, Google Sheets và Email**

## **Giải pháp cho các sếp muốn mua sắm thông minh**
Bạn đã bao giờ mệt mỏi vì phải thủ công theo dõi giá sản phẩm trên Amazon (hoặc các website khác) để tìm ra thời điểm mua hàng tốt nhất? Hay phải mất nhiều thời gian để phân tích xu hướng giá trong nhiều tháng? **Workflow này sẽ tự động hóa toàn bộ quá trình** với sự hỗ trợ của AI, giúp bạn:
✅ **Tự động lấy giá hiện tại** từ Amazon (hoặc website khác) mỗi ngày.
✅ **Dự đoán xu hướng giá** (tăng/giảm/ổn định) bằng AI GPT-4o-mini.
✅ **Cảnh báo qua email** khi giá đạt mức mục tiêu hoặc có xu hướng giảm.
✅ **Cập nhật lịch sử giá** trên Google Sheets với biểu đồ trực quan.
✅ **Tối ưu hóa quyết định mua bán** bằng dữ liệu thống kê và phân tích AI.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để tránh giới hạn của phiên bản miễn phí.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần theo dõi giá thủ công hàng ngày.
- **Dự đoán chính xác**: AI phân tích xu hướng giá trong 60 ngày để đưa ra quyết định mua bán thông minh.
- **Cảnh báo kịp thời**: Nhận email khi giá đạt mức mục tiêu hoặc có xu hướng giảm.
- **Dữ liệu toàn diện**: Lịch sử giá được cập nhật tự động trên Google Sheets với biểu đồ trực quan.
- **Tối ưu hóa chi phí**: Tránh mua hàng khi giá cao hoặc bỏ lỡ cơ hội giảm giá.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Sheets**:
   - **2 bảng Google Sheets** (cấu trúc chi tiết ở phần sau).
   - **Quản lý quyền OAuth2** cho Google Sheets (cài đặt trong n8n).
2. **Tài khoản Gmail**:
   - **Quản lý quyền OAuth2** để gửi email cảnh báo.
3. **API Key OpenAI**:
   - **Mã API OpenAI** (đăng ký tại [OpenAI](https://platform.openai.com/)).
4. **Danh sách sản phẩm**:
   - Danh sách sản phẩm trên Amazon (hoặc website khác) với các thông tin:
     - **URL sản phẩm** (Amazon).
     - **Tên sản phẩm**.
     - **Giá mục tiêu** (giá bạn muốn mua).
     - **Email nhận cảnh báo**.

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/11273](https://n8n.io/workflows/11273).
- **Import vào n8n Editor**:
  - Mở n8n Studio → Nhấn **"Import"** → Chọn file JSON.
  - **Hoặc copy/paste** JSON từ file vào ô **"Import Workflow"**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **16 node**, các bước quan trọng cần cấu hình:

##### **A. Cấu hình Google Sheets**
1. **Thiết lập OAuth2**:
   - Trong n8n, đi đến **"Credentials"** → **"Add"** → Chọn **"Google Sheets OAuth2"**.
   - Theo hướng dẫn để kết nối tài khoản Google Sheets.
2. **Tạo 2 bảng Google Sheets**:
   - **Bảng "Products"** (danh sách sản phẩm cần theo dõi).
     - **Cột bắt buộc**:
       - `URL_Product` (URL Amazon).
       - `Product_Name` (tên sản phẩm).
       - `Target_Price` (giá mục tiêu).
       - `User_Email` (email nhận cảnh báo).
   - **Bảng "Price History"** (lịch sử giá).
     - Cấu trúc tự động tạo khi chạy workflow.

##### **B. Cấu hình Gmail**
1. **Thiết lập OAuth2**:
   - Trong **"Credentials"** → **"Add"** → Chọn **"Gmail OAuth2"**.
   - Theo hướng dẫn để kết nối tài khoản Gmail.

##### **C. Cấu hình OpenAI**
1. **Thêm API Key**:
   - Trong **"Credentials"** → **"Add"** → Chọn **"OpenAI API"**.
   - Điền **API Key** từ OpenAI vào ô **"API Key"**.

##### **D. Cấu hình Node "Fetch Product Page"**
- **Selector CSS**:
  - Mặc định là `.a-price-whole` (cho Amazon).
  - **Nếu sử dụng website khác**, mở **DevTools (F12)** trên trang sản phẩm → Tìm thẻ HTML chứa giá → Cập nhật selector trong node **"Extract Price"**.

##### **E. Cấu hình Node "AI Agent"**
- **Model AI**:
  - Mặc định là `gpt-4o-mini` (rẻ và hiệu quả).
  - **Nếu muốn chất lượng cao hơn**, thay bằng `gpt-4o` (tốn kém hơn).

##### **F. Cấu hình Node "Send Email Alert"**
- **Chọn tài khoản Gmail**:
  - Trong node **"Send Email Alert"**, chọn **credentials** là **"gmailOAuth2"**.
- **Chủ đề và nội dung email**:
  - Workflow tự động tạo email với:
    - **Dự đoán xu hướng giá** (tăng/giảm/ổn định).
    - **Biểu đồ lịch sử giá** (link QuickChart.io).
    - **Đánh giá "Should Buy?"** (CÓ/KHÔNG).

##### **G. Cấu hình Node "Update Products Sheet"**
- **Cập nhật các trường**:
  - `Last_Price` (giá hiện tại).
  - `Last_Check` (thời gian kiểm tra).
  - `AI_Recommendation` (BUY/WAIT).
  - `AI_Confidence` (độ tin cậy %).
  - `Urgency_Score` (độ khẩn cấp 0-100).
  - `Predicted_Trend` (xu hướng giá).

---

#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Chọn node **"Manual Trigger"** → Nhấn **"Run Workflow"**.
   - Kiểm tra kết quả trên **Google Sheets** và **email**.
2. **Bật Active**:
   - Sau khi kiểm tra thành công, chuyển workflow sang **Active**.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tự động chạy hàng ngày**:
   - Thay đổi node **"Manual Trigger"** thành **"Schedule Trigger"** (ví dụ: chạy mỗi ngày lúc 8h sáng).
2. **Lưu log hoạt động**:
   - Thêm node **"Sticky Note"** để ghi lại lỗi hoặc thông tin debug.
3. **Kết hợp với Slack/Telegram**:
   - Thêm node **"Webhook"** để gửi cảnh báo đến Slack/Telegram thay vì email.
4. **Phân tích nhiều sản phẩm cùng lúc**:
   - Sử dụng node **"Split in Batches"** để xử lý nhiều sản phẩm hiệu quả.
5. **Tối ưu hóa AI**:
   - Cập nhật **prompt** trong node **"Prepare AI Data"** để AI phân tích chi tiết hơn.

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa việc theo dõi giá và tối ưu hóa quyết định mua bán. Với sự hỗ trợ của **AI GPT-4o-mini**, bạn sẽ không chỉ biết giá hiện tại mà còn dự đoán xu hướng trong tương lai, giúp tiết kiệm thời gian và tiền bạc.

**Hãy áp dụng ngay và bắt đầu mua sắm thông minh!** 🚀
---
**Liên hệ tác giả**:
- Tác giả: Prueba (Automation consultant).
- **Liên hệ**: [Custom Link](https://prueba.automation) (để yêu cầu hỗ trợ hoặc tùy chỉnh workflow).