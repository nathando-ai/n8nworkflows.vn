---
title: "🎯 Phân đoạn khách hàng WooCommerce bằng RFM Analysis - Tự động hóa Marketing Hiệu quả"
description: "Tự động phân tích hành vi mua hàng của khách hàng WooCommerce, phân đoạn theo RFM (Recency, Frequency, Monetary) và tạo báo cáo marketing tự động hàng tuần. Giúp các sếp tối ưu chiến dịch quảng cáo, tăng doanh thu và cá nhân hóa tương tác."
slug: "phan-segment-woocommerce-rfm-analysis"
tags: [n8n, automation, marketing, ecommerce, woocommerce, rfm-analysis]
keywords: [n8n workflow woocommerce, phân đoạn khách hàng, rfm analysis tự động, marketing automation, tự động hóa bán hàng online]
---

# 🚀 Phân đoạn khách hàng WooCommerce bằng RFM Analysis - Tự động hóa Marketing Hiệu quả

Bạn đã bao giờ cảm thấy khó khăn khi phải phân tích hàng trăm khách hàng WooCommerce để tìm ra những nhóm mục tiêu phù hợp cho chiến dịch marketing? Hay phải mất nhiều thời gian để thủ công tính toán chỉ số **Recency (Tần suất mua gần đây)**, **Frequency (Tần suất mua hàng)** và **Monetary (Giá trị mua hàng)** để phân loại khách hàng?

**Workflow này sẽ giải quyết tất cả những vấn đề đó!** Với chỉ một lần cấu hình, bạn sẽ tự động:
- **Lấy dữ liệu đơn hàng** từ WooCommerce hàng tuần.
- **Phân tích RFM** để phân loại khách hàng thành các nhóm mục tiêu (chẳng hạn: "Khách hàng tiềm năng", "Khách hàng trung thành", "Khách hàng tiềm năng tái mua").
- **Tạo báo cáo HTML** dễ đọc, giúp bạn đưa ra quyết định marketing chính xác và cá nhân hóa.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần phân tích thủ công hàng tuần.
- **Chiến dịch marketing chính xác**: Phân đoạn khách hàng theo hành vi mua hàng thực tế.
- **Tăng doanh thu**: Nhắm mục tiêu khách hàng có giá trị cao nhất.
- **Cá nhân hóa tương tác**: Gửi email, quảng cáo hoặc khuyến mãi phù hợp với từng nhóm khách hàng.
- **Báo cáo tự động**: Nhận file HTML chi tiết mỗi tuần để phân tích.
:::

---

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản WooCommerce** và **API Key**:
   - API Key của WooCommerce (tạo từ **WooCommerce → Settings → Advanced → REST API**).
   - Đảm bảo API Key có quyền truy cập vào dữ liệu đơn hàng (`wc_api`).
2. **Tài khoản n8n** (cài đặt trên VPS hoặc dùng phiên bản cloud miễn phí).
3. **Dữ liệu đơn hàng**: Workflow sẽ lấy tất cả đơn hàng từ WooCommerce (không giới hạn thời gian).
:::

---

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- **Bước 1**: Tải file JSON của workflow từ [đây](https://n8n.io/workflows/4880) hoặc copy toàn bộ mã JSON từ trang gốc.
- **Bước 2**: Mở **n8n Editor** (trên VPS hoặc phiên bản cloud).
- **Bước 3**:
  - Nếu import từ file JSON: Nhấn **Import** → Chọn file → **Import**.
  - Nếu copy/paste: Nhấn **Import** → Chọn **Paste JSON** → Dán mã → **Import**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
##### **A. Cấu hình WooCommerce API**
- Mở node **"Fetch Orders From WooCommerce"**.
- Nhấn **Credentials** → Chọn **"wooCommerceApi"** (nếu chưa có, tạo mới bằng **Add Credential**).
- Điền thông tin:
  - **API URL**: `https://[domain-of-your-store].com` (ví dụ: `https://tudong.com`).
  - **Consumer Key** và **Consumer Secret**: Lấy từ **WooCommerce → Settings → Advanced → REST API**.
  - **Authentication**: Chọn **OAuth 1.0a** (nếu dùng API OAuth) hoặc **Basic Auth** (nếu dùng API Key).

##### **B. Cấu hình RFM Analysis (Node Code)**
- Mở node **"Compute RFM Segmentation"**.
- **Lưu ý**: Workflow đã sử dụng mã JavaScript mặc định để tính toán RFM. Nếu muốn **cập nhật logic phân đoạn**, các sếp có thể chỉnh sửa mã trong tab **Code** của node này.
  - **Recency (R)**: Số ngày từ ngày mua gần nhất.
  - **Frequency (F)**: Số lần mua trong khoảng thời gian xác định.
  - **Monetary (M)**: Tổng giá trị mua hàng.
- **Cách phân đoạn mặc định**:
  - **Champions**: Khách hàng mua gần đây, tần suất cao và giá trị cao.
  - **Loyal Customers**: Mua thường xuyên, giá trị cao nhưng không gần đây.
  - **Potential Loyalists**: Mua gần đây, giá trị cao nhưng tần suất thấp.
  - **At Risk**: Mua gần đây, tần suất cao nhưng giá trị thấp.
  - **Can’t Lose Them**: Giá trị cao, tần suất cao nhưng không gần đây.
  - **Hibernating**: Mua gần đây, giá trị cao nhưng tần suất thấp.
  - **Lost**: Không mua trong thời gian dài.

##### **C. Cấu hình Báo cáo (Node HTML)**
- Mở node **"Build Report Page"**.
- Workflow sẽ tự động tạo một trang HTML với:
  - **Bảng phân đoạn khách hàng** (theo RFM).
  - **Gợi ý marketing** cho từng nhóm (ví dụ: "Gửi email khuyến mãi cho nhóm 'At Risk'").
- **Lưu ý**: Nếu muốn **cập nhật nội dung gợi ý**, mở tab **Code** trong node này và chỉnh sửa phần `Generate Segment Summary`.

#### 3. Kích hoạt ⚡️
- **Test Run**:
  - Nhấn **Manual Start** để chạy một lần và kiểm tra kết quả.
  - Kiểm tra node **"Build Report Page"** để xem báo cáo HTML được tạo ra.
- **Bật tự động hàng tuần**:
  - Mở node **"Weekly Trigger"**.
  - Nhấn **Edit** → Chọn **Active** và đặt ngày giờ chạy (mặc định là **Thứ 7 hàng tuần**).
  - Lưu và kích hoạt workflow.

---

### ✍️ Mẹo & gợi ý nâng cao
1. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram Bot** sau node **"Build Report Page"** để gửi báo cáo tự động mỗi tuần.
   - Cách làm: Tạo một node **Set** để lưu kết quả HTML vào một biến, rồi sử dụng node **Slack Webhook** để gửi tin nhắn với nội dung báo cáo.

2. **Lưu log và phân tích dài hạn**:
   - Thêm node **Google Sheets** hoặc **Airtable** sau node **"Compute RFM Segmentation"** để lưu dữ liệu RFM của khách hàng vào bảng tính.
   - Cách làm: Tạo một sheet mới với các cột: `Customer ID`, `Recency`, `Frequency`, `Monetary`, `Segment`.
   - Sau đó, sử dụng node **Google Sheets** với operation **Create Row**.

3. **Gửi email cá nhân hóa**:
   - Kết hợp với node **SendGrid** hoặc **Mailgun** để gửi email marketing cho từng nhóm khách hàng.
   - Ví dụ: Gửi email khuyến mãi cho nhóm **"At Risk"**, hoặc email cảm ơn cho nhóm **"Champions"**.

4. **Tối ưu chiến dịch quảng cáo**:
   - Sử dụng dữ liệu RFM để nhắm mục tiêu quảng cáo trên Facebook Ads, Google Ads hoặc Meta Business Suite.
   - Ví dụ: Nhắm nhóm **"Potential Loyalists"** với quảng cáo khuyến mãi đặc biệt.

---

### 📌 Kết luận
Workflow này giúp các sếp **tự động hóa phân đoạn khách hàng WooCommerce** một cách hiệu quả, tiết kiệm thời gian và cải thiện chiến dịch marketing. Bằng cách phân tích **Recency, Frequency và Monetary**, bạn có thể:
✅ **Nhắm mục tiêu chính xác** khách hàng có giá trị cao nhất.
✅ **Cá nhân hóa tương tác** để tăng tỷ lệ chuyển đổi.
✅ **Tối ưu hóa ngân sách marketing** bằng cách tập trung vào nhóm khách hàng phù hợp.

**Hãy áp dụng ngay workflow này và bắt đầu tự động hóa marketing của mình từ hôm nay!** 🚀

---
**💡 Lưu ý cuối cùng**:
- Nếu gặp lỗi với WooCommerce API, kiểm tra lại **Consumer Key** và **Consumer Secret**.
- Để nâng cao hiệu quả, các sếp có thể kết hợp với **Google Analytics** hoặc **Hotjar** để phân tích hành vi khách hàng thêm chi tiết.