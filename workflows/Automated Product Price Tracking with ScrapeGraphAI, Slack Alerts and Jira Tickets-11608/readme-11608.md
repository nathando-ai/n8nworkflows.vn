---
title: "🚀 Tự Động Hóa Theo Dõi Giá Sản Phẩm với ScrapeGraphAI, Thông Báo Slack & Tạo Tickets Jira - Không Cần Code"
description: "Workflow tự động hóa theo dõi giá sản phẩm từ URL, so sánh với giá kỳ vọng, cảnh báo giảm giá lớn trên Slack và ghi nhận tất cả thay đổi vào Jira. Giúp doanh nghiệp tiết kiệm thời gian, tối ưu giá cả và phản ứng nhanh chóng với thị trường."
slug: "tu-dong-hoa-theo-doi-gia-san-pham-scrapegraphai-slack-jira"
tags: [n8n, automation, market-research, ai-summarization, scrapegraphai, jira, slack, no-code]
keywords: [tự động hóa theo dõi giá sản phẩm, n8n workflow, cảnh báo giảm giá, ScrapeGraphAI, Jira automation, Slack alert]
---

# 🚀 **Tự Động Hóa Theo Dõi Giá Sản Phẩm: Từ URL Đến Cảnh Báo Giá Giảm & Ghi Chép Tất Cả Thay Đổi**

### **Giải quyết vấn đề gì?**
Các sếp đang mất thời gian thủ công theo dõi giá sản phẩm trên các trang thương mại điện tử, so sánh với giá kỳ vọng, và phải nhớ ghi chép lại mọi thay đổi để phân tích sau? **Workflow này tự động hóa toàn bộ quy trình:**
- **Scrape** giá thực tế từ URL sản phẩm (thậm chí là trang web động).
- **So sánh** với giá kỳ vọng của bạn.
- **Cảnh báo** ngay khi giá giảm **10%+** trên Slack (để phản ứng kịp thời).
- **Ghi chép** tất cả thay đổi (ngay cả những thay đổi nhỏ) vào **Jira** để phân tích định kỳ.

Không cần viết một dòng code, chỉ cần **import workflow** và cấu hình 5 phút là hoạt động 24/7!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính bảo mật và không bị giới hạn API.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Không cần theo dõi thủ công hàng ngày.
✅ **Cảnh báo kịp thời**: Nhận thông báo Slack khi giá giảm **10%+** để có thể mua sắm hoặc điều chỉnh chiến lược.
✅ **Ghi chép toàn bộ dữ liệu**: Tất cả thay đổi (ngay cả nhỏ) được lưu vào **Jira** để phân tích tuần/month.
✅ **Hoạt động liên tục**: Workflow chạy tự động 24/7, không phụ thuộc vào giờ làm việc.
✅ **Dễ mở rộng**: Thêm logic mới (ví dụ: cảnh báo khi sản phẩm hết hàng) chỉ cần chỉnh **1 node**.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **ScrapeGraphAI API Key**:
   - Đăng ký tại [ScrapeGraphAI](https://scrapegraph.ai/) và lấy **API Key**.
   - *Lưu ý*: ScrapeGraphAI có giới hạn scrape/ngày, nên **không nên scrape quá nhiều URL cùng lúc** (xem phần **Mẹo nâng cao**).
2. **Credentials Slack**:
   - Tạo **App Slack** và lấy **Bot Token** (tại [API Slack](https://api.slack.com/apps)).
   - Chọn **channel** để nhận cảnh báo.
3. **Credentials Jira Cloud**:
   - Tạo **App Jira** và lấy **Email** + **API Token** (tại [Jira Cloud](https://id.atlassian.com/manage-profile/security/api-tokens)).
   - Chọn **Project Key** để tạo tickets.
4. **Webhook URL**:
   - Sau khi import workflow, **copy URL Webhook** từ node `Incoming Product List` để gửi dữ liệu từ hệ thống bên ngoài.

---
### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/11608](https://n8n.io/workflows/11608) và import vào **n8n Editor**.
- **Cách 2**: Copy toàn bộ JSON từ link trên và **paste** vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflows này có **11 node**, nhưng chỉ **3 node quan trọng** cần cấu hình kỹ:

##### **A. Node `Scrape Product Page` (ScrapeGraphAI)**
- **Tham số cần điền**:
  - **API Key**: Dán **API Key** từ ScrapeGraphAI vào trường `apiKey`.
  - **Throttling (giảm tải)**: Để mặc định `1000ms` (1 giây giữa mỗi scrape) để tránh bị chặn.
  - **Headers (nếu cần)**: Nếu trang web yêu cầu headers, thêm vào `headers` (ví dụ: `User-Agent`).

##### **B. Node `Significant Price Drop?` (IF)**
- **Điều kiện mặc định**: Kiểm tra `priceChangePercent < -10` (giá giảm **10%+**).
- **Lưu ý**:
  - Nếu muốn **cảnh báo giảm giá 5%** thay vì 10%, chỉnh `priceChangePercent < -5`.
  - Có thể thêm điều kiện khác (ví dụ: `season === "Summer"`).

##### **C. Node `Send Slack Message` & `Create an issue` (Jira)**
- **Slack**:
  - Chọn **channel** nhận cảnh báo.
  - Đảm bảo **Bot Token** có quyền gửi tin nhắn.
- **Jira**:
  - Chọn **Project Key** (ví dụ: `MARK`).
  - Đặt **Issue Type** là `Task` (hoặc `Bug` nếu muốn).
  - **Summary** và **Description** sẽ tự động được format từ dữ liệu scrape.

#### **3. Kích hoạt ⚡️**
1. **Test run** với dữ liệu mẫu:
   - Gửi **POST request** đến Webhook với payload:
     ```json
     {
       "products": [
         {
           "url": "https://example.com/product1",
           "expectedPrice": 19.99
         },
         {
           "url": "https://example.com/product2",
           "expectedPrice": 99.99
         }
       ]
     }
     ```
   - Kiểm tra Slack và Jira có nhận được thông báo không.
2. **Bật Active workflow** khi đã kiểm tra xong.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Throttling scrape**:
   - Nếu scrape quá nhiều URL cùng lúc, ScrapeGraphAI có thể **chặn IP**. Giải pháp:
     - Tăng `delay` trong node `SplitInBatches` (ví dụ: `2000ms` = 2 giây giữa mỗi scrape).
     - Sử dụng **node `Set`** để thêm `delay` động:
       ```javascript
       // Trong node Code (Validate & Prepare Data)
       $input.all().forEach((item, index) => {
         item.delay = (index * 1000); // Delay 1s giữa mỗi scrape
       });
       ```

2. **Lưu log scrape thành công/thất bại**:
   - Thêm **node `Set`** sau `Scrape Product Page` để ghi `status` (success/failure) vào `item`.
   - Sau đó, **route** các item thất bại đến **node `Slack`** để cảnh báo lỗi.

3. **Tạo báo cáo tuần/ngày**:
   - Sử dụng **node `Jira`** để tạo **daily report** với tổng số sản phẩm giảm giá, trung bình giảm bao nhiêu %, và danh sách sản phẩm.
   - Ví dụ:
     ```json
     {
       "summary": "Báo cáo Giá Sản Phẩm - Ngày 10/10/2024",
       "description": "Tổng số sản phẩm giảm giá: 5\nTrung bình giảm: 12%\nDanh sách:\n- [Product A](link) (-15%)"
     }
     ```

4. **Kết hợp với Google Sheets/Excel**:
   - Thay vì Jira, có thể **export** dữ liệu vào **Google Sheets** bằng node `Google Sheets`.
   - Cấu hình **automatically create new row** cho mỗi sản phẩm thay đổi.

5. **Cảnh báo email thay vì Slack**:
   - Thay node `Slack`, thêm **node `Email`** (n8n-nodes-base.email) để gửi cảnh báo đến email cá nhân.

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** của các sếp để tập trung vào chiến lược kinh doanh chứ không phải theo dõi giá sản phẩm thủ công. **Cài đặt chỉ mất 5 phút**, và sau đó nó hoạt động **tự động 24/7** với:
✔ **Cảnh báo giảm giá kịp thời** trên Slack.
✔ **Ghi chép tất cả thay đổi** vào Jira.
✔ **Dễ mở rộng** cho các logic mới.

**Hãy import ngay và bắt đầu tự động hóa theo dõi giá sản phẩm của mình!** 🚀
---
**Cần hỗ trợ?** Để lại comment bên dưới hoặc liên hệ tại [n8n Community](https://community.n8n.io/).