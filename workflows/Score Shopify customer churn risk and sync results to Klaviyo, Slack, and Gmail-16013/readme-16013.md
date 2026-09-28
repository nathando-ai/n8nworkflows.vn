---
title: "🚀 **Tự Động Hóa Đánh Giá Rủi Ro Churn Khách Hàng Shopify & Đồng Bộ Hóa Kết Quả Với Klaviyo, Slack & Gmail**"
description: "Giải pháp tự động hóa 100% không code để dự đoán khách hàng có nguy cơ rời đi, đồng bộ dữ liệu vào Klaviyo, cảnh báo qua Slack/Gmail và báo cáo định kỳ hàng tuần. Tiết kiệm thời gian phân tích thủ công, giảm thiểu mất khách hàng và tối ưu hóa chiến dịch marketing."
slug: "tieu-dong-hoa-danh-gia-churn-khach-hang-shopify"
tags: [n8n, automation, Shopify, Klaviyo, CRM, AI, no-code, e-commerce, Slack, Gmail]
keywords: [tự động hóa churn Shopify, dự đoán rời đi khách hàng, đồng bộ Klaviyo n8n, cảnh báo Slack Gmail, workflow tự động hóa e-commerce, giảm thiểu mất khách hàng]
---

# 🚀 **Tự Động Hóa Đánh Giá Rủi Ro Churn Khách Hàng Shopify & Đồng Bộ Hóa Kết Quả Với Klaviyo, Slack & Gmail**

### **Giải pháp cho những sếp e-commerce đang mất khách hàng vì không biết ai sẽ rời đi trước**
Bạn đã từng phải **quét thủ công** danh sách khách hàng, tính toán khoảng cách giữa các lần mua hàng, và lo lắng không biết ai sẽ rời đi trong tuần tới? Hay phải **phân tích dữ liệu** để quyết định gửi email khuyến mãi cho khách hàng "ngủ yên" mà không biết họ có thực sự cần không?

**Workflow này sẽ:**
✅ **Dự đoán chính xác** khách hàng có nguy cơ rời đi dựa trên **thói quen mua hàng cá nhân** (không dựa vào ngày tháng cố định).
✅ **Đồng bộ tự động** dữ liệu `churn_risk` và `days_since_last_order` vào **Klaviyo** để marketing team có thể hành động kịp thời.
✅ **Cảnh báo ngay** qua **Slack** và **Gmail** với báo cáo chi tiết (CSV đính kèm) khi có khách hàng ở mức **rủi ro trung bình hoặc cao**.
✅ **Chạy tự động hàng tuần** mà không cần can thiệp thủ công.

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm 10-15 giờ/tháng** phân tích dữ liệu thủ công.
- **Giảm thiểu mất khách hàng** bằng cách phát hiện và hành động trước khi họ rời đi.
- **Cá nhân hóa marketing** với dữ liệu chính xác về `churn_risk` trên Klaviyo.
- **Báo cáo tự động** hàng tuần với CSV chi tiết, dễ dàng chia sẻ với team.
- **Hệ thống hóa quy trình** để không phụ thuộc vào ai đó "quên" gửi email khuyến mãi.
:::

---
## 🔧 **Yêu cầu cần thiết**
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Shopify Admin** với **API Token** (để truy cập GraphQL API).
2. **Tài khoản Klaviyo** với **Private API Key**.
3. **Tài khoản Gmail** (để gửi email cảnh báo, cần **OAuth2**).
4. **Tài khoản Slack** (để gửi cảnh báo, cần **API Token**).
5. **VPS n8n** (để chạy workflow 24/7, không phụ thuộc vào máy tính cá nhân).

:::info[**Gợi ý hạ tầng cho n8n**]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/16013](https://n8n.io/workflows/16013) và import vào **n8n Editor**.
- **Cách 2:** Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/16013) và dán vào **Import Workflow** trong n8n.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này có **22 node** và cần cấu hình chi tiết như sau:

#### **A. Cấu hình cơ bản (Node "Set Workflow Config")**
- **Shopify Domain:** Nhập domain của shop (ví dụ: `tudonghoa.shopify.com`).
- **Toggles:**
  - `emailAlert` → `true` (nếu muốn gửi email cảnh báo).
  - `slackAlert` → `true` (nếu muốn cảnh báo Slack).
  - `klaviyoEvent` → `true` (nếu muốn đồng bộ dữ liệu vào Klaviyo).
- **Thresholds (có thể điều chỉnh):**
  - `customerActiveDays` → Số ngày xem xét lịch sử mua (mặc định: **180**).
  - `minimumOrderRequired` → Số lần mua tối thiểu để tính toán (mặc định: **3**).
  - `safeDays` → Loại bỏ khách hàng mua gần đây (mặc định: **30**).

#### **B. Cấu hình API & Credentials**
| **Node**               | **Yêu cầu**                                                                 | **Lưu ý**                                                                 |
|------------------------|-----------------------------------------------------------------------------|---------------------------------------------------------------------------|
| **Fetch Customer Data** | API Token Shopify (Header Auth)                                            | Lấy từ **Shopify Admin → Apps → API Credentials**.                        |
| **Send to Klaviyo API** | Klaviyo Private API Key (Header Auth)                                       | Lấy từ **Klaviyo → Settings → API Keys**.                                |
| **Send Email Alert**    | Gmail OAuth2 (đăng nhập tài khoản Gmail)                                   | Cần cấp quyền cho n8n truy cập email.                                  |
| **Send CSV to Slack**   | Slack API Token (đăng ký tại [api.slack.com](https://api.slack.com))        | Chọn **Bot Token** và cấp quyền `files:write`, `chat:write`.            |
| **Post Error to Slack** | Slack API Token (giống trên)                                                | Dùng cùng token với node Slack khác.                                    |

#### **C. Cấu hình Node "Calculate Churn Risk" (Code)**
- **Logic tính toán:**
  - **MEDIUM RISK:** Khách hàng mua với khoảng cách **>1.5x** so với trung bình.
  - **HIGH RISK:** Khách hàng mua với khoảng cách **>2.0x** so với trung bình.
- **Không cần chỉnh sửa** nếu muốn sử dụng logic mặc định.

#### **D. Node "Fetch Customer Data" (GraphQL)**
- **Query mặc định** đã lấy tất cả khách hàng (paginated, 100/lần).
- **Không cần chỉnh sửa** trừ khi muốn lọc thêm điều kiện (ví dụ: chỉ khách hàng mua trong 6 tháng qua).

#### **E. Node "Send CSV to Slack" & "Send Email Alert"**
- **Tên file CSV:** `churn_risk_report_<ngày-tháng-năm>.csv`.
- **Nội dung email/Slack:** Bao gồm:
  - Tổng số khách hàng ở mức **MEDIUM** và **HIGH RISK**.
  - Tổng doanh thu có nguy cơ mất.
  - **CSV đính kèm** với danh sách chi tiết.

---
### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Chọn **Fetch Customer Data** → **Run**.
   - Kiểm tra kết quả trong **Aggregate Churn Results** và **Combine Export Data**.
2. **Bật Active workflow**:
   - Đảm bảo **Weekly Schedule Trigger** được kích hoạt (cài đặt ngày giờ chạy hàng tuần).
   - Kiểm tra **On Global Error** để đảm bảo lỗi sẽ được báo cáo Slack.

---
## ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết hợp với Zapier/Make:**
   - Nếu muốn gửi **email cá nhân hóa** cho từng khách hàng ở mức **HIGH RISK**, có thể kết nối với **Zapier** hoặc **Make** để tự động gửi email từ Gmail/Outlook.

2. **Lưu log vào Google Sheets:**
   - Thêm node **Google Sheets** để ghi lại **tất cả các lần chạy**, bao gồm:
     - Ngày chạy.
     - Số khách hàng ở mức **MEDIUM/HIGH**.
     - Doanh thu có nguy cơ mất.
     - Link CSV.

3. **Cảnh báo qua Telegram:**
   - Thay thế node Slack bằng **Telegram Bot** để nhận cảnh báo trên điện thoại.

4. **Tự động gửi báo cáo định kỳ cho CEO:**
   - Sử dụng **n8n Schedule Trigger** để gửi **tóm tắt báo cáo hàng tháng** qua email.

5. **Tối ưu hóa Klaviyo:**
   - Sau khi đồng bộ `churn_risk`, có thể tạo **flow tự động** trong Klaviyo để:
     - Gửi **email khuyến mãi** cho khách hàng **MEDIUM RISK**.
     - Gửi **câu hỏi khảo sát** cho khách hàng **HIGH RISK** để hiểu lý do rời đi.

---
## 📌 **Kết luận**
Workflow này **giải quyết vấn đề mất khách hàng** một cách **tự động hóa hoàn toàn**, giúp các sếp:
✔ **Tiết kiệm thời gian** phân tích thủ công.
✔ **Cảnh báo kịp thời** trước khi khách hàng rời đi.
✔ **Cá nhân hóa marketing** với dữ liệu chính xác.
✔ **Báo cáo tự động** hàng tuần với CSV chi tiết.

**Hành động ngay:**
1. **Import workflow** và cấu hình theo hướng dẫn trên.
2. **Test Run** trước khi kích hoạt.
3. **Bật Schedule Trigger** để chạy hàng tuần.

**Nếu có vấn đề, hãy để lại comment bên dưới hoặc liên hệ với team Tricore Infotech (tác giả của workflow) để hỗ trợ!** 🚀

---
**🔗 [Tải workflow nguyên bản tại n8n.io](https://n8n.io/workflows/16013)**
**📌 [Cài đặt VPS n8n với mã giảm giá](https://tino.vn/vps-n8n?affid=388)**