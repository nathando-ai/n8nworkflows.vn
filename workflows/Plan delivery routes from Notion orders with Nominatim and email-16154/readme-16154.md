---
title: "🚀 Tự Động Hoàn Thành & Gửi Lộ Trình Giao Hàng Từ Notion Sang Email (Không Code)"
description: "Giải pháp tự động hóa hoàn toàn cho các doanh nghiệp giao hàng nhỏ (lunch box, bánh ngọt, meal prep) để tự động thu thập đơn hàng từ Notion, tính toán lộ trình giao hàng tối ưu bằng Nominatim, và gửi báo cáo định kỳ qua email. Tiết kiệm thời gian lên đến 80% so với cách làm thủ công."
slug: "tieu-dong-hoan-thanh-va-gui-lo-trinh-giao-hang-tu-notion-sang-email"
tags: [n8n, automation, notion, delivery, email, geocoding, no-code, self-hosted]
keywords: [n8n workflow giao hàng, tự động hóa lộ trình giao hàng, Notion + Nominatim, gửi báo cáo giao hàng qua email, tối ưu hóa lộ trình giao hàng]
---

# 🚀 **Tự Động Hoàn Thành & Gửi Lộ Trình Giao Hàng Từ Notion Sang Email (Không Code)**

## **Nỗi Đau Của Các Sếp Giao Hàng**
Hàng ngày, các sếp quản lý **lunch box, bánh ngọt, hoặc meal prep** phải:
✅ **Nhập đơn hàng thủ công** vào Notion (hoặc Excel) từ khách hàng gọi điện hoặc qua form.
✅ **Tính toán lộ trình giao hàng** bằng cách vẽ bản đồ trên Google Maps, tính khoảng cách giữa từng địa chỉ, và sắp xếp theo thứ tự gần nhất.
✅ **Ghi nhớ trạng thái thanh toán** (trả trước hay thu tại giao hàng) cho từng đơn.
✅ **Gửi báo cáo lộ trình** cho đội giao hàng trước khi bắt đầu ngày mới.

**Kết quả?** Thời gian mất **3-5 tiếng/tuần** chỉ để làm việc này, và dễ xảy ra **lỗi tính toán, quên địa chỉ, hoặc không cá nhân hóa** cho từng đơn hàng.

---
## **🎯 Kết Quả Các Sếp Nhận Được**
Sau khi áp dụng workflow này, các sếp sẽ:
✔ **Tự động hóa 100% quá trình** từ thu đơn đến gửi lộ trình (không cần code).
✔ **Tính toán lộ trình tối ưu** bằng thuật toán **Nearest-Neighbor** (gần nhất), giảm thời gian giao hàng.
✔ **Cá nhân hóa từng đơn** với thông tin **trạng thái thanh toán** ([PAID] hoặc [COLLECT ON DELIVERY]).
✔ **Gửi báo cáo định kỳ** (ví dụ: **6h tối thứ Sáu**) qua email, không cần can thiệp thủ công.
✔ **Giảm lỗi** do tính toán thủ công (không quên địa chỉ, không nhầm lộ trình).

---
## **🔧 Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✅ **Tài khoản Notion** (đã tạo **Internal Integration** và **Database** theo mẫu dưới đây).
✅ **Tài khoản SMTP** để gửi email (Gmail, SendGrid, hoặc server riêng).
✅ **API Key Nominatim** (miễn phí, không cần đăng ký).
✅ **n8n Self-hosted** (khuyến nghị để workflow hoạt động 24/7).

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
## **📊 Cấu Trúc Database Notion (Bắt Buộc)**
Workflow yêu cầu **Notion Database** có các cột sau (tên và tùy chọn **case-sensitive**):
| Tên Cột          | Loại Dữ liệu       | Ghi Chú                          |
|-------------------|---------------------|-----------------------------------|
| Customer Name     | Title               | Tên khách hàng                    |
| Order ID          | Text                | Mã đơn hàng (tự động sinh)       |
| Phone             | Phone               | Số điện thoại khách hàng         |
| Address           | Text                | Địa chỉ giao hàng                |
| Items             | Text                | Nội dung đơn (ví dụ: "1 bánh ngọt")|
| Total             | Number              | Tổng tiền                        |
| Day               | Select              | Ngày giao hàng (**Saturday/Sunday**) |
| Paid              | Checkbox            | Trạng thái thanh toán (✅/❌)     |
| Notes             | Text                | Ghi chú thêm                     |
| Status            | Select              | **pending/done**                  |
| Received At       | Date                | Thời gian nhận đơn               |

**Cách tạo:**
1. Tạo **Database** mới trong Notion.
2. Thêm các cột theo bảng trên.
3. **Chọn "Internal Integration"** trong Notion → **Add Integration** → Copy **Secret Key** để dùng trong n8n.

---
## **🚀 Cách Import & Cấu Hình Workflow**

### **1. Import Workflow từ JSON**
1. **Tải workflow** từ [n8n.io/workflows/16154](https://n8n.io/workflows/16154).
2. **Import vào n8n Editor**:
   - Nhấn **Import** → Chọn file JSON.
   - Hoặc **Copy JSON** và dán vào **Import Workflow** (Ctrl+Shift+V).

### **2. Cấu Hình Cần Thiết (Bắt Buộc)**
#### **A. Cấu Hình Notion**
1. **Thêm Credential Notion**:
   - Trong n8n, nhấn **Credentials** → **Add Credential** → **Notion**.
   - Nhập **Secret Key** từ Notion Integration.
2. **Điền Database ID**:
   - Mở node **"Notion: Create Order"** và **"Notion: Get Pending"**.
   - Tìm **Database ID** trong URL Notion của bạn (ví dụ: `https://www.notion.so/workspace/xxxxxxxxxxxxxxxxxxxxxxxxxx` → **xxxxxxxxxxxxxxxxxxxxxxxxxx** là ID cần điền).

#### **B. Cấu Hình Email (SMTP)**
1. **Thêm Credential SMTP**:
   - Nhấn **Credentials** → **Add Credential** → **Email**.
   - Chọn **SMTP** (ví dụ: Gmail).
   - Điền:
     - **Host**: `smtp.gmail.com`
     - **Port**: `465` (hoặc `587` cho TLS)
     - **Username**: Email của bạn
     - **Password**: **App Password** (nếu dùng Gmail, tạo tại [My Google Account → Security](https://myaccount.google.com/security))
     - **From Email**: Email gửi
     - **From Name**: Tên hiển thị (ví dụ: "Lộ Trình Giao Hàng")
2. **Cấu hình node "Email Plan"**:
   - Đặt **To Email** là email của đội giao hàng.
   - **Subject**: "Lộ Trình Giao Hàng - [Ngày]"

#### **C. Cấu Hình Schedule (Lịch Trình)**
- Mở node **"Friday 6pm Plan"** → Đặt **Cron Expression** thành:
  ```
  0 18 * * 5
  ```
  (Gửi lúc **6h tối thứ Sáu**).

#### **D. Test Run (Kiểm Tra Trước Khi Bật)**
1. Nhấn **Test Run** trên node **"Test Run"** để kiểm tra logic.
2. Kiểm tra email có nhận được không.

---
## **⚡ Kích Hoạt Workflow**
1. **Bật Active** trên workflow.
2. **Chia sẻ Form Thu Đơn**:
   - Mở node **"Order Intake Form"** → Copy **Production URL**.
   - Chia sẻ link này cho khách hàng để nhập đơn.

---
## **✍️ Mẹo & Nâng Cao**
### **1. Thay Đổi Ngày Giao Hàng**
- Mở node **"Notion: Get Pending"** → Filter **Day** thành ngày muốn giao (ví dụ: **Monday**).

### **2. Gửi Lộ Trình Qua Slack/Telegram**
- Thay node **"Email Plan"** bằng:
  - **Slack**: Nodes `slackWebhook` + `slackMessage`.
  - **Telegram**: Nodes `telegramSendMessage`.

### **3. Sử Dụng Geocoder Trả Tiền (Nếu Có Nhiều Đơn)**
- Thay node **"Geocode (Nominatim)"** bằng:
  - **Google Maps Geocoding** (nếu có API Key).
  - **Mapbox** (tốc độ nhanh hơn).

### **4. Lưu Log Lịch Sử**
- Thêm node **"Sticky Note"** để ghi lại lịch sử giao hàng.

---
## **📌 Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp giao hàng khỏi công việc thủ công, **tối ưu hóa lộ trình**, và **giảm lỗi** đáng kể. **Chỉ cần 10 phút cấu hình**, workflow sẽ hoạt động tự động hàng tuần!

**Bắt đầu ngay:**
1. **Import workflow** vào n8n.
2. **Cấu hình Notion + Email**.
3. **Bật Active** và chia sẻ form thu đơn!

👉 **Cần hỗ trợ?** Đăng ký VPS n8n tại [TinoHost](https://tino.vn/vps-n8n?affid=388) để workflow chạy 24/7!