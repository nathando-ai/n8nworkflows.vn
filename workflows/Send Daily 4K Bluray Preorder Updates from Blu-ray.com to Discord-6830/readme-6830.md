---
title: "🚀 Tự Động Hóa Báo Cáo Đơn Hàng Blu-ray 4K Mới Nhập Khẩu Từ Blu-ray.com Sang Discord Hàng Ngày"
description: "Giải pháp tự động hóa 100% không code để các sếp theo dõi tất cả các sản phẩm Blu-ray 4K mới được phát hành hàng ngày từ trang Blu-ray.com và gửi thông báo trực tiếp lên Discord. Tiết kiệm thời gian theo dõi thủ công, tránh bỏ lỡ bất kỳ sản phẩm mới nào."
slug: "tu-dong-hoa-bao-cao-bluray-4k-nhap-khau-sang-discord"
tags: [n8n, automation, market-research, discord, web-scraping]
keywords: [tự động hóa n8n, báo cáo sản phẩm mới, blu-ray 4K, web scraping, discord automation]
---

# 🚀 **Tự Động Hóa Báo Cáo Đơn Hàng Blu-ray 4K Mới Nhập Khẩu Từ Blu-ray.com Sang Discord**

### **🔍 Nỗi Đau Của Các Sếp**
Các sếp yêu thích phim Blu-ray 4K hay là những người theo dõi thị trường giải trí cao cấp thường phải **tốn thời gian hàng ngày** để:
- **Quét thủ công** trang Blu-ray.com để tìm kiếm sản phẩm mới được phát hành.
- **So sánh và lưu trữ** thông tin sản phẩm để không bỏ lỡ bất kỳ bộ phim hay chương trình mới nào.
- **Gửi thông báo** cho nhóm hoặc cộng đồng Discord để mọi người cùng theo dõi.

Với **workflow này**, các sếp sẽ **tự động hóa toàn bộ quá trình** chỉ trong vài phút thiết lập, giúp tiết kiệm **tối thiểu 30 phút/ngày** và **tránh bỏ lỡ bất kỳ sản phẩm mới nào**.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần quét trang web thủ công hàng ngày.
- **Tính chính xác cao**: Lấy dữ liệu trực tiếp từ nguồn chính thức (Blu-ray.com).
- **Cá nhân hóa thông báo**: Chỉ gửi thông tin sản phẩm mới, không có spam.
- **Hoạt động liên tục**: Chạy tự động hàng ngày vào thời gian đã thiết lập.
- **Tích hợp Discord**: Thông báo ngay lập tức cho nhóm hoặc channel riêng.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần:
1. **Tài khoản Blu-ray.com** (để xác thực nếu cần).
2. **Webhook Discord** (để gửi thông báo).
3. **Thời gian khu vực (TimeZone)** của các sếp (do workflow mặc định chạy vào **11h tối** theo GMT).
4. **n8n Self-hosted** (để chạy 24/7, không phụ thuộc vào phiên bản cloud).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/6830) (hoặc copy JSON từ trang này).
- Mở **n8n Editor** → Nhấn **"Import"** → Dán JSON và nhấn **"Import"**.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
##### **A. Cấu Hình Thời Gian Khu Vực (TimeZone)**
- Workflow mặc định chạy vào **11h tối theo GMT**.
- **Cần chỉnh lại** theo **thời gian khu vực của các sếp** để phù hợp:
  - Mở node **"Schedule Trigger"** → Chọn **"Time"** → Điền thời gian mới (ví dụ: `22:00` nếu các sếp ở Việt Nam).
  - **Lưu ý**: Nếu các sếp ở **Việt Nam (GMT+7)**, nên đặt thời gian là **6h sáng** (do workflow chạy vào **11h tối GMT** tương đương **6h sáng ngày hôm sau**).

##### **B. Kết Nối Webhook Discord**
- Mở node **"Post to Discord"** → Chọn **"Credentials"** → Chọn **"discordWebhookApi"**.
- Nhập **URL Webhook** của Discord channel cần gửi thông báo:
  - Mở Discord → Channel muốn gửi thông báo → Nhấn **3 chấm (⋮)** → **"Copy Link"** → **"Copy Webhook URL"**.
  - Dán URL vào trường **"Webhook URL"** trong node.

##### **C. Cấu Hình Node "Scrape Page"**
- Node này **trích xuất dữ liệu** từ trang Blu-ray.com.
- **Không cần chỉnh sửa** nếu trang web không thay đổi cấu trúc HTML.
- **Lưu ý**: Nếu trang web thay đổi, có thể cần chỉnh sửa node **"Get Hyperlinks"** để trích xuất dữ liệu chính xác.

##### **D. Cấu Hình Node "Format Message"**
- Node này **định dạng thông báo** trước khi gửi sang Discord.
- **Không cần chỉnh sửa** nếu các sếp muốn giữ mặc định.
- **Nếu muốn cá nhân hóa**:
  - Mở node **"Format Message"** → Chỉnh sửa **template** để thêm thông tin như:
    ```javascript
    `🎬 **BLU-RAY 4K NEW RELEASE ALERT** 🎬
    Ngày: ${{ $node["Format Todays Date"].json() }}
    Sản phẩm mới:
    ${{ $node["Get Hyperlinks"].json() | arrayMap(item => `- [${item.title}](${item.url})`) | arrayJoin("\n") }}`
    ```

#### **3. Kích Hoạt ⚡️**
- **Test Run** với dữ liệu mẫu:
  - Nhấn **"Execute Workflow"** để kiểm tra nếu không muốn chạy tự động.
  - Kiểm tra **Discord channel** đã nhận được thông báo chưa.
- **Bật Active**:
  - Sau khi kiểm tra thành công, **bật node "Schedule Trigger"** để workflow chạy tự động hàng ngày.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[TIẾP CẬN HƠN]
1. **Lưu Log Lịch Sử**:
   - Thêm node **"Set"** sau node **"Post to Discord"** để lưu thông tin sản phẩm vào **Google Sheets** hoặc **Database** để theo dõi lịch sử.
   - Cài đặt node **"Google Sheets"** và cấu hình để ghi dữ liệu vào sheet mới.

2. **Gửi Thông Báo Email**:
   - Thêm node **"Send Email"** (ví dụ: **Gmail** hoặc **SendGrid**) để gửi báo cáo hàng ngày cho email cá nhân.

3. **Kết Nối Telegram**:
   - Thay vì Discord, các sếp có thể sử dụng **Telegram Bot** để gửi thông báo.
   - Cài đặt node **"Telegram Bot"** và cấu hình webhook tương tự.

4. **Lọc Sản Phẩm Theo Loại**:
   - Sử dụng node **"Code"** để **lọc chỉ sản phẩm mới nhất** (ví dụ: chỉ Blu-ray 4K mới ra mắt trong tháng).
   - Ví dụ:
     ```javascript
     $node["Filter Todays Items"].json().filter(item => item.releaseDate >= new Date($node["Format Todays Date"].json()));
     ```

5. **Tự Động Chỉnh Sửa Thời Gian**:
   - Sử dụng **n8n API** hoặc **Zapier** để **cập nhật thời gian chạy** tự động khi các sếp thay đổi giờ làm việc.
:::

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp yêu thích phim Blu-ray 4K muốn **tự động hóa việc theo dõi sản phẩm mới** mà không cần mất thời gian quét trang web hàng ngày. Với **cấu hình đơn giản** và **tích hợp Discord**, các sếp sẽ **luôn được thông báo ngay lập tức** khi có sản phẩm mới ra mắt.

**🚀 Hãy áp dụng ngay và không bỏ lỡ bất kỳ bộ phim hay nào nữa!**

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::