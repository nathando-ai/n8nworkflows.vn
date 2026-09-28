---
title: "🚀 Tạo Bot Try-On Áo Mặc ảo trên Telegram với AI - Tự Động Hóa 100% Không Code"
description: "Workflow này giúp các sếp xây dựng một bot Telegram AI tự động tạo hình ảnh thử áo mặc ảo từ ảnh người dùng và sản phẩm. Tiết kiệm thời gian thiết kế, tăng trải nghiệm khách hàng, và hoạt động liên tục 24/7."
slug: "tao-bot-try-on-ao-mac-ao-telegram-ai"
tags: [n8n, automation, no-code, ai-chatbot, content-creation, google-sheets, telegram-bot]
keywords: [n8n workflow try-on, tự động hóa bot Telegram, AI try-on áo mặc, google sheets n8n, tự động hóa e-commerce]
---

# 🚀 Bot Try-On Áo Mặc ảo trên Telegram với AI - Hướng Dẫn Cài Đặt & Sử Dụng

## 💡 Giải quyết vấn đề gì?
Các sếp trong ngành **e-commerce, thời trang, hoặc marketing** thường phải đối mặt với những thách thức sau khi bán hàng trực tuyến:
- **Khách hàng khó hình dung** sản phẩm trên mình.
- **Quá trình thiết kế hình ảnh thử áo** tốn thời gian và chi phí.
- **Không có giải pháp tự động hóa** để cá nhân hóa trải nghiệm mua sắm.

Workflow này **giải quyết tất cả** bằng cách tạo một **bot Telegram AI tự động** cho phép khách hàng:
✅ **Gửi ảnh chân dung** của mình.
✅ **Gửi ảnh sản phẩm** (ví dụ: áo, quần) với caption `garment`.
✅ **Nhận kết quả** là hình ảnh AI "đóng" sản phẩm lên người trong vài giây!

---

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian thiết kế**: Không cần phải tạo hình ảnh thủ công cho từng sản phẩm.
- **Tăng trải nghiệm khách hàng**: Khách hàng cảm thấy được **cá nhân hóa** và hài lòng hơn.
- **Hoạt động liên tục 24/7**: Bot hoạt động tự động, không cần can thiệp của nhân viên.
- **Tăng tỷ lệ chuyển đổi**: Hình ảnh thử áo ảo giúp khách hàng **quyết định mua hàng nhanh hơn**.
- **Dữ liệu khách hàng**: Lưu trữ thông tin người dùng trong Google Sheets để phân tích hành vi.
:::

---

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Telegram** và một **bot Telegram** (tạo tại [@BotFather](https://t.me/BotFather)).
2. **Google Sheets** với:
   - Một **bảng tên là `tryon-state`** có hai cột: `chat_id` và `person_file_id`.
   - **Chia sẻ quyền truy cập** cho n8n với quyền **Sửa đổi**.
3. **API Key của Try-On Service** (nếu không có, có thể sử dụng [AppStoneLab](https://appstonelab.com/) hoặc dịch vụ tương tự).
4. **VPS để self-host n8n** (khuyến nghị để workflow hoạt động 24/7).
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
5. **N8n Community Edition** đã cài đặt và chạy trên VPS.
:::

---

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Tải workflow từ [n8n.io/workflows/14006](https://n8n.io/workflows/14006).
2. Trên trang **n8n Editor**, nhấn **Import** và chọn file JSON.
3. Hoặc copy toàn bộ JSON và dán vào **Import Workflow** trong menu.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

#### 🔧 **Cấu hình Config Node (⚙️ Config)**
- **Tham số bắt buộc**:
  - `botToken`: **Token của bot Telegram** (lấy từ @BotFather).
  - `sheetId`: **ID của Google Sheet** (lấy từ URL của bảng, ví dụ: `https://docs.google.com/spreadsheets/d/1AbCdEfGhIjKlMnOpQrStUvWxYz/` → `1AbCdEfGhIjKlMnOpQrStUvWxYz`).
  - **Thêm các tham số này** (nếu cần):
    - `tryonApiKey`: API Key của dịch vụ Try-On (nếu không có, liên hệ AppStoneLab).
    - `tryonApiBase`: URL của API Try-On (ví dụ: `https://api.appstonelab.com/v1`).

#### 📄 **Cấu hình Google Sheets**
- **Tạo bảng `tryon-state`** với hai cột:
  - `chat_id` (lưu trữ ID chat Telegram của người dùng).
  - `person_file_id` (lưu trữ file ID của ảnh người dùng).
- **Chia sẻ bảng** với n8n bằng quyền **Sửa đổi** (n8n sẽ cần quyền này để ghi/xóa dữ liệu).

#### 🤖 **Cấu hình Telegram Credentials**
- Trong **n8n Credentials**, thêm một **Telegram API** với:
  - **Token**: Token bot Telegram (đã lấy từ @BotFather).
  - **Chat ID**: Để trống (n8n sẽ tự động lấy từ message).

#### 🔄 **Cấu hình Node `Has Photo?` và `Is Garment Photo?`**
- Các node này **kiểm tra điều kiện** để xác định:
  - Nếu message có ảnh → tiếp tục.
  - Nếu ảnh có caption `garment` → xử lý như ảnh sản phẩm.

#### 📥 **Node `Save Person to Sheet` và `Lookup Person from Sheet`**
- **Save Person to Sheet**: Lưu `chat_id` và `person_file_id` vào Google Sheets khi người dùng gửi ảnh.
- **Lookup Person from Sheet**: Tìm kiếm `chat_id` trong Sheets để lấy `person_file_id` khi người dùng gửi ảnh sản phẩm.

#### 🔄 **Node `Wait 15 Seconds` và Polling Loop**
- **Submit Try-On Job**: Gửi yêu cầu API Try-On và lấy `jobId`.
- **Check Job Status**: Kiểm tra trạng thái `jobId` sau mỗi 15 giây (đến khi hoàn thành hoặc thất bại).

#### 📥 **Node `Send Result Photo`**
- **Download result image** từ URL trả về của API Try-On trước khi gửi đến Telegram (đảm bảo hình ảnh không bị lỗi).

---

### ⚡️ Kích hoạt Workflow
1. **Test Run**:
   - Gửi một ảnh bất kỳ đến bot Telegram và kiểm tra phản hồi.
   - Nếu có lỗi, kiểm tra **Logs** trong n8n Editor.
2. **Bật Active**:
   - Sau khi cấu hình xong, nhấn **Active** để workflow bắt đầu hoạt động.

---

## ✍️ Mẹo & gợi ý nâng cao
:::info[TIẾP CẬN HƠN]
- **Thêm tính năng phản hồi nhanh**: Sử dụng **Slack/Telegram Admin Channel** để thông báo khi có yêu cầu mới.
- **Lưu log hoạt động**: Sử dụng **Google Sheets** hoặc **n8n Database** để lưu trữ lịch sử yêu cầu.
- **Gửi báo cáo định kỳ**: Tạo một workflow riêng để gửi báo cáo thống kê (ví dụ: số lượng yêu cầu, sản phẩm phổ biến).
- **Cải thiện UI bot**: Thêm **keyboard inline** cho Telegram để người dùng dễ dàng gửi ảnh.
- **Kết hợp với Shopify**: Sử dụng **n8n Shopify Node** để tự động tạo sản phẩm khi có yêu cầu try-on.
:::

---

## 📌 Kết luận
Workflow này **giải phóng thời gian** cho các sếp trong việc thiết kế hình ảnh thử áo và **tăng trải nghiệm khách hàng** một cách đáng kể. Với **Google Sheets làm bộ nhớ chia sẻ**, bot có thể xử lý nhiều yêu cầu đồng thời mà không mất dữ liệu.

🚀 **Hãy áp dụng ngay** và biến bot Telegram của mình thành **công cụ marketing mạnh mẽ** cho doanh nghiệp!

---
**Cần hỗ trợ?** Đăng ký **VPS n8n** tại [TinoHost](https://tino.vn/vps-n8n?affid=388) và liên hệ với chúng tôi để tối ưu hóa workflow!