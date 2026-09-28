---
title: "🚀 Tự động chụp ảnh màn hình website với Bright Data Web Unlocker & lưu vào Disk"
description: "Workflow n8n giúp bạn chụp screenshot bất kỳ trang web nào bằng proxy Bright Data, lưu ngay vào ổ đĩa mà không cần viết code."
slug: "capture-website-screenshot-bright-data"
tags: [n8n, automation, no-code, web-scraping, screenshot, bright-data]
keywords: [n8n workflow, tự động hóa, capture screenshot, bright data, lưu file, web unlocker]
---

# 🚀 Tự động chụp ảnh màn hình website với Bright Data Web Unlocker & lưu vào Disk

Khi các sếp còn phải mở trình duyệt, đăng nhập, chụp màn hình thủ công để lưu lại báo cáo, **thời gian** và **độ chính xác** luôn bị ảnh hưởng. Đặc biệt với các trang web có cơ chế chống bot, việc tự động lấy ảnh màn hình gần như không thể nếu không có proxy mạnh.  
Workflow này giải quyết **100%** vấn đề: chỉ cần nhập URL, tên file và zone của Bright Data, n8n sẽ tự động gọi Web Unlocker, lấy screenshot và lưu trực tiếp vào ổ đĩa – **không cần viết một dòng code nào**.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Chỉ vài giây để có screenshot thay vì vài phút thủ công.  
- **Độ chính xác cao**: Proxy Bright Data vượt qua hầu hết các cơ chế anti‑bot.  
- **Tự động hoá liên tục**: Có thể lên lịch chạy hàng ngày/giờ mà không gián đoạn.  
- **Lưu trữ ngay trên server**: File được ghi trực tiếp vào ổ đĩa, dễ dàng tích hợp với các quy trình khác.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản Bright Data** (trước đây là Luminati) với **Web Unlocker** được kích hoạt.  
- **API Token** hoặc **Header Authentication** cho Bright Data (sử dụng credential `httpHeaderAuth`).  
- **Zone** (region) của Bright Data mà bạn muốn dùng (ví dụ: `us-west`).  
- Đường dẫn **folder** trên server nơi lưu screenshot (ví dụ: `/home/n8n/screenshots`).  
- Quyền ghi (write) trên thư mục đã chọn.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n → **Workflows** → **Import**.  
2. Chọn **Upload JSON** và tải file JSON của workflow (hoặc copy toàn bộ JSON và dán vào ô **Import from Clipboard**).  
3. Nhấn **Import** → Workflow sẽ xuất hiện trên canvas.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Cấu hình cần thay đổi | Hướng dẫn chi tiết |
|------|----------------------|--------------------|
| **Set URL, Filename and Bright Data Zone** | - `url` (URL cần chụp) <br> - `filename` (tên file, ví dụ `homepage.png`) <br> - `zone` (Bright Data zone) | 1. Click vào node → **Set** → **Add Value** → Chọn **String** và nhập tên trường (`url`, `filename`, `zone`). <br>2. Điền giá trị thực tế cho từng trường. |
| **Capture a screenshot** (httpRequest) | - **Credentials**: chọn `httpHeaderAuth` đã cấu hình với token Bright Data. <br> - **URL**: `https://webunlocker.brightdata.com/screenshot` (hoặc endpoint do Bright Data cung cấp). <br> - **Query Parameters**: `url`, `zone` (được truyền từ node Set). | 1. Click node → **HTTP Request**. <br>2. Chọn **GET**. <br>3. Trong **Authentication**, chọn credential `httpHeaderAuth`. <br>4. Thêm **Query Parameters**: `url` = `{{$json["url"]}}`, `zone` = `{{$json["zone"]}}`. |
| **Write a file to disk** (readWriteFile) | - **Operation**: `write` (đã mặc định). <br> - **File Path**: `{{ $json["filename"] }}` hoặc đường dẫn đầy đủ như `/home/n8n/screenshots/{{$json["filename"]}}`. <br> - **Binary Data**: chọn **Binary Property** là `data` (được trả về từ node HTTP). | 1. Click node → **Read/Write File**. <br>2. Đặt **File Path** = `/home/n8n/screenshots/{{$json["filename"]}}`. <br>3. Trong **Binary Property**, nhập `data`. |
| **When clicking ‘Test workflow’** (manualTrigger) | Không cần cấu hình, dùng để test nhanh. | Nhấn **Execute Workflow** → **Run** để kiểm tra. |

> **Lưu ý:** Đảm bảo rằng **Binary Data** từ node `Capture a screenshot` được truyền đúng sang node `Write a file to disk`. Nếu không, file sẽ rỗng.

#### 3. Kích hoạt ⚡️
1. **Test run**: Nhấn nút **Execute Workflow** → **Run** trên node `manualTrigger`. Kiểm tra thư mục lưu file, xác nhận screenshot đã được tạo.  
2. Khi mọi thứ hoạt động ổn, bật **Active** (nút chuyển đổi ở góc trên bên phải).  
3. (Tuỳ chọn) Thêm **Cron** node để tự động chạy theo lịch (hàng ngày, mỗi giờ, …).

### ✍️ Mẹo & gợi ý nâng cao
- **Gửi screenshot qua Email**: Thêm node **Send Email** sau node `Write a file to disk`, đính kèm file vừa lưu.  
- **Thông báo Slack/Telegram**: Dùng node **Slack** hoặc **Telegram** để gửi link hoặc file tới kênh nhóm.  
- **Lưu trữ trên Cloud**: Thay node `Write a file to disk` bằng **AWS S3** hoặc **Google Cloud Storage** để có backup đa vùng.  
- **Lưu log chi tiết**: Thêm node **Set** + **Write Binary File** để ghi log JSON của mỗi lần chạy vào file `log.json`.  

### 📌 Kết luận
Với workflow này, các sếp có thể **tự động chụp ảnh màn hình** bất kỳ website nào, vượt qua các rào cản anti‑bot nhờ Bright Data, và **lưu trữ ngay trên server** để tích hợp vào báo cáo, dashboard hoặc quy trình CI/CD. Hãy triển khai ngay, tiết kiệm thời gian và tăng độ tin cậy cho công việc của bạn! 🚀