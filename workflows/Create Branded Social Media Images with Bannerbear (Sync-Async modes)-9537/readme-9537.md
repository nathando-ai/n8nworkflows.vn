---
title: "🎨 Tự Động Hóa Tạo Ảnh Social Media Branded Với Bannerbear (Sync & Async)"
description: "Workflow n8n giúp các sếp tự động tạo hàng loạt ảnh social media chuyên nghiệp, đồng nhất thương hiệu chỉ với vài dòng text, hỗ trợ cả chế độ đồng bộ và bất đồng bộ."
slug: "tu-dong-hoa-tao-anh-social-media-bannerbear"
tags: [n8n, bannerbear, social-media, marketing-automation, no-code]
keywords: [n8n workflow bannerbear, tự động hóa tạo ảnh, social media automation, bannerbear api, n8n marketing]
---

# 🎨 Tự Động Hóa Tạo Ảnh Social Media Branded Với Bannerbear (Sync & Async)

Trong kỷ nguyên nội dung số, việc thiếu đi những hình ảnh minh họa bắt mắt, đồng nhất về màu sắc và font chữ là một "nỗi đau" lớn của các team marketing và content creator. Mỗi khi có một bài đăng mới, các sếp thường phải mở Photoshop hoặc Canva, chỉnh sửa từng chi tiết, thay đổi text, và chờ đợi render. Quy trình thủ công này không chỉ tốn thời gian mà còn dễ gây ra sự lệch lạc về nhận diện thương hiệu (branding) nếu nhiều người cùng làm.

Workflow n8n này là giải pháp "chữa cháy" hoàn hảo. Nó kết nối trực tiếp với **Bannerbear** – nền tảng tạo ảnh API hàng đầu – để biến các dữ liệu text đơn giản thành những bức ảnh social media chuyên nghiệp, sẵn sàng đăng tải. Điểm đặc biệt của workflow này là hỗ trợ cả hai chế độ: **Synchronous (Đồng bộ)** cho nhu cầu nhanh gọn và **Asynchronous (Bất đồng bộ)** cho các tác vụ nặng hoặc hàng loạt, đảm bảo hiệu suất tối ưu nhất.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, đặc biệt khi sử dụng chế độ Async với Webhook, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian thiết kế:** Chỉ cần nhập tiêu đề và mô tả, ảnh được tạo ra trong vài giây.
- **Nhất quán thương hiệu 100%:** Mọi ảnh đều sử dụng cùng một template Bannerbear, đảm bảo màu sắc, logo và font chữ luôn đồng nhất.
- **Linh hoạt cao:** Dễ dàng chuyển đổi giữa chế độ Sync (chờ kết quả ngay) và Async (nhận thông báo qua Webhook khi xong) tùy theo khối lượng công việc.
- **Tích hợp dễ dàng:** Có thể kết nối đầu vào từ Google Sheets, Airtable, hoặc bất kỳ nguồn dữ liệu nào khác để tạo hàng loạt ảnh tự động.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** Bản Self-hosted hoặc Cloud.
- **Tài khoản Bannerbear:**
    - Đăng ký tại [bannerbear.com](https://bannerbear.com).
    - Tạo một **Project** và thiết kế một **Template** (ảnh mẫu) mà các sếp muốn sử dụng.
    - Lấy **API Key** từ Settings > API Key.
    - Lấy **Template ID** từ API Console hoặc khi tạo template.
- **Creds n8n:** Tạo credential mới cho Bannerbear trong n8n và dán API Key vào.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Tải xuống file JSON của workflow từ link gốc hoặc copy toàn bộ code JSON.
2. Mở n8n Editor, chọn **Import from URL** hoặc **Import from File**.
3. Dán JSON vào hoặc chọn file đã tải về.
4. Workflow sẽ hiển thị với các node chính: `SetParameters`, `IfSynchrounousCall`, `SynchronouslyCreateImage`, `AsynchronouslyCreateImage`, và `Webhook_OnImageCreated`.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

Đây là phần quan trọng nhất. Các sếp cần cấu hình kỹ các node sau để workflow hoạt động đúng ý đồ:

**A. Node `SetParameters` (Cấu hình dữ liệu đầu vào)**
Đây là node trung tâm để các sếp định nghĩa dữ liệu sẽ đưa vào ảnh.
- **API Key & Template ID:** Mặc dù workflow có thể dùng credential, nhưng trong node này, các sếp cần kiểm tra xem có trường nào yêu cầu nhập trực tiếp không (thường là `template_id`). Hãy thay thế bằng Template ID của riêng các sếp.
- **Dữ liệu Text:** Tìm các trường `title` và `subtitle` (hoặc tên trường tương ứng trong template Bannerbear của bạn). Thay đổi giá trị mẫu bằng nội dung thực tế.
- **Chế độ gọi API (`call_mode`):**
    - Đặt giá trị là `"sync"` nếu muốn workflow chờ đến khi ảnh tạo xong rồi mới trả về link.
    - Đặt giá trị là `"async"` nếu muốn workflow gửi yêu cầu và nhận thông báo sau này qua Webhook (khuyến nghị cho tốc độ phản hồi nhanh).

**B. Node `AsynchronouslyCreateImage` (Chế độ Async)**
- **Credentials:** Click vào node, chọn tab **Credentials** và chọn credential Bannerbear mà các sếp đã tạo ở bước chuẩn bị.
- **Template ID:** Đảm bảo trường này trỏ đúng đến Template ID của các sếp.
- **Data:** Kiểm tra mapping dữ liệu từ node `SetParameters` vào đây.

**C. Node `Webhook_OnImageCreated` (Chế độ Async)**
Nếu các sếp chọn chế độ Async, node này đóng vai trò "điểm hẹn" để Bannerbear gửi thông báo khi ảnh đã render xong.
- **Path:** Giữ nguyên hoặc đổi path cho dễ nhớ (ví dụ: `bannerbear-callback`).
- **HTTP Method:** Phải là **POST**.
- **Production URL:** Sau khi bật Active workflow, các sếp cần copy **Production URL** của node này.
- **Cấu hình Webhook trong Bannerbear:**
    1. Vào trang quản trị Bannerbear.
    2. Chọn **Settings > Webhooks > Create a Webhook**.
    3. Dán **Production URL** của n8n vào ô URL.
    4. Chọn Event type: **`image_created`**.
    5. Lưu lại.

:::note[Lưu ý quan trọng về Webhook]
- Webhook trong Bannerbear **bắt buộc** phải là loại **POST**.
- Các sếp **bắt buộc** phải dùng **Production URL** (không dùng Test URL) và workflow n8n phải ở trạng thái **Active** thì Bannerbear mới gửi được dữ liệu về.
- Nếu gặp lỗi kết nối, các sếp có thể dùng Postman để tạo webhook thủ công bằng lệnh POST đến `https://api.bannerbear.com/v2/webhooks` với body JSON chứa URL n8n và event `image_created`.
:::

**D. Node `IfSynchrounousCall` (Phân nhánh logic)**
- Node này kiểm tra giá trị `call_mode` từ node `SetParameters`.
- Nếu là `sync`, nó sẽ đi sang nhánh `SynchronouslyCreateImage`.
- Nếu là `async`, nó sẽ đi sang nhánh `AsynchronouslyCreateImage`.
- Các sếp không cần chỉnh gì ở đây nếu đã cấu hình đúng `call_mode` ở trên.

**E. Node `SynchronouslyCreateImage` (Chế độ Sync)**
- Đây là node `HTTP Request` gọi trực tiếp API Bannerbear.
- Các sếp cần đảm bảo **API Key** trong header Authorization được điền đúng (hoặc dùng credential nếu node hỗ trợ).
- **Body:** Kiểm tra JSON body, đảm bảo `template_id` và các trường dữ liệu text khớp với template của Bannerbear.

#### 3. Kích hoạt ⚡️

1. **Test Run:**
    - Click vào node `When clicking ‘Execute workflow’` (Manual Trigger).
    - Chọn **Execute Workflow**.
    - Quan sát luồng dữ liệu:
        - Nếu chọn `sync`: Các sếp sẽ thấy link ảnh xuất hiện ngay trong output của node cuối cùng.
        - Nếu chọn `async`: Workflow sẽ dừng lại sau khi gửi yêu cầu. Các sếp cần chờ Bannerbear render xong (vài giây đến vài phút tùy độ phức tạp), sau đó Webhook sẽ được kích hoạt và dữ liệu sẽ chảy tiếp qua các node `GetUidAndStatus` -> `GetCompletedImageInfo`.
2. **Bật Active:**
    - Sau khi test thành công, click nút **Active** ở góc trên bên phải n8n để workflow sẵn sàng nhận dữ liệu từ các nguồn khác (Sheets, Webhook khác...).

### ✍️ Mẹo & gợi ý nâng cao

- **Tạo hàng loạt từ Google Sheets:** Thay vì dùng Manual Trigger, các sếp có thể thay node đầu vào bằng `Google Sheets Trigger` hoặc `Schedule Trigger`. Mỗi dòng trong Sheet sẽ chứa tiêu đề và mô tả, workflow sẽ tự động tạo ảnh và lưu link vào cột mới trong Sheet.
- **Gửi ảnh tự động lên Social Media:** Kết nối đầu ra của workflow (nơi có URL ảnh) với các node như `Facebook Graph API`, `Instagram`, hoặc `LinkedIn` để tự động đăng bài kèm ảnh vừa tạo.
- **Tích hợp AI để viết nội dung:** Thêm node `OpenAI` hoặc `Anthropic` trước node `SetParameters` để AI tự động viết tiêu đề và mô tả hấp dẫn dựa trên chủ đề, sau đó mới tạo ảnh.
- **Lưu trữ ảnh vào Cloud Storage:** Sau khi có URL ảnh, các sếp có thể dùng node `HTTP Request` để tải ảnh về và lưu vào `Google Drive`, `AWS S3`, hoặc `Dropbox` để quản lý tập trung.

### 📌 Kết luận

Workflow **Create Branded Social Media Images with Bannerbear** là một công cụ "vũ khí" mạnh mẽ giúp các sếp thoát khỏi vòng lặp thiết kế thủ công. Với khả năng hỗ trợ cả chế độ Sync và Async, nó linh hoạt đáp ứng từ nhu cầu tạo ảnh nhanh cho bài đăng cá nhân đến việc tạo hàng trăm ảnh cho chiến dịch marketing lớn.

Hãy bắt đầu bằng việc tạo một template đẹp mắt trên Bannerbear, import workflow này vào n8n, và trải nghiệm sự khác biệt khi mọi hình ảnh đều được tạo ra tự động, chính xác và đúng thương hiệu. Chúc các sếp thành công! 🚀