---
title: "🚀 Tự Động Đăng Bài Viết Lên Medium Với n8n (Không Code)"
description: "Hướng dẫn chi tiết cách sử dụng n8n để tự động hóa việc đăng bài viết lên Medium. Tối ưu hóa quy trình marketing nội dung, tiết kiệm thời gian và đảm bảo tính nhất quán."
slug: "tu-dong-dang-bai-viet-len-medium-voi-n8n"
tags: [n8n, automation, no-code, medium, content-marketing, blogging]
keywords: [n8n workflow, tự động hóa medium, đăng bài tự động, marketing nội dung, n8n medium integration]
---

# 🚀 Tự Động Đăng Bài Viết Lên Medium Với n8n (Không Code)

Trong kỷ nguyên nội dung số, việc duy trì lịch đăng bài đều đặn trên các nền tảng như Medium là yếu tố sống còn để xây dựng thương hiệu cá nhân và thu hút traffic chất lượng. Tuy nhiên, việc thủ công sao chép nội dung, chỉnh sửa định dạng và bấm nút "Publish" mỗi ngày không chỉ tốn thời gian mà còn dễ dẫn đến sai sót về thời gian đăng hoặc lỗi định dạng.

Workflow n8n này được thiết kế để giải quyết triệt để nỗi đau đó. Với sự kết hợp đơn giản giữa trigger thủ công và API của Medium, các sếp có thể biến quy trình đăng bài thành một thao tác "một chạm", sẵn sàng để mở rộng thành hệ thống tự động hóa hoàn toàn dựa trên lịch trình hoặc nguồn dữ liệu bên ngoài.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian tối đa:** Loại bỏ các thao tác thủ công lặp đi lặp lại trên giao diện Medium.
- **Độ chính xác cao:** Đảm bảo bài viết được đăng đúng định dạng Markdown/HTML mà Medium hỗ trợ, tránh lỗi hiển thị.
- **Nền tảng mở rộng:** Workflow này là "viên gạch đầu tiên" để tích hợp thêm AI viết bài, lưu trữ trong Google Sheets, hoặc lên lịch đăng tự động.
- **Không cần code:** Toàn bộ quy trình được thực hiện thông qua giao diện kéo-thả trực quan của n8n.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản n8n:** Có thể dùng bản cloud hoặc self-hosted.
2. **Tài khoản Medium:** Tài khoản người dùng hoặc Publication (tạp chí) trên Medium.
3. **API Key của Medium:** Các sếp cần tạo API Key tại [Medium API](https://medium.com/me/settings) (mục "API").
4. **Nội dung bài viết:** Dữ liệu đầu vào (tiêu đề, nội dung, tag, thumbnail...) có thể là tĩnh hoặc lấy từ nguồn khác.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n Editor.
2. Chọn **Import from File** hoặc **Import from URL**.
3. Tải file JSON của workflow này (hoặc copy mã JSON từ link gốc) và dán vào khung nhập liệu.
4. Nhấn **Import** để đưa workflow vào không gian làm việc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này khá tối giản với 2 nodes chính, nhưng các sếp cần chú ý cấu hình node **Medium** để đảm bảo kết nối và dữ liệu chính xác:

*   **Node: `Medium`**
    *   **Credentials:** Chọn hoặc tạo mới credential `mediumApi`.
        *   *Cách tạo:* Vào **Credentials** -> **Add New Credential** -> Chọn **Medium API**.
        *   Dán **API Key** của các sếp vào trường `API Key`.
    *   **Operation:** Chọn `Create Post`.
    *   **Publication ID:**
        *   Nếu đăng vào **tạp chí (Publication)**: Các sếp cần tìm ID của publication đó (thường nằm trong URL hoặc có thể lấy qua API).
        *   Nếu đăng vào **tài khoản cá nhân**: Có thể để trống hoặc chọn chế độ phù hợp tùy phiên bản node.
    *   **Title:** Nhập tiêu đề bài viết.
    *   **Content:** Nhập nội dung bài viết (hỗ trợ Markdown hoặc HTML tùy cấu hình).
    *   **Tags:** Thêm các tag liên quan (phân tách bằng dấu phẩy).
    *   **Publish:** Chọn `true` nếu muốn đăng ngay lập tức, hoặc `false` nếu muốn lưu làm bản nháp (Draft) để kiểm tra trước.

*   **Node: `On clicking 'execute'`**
    *   Đây là trigger thủ công. Khi các sếp nhấn nút **Execute Workflow**, nó sẽ kích hoạt node Medium phía sau.
    *   *Gợi ý nâng cao:* Sau khi test thành công, các sếp có thể thay thế node này bằng `Cron` (để lên lịch) hoặc `Webhook` (để nhận dữ liệu từ bên ngoài) hoặc `Google Sheets Trigger` (để đọc bài viết từ bảng tính).

#### 3. Kích hoạt ⚡️
1. Nhấn nút **Execute Workflow** (hoặc icon Play) để chạy thử với dữ liệu mẫu.
2. Kiểm tra kết quả:
    *   Nếu thành công, n8n sẽ trả về thông tin chi tiết về bài viết đã tạo (ID, URL...).
    *   Truy cập vào tài khoản Medium của các sếp để xác nhận bài viết đã xuất hiện.
3. Nếu mọi thứ ổn, nhấn nút **Active** (góc trên bên phải) để kích hoạt workflow.

### ✍️ Mẹo & gợi ý nâng cao
Để biến workflow đơn giản này thành một cỗ máy marketing mạnh mẽ, các sếp có thể tham khảo các ý tưởng sau:

1. **Tích hợp AI viết bài:** Thêm node `OpenAI` hoặc `Anthropic` trước node Medium. Nút trigger sẽ là "Chủ đề bài viết", AI sẽ sinh ra nội dung, sau đó tự động đăng lên Medium.
2. **Lấy dữ liệu từ Google Sheets:** Thay vì nhập thủ công, các sếp có thể tạo một bảng tính chứa các bài viết đã soạn sẵn. Dùng node `Google Sheets` để đọc từng dòng và chuyển sang node Medium.
3. **Lên lịch đăng tự động:** Thay thế `Manual Trigger` bằng `Cron`. Ví dụ: Đăng bài mới vào lúc 8:00 sáng mỗi thứ Hai.
4. **Gửi thông báo qua Telegram/Slack:** Sau khi đăng bài thành công, thêm node `Telegram` hoặc `Slack` để gửi link bài viết mới nhất cho team hoặc bản thân, giúp theo dõi hiệu quả dễ dàng.

### 📌 Kết luận
Việc tự động hóa việc đăng bài lên Medium không chỉ giúp các sếp tiết kiệm thời gian mà còn đảm bảo sự nhất quán trong chiến lược nội dung. Với workflow n8n này, các sếp có thể bắt đầu từ những bước cơ bản và dần dần xây dựng một hệ thống content marketing tự động hóa hoàn toàn. Hãy thử áp dụng ngay hôm nay và trải nghiệm sự khác biệt!