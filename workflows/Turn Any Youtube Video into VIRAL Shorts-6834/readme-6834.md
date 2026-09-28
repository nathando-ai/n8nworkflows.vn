---
title: "🚀 Tự động chuyển đổi Video YouTube thành Shorts Viral với n8n và AI"
description: "Hướng dẫn tự động hóa quá trình tạo nội dung Shorts từ video YouTube bằng công cụ n8n kết hợp trí tuệ nhân tạo. Tiết kiệm thời gian và tăng khả năng tiếp cận nội dung."
slug: "tu-dong-tao-shorts-youtube-voi-n8n-ai"
tags: [n8n, automation, no-code, content creation, ai]
keywords: [n8n workflow, tự động hóa nội dung, tạo shorts, youtube shorts, trí tuệ nhân tạo]
---

# 🚀 Tự động chuyển đổi Video YouTube thành Shorts Viral với n8n và AI

[Các sếp] có biết không? Với công cụ n8n kết hợp trí tuệ nhân tạo, các sếp có thể tự động hóa quá trình tạo nội dung Shorts từ video YouTube một cách hoàn toàn không cần code. Thay vì phải tốn thời gian cắt ghép và viết kịch bản thủ công, workflow này sẽ giúp các sếp tiết kiệm đến 80% thời gian và tạo ra nội dung hấp dẫn hơn.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hóa quá trình tạo nội dung Shorts trong vòng vài phút.
- **Nội dung hấp dẫn**: AI sẽ chọn các đoạn clip và tạo kịch bản phù hợp với xu hướng.
- **Tăng khả năng tiếp cận**: Nội dung được tối ưu hóa cho nền tảng Shorts, giúp tăng tỷ lệ tương tác.
- **Hoạt động liên tục**: Workflow có thể chạy tự động theo lịch trình hoặc khi có video mới.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản YouTube API (để lấy transcript và thông tin video).
- Tài khoản Mistral Cloud (để sử dụng trí tuệ nhân tạo).
- Tài khoản lưu trữ (Google Drive, Dropbox...) để lưu các đoạn clip đã tạo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của các sếp.
2. Nhấn vào nút "Import from URL" và dán link sau: [https://n8n.io/workflows/6834](https://n8n.io/workflows/6834).
3. Hoặc các sếp có thể tải file JSON về và import từ máy tính.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Mistral Cloud Chat Model"**:
   - Cấu hình credentials cho Mistral Cloud.
   - Điền API Key của Mistral Cloud vào trường "API Key".

2. **Node "Get Transcript"**:
   - Cấu hình credentials cho YouTube API.
   - Điền YouTube API Key vào trường "API Key".
   - Thay đổi tham số `videoId` trong URL request để lấy transcript của video mong muốn.

3. **Node "Save Clips"**:
   - Cấu hình credentials cho dịch vụ lưu trữ (Google Drive, Dropbox...).
   - Thay đổi đường dẫn lưu trữ trong URL request để lưu các đoạn clip vào thư mục mong muốn.

4. **Node "Select Clips"**:
   - Thay đổi prompt trong node này để phù hợp với chủ đề và phong cách của các sếp.
   - Ví dụ: "Tạo kịch bản Shorts từ transcript này, tập trung vào các điểm nổi bật và câu chuyện hấp dẫn."

#### 3. Kích hoạt ⚡️
1. Các sếp có thể test workflow bằng cách nhấn nút "Execute workflow" để kiểm tra kết quả.
2. Sau khi đảm bảo workflow hoạt động đúng, các sếp có thể bật chế độ "Active" để workflow chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tự động hóa theo lịch trình**: Các sếp có thể kết hợp workflow này với các node như "Schedule Trigger" để tự động tạo nội dung Shorts theo lịch trình.
- **Tích hợp với Slack/Telegram**: Thêm node gửi thông báo khi workflow hoàn thành để các sếp biết khi nào nội dung đã sẵn sàng.
- **Tối ưu hóa nội dung**: Các sếp có thể thêm node để phân tích dữ liệu tương tác của các Shorts đã tạo để cải thiện nội dung trong tương lai.
- **Tạo nhiều phiên bản**: Các sếp có thể chạy workflow nhiều lần với các prompt khác nhau để tạo ra nhiều phiên bản nội dung khác nhau.

### 📌 Kết luận
Workflow "Turn Any Youtube Video into VIRAL Shorts" là công cụ mạnh mẽ giúp các sếp tự động hóa quá trình tạo nội dung Shorts từ video YouTube. Với sự kết hợp của trí tuệ nhân tạo và công cụ n8n, các sếp có thể tiết kiệm thời gian và tạo ra nội dung hấp dẫn hơn. Hãy áp dụng ngay workflow này để nâng cao hiệu quả tạo nội dung của các sếp!