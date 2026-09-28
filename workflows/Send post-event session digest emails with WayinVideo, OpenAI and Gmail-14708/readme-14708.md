---
title: "📩 Tự động hóa gửi email tóm tắt sự kiện sau khi kết thúc phiên họp với WayinVideo, OpenAI và Gmail"
description: "Hướng dẫn chi tiết cách tự động hóa gửi email tóm tắt sự kiện sau khi kết thúc phiên họp sử dụng n8n, WayinVideo, OpenAI và Gmail. Tiết kiệm thời gian và nâng cao hiệu quả truyền thông sự kiện."
slug: "tu-dong-hoa-gui-email-tom-tat-su-kien"
tags: [n8n, automation, no-code, social-media, ai-summarization]
keywords: [n8n workflow, tự động hóa, AI summarization, email marketing, sự kiện]
---

# 📩 Tự động hóa gửi email tóm tắt sự kiện sau khi kết thúc phiên họp với WayinVideo, OpenAI và Gmail

[Các sếp] có bao giờ phải tự tay ghi lại nội dung các phiên họp quan trọng, tóm tắt lại và gửi email báo cáo cho hàng chục người tham gia? Quá trình này tốn thời gian, dễ bị lỗi và không thể đảm bảo tính nhất quán. Với workflow này, các sếp có thể tự động hóa hoàn toàn quy trình này chỉ trong vài bước đơn giản.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hóa hoàn toàn quy trình từ ghi nhận thông tin đến gửi email.
- **Nội dung chuyên nghiệp**: Sử dụng AI để tóm tắt và viết email báo cáo chất lượng cao.
- **Tăng cường tương tác**: Gửi email báo cáo kịp thời cho tất cả người tham gia.
- **Tính nhất quán**: Đảm bảo nội dung báo cáo được gửi đồng đều cho tất cả người nhận.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Gmail với quyền truy cập OAuth2.
- API Key từ WayinVideo.
- Tài khoản OpenAI với API Key.
- URL của các phiên họp cần tóm tắt.
- Danh sách email của người tham gia sự kiện.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow gốc](https://n8n.io/workflows/14708).
2. Nhấn nút "Download" để tải file JSON về máy.
3. Trong n8n Editor, nhấn vào "Import from File" và chọn file JSON đã tải về.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node 1. Form — Event Details + Session URLs**:
   - Không cần cấu hình gì thêm, chỉ cần điền thông tin vào form khi chạy workflow.

2. **Nodes 2, 3, 4 (WayinVideo — Submit Session)**:
   - Mở từng node và thay thế `YOUR_WAYINVIDEO_API_KEY` trong phần Authorization header bằng API Key thực của bạn.

3. **Nodes 6, 7, 8 (WayinVideo — Get Session Summary)**:
   - Mở từng node và thay thế `YOUR_WAYINVIDEO_API_KEY` trong phần Authorization header bằng API Key thực của bạn.

4. **Node 11. OpenAI — GPT-4o-mini Model**:
   - Kết nối credential OpenAI của bạn trong phần "Authentication".

5. **Node 13. Gmail — Send Digest Email**:
   - Kết nối tài khoản Gmail của bạn thông qua OAuth2.

#### 3. Kích hoạt ⚡️
1. **Test run dữ liệu mẫu**:
   - Nhấn vào nút "Execute Workflow" để chạy thử với dữ liệu mẫu.
   - Kiểm tra kết quả ở từng node để đảm bảo dữ liệu được xử lý đúng.

2. **Bật Active workflow**:
   - Sau khi test thành công, nhấn vào nút "Activate" để kích hoạt workflow.
   - Truy cập URL của form để bắt đầu sử dụng.

### ✍️ Mẹo & gợi ý nâng cao
1. **Nâng cấp mô hình OpenAI**:
   - Thay đổi `gpt-4o-mini` thành `gpt-4o` trong node 11 để có chất lượng email tốt hơn.

2. **Thêm BCC**:
   - Thêm trường BCC trong node Gmail để gửi bản sao cho đội ngũ nội bộ.

3. **Xử lý trường hợp lỗi**:
   - Thêm node IF sau mỗi node Get Summary để kiểm tra nếu `data.summary` không rỗng trước khi tiếp tục.
   - Nếu rỗng, thêm node Wait và vòng lặp retry để chờ WayinVideo xử lý xong.

4. **Thêm phiên họp thứ 4**:
   - Sao chép nodes 4 và 8, sau đó thêm một input mới vào node Merge.

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quy trình gửi email tóm tắt sự kiện sau khi kết thúc phiên họp. Với sự kết hợp của WayinVideo, OpenAI và Gmail, các sếp có thể tiết kiệm thời gian và nâng cao hiệu quả truyền thông sự kiện. Hãy áp dụng ngay để trải nghiệm sự tiện lợi và chuyên nghiệp mà tự động hóa mang lại!