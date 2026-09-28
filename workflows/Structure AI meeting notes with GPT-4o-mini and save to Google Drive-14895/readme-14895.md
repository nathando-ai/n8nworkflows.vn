---
title: "🚀 Tự động hóa ghi chú cuộc họp với GPT-4o-mini và lưu vào Google Drive"
description: "Giải pháp tự động hóa hoàn toàn không cần code giúp chuyển đổi ghi chú cuộc họp thô thành tài liệu có cấu trúc chuyên nghiệp và lưu trực tiếp vào Google Drive"
slug: "tu-dong-hoa-ghi-chu-cuoc-hop-gpt-4o-mini-google-drive"
tags: [n8n, automation, no-code, ai, google-drive]
keywords: [n8n workflow, tự động hóa, ghi chú cuộc họp, GPT-4o-mini, Google Drive]
---

# 🚀 Tự động hóa ghi chú cuộc họp với GPT-4o-mini và lưu vào Google Drive

[Các sếp] có bao giờ phải đối mặt với tình trạng ghi chú cuộc họp rối rắm, không có cấu trúc, khó đọc và tìm kiếm không? Với workflow này, các sếp có thể chuyển đổi nhanh chóng những ghi chú thô thành tài liệu có cấu trúc chuyên nghiệp, sẵn sàng sử dụng ngay trong Google Drive.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hóa toàn bộ quy trình từ 5-10 phút xuống còn vài giây
- **Tài liệu chuyên nghiệp**: Chuyển đổi ghi chú thô thành tài liệu có 6 phần cấu trúc rõ ràng
- **Tích hợp liền mạch**: Lưu trực tiếp vào Google Drive mà không cần can thiệp
- **Dễ dàng chia sẻ**: Tài liệu đã được định dạng sẵn sàng chia sẻ với khách hàng hoặc đồng nghiệp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản OpenAI với API key (để sử dụng GPT-4o-mini)
- Tài khoản Google với quyền truy cập Google Drive
- Một thư mục Google Drive để lưu tài liệu (cần ID thư mục)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [link workflow gốc](https://n8n.io/workflows/14895)
2. Click vào nút "Import" và chọn "Import from URL"
3. Dán link workflow vào ô nhập liệu và nhấn "Import"

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node 4. OpenAI — GPT-4o-mini Model**:
   - Kết nối credential OpenAI của bạn
   - Đảm bảo tài khoản OpenAI có đủ credit để sử dụng GPT-4o-mini

2. **Node 7. Google Drive — Save Notes Document**:
   - Kết nối credential Google Drive OAuth2 của bạn
   - Đảm bảo tài khoản Google có quyền truy cập vào thư mục bạn muốn lưu tài liệu
   - Lưu ý: Nếu không kết nối credential, workflow sẽ thất bại ở bước cuối cùng

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong các node quan trọng, nhấn nút "Activate" để kích hoạt workflow
2. Copy URL của Form từ node 1 (Form — Meeting Notes Submission)
3. Mở URL này trong trình duyệt và điền đầy đủ thông tin:
   - Tên khách hàng
   - Ngày họp
   - Danh sách người tham gia
   - Ghi chú thô
   - Tên của bạn
   - ID thư mục Google Drive (có thể lấy từ URL của thư mục trong trình duyệt)

### ✍️ Mẹo & gợi ý nâng cao
1. **Tùy chỉnh prompt**: Các sếp có thể chỉnh sửa prompt trong node 3 để phù hợp với nhu cầu cụ thể của dự án
2. **Kết hợp với Slack/Teams**: Thêm node gửi thông báo khi tài liệu đã sẵn sàng
3. **Lưu trữ phiên bản**: Thêm node lưu bản sao lưu của tài liệu vào một thư mục khác
4. **Tự động gửi email**: Kết nối với node gửi email để thông báo khi tài liệu đã được tạo

### 📌 Kết luận
Workflow này không chỉ tiết kiệm thời gian mà còn nâng cao chất lượng ghi chú cuộc họp. Với sự tích hợp liền mạch với Google Drive và sức mạnh của GPT-4o-mini, các sếp có thể tập trung vào công việc quan trọng hơn thay vì phải lo lắng về việc định dạng tài liệu. Hãy thử ngay và trải nghiệm sự khác biệt!