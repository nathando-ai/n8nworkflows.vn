---
title: "🚀 Tự động bật đèn Home Assistant khi có cập nhật trên GitHub"
description: "Workflow n8n tự động bật đèn Home Assistant sang màu đỏ khi có cập nhật trên kho lưu trữ GitHub. Giải pháp hoàn hảo cho các nhà phát triển cần theo dõi thay đổi mã nguồn."
slug: "tu-dong-bat-den-home-assistant-khi-cap-nhat-github"
tags: [n8n, automation, no-code, home-assistant, github]
keywords: [n8n workflow, tự động hóa, home assistant, github, iot]
---

# 🚀 Tự động bật đèn Home Assistant khi có cập nhật trên GitHub

[Các sếp làm việc với mã nguồn mở hay phát triển phần mềm thường gặp tình trạng: "Mỗi lần có thay đổi trên GitHub, phải nhớ tắt bật đèn để báo hiệu". Với workflow này, các sếp có thể tự động hóa hoàn toàn quy trình này chỉ trong 5 phút!]

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần can thiệp thủ công mỗi khi có cập nhật
- **Chính xác 100%**: Mỗi thay đổi trên GitHub đều được phản ánh ngay lập tức
- **Cá nhân hóa**: Có thể điều chỉnh màu sắc và đèn cụ thể theo nhu cầu
- **Hoạt động liên tục**: Không bị gián đoạn ngay cả khi các sếp không trực tiếp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản GitHub với quyền truy cập vào kho lưu trữ cần theo dõi
- Tài khoản Home Assistant đã cài đặt và cấu hình đèn
- API keys cho cả GitHub và Home Assistant
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [trang workflow gốc](https://n8n.io/workflows/1856)
2. Click vào nút "Copy to Clipboard" để sao chép JSON workflow
3. Trong n8n Editor, click vào "Import from Clipboard" và dán JSON đã sao chép

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "On any update in repository"**:
   - Chọn credentials "githubApi" đã được cấu hình
   - Đảm bảo tài khoản GitHub có quyền truy cập vào kho lưu trữ cần theo dõi

2. **Node "Turn a light red"**:
   - Chọn credentials "homeAssistantApi" đã được cấu hình
   - Thay đổi tham số "entity_id" trong phần "Additional Fields" để khớp với đèn của các sếp
   - Có thể thay đổi màu sắc bằng cách chỉnh sửa giá trị RGB trong phần "Additional Fields"

#### 3. Kích hoạt ⚡️
1. Click vào nút "Execute Node" để test với dữ liệu mẫu
2. Sau khi xác nhận hoạt động đúng, click vào nút "Activate" để kích hoạt workflow

### ✍️ Mẹo & gợi ý nâng cao
- Thay đổi màu sắc đèn: Sử dụng [RGB color picker](https://www.google.com/search?q=rgb+color+picker) để chọn màu mong muốn
- Kết hợp với Slack: Thêm node Slack để thông báo khi có cập nhật
- Theo dõi nhiều kho lưu trữ: Sao chép node GitHub và cấu hình cho các kho khác
- Tạo cảnh báo âm thanh: Kết hợp với node Home Assistant để phát âm thanh cảnh báo

### 📌 Kết luận
Workflow này giúp các sếp phát triển phần mềm tự động hóa hoàn toàn quy trình theo dõi thay đổi mã nguồn. Với chỉ 5 phút cấu hình, các sếp có thể tiết kiệm hàng giờ làm việc thủ công mỗi ngày. Hãy áp dụng ngay để nâng cao hiệu suất làm việc!