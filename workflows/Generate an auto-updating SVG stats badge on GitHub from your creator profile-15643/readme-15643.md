---
title: "🚀 Tự động cập nhật huy hiệu SVG thống kê n8n Creator lên GitHub Profile"
description: "Hướng dẫn xây dựng workflow n8n tự động lấy thông tin Creator profile, vẽ huy hiệu SVG cá nhân hóa và push trực tiếp lên GitHub README."
slug: "tu-dong-cap-nhat-huy-hieu-svg-github-n8n-creator"
tags: [n8n, automation, github, api, svg, no-code]
keywords: [n8n workflow, github stats badge, svg badge automation, n8n creator profile, tu dong hoa github]
---

# 🚀 Tự động cập nhật huy hiệu SVG thống kê n8n Creator lên GitHub Profile

Các sếp là một nhà sáng tạo (Creator) tích cực chia sẻ các workflow hữu ích trên n8n.io? Chắc hẳn các sếp luôn muốn profile GitHub của mình trông thật chuyên nghiệp với một bảng thống kê (stats badge) cập nhật liên tục số lượng template, lượt tải hoặc thông tin cá nhân. 

Việc cập nhật thủ công những con số này mỗi khi có thay đổi thực sự rất mất thời gian. Giải pháp ư? Workflow n8n này sẽ tự động hóa từ A-Z: gọi API lấy dữ liệu, vẽ ảnh SVG chuẩn nét kèm avatar, sau đó tự động push lên kho lưu trữ GitHub của các sếp 24/7 mà không cần đụng tay vào code!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động 100%:** Huy hiệu SVG trên GitHub README của các sếp sẽ tự làm mới theo lịch trình (hàng ngày/hàng tuần).
- **Cá nhân hóa chuyên nghiệp:** Thiết kế thẻ SVG kích thước 495x190px cực đẹp, tích hợp hình đại diện (avatar) dạng Base64 và các chỉ số creator chính xác.
- **Xử lý thông minh:** Workflow tự động kiểm tra xem file SVG đã tồn tại trên GitHub hay chưa để thực hiện sửa (Edit) hoặc tạo mới (Create) một cách mượt mà.
- **Tiết kiệm thời gian:** Không bao giờ phải cập nhật thủ công các con số thống kê profile nữa.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **GitHub Account & Personal Access Token (PAT):** Tài khoản GitHub và Token có quyền đọc/ghi (repo permissions) để đẩy file SVG lên repository.
- **n8n Creator Profile:** Đã có tài khoản Creator công khai trên n8n.io.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể sử dụng file JSON của workflow này, copy và paste trực tiếp vào giao diện n8n Editor của mình. Workflow bao gồm 11 nodes được thiết kế mạch lạc: *Schedule Trigger, ⚙️ Config, Fetch Creator Profile, Parse Creator Data, Download Avatar, Encode Avatar to Base64, Build SVG Card, GitHub (Edit), GitHub (Create), Merge Results, và Output Embed URLs*.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow hoạt động trơn tru, các sếp cần chú ý cấu hình kỹ các node sau:
- **Node `⚙️ Config`**: Điền đầy đủ tất cả các thông tin cá nhân, username n8n, thông tin repository GitHub đích (tên repo, nhánh branch, tên file SVG...).
- **Node `GitHub – Edit Existing File` & `GitHub – Create New File`**: Kết nối tài khoản GitHub của các sếp (GitHub Credentials) vào **cả hai** node này. Đảm bảo repository đích là **Public** để file SVG có thể hiển thị ảnh công khai.
- **Node `Schedule Trigger`**: Tùy chỉnh khoảng thời gian chạy tự động mong muốn (mặc định chạy định kỳ hàng ngày).

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** để test thử nghiệm lần đầu và kiểm tra xem file `.svg` đã xuất hiện trên repository GitHub chưa.
- Sau khi test thành công, gạt công tắc sang **Active** để bật chế độ chạy tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm node Telegram hoặc Slack vào sau quá trình đẩy file thành công để nhận thông báo mỗi khi huy hiệu được cập nhật.
- **Tùy biến giao diện SVG:** Các sếp có thể chỉnh sửa code dựng SVG trong node `Build SVG Card` để đổi màu sắc, font chữ hoặc thêm các chỉ số phụ phù hợp với style cá nhân.
- **Cache CDN:** Sử dụng các đường dẫn CDN (như jsDelivr hoặc GitHub raw) được trả về ở node cuối cùng để tối ưu tốc độ load ảnh trên profile GitHub.

### 📌 Kết luận
Một mẹo nhỏ nhưng cực kỳ "flex" độ chuyên nghiệp dành cho lập trình viên và n8n Creator. Hãy cài đặt ngay workflow này để profile GitHub của các sếp luôn nổi bật và sống động nhé! Chúc các sếp thao tác thành công!