---
title: "🚀 Tự động nhận thông báo GitHub Issue qua Telegram với n8n"
description: "Hướng dẫn cấu hình workflow n8n tự động lấy cập nhật GitHub Issue mỗi 10 phút và gửi thông báo trực tiếp qua Telegram cực kỳ tiện lợi."
slug: "tu-dong-nhan-thong-bao-github-issue-qua-telegram-voi-n8n"
tags: [n8n, automation, no-code, github, telegram, devops]
keywords: [n8n workflow, github issue telegram, tu dong hoa github, tich hop telegram, devops automation]
---

# 🚀 Tự động nhận thông báo GitHub Issue qua Telegram với n8n

Các sếp làm kỹ sư phần mềm hay quản lý dự án chắc hẳn luôn đau đầu vì việc phải liên tục truy cập vào GitHub để kiểm tra xem có Issue mới hay có ai bình luận gì không. Việc kiểm tra thủ công này vừa tốn thời gian, lại dễ bỏ lỡ các thảo luận quan trọng của đội ngũ.

Giải pháp là đây! Với workflow n8n này, các sếp sẽ tự động hóa 100% quy trình: hệ thống sẽ tự động quét các Issue mới trên GitHub, lọc các thông tin cần thiết và bắn thông báo "ting ting" thẳng về tài khoản Telegram cá nhân. Không cần code phức tạp, chỉ mất 5 phút thiết lập là xong!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Cập nhật thời gian thực:** Nhận thông báo Issue hoặc bình luận mới ngay lập tức (chu kỳ quét 10 phút/lần).
- **Không bỏ lỡ việc quan trọng:** Mọi thông tin về tiêu đề, đường dẫn (URL) Issue được gửi trực tiếp đến Telegram cá nhân.
- **Tùy biến linh hoạt:** Dễ dàng lọc các Issue theo trạng thái, nhãn (labels) hoặc số lượng bình luận.
- **Hoạt động 24/7:** Chạy ngầm liên tục trên server mà không cần sự can thiệp thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Tài khoản GitHub:** Cần có Personal Access Token hoặc kết nối GitHub API để quyền đọc kho lưu trữ (repository).
- **Telegram Bot:** Một Telegram Bot Token (tạo qua `@BotFather`) và Chat ID của các sếp.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trên n8n, sau đó copy toàn bộ mã JSON của workflow (từ nguồn n8n template #3021) và dán trực tiếp vào giao diện n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 5 nodes chính, các sếp cần chú ý cấu hình kỹ các phần sau:

- **Run every 10 minutes (`scheduleTrigger`):**
  - Node này quyết định tần suất quét dữ liệu. Mặc định là 10 phút/lần. Các sếp có thể tăng hoặc giảm thời gian tùy theo nhu cầu dự án.

- **Get Github Issues (`github`):**
  - Kết nối tài khoản GitHub của các sếp tại phần **Credentials**.
  - **Lưu ý quan trọng:** Điền chính xác thông tin `OWNER` (tên tổ chức/tài khoản cá nhân) và `REPO NAME` (tên kho lưu trữ) trong các trường tương ứng.
  - Query parameters được cấu hình sẵn với các biến như `state`, `since`, và `labels`. Các sếp có thể điều chỉnh để lọc chính xác các Issue cần theo dõi.

- **Map title, url, created, comments (`set`):**
  - Node này dùng để trích xuất các trường dữ liệu quan trọng từ JSON trả về của GitHub API (như tiêu đề issue, đường dẫn url, thời gian tạo, số lượng bình luận). Không cần thay đổi nhiều trừ khi muốn lấy thêm thông tin khác.

- **Check for comments (`filter`):**
  - Dùng để lọc các issue dựa trên điều kiện (ví dụ: số lượng bình luận hoặc trạng thái). Các sếp có thể tinh chỉnh lại điều kiện lọc sao cho phù hợp với tiêu chí thông báo của đội ngũ.

- **Send Message to @user (`telegram`):**
  - Kết nối **Telegram API** bằng Bot Token đã tạo (tham khảo cách tạo bot [tại đây](https://core.telegram.org/bots/tutorial#obtain-your-bot-token)).
  - Điền **Chat ID** (có thể là username hoặc chat ID số của các sếp) vào phần cấu hình để bot gửi tin nhắn chuẩn xác. Nội dung tin nhắn sẽ hiển thị tiêu đề Issue và URL dẫn trực tiếp.

#### 3. Kích hoạt ⚡️
- Bấm nút **Execute Workflow** để chạy thử và kiểm tra xem dữ liệu từ GitHub có đẩy về Telegram thành công hay không.
- Nếu mọi thứ mượt mà, gạt công tắc sang **Active** để workflow chính thức tự động vận hành 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Đa kênh thông báo:** Kết hợp thêm node **Slack** hoặc **Discord** để bắn tin nhắn đồng thời vào kênh chat của nhóm dev.
- **Lưu trữ lịch sử:** Thêm node **Google Sheets** hoặc **Notion** để lưu lại danh sách các Issue đã thông báo, tiện cho việc thống kê báo cáo tuần/tháng.
- **Phân loại mức độ:** Sử dụng thêm các điều kiện lọc (If/Switch) để phân loại Issue theo Label (Bug, Feature, Urgent) và gửi vào các nhóm Telegram khác nhau.

### 📌 Kết luận
Chỉ với vài bước cấu hình đơn giản trên n8n, các sếp đã tiết kiệm được hàng giờ kiểm tra GitHub mỗi tuần. Hãy triển khai ngay để tối ưu hóa quy trình làm việc của đội ngũ kỹ thuật nhé! Chúc các sếp thao tác thành công!