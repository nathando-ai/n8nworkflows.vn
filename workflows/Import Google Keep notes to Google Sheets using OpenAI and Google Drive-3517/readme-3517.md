---
title: "🚀 Tự động hóa đồng bộ ghi chú Google Keep lên Google Sheets bằng OpenAI và n8n"
description: "Hướng dẫn chi tiết cách gom toàn bộ ghi chú Google Keep qua Google Takeout, xử lý thông minh bằng AI và lưu trữ tự động vào Google Sheets."
slug: "import-google-keep-notes-to-google-sheets-openai"
tags: [n8n, automation, no-code, google-keep, google-sheets, openai, google-drive]
keywords: [n8n workflow, tự động hóa google keep, google keep sang google sheets, ai xử lý ghi chú, pollupai workflow]
---

# 🚀 Đồng bộ Google Keep Notes vào Google Sheets tự động với AI

Các sếp có đang lưu trữ hàng trăm ghi chú rời rạc trên **Google Keep** nhưng lại khó tổng hợp, tìm kiếm hay phân tích dữ liệu? Việc sao chép thủ công từng ghi chú sang Google Sheets là một "cực hình" mất rất nhiều thời gian. 

Đừng lo, workflow n8n được thiết kế bởi **PollupAI** này sẽ giúp các sếp giải quyết triệt để bài toán trên. Workflow tự động quét toàn bộ file ghi chú từ Google Drive, lọc nội dung, ứng dụng sức mạnh của **OpenAI (GPT-4o-mini)** để phân tích/xử lý và cuối cùng đồng bộ gọn gàng vào **Google Sheets** chỉ trong một nốt nhạc!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Gom toàn bộ ghi chú cũ lên Google Sheets mà không cần copy/paste thủ công.
- **Sức mạnh AI:** Tích hợp OpenAI để tóm tắt, trích xuất thông tin hoặc phân loại ghi chú theo ý muốn.
- **Quản lý thông minh:** Dễ dàng lọc ghi chú theo từ khóa, ngày tháng hoặc trạng thái lưu trữ (`is archived`).
- **Hoạt động tối ưu:** Xử lý dữ liệu theo lô (`Split in Batches`) giúp tránh quá tải hệ thống.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Google Drive Account & Credentials**: Nơi lưu trữ các file JSON xuất từ Google Keep.
- **Google Sheets Account & Credentials**: Bảng tính đích để lưu dữ liệu ghi chú.
- **OpenAI API Key**: Dành cho node xử lý ngôn ngữ tự nhiên (`OpenAI Chat Model`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy trực tiếp mã nguồn.
- Mở n8n Editor, chọn **Add workflow** -> **Import from File** (hoặc dán trực tiếp vào màn hình canvas).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy mượt mà, các sếp cần cấu hình lần lượt các bước sau:

1. **Chuẩn bị dữ liệu Google Keep:**
   - Truy cập [Google Takeout](https://takeout.google.com/).
   - Click **"Deselect all"**, chỉ chọn duy nhất **Google Keep** và nhấn **Next**.
   - Chọn phương thức nhận link qua email (`Send download link via mail`).
   - Tải file về, giải nén và upload toàn bộ các file `.json` vào một thư mục riêng biệt trên **Google Drive**.

2. **Cấu hình node `Search in "Keep" folder` (Google Drive):**
   - Kết nối tài khoản Google Drive OAuth2.
   - Chỉ định chính xác tên hoặc ID thư mục chứa các file ghi chú Keep mà các sếp vừa upload ở trên.

3. **Cấu hình bộ lọc (`If extension is json` & `If is archived is false` & `Filter`):**
   - Kiểm tra lại điều kiện lọc định dạng file (`.json`).
   - Tùy chỉnh bộ lọc thời gian hoặc từ khóa trong nội dung ghi chú nếu cần. (Nếu không cần lọc, các sếp có thể xóa node này).

4. **Cấu hình AI (`OpenAI Chat Model` & `Put some AI treatment here if you need it`):**
   - Thêm OpenAI API Credentials.
   - Chọn model `gpt-4o-mini` (hoặc model tùy ý). Viết Prompt hướng dẫn AI cách trích xuất, tóm tắt nội dung ghi chú. Nếu không dùng AI, các sếp có thể xóa node này để tối ưu tốc độ.

5. **Cấu hình node `Add to google sheet` (Google Sheets):**
   - Kết nối tài khoản Google Sheets.
   - Trỏ tới file Google Sheets trống đã chuẩn bị sẵn.
   - Chọn Operation là `Append or Update` và map các trường dữ liệu từ node `Set the fields for export` vào các cột tương ứng trên Sheet.

#### 3. Kích hoạt ⚡️
- Click nút **Test workflow** để n8n chạy thử nghiệm với một vài bản ghi mẫu.
- Kiểm tra kết quả trên Google Sheets. Nếu mọi thứ khớp lệnh, hãy gạt công tắc sang **Active** để hoàn tất!

### ✍️ Mẹo & gợi ý nâng cao
- **Thông báo qua Telegram/Slack:** Thêm một node Telegram hoặc Slack ở cuối workflow để nhận thông báo ngay khi quá trình đồng bộ hoàn tất.
- **Lưu Log định kỳ:** Kết hợp thêm Google Sheets log để theo dõi số lượng ghi chú đã đồng bộ thành công mỗi lần chạy.
- **Tự động hóa hàng tuần:** Thay vì chạy thủ công (`Manual Trigger`), các sếp có thể đổi sang node **Schedule Trigger** để hệ thống tự quét ghi chú mới định kỳ hàng tuần.

### 📌 Kết luận
Workflow này là "cứu tinh" cho những ai sở hữu kho tàng ghi chú khổng lồ trên Google Keep và muốn đưa chúng về Google Sheets để phân tích dữ liệu chuyên sâu hơn. Áp dụng ngay để tối ưu hóa không gian làm việc của các sếp nhé!