---
title: "🎙️ Tự động chuyển đổi tin tức BBC thành podcast sử dụng Hugging Face và Google Gemini"
description: "Hướng dẫn chi tiết cách tự động hóa quá trình chuyển đổi tin tức BBC thành podcast sử dụng công nghệ AI, tiết kiệm thời gian và nâng cao hiệu quả truyền thông"
slug: "tu-dong-chuyen-doi-tin-tuc-bbc-thanh-podcast-su-dung-hugging-face-va-google-gemini"
tags: [n8n, automation, no-code, AI, marketing]
keywords: [n8n workflow, tự động hóa, AI, podcast, tin tức BBC]
---

# 🎙️ Tự động chuyển đổi tin tức BBC thành podcast sử dụng Hugging Face và Google Gemini

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Các sếp có biết rằng mỗi ngày có hàng trăm tin tức mới xuất hiện trên BBC News, nhưng việc chuyển đổi chúng thành podcast thủ công lại tốn nhiều thời gian và công sức? Với workflow này, các sếp có thể tự động hóa toàn bộ quá trình từ việc lấy tin tức đến tạo podcast hoàn chỉnh, chỉ với vài bước đơn giản.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian đáng kể trong quá trình chuyển đổi tin tức thành podcast
- Tự động hóa toàn bộ quy trình từ lấy tin tức đến tạo podcast hoàn chỉnh
- Tăng cường hiệu quả truyền thông với nội dung podcast chất lượng cao
- Hoạt động liên tục 24/7 mà không cần can thiệp thủ công
- Tạo ra nội dung podcast cá nhân hóa phù hợp với đối tượng mục tiêu
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Google Gemini API (không cần access token)
- Tài khoản Hugging Face API (cần access token)
- Kiến thức cơ bản về cách sử dụng n8n
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập vào n8n Editor của bạn
2. Nhấp vào nút "Import from URL" trên thanh công cụ
3. Dán link sau vào ô nhập liệu: `https://n8n.io/workflows/2972`
4. Nhấp vào nút "Import" để hoàn tất quá trình import

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
1. **Node "Gemini"**:
   - Chọn credentials "googlePalmApi" đã được thiết lập trước đó
   - Đảm bảo tài khoản Google Gemini API hoạt động bình thường

2. **Node "Hugging Face Text-to-Speech"**:
   - Chọn credentials "huggingFaceApi" đã được thiết lập trước đó
   - Đảm bảo tài khoản Hugging Face API có quyền truy cập vào model text-to-speech
   - Cần có access token để xác thực với Hugging Face API

3. **Node "Fetch BBC News Page"**:
   - URL mặc định đã được thiết lập là trang chủ BBC News
   - Có thể thay đổi URL nếu muốn lấy tin tức từ các trang khác

4. **Node "Limit 10 Items"**:
   - Giới hạn số lượng tin tức được xử lý trong mỗi lần chạy workflow
   - Có thể điều chỉnh số lượng này theo nhu cầu

5. **Node "News Classifier"**:
   - Đảm bảo model phân loại tin tức hoạt động chính xác
   - Có thể điều chỉnh các tham số phân loại theo nhu cầu cụ thể

#### 3. Kích hoạt ⚡️
1. Nhấp vào nút "Test workflow" để kiểm tra dữ liệu mẫu
2. Kiểm tra kết quả đầu ra để đảm bảo workflow hoạt động đúng
3. Sau khi kiểm tra thành công, nhấp vào nút "Activate" để kích hoạt workflow
4. Workflow sẽ tự động chạy theo lịch trình đã thiết lập

### ✍️ Mẹo & gợi ý nâng cao
1. **Tự động hóa lịch trình**:
   - Thiết lập lịch trình chạy workflow hàng ngày để luôn cập nhật nội dung mới nhất
   - Sử dụng node "Schedule Trigger" để điều chỉnh thời gian chạy workflow

2. **Tích hợp với các nền tảng khác**:
   - Kết nối với Slack hoặc Telegram để thông báo khi có podcast mới được tạo
   - Lưu trữ các podcast đã tạo trong Google Drive hoặc Dropbox

3. **Tùy chỉnh nội dung**:
   - Điều chỉnh prompt trong node "Basic Podcast LLM Chain" để phù hợp với phong cách podcast của bạn
   - Thêm các thông tin bổ sung vào script podcast như giới thiệu, kết luận,...

4. **Phân tích hiệu suất**:
   - Sử dụng các công cụ phân tích để theo dõi hiệu suất của podcast
   - Thu thập phản hồi từ người nghe để cải thiện nội dung

### 📌 Kết luận
Workflow "Turn BBC News Articles into Podcasts using Hugging Face and Google Gemini" là giải pháp hoàn hảo cho các sếp muốn tự động hóa quá trình chuyển đổi tin tức thành podcast. Với công nghệ AI tiên tiến và giao diện thân thiện, workflow này giúp tiết kiệm thời gian đáng kể và nâng cao hiệu quả truyền thông. Hãy áp dụng ngay để tạo ra những podcast chất lượng cao và thu hút người nghe!