---
title: "📸 Tự Động Chụp Ảnh Website từ Google Sheets Lưu về Drive"
description: "Workflow n8n tự động chụp ảnh màn hình các URL trong Google Sheets và lưu trữ vào Google Drive. Giải pháp hoàn hảo cho việc theo dõi thay đổi website hoặc tạo thư viện hình ảnh hàng loạt."
slug: "tu-dong-chup-anh-website-tu-google-sheets"
tags: [n8n, automation, no-code, google-sheets, google-drive, web-scraping]
keywords: [n8n workflow, chụp ảnh website, tự động hóa google sheets, lưu ảnh drive, n8n screenshot]
---

# 📸 Tự Động Chụp Ảnh Website từ Google Sheets Lưu về Drive

Trong quá trình vận hành website, marketing hoặc phát triển sản phẩm, các sếp thường xuyên gặp phải tình huống cần chụp ảnh màn hình (screenshot) của nhiều trang web khác nhau. Việc làm thủ công bằng cách mở từng tab, chụp ảnh, đổi tên file và tải lên Google Drive là một quy trình cực kỳ tốn thời gian, dễ gây nhầm lẫn và khó kiểm soát khi số lượng URL lên đến hàng chục hay hàng trăm.

Workflow **"Capture Website Screenshots via Google Sheets to Google Drive with CustomJS"** chính là giải pháp "chìa khóa trao tay" giúp các sếp tự động hóa toàn bộ quy trình này. Chỉ cần nhập danh sách URL vào Google Sheets, n8n sẽ tự động truy cập, chụp ảnh chất lượng cao và lưu trữ ngay vào thư mục Google Drive chỉ định. Không cần code, không cần cài đặt phần mềm phức tạp, mọi thứ diễn ra mượt mà và chính xác 100%.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, đặc biệt khi cần xử lý số lượng lớn URL hoặc chạy theo lịch (cron), các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 100% thời gian thủ công:** Xử lý hàng trăm URL chỉ trong vài phút thay vì hàng giờ.
- **Độ chính xác tuyệt đối:** Không lo sai sót tên file hay thất lạc ảnh do con người.
- **Tổ chức dữ liệu chuyên nghiệp:** Ảnh được lưu có hệ thống trong Google Drive, dễ dàng chia sẻ và quản lý.
- **Linh hoạt & Mở rộng:** Dễ dàng thêm cột dữ liệu mới (như ngày chụp, trạng thái) để theo dõi lịch sử thay đổi website.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Google:** Đã kích hoạt Google Sheets và Google Drive.
2. **Tài khoản n8n:** Có thể dùng n8n Cloud hoặc Self-hosted.
3. **Node Custom:** Workflow sử dụng node `@custom-js/n8n-nodes-pdf-toolkit.websiteScreenshot`. Các sếp cần đảm bảo node này đã được cài đặt trong n8n (thường có sẵn trong các bản n8n mới hoặc cần cài thêm qua n8n community nodes nếu dùng bản cũ).
4. **Google Credentials:** Tạo OAuth2 credentials cho Google Sheets và Google Drive trong n8n.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n Editor.
2. Chọn **Import from URL** và dán link: `https://n8n.io/workflows/3332` HOẶC copy nội dung JSON của workflow và dán vào editor.
3. Sau khi import, các sếp sẽ thấy 3 node chính: `Google Sheets Trigger`, `Take a screenshot of a website`, và `Store Screenshots`.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

**Node 1: Google Sheets Trigger**
- **Chọn Credentials:** Chọn tài khoản Google đã cấu hình.
- **Sheet Name:** Chọn đúng tên Sheet chứa danh sách URL.
- **Column to Trigger On:** Chọn cột chứa URL (ví dụ: cột "URL" hoặc "Link").
- **Trigger On:** Chọn "Row Added" (khi có dòng mới) hoặc "Row Updated" tùy nhu cầu.

**Node 2: Take a screenshot of a website**
- **URL:** Đảm bảo node này nhận đúng dữ liệu URL từ node trước. Thường là `{{ $json.URL }}` hoặc tham chiếu trực tiếp đến cột URL.
- **Options:**
  - **Full Page:** Bật lên `true` nếu muốn chụp toàn bộ trang web (scroll hết chiều dài).
  - **Viewport Width/Height:** Điều chỉnh kích thước màn hình giả lập (ví dụ: 1920x1080 cho desktop, 375x667 cho mobile).
  - **Wait for Selector:** Nếu website có nội dung tải động (lazy load), các sếp nên thêm selector CSS và thời gian chờ (ví dụ: `wait: 2000ms`) để đảm bảo ảnh chụp rõ nét.

**Node 3: Store Screenshots**
- **Chọn Credentials:** Chọn tài khoản Google Drive.
- **Folder:** Chọn thư mục đích trong Drive mà các sếp muốn lưu ảnh.
- **File Name:** Đặt tên file theo cấu trúc dễ hiểu, ví dụ: `{{ $json.URL }}_{{ $now.format('YYYY-MM-DD') }}.png` để tránh trùng tên và dễ tra cứu.
- **Operation:** Chọn "Upload".

#### 3. Kích hoạt ⚡️
1. **Test Run:** Thêm một dòng URL mẫu vào Google Sheets. Chờ 1-2 phút, kiểm tra xem n8n có chạy và ảnh có xuất hiện trong Google Drive không.
2. **Active Workflow:** Bật công tắc **Active** ở góc trên bên phải để workflow hoạt động liên tục.

### ✍️ Mẹo & gợi ý nâng cao
- **So sánh thay đổi:** Kết hợp thêm node AI (LLM) hoặc Image Comparison để so sánh ảnh chụp hôm nay với ảnh chụp hôm qua, phát hiện thay đổi giao diện website.
- **Gửi thông báo:** Thêm node Telegram hoặc Email để gửi thông báo cho các sếp khi có ảnh mới được lưu hoặc khi phát hiện lỗi (website không truy cập được).
- **Lưu metadata:** Thêm cột "Timestamp" và "Status" vào Google Sheets để ghi lại thời gian chụp và trạng thái thành công/thất bại.
- **Định kỳ chụp:** Thay vì trigger theo dòng mới, các sếp có thể dùng Cron Trigger để chụp lại toàn bộ danh sách URL mỗi ngày vào lúc 8h sáng, tạo thành thư viện lịch sử.

### 📌 Kết luận
Workflow này là công cụ "vô địch" cho các sếp cần theo dõi, lưu trữ hoặc tạo tài liệu hình ảnh từ các website một cách tự động. Với chỉ 3 node đơn giản, các sếp đã có thể giải quyết bài toán chụp ảnh hàng loạt một cách chuyên nghiệp, tiết kiệm thời gian và đảm bảo độ chính xác cao. Hãy import ngay và trải nghiệm sự khác biệt mà tự động hóa mang lại!