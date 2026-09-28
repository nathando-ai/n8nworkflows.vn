---
title: "🚀 Tự Động Hóa Facebook Affiliate: Tạo Bài Đăng AI Từ Link Amazon"
description: "Workflow n8n tự động lấy dữ liệu sản phẩm Amazon, dùng AI tạo caption và hình ảnh, sau đó đăng lên Facebook và cập nhật Google Sheets chỉ với 1 link."
slug: "tu-dong-hoa-facebook-affiliate-ai-amazon"
tags: [n8n, automation, no-code, affiliate-marketing, ai-content, facebook-automation]
keywords: [n8n workflow, tự động hóa facebook, affiliate amazon, ai content generator, gemini image]
---

# 🚀 Tự Động Hóa Facebook Affiliate: Tạo Bài Đăng AI Từ Link Amazon

Làm Affiliate Marketing trên Facebook nhưng mỗi lần đăng bài lại phải copy link Amazon, tìm ảnh sản phẩm, ngồi viết caption bắt mắt và chờ đợi? Đây là nỗi đau chung của nhiều người làm Affiliate khi muốn scale số lượng bài đăng mà không muốn tốn quá nhiều thời gian cho các thao tác thủ công lặp đi lặp lại.

Workflow **Create AI-Enhanced Facebook Posts from Amazon Affiliate Links with Gemini** chính là giải pháp "chốt hạ" cho vấn đề này. Chỉ cần bạn thêm một link sản phẩm vào Google Sheets, hệ thống sẽ tự động:
1. Lấy thông tin chi tiết sản phẩm từ Amazon.
2. Dùng AI (Gemini) để tạo caption hấp dẫn và sinh hình ảnh sản phẩm chuyên nghiệp.
3. Đăng bài lên Facebook Page của bạn.
4. Cập nhật trạng thái "Hoàn thành" trên Sheet để bạn theo dõi.

Toàn bộ quy trình diễn ra tự động 100%, không cần code, giúp bạn tập trung vào chiến lược thay vì vận hành.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Chỉ mất 5 giây để thêm link, phần còn lại AI lo.
- **Nội dung chất lượng cao:** Caption được viết bởi LLM (Gemini) tối ưu cho tương tác, hình ảnh được sinh ra phù hợp với sản phẩm.
- **Quy trình khép kín:** Tự động đăng bài và cập nhật log trên Google Sheets, tránh trùng lặp hoặc bỏ sót.
- **Scale dễ dàng:** Có thể xử lý hàng chục link sản phẩm mỗi ngày mà không cần can thiệp thủ công.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị các tài khoản và API Keys sau:
1. **Tài khoản n8n:** Cloud hoặc Self-hosted.
2. **Google Sheets:** Tạo một sheet với các cột: `Product Link` và `Facebook Upload` (hoặc tên cột tương ứng trong workflow).
3. **RapidAPI:** Đăng ký và lấy API Key cho service lấy dữ liệu Amazon (thường là "Amazon Product Details" hoặc tương tự).
4. **OpenRouter:** Tài khoản OpenRouter để truy cập model AI (workflow mặc định dùng `google/gemini-2.0-flash-exp:free`).
5. **Google Gemini API Key:** Lấy từ [Google AI Studio](https://aistudio.google.com/apikey) để dùng cho việc sinh hình ảnh.
6. **Facebook Graph API:** Kết nối tài khoản Facebook Page có quyền đăng bài.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n Editor.
2. Chọn **Import from File** hoặc **Import from URL**.
3. Dán link workflow gốc: `https://n8n.io/workflows/7422` hoặc tải file JSON về và import.
4. Sau khi import, các sếp sẽ thấy một workflow với 15 nodes chính.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Đây là phần quan trọng nhất. Các sếp cần click vào từng node và cấu hình credentials/tham số:

*   **Node: `Google Sheets Trigger`**
    *   Chọn **Credential** Google Sheets của bạn.
    *   Chọn đúng **Sheet Name** và **Range** (ví dụ: `Sheet1!A:B`).
    *   Đảm bảo cột đầu tiên chứa `Product Link` và cột thứ hai là cột trạng thái (ví dụ: `Facebook Upload`).

*   **Node: `Amazon Product Details` (HTTP Request)**
    *   Đây là node gọi API RapidAPI để lấy thông tin sản phẩm.
    *   Trong phần **Headers**, tìm key `X-RapidAPI-Key` và thay `YOUR_API_KEY` bằng API Key RapidAPI của bạn.
    *   Kiểm tra URL để đảm bảo nó trỏ đúng endpoint lấy chi tiết sản phẩm theo ASIN.

*   **Node: `OpenRouter Chat Model` (và các node AI khác)**
    *   Workflow sử dụng model `google/gemini-2.0-flash-exp:free` qua OpenRouter.
    *   Các sếp cần tạo **Credential** cho OpenRouter trong n8n.
    *   Chọn credential này trong các node: `FB caption`, `Image Prompt Generate`, `asin number`.
    *   *Lưu ý:* Nếu model free bị giới hạn, các sếp có thể đổi sang model trả phí khác trên OpenRouter nếu cần độ ổn định cao hơn.

*   **Node: `ai image generator` (HTTP Request)**
    *   Node này gọi API của Google Gemini để sinh hình ảnh.
    *   Trong phần **Body** hoặc **Headers**, tìm vị trí chứa `YOUR_GEMINI_API_KEY` và thay bằng API Key Gemini của bạn.
    *   Đảm bảo prompt sinh ảnh được cấu hình hợp lý trong node `Image Prompt Generate` (Agent) trước đó.

*   **Node: `Facebook Graph API`**
    *   Chọn **Credential** Facebook Graph API.
    *   Chọn **Resource**: `Post`.
    *   Chọn **Operation**: `Create`.
    *   Chọn đúng **Page ID** hoặc **Profile ID** mà bạn muốn đăng bài.
    *   Kiểm tra các trường `message` (caption) và `link` (link affiliate) đã được map đúng từ các node trước đó.

*   **Node: `Google Sheets` (Update)**
    *   Sau khi đăng bài thành công, node này sẽ cập nhật cột trạng thái trên Sheet.
    *   Chọn đúng **Credential** Google Sheets.
    *   Chọn **Operation**: `Update`.
    *   Đảm bảo **Document ID** và **Sheet Name** khớp với Trigger.
    *   Map giá trị cần cập nhật (ví dụ: "Done ✅") vào cột tương ứng.

*   **Node: `Wait`**
    *   Workflow có một node `Wait` để tạo khoảng thời gian giữa các bước (có thể là để tránh rate limit hoặc chờ xử lý). Các sếp có thể chỉnh thời gian chờ nếu cần (ví dụ: 5-10 giây).

#### 3. Kích hoạt ⚡️
1. **Test Run:**
    *   Thêm một link sản phẩm Amazon vào cột `Product Link` trên Google Sheets.
    *   Chạy workflow thủ công (Test Workflow) hoặc đợi Trigger hoạt động.
    *   Kiểm tra từng node:
        *   `asin number`: Có lấy được mã ASIN không?
        *   `Amazon Product Details`: Có trả về tên, giá, mô tả sản phẩm không?
        *   `FB caption`: Caption AI có hay không?
        *   `ai image generator`: Có trả về URL ảnh không?
        *   `Facebook Graph API`: Bài có được đăng lên Page không?
        *   `Google Sheets`: Cột trạng thái có chuyển thành "Done" không?
2. **Bật Active:**
    *   Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải.
    *   Workflow sẽ tự động chạy mỗi khi có dòng mới được thêm vào Sheet.

### ✍️ Mẹo & gợi ý nâng cao
- **Tùy biến Prompt Caption:** Trong node `FB caption` (Agent), các sếp có thể chỉnh sửa System Prompt để yêu cầu AI viết caption theo phong cách riêng (ví dụ: hài hước, sang trọng, hoặc tập trung vào ưu đãi).
- **Đa dạng hóa hình ảnh:** Thay vì chỉ dùng 1 prompt cố định, các sếp có thể thêm logic để tạo 2-3 biến thể hình ảnh và chọn ngẫu nhiên một cái để đăng, giúp nội dung không bị nhàm chán.
- **Gửi thông báo qua Telegram/Slack:** Thêm node `Telegram` hoặc `Slack` sau node `Facebook Graph API` để nhận thông báo ngay khi bài đăng thành công hoặc lỗi, giúp giám sát tốt hơn.
- **Lọc sản phẩm theo ngách:** Thêm một cột `Category` trên Sheet và dùng node `IF` để chỉ xử lý các sản phẩm thuộc ngách cụ thể, tránh đăng nhầm sản phẩm không liên quan.

### 📌 Kết luận
Workflow này là công cụ "vũ khí" mạnh mẽ cho bất kỳ ai làm Affiliate Marketing trên Facebook. Bằng cách tự động hóa toàn bộ quy trình từ lấy dữ liệu, tạo nội dung AI đến đăng bài, các sếp có thể tăng gấp nhiều lần số lượng bài đăng chất lượng mà không tốn thêm chi phí nhân sự. Hãy thử ngay hôm nay để trải nghiệm sự khác biệt! 🚀