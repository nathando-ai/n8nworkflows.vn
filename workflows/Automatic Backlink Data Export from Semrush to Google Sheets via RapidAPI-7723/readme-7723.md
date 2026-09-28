---
title: "🚀 Tự Động Hóa Kiểm Tra Backlink Semrush & Lưu Google Sheets"
description: "Workflow n8n giúp các sếp nhập URL, tự động gọi API Semrush (qua RapidAPI) và xuất dữ liệu backlink chi tiết cùng tổng quan vào Google Sheets chỉ trong vài giây."
slug: "tu-dong-hoa-kiem-tra-backlink-semrush-google-sheets"
tags: [n8n, automation, no-code, seo, semrush, google-sheets]
keywords: [n8n workflow, tự động hóa seo, semrush api, backlink checker, google sheets automation]
---

# 🚀 Tự Động Hóa Kiểm Tra Backlink Semrush & Lưu Google Sheets

Trong thế giới SEO cạnh tranh khốc liệt, việc kiểm tra backlink (liên kết ngược) là một phần không thể thiếu. Tuy nhiên, việc thủ công đăng nhập vào Semrush, chờ đợi dữ liệu tải về, rồi copy-paste vào Excel hay Google Sheets là một quy trình tẻ nhạt, dễ sai sót và tốn rất nhiều thời gian. Đặc biệt, khi cần kiểm tra hàng loạt domain hoặc lập báo cáo định kỳ, quy trình thủ công trở thành một "nút thắt cổ chai" lớn.

Workflow n8n này chính là giải pháp "chữa cháy" hoàn hảo. Nó cho phép các sếp tạo một form nhập liệu đơn giản, sau đó tự động gọi API Semrush (thông qua RapidAPI) để lấy dữ liệu backlink và tổng quan, rồi đẩy thẳng vào Google Sheets. Không cần code, không cần copy-paste, mọi thứ diễn ra mượt mà và chính xác 100%.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, đặc biệt khi cần xử lý lượng lớn yêu cầu hoặc tích hợp với các hệ thống khác, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian tối đa:** Thay vì mất 5-10 phút cho mỗi lần kiểm tra thủ công, quy trình chỉ mất vài giây từ lúc submit form đến khi dữ liệu nằm trong Sheet.
- **Chính xác tuyệt đối:** Loại bỏ hoàn toàn lỗi copy-paste, sai định dạng dữ liệu do con người gây ra.
- **Dữ liệu tập trung:** Tất cả lịch sử kiểm tra backlink được lưu trữ có hệ thống trong Google Sheets, dễ dàng phân tích xu hướng và so sánh theo thời gian.
- **Cá nhân hóa linh hoạt:** Các sếp có thể tùy chỉnh form nhập liệu và cấu trúc cột trong Sheet theo nhu cầu báo cáo riêng của team.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản n8n:** Đã cài đặt và chạy (cloud hoặc self-hosted).
2. **Tài khoản RapidAPI:** Đăng ký và subscribe gói **Semrush** trên RapidAPI. Lấy `X-RapidAPI-Key` và `X-RapidAPI-Host` từ dashboard RapidAPI.
3. **Tài khoản Google:** Đã tạo một Google Sheet mới.
   - Tạo 2 tab (sheet) trong file đó:
     - Tab 1: Đặt tên là `backlink overflow` (hoặc tên tương tự, khớp với cấu hình node).
     - Tab 2: Đặt tên là `backlinks`.
   - Copy **Spreadsheet ID** (mã nằm giữa `/d/` và `/edit` trong URL của Google Sheet).
4. **Google Credentials:** Đã tạo và kết nối credentials Google API trong n8n.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n Editor.
2. Chọn **Import from URL** hoặc **Import from File** (nếu các sếp đã tải file JSON về).
3. Dán link workflow: `https://n8n.io/workflows/7723` hoặc chọn file JSON đã tải.
4. Workflow sẽ được import với 6 nodes chính.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

Dưới đây là các node quan trọng cần cấu hình lại cho phù hợp với tài khoản của các sếp:

**1. Node: `On form submission` (Form Trigger)**
- Đây là điểm bắt đầu. Các sếp có thể chỉnh sửa các trường (fields) trong form nếu muốn thêm thông tin (ví dụ: tên dự án, người thực hiện).
- Mặc định workflow yêu cầu nhập **Website URL**. Hãy đảm bảo trường này bắt buộc (required).

**2. Node: `HTTP Request`**
- Đây là node gọi API Semrush.
- **Authentication:** Chọn **Header Auth**.
- **Headers:**
  - `X-RapidAPI-Key`: Dán API Key của các sếp từ RapidAPI.
  - `X-RapidAPI-Host`: Dán Host (thường là `semrush.p.rapidapi.com`).
- **Body:** Kiểm tra xem tham số `url` có được map đúng từ output của Form Trigger không (thường là `{{ $json.url }}`).

**3. Node: `Reformat 1` & `Reformat 2` (Code Nodes)**
- Hai node này dùng JavaScript để tách dữ liệu từ response JSON của Semrush.
- **Reformat 1:** Tách phần `backlinksOverview` (tổng quan: tổng số backlink, domain referring, v.v.).
- **Reformat 2:** Tách phần `backlinks` (chi tiết từng link: source, anchor, score, v.v.).
- *Lưu ý:* Nếu Semrush thay đổi cấu trúc API, các sếp có thể cần chỉnh sửa code trong 2 node này. Tuy nhiên, với phiên bản hiện tại, code đã được tối ưu sẵn.

**4. Node: `Backlink overview` (Google Sheets)**
- **Operation:** Append (Thêm dòng mới).
- **Document ID:** Dán **Spreadsheet ID** của Google Sheet mà các sếp đã tạo.
- **Sheet Name:** Đặt tên tab chứa dữ liệu tổng quan (ví dụ: `backlink overflow`).
- **Mapping:** Kiểm tra các cột mapping. Đảm bảo các trường như `total_backlinks`, `referring_domains`... được map đúng vào các cột tương ứng trong Sheet.

**5. Node: `Backlinks` (Google Sheets)**
- **Operation:** Append.
- **Document ID:** Dán cùng **Spreadsheet ID** ở trên.
- **Sheet Name:** Đặt tên tab chứa dữ liệu chi tiết (ví dụ: `backlinks`).
- **Mapping:** Map các trường chi tiết như `source_url`, `anchor_text`, `authority_score`... vào các cột trong Sheet.

:::note[Lưu ý quan trọng về Google Sheets]
Hãy đảm bảo rằng tên các tab (Sheet Name) trong Google Sheet của các sếp **khớp hoàn toàn** với tên được cấu hình trong 2 node Google Sheets của workflow. Nếu tên không khớp, workflow sẽ báo lỗi "Sheet not found".
:::

#### 3. Kích hoạt ⚡️
1. **Test Run:**
   - Nhấn vào nút **Test Workflow** (hoặc chạy từng node).
   - Mở form (URL sẽ hiển thị khi chạy test), nhập một website mẫu (ví dụ: `https://tino.vn`).
   - Chạy workflow.
   - Kiểm tra xem dữ liệu có xuất hiện trong Google Sheets không.
2. **Bật Active:**
   - Nếu test thành công, nhấn nút **Active** ở góc trên bên phải để kích hoạt workflow.
   - Copy **Production URL** của Form Trigger để chia sẻ cho team hoặc nhúng vào website.

### ✍️ Mẹo & gợi ý nâng cao
- **Gửi thông báo qua Telegram/Slack:** Sau khi dữ liệu được lưu vào Sheet, các sếp có thể thêm một node `Telegram` hoặc `Slack` để gửi thông báo "Đã hoàn tất kiểm tra backlink cho [URL]" kèm link xem Sheet.
- **Lập lịch kiểm tra định kỳ:** Thay vì dùng Form Trigger, các sếp có thể thay bằng `Schedule Trigger` và một danh sách URL trong Google Sheets để tự động kiểm tra hàng loạt domain mỗi tuần.
- **Cảnh báo thay đổi đột ngột:** Thêm một node `If` để so sánh số lượng backlink hiện tại với lần kiểm tra trước đó. Nếu có sự sụt giảm hoặc tăng đột biến, gửi cảnh báo ngay lập tức.
- **Tích hợp AI:** Dùng node `OpenAI` hoặc `Anthropic` để phân tích dữ liệu backlink vừa lấy được và tạo ra một báo cáo tóm tắt bằng ngôn ngữ tự nhiên (ví dụ: "Chất lượng backlink tốt, nhưng có 5 link từ domain spam, cần xem xét").

### 📌 Kết luận
Việc tự động hóa quy trình kiểm tra backlink không chỉ giúp tiết kiệm thời gian mà còn nâng cao độ chính xác và khả năng phân tích dữ liệu SEO. Với workflow n8n này, các sếp có thể tập trung vào chiến lược thay vì những thao tác lặp đi lặp lại nhàm chán. Hãy import, cấu hình và bắt đầu tối ưu hóa quy trình SEO của mình ngay hôm nay!