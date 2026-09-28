---
title: "🚀 Tự động tìm cơ hội Internal Link chuẩn SEO với SerpAPI và Google Sheets trên n8n"
description: "Khám phá cách tự động hóa quy trình tìm kiếm và gợi ý internal link cho website của bạn bằng n8n, SerpAPI và Google Sheets, giúp tối ưu SEO hiệu quả mà không tốn công sức."
slug: "tu-dong-tim-co-hoi-internal-link-serpapi-google-sheets"
tags: [n8n, automation, seo, google-sheets, serpapi, content-creation]
keywords: [n8n workflow, tự động hóa internal link, seo automation, serpapi google sheets, n8n seo]
---

# 🚀 Tự động tìm cơ hội Internal Link chuẩn SEO với SerpAPI và Google Sheets

Các sếp làm SEO chắc chắn đều hiểu tầm quan trọng của **Internal Link (liên kết nội bộ)** đối với việc phân phối sức mạnh website (PageRank) và giúp bot Google cào dữ liệu hiệu quả hơn. Tuy nhiên, việc ngồi thủ công tìm kiếm các bài viết liên quan trên cùng một site để trỏ link qua lại cho hàng trăm bài viết là một "cực hình" tốn rất nhiều thời gian.

Giải pháp là đây! Workflow n8n này sẽ tự động hóa 100% quy trình: đọc danh sách URL và từ khóa mục tiêu từ Google Sheets, sử dụng **SerpAPI** để quét các bài viết liên quan trên chính website của bạn (sử dụng toán tử `site:` và loại trừ URL hiện tại), sau đó tự động ghi nhận các gợi ý internal link ngược trở lại Google Sheets.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không lo gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm hàng chục giờ:** Tự động hóa hoàn toàn việc tìm kiếm cơ hội chèn internal link thay vì search thủ công trên Google.
- **Tối ưu SEO On-page liên tục:** Giúp cấu trúc website chặt chẽ, cải thiện thứ hạng từ khóa nhanh chóng.
- **Tránh ghi đè dữ liệu cũ:** Workflow thông minh tự động lọc các dòng đã xử lý (`internal link 1`), chỉ quét các URL mới.
- **Xử lý mượt mà theo lô (Batch):** Giúp tránh chạm ngưỡng Rate Limit của các API bên thứ ba.
:::

### 📦 Yêu cầu cần thiết
:::info[CHUẨN BỊ TRƯỚC KHI "LÊN ĐỒ"]
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Tài khoản SerpAPI** để lấy API Key thực hiện truy vấn tìm kiếm.
- **Google Sheets**: Tạo sẵn một bảng tính chứa các cột: URL mục tiêu, Từ khóa (Keyword), và các cột chứa kết quả Internal Link.
- **Google Sheets OAuth2 Credentials** để n8n có thể đọc/ghi dữ liệu trên Google Sheets của các sếp.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow hoặc copy toàn bộ mã JSON từ nguồn gốc.
- Trong giao diện n8n Editor, bấm vào menu **Add workflow** -> Chọn **Import from File** hoặc dán trực tiếp JSON vào workspace.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình chính xác các node trọng điểm sau đây trong workflow:

- **Node `Get URLs and keywords` (Google Sheets):**
  - Chọn tài khoản kết nối (`Google Sheets OAuth2 API`).
  - Trỏ đến đúng Spreadsheet ID và Sheet Name chứa danh sách URL và từ khóa của các sếp.
  - Lưu ý logic lọc dữ liệu trong node này đã được thiết lập sẵn để bỏ qua các dòng đã có giá trị ở cột `internal link 1`.

- **Node `Loop Over Items` (Split In Batches):**
  - Mặc định batch size đang để là `5`. 
  - *Lưu ý:* Không nên chỉnh thông số này quá cao để tránh dính lỗi Rate Limit từ Google Sheets và SerpAPI.

- **Node `Get search results using SerpAPI` (HTTP Request):**
  - Cần thêm Credentials cho SerpAPI (`serpApi` hoặc `httpHeaderAuth`).
  - Node này sẽ thực hiện câu lệnh tìm kiếm kết hợp `site:<domain>` và từ khóa mục tiêu, đồng thời loại trừ chính URL hiện tại (`-inurl:<url>`).

- **Node `Extract links from JSON` (Set):**
  - Node này giúp trích xuất các URL dạng organic từ kết quả trả về cồng kềnh của SerpAPI.

- **Node `Add internal URL to Google Sheet` (Google Sheets):**
  - Cấu hình Operation là `update`.
  - Sử dụng cú pháp biểu thức (inline `if`) để nếu không tìm thấy URL phù hợp, hệ thống sẽ tự động điền giá trị `'N/A'`.

#### 3. Kích hoạt ⚡️
- Bấm nút **Execute Workflow** chạy thử nghiệm thủ công với 1-2 dòng dữ liệu mẫu để kiểm tra kết quả trả về trên Google Sheets.
- Sau khi kiểm tra mọi thứ hoạt động trơn tru, hãy chuyển trạng thái sang **Active** để sẵn sàng sử dụng.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo Telegram/Slack:** Thêm một node thông báo vào cuối chuỗi để n8n gửi tin nhắn báo cáo ngay khi quét xong danh sách internal link mới.
- **Sử dụng Google Custom Search Engine:** Nếu số lượng URL cần quét cực kỳ lớn, các sếp có thể thay thế SerpAPI bằng Google Programmable Search Engine để tiết kiệm chi phí.
- **Lập lịch chạy định kỳ (Schedule Trigger):** Thay thế `Manual trigger` bằng `Schedule Trigger` để hệ thống tự động quét và gợi ý link hàng tuần hoặc hàng tháng.

### 📌 Kết luận
Việc xây dựng hệ thống Internal Link chưa bao giờ dễ dàng đến thế với sức mạnh của tự động hóa n8n. Hãy áp dụng ngay workflow này để tiết kiệm thời gian, tối ưu hóa SEO và đẩy nhanh tốc độ thăng hạng cho website của các sếp!