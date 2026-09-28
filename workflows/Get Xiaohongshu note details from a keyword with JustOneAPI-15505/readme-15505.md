---
title: "🚀 Tự động lấy chi tiết bài viết Xiaohongshu theo từ khóa với n8n và JustOneAPI"
description: "Hướng dẫn xây dựng workflow n8n tự động tìm kiếm từ khóa trên Xiaohongshu, trích xuất ID và lấy toàn bộ chi tiết bài viết qua JustOneAPI một cách nhanh chóng."
slug: "tu-dong-lay-chi-tiet-bai-viet-xiaohongshu-n8n-justoneapi"
tags: [n8n, automation, xiaohongshu, justoneapi, market-research, web-scraping]
keywords: [n8n workflow, xiaohongshu automation, justoneapi, nghiên cứu thị trường, trích xuất dữ liệu xiaohongshu]
---

# 🚀 Tự động lấy chi tiết bài viết Xiaohongshu theo từ khóa với n8n và JustOneAPI

Các sếp làm trong lĩnh vực nghiên cứu thị trường, sáng tạo nội dung hay marketing chắc hẳn đều hiểu cảm giác "ngợp" khi phải tìm kiếm thủ công từng bài viết trên Xiaohongshu (RED) để phân tích xu hướng. Việc copy, paste, thống kê lượt like, comment, share thủ công vừa tốn thời gian lại dễ bỏ sót thông tin quan trọng.

Giải pháp ở đây là gì? Workflow n8n này sẽ giúp các sếp tự động hóa 100% quy trình: nhập từ khóa -> tìm kiếm bài viết -> lọc ID độc nhất -> gọi API lấy chi tiết bài viết (tiêu đề, nội dung, tác giả, lượt tương tác...) và trả về cấu trúc dữ liệu cực kỳ sạch sẽ để phục vụ các bước tiếp theo.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Chỉ cần nhập từ khóa, hệ thống lo phần còn lại.
- **Dữ liệu cấu trúc sạch sẽ:** Trả về đầy đủ `noteId`, `title`, `desc`, `authorName`, `likeCount`, `commentCount`, `shareCount`, `collectedCount`, và `noteUrl`.
- **Linh hoạt mở rộng:** Dễ dàng điều chỉnh số lượng bài viết cần lấy (`maxNotes`), thời gian bài đăng (`noteTime`) tùy theo nhu cầu nghiên cứu.
- **Tích hợp linh hoạt:** Kết nối mượt mà với Google Sheets, Notion, Airtable hoặc các mô hình AI để phân tích sâu hơn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một tài khoản và **API Token từ JustOneAPI**.
- Môi trường n8n hỗ trợ các node `HTTP Request` và `Code`.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể sử dụng file JSON của workflow này và import trực tiếp vào n8n Editor của mình thông qua tính năng **Import from File** hoặc copy/paste trực tiếp.

Danh sách các nodes chính trong workflow bao gồm:
- **Manual Execution Trigger**: Kích hoạt chạy thủ công theo nhu cầu.
- **Prepare API and Research Inputs** (Set): Nơi khai báo token và từ khóa tìm kiếm.
- **Fetch Xiaohongshu Notes by Keyword** (HTTP Request): Gọi API tìm kiếm V2 của Xiaohongshu.
- **Output Search Results Data** (Set): Chuẩn hóa dữ liệu kết quả tìm kiếm thô.
- **Extract Note IDs from Results** (Code): Lọc ID bài viết độc nhất và giới hạn số lượng.
- **Output Extracted Note IDs** (Set): Chuyển tiếp danh sách ID đã lọc.
- **Fetch Xiaohongshu Note Details** (HTTP Request): Gọi API lấy chi tiết từng bài viết.
- **Build Note Details List** (Code): Tổng hợp và cấu trúc lại thông tin chi tiết.
- **Output Final Note Details** (Set): Trả về kết quả cuối cùng.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
- **Node `Prepare API and Research Inputs`**: 
  - Điền `token` của JustOneAPI vào thông số cấu hình.
  - Cập nhật `keyword` (từ khóa muốn nghiên cứu).
  - Tùy chỉnh các thông số tùy chọn nếu cần: `page`, `sortSearchNoteV2`, `noteType`, `noteTime` (mặc định: `一天内` - trong ngày), và `maxNotes` (mặc định để `1` nếu chỉ muốn lấy kết quả đầu tiên).
- **Nodes HTTP Request**: Đảm bảo cấu hình kết nối đúng với endpoint của JustOneAPI dựa trên tài liệu của nhà cung cấp.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để chạy thử với dữ liệu mẫu và kiểm tra kết quả trả về ở node cuối cùng (`Output Final Note Details`).
- Sau khi kiểm tra mọi thứ hoạt động trơn tru, các sếp có thể kết nối thêm các đích đến khác hoặc giữ nguyên để trigger thủ công khi cần.

### ✍️ Mẹo & gợi ý nâng cao
- **Lưu trữ tự động:** Nối thêm node Google Sheets hoặc Airtable vào sau node cuối cùng để tự động lưu lại toàn bộ kết quả nghiên cứu.
- **Phân tích bằng AI:** Gửi các trường `desc` và `title` vào node OpenAI/Anthropic để AI tóm tắt xu hướng nội dung hoặc phân tích Sentiment (cảm xúc người dùng).
- **Cảnh báo qua Chat:** Kết hợp thêm node Telegram hoặc Slack để nhận thông báo ngay khi có bài viết hot theo từ khóa chiến lược.

### 📌 Kết luận
Workflow này là một "vũ khí" cực kỳ lợi hại cho các đội ngũ marketing và nghiên cứu thị trường muốn khai thác dữ liệu từ Xiaohongshu một cách tự động và chuyên nghiệp. Hãy cài đặt ngay lên hệ thống n8n của các sếp để tối ưu hóa thời gian làm việc nhé!