---
title: "🚀 Tự động trích xuất xu hướng từ khóa YouTube hot nhất bằng n8n"
description: "Hướng dẫn sử dụng workflow n8n để phân tích, tính toán tỷ lệ tương tác và tự động tổng hợp từ khóa xu hướng từ các video YouTube hot nhất."
slug: "trich-xuat-tu-khoa-youtube-xu-huong-bang-n8n"
tags: [n8n, automation, youtube-api, market-research, ai-content-strategy]
keywords: [n8n workflow, trích xuất từ khóa youtube, phân tích xu hướng youtube, youtube data api v3, tự động hóa marketing]
---

# 🚀 Tự động trịch xuất từ khóa YouTube xu hướng để tối ưu chiến lược nội dung

Các sếp làm sáng tạo nội dung (Content Creator) hoặc Marketer chắc chắn hiểu cảm giác "cạn kiệt ý tưởng" hoặc vật lộn để tìm ra những từ khóa thực sự có lượng tương tác cao thay vì chỉ nhìn vào số lượt xem ảo. Việc ngồi thủ công lướt từng video thịnh hành, thống kê lượt thích, bình luận và lọc từ khóa mất hàng giờ đồng hồ mỗi tuần.

Giải pháp là gì? Workflow n8n tự động hóa 100% này sẽ thay các sếp gọi API YouTube, tính toán chính xác tỷ lệ tương tác (`Engagement Rate`), xếp hạng Top video và trích xuất toàn bộ bộ từ khóa xu hướng chất lượng cao một cách nhanh chóng.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian nghiên cứu thị trường:** Không còn phải thủ công copy-paste tiêu đề hay tag video.
- **Dữ liệu tương tác thực chiến:** Tự động tính toán chỉ số `Engagement Rate` (Likes + Comments / Views) để tìm ra nội dung giữ chân người xem tốt nhất.
- **Bộ từ khóa chuẩn SEO:** Lọc và tổng hợp các thẻ (tags) từ 20 video có độ tương tác cao nhất thành một danh sách gọn gàng để tối ưu hóa tiêu đề và mô tả video mới.
- **Hoạt động linh hoạt:** Dễ dàng chuyển đổi từ chạy thủ công sang tự động chạy định kỳ bằng Cron node.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **YouTube Data API v3 Key:** Cần có tài khoản Google Cloud Console và kích hoạt YouTube Data API v3 để lấy API Key điền vào node HTTP Request.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy đoạn JSON của workflow (hoặc tải file JSON từ nguồn gốc) và dán trực tiếp vào n8n Editor của mình thông qua tính năng Import từ clipboard.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 7 nodes chính được liên kết chặt chẽ:

- **Node `When clicking ‘Execute workflow’` (manualTrigger):** Điểm khởi đầu thủ công. Các sếp có thể thay thế node này bằng *Schedule (Cron)* để chạy tự động mỗi ngày/tuần sau khi đã kiểm tra xong.
- **Node `HTTP Request – YouTube Most Popular` (httpRequest):** 
  - Cấu hình gọi API tới endpoint `videos` của YouTube Data API v3.
  - Tham số cần truyền: `part=snippet,statistics`, `chart=mostPopular`, `regionCode=DE` (hoặc quốc gia các sếp muốn nghiên cứu như `VN`, `US`...), và `key` (YouTube API Key của các sếp).
- **Node `Split Out – Items` (splitOut):** Tách mảng `items[]` từ kết quả trả về của API thành từng item độc lập để xử lý mượt mà hơn.
- **Node `Set – Derive Context` (set):** Trích xuất các trường dữ liệu quan trọng như tiêu đề, kênh, ngày đăng và tính toán chỉ số tỷ lệ tương tác qua công thức: `engagementRate = (likes + comments) / (views + 1)`.
- **Node `Item Lists – Top by Engagement` (itemLists):** 
  - Cấu hình operation: **Sort**.
  - Sắp xếp danh sách theo `engagementRate` giảm dần (descending) và giữ lại **Top 20** video chất lượng nhất.
- **Node `Aggregate – Collect Tags` (aggregate):** Thu thập toàn bộ `snippet.tags` từ Top 20 video đã lọc và gộp chúng vào chung một mảng dữ liệu.
- **Node `Summarize – Tag Summary` (summarize):** Nối toàn bộ các thẻ tag lại thành một chuỗi (string) duy nhất – tạo ra danh sách từ khóa xu hướng sạch sẽ, sẵn sàng phục vụ cho chiến lược nội dung.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để test lần đầu xem dữ liệu trả về từ YouTube API có chuẩn chỉnh không.
- Sau khi test thành công, bật nút **Active** ở góc trên bên phải để workflow sẵn sàng hoạt động tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Telegram/Slack:** Thêm một node gửi thông báo để kết quả bộ từ khóa xu hướng được bắn thẳng về nhóm Telegram hoặc Slack của team Content mỗi sáng thứ Hai.
- **Lưu trữ tự động:** Kết nối node cuối cùng với Google Sheets hoặc Airtable để lưu lịch sử các xu hướng từ khóa theo từng tuần, phục vụ việc phân tích dài hạn.
- **Mở rộng đa quốc gia:** Nhân bản HTTP Request node cho các quốc gia khác nhau (`US`, `VN`, `GB`) để so sánh sự khác biệt về xu hướng nội dung toàn cầu.

### 📌 Kết luận
Với workflow tự động hóa này, việc nghiên cứu từ khóa và xu hướng YouTube không còn là bài toán đau đầu nữa. Hãy cài đặt ngay để tối ưu hóa năng suất làm nội dung cho kênh của các sếp!