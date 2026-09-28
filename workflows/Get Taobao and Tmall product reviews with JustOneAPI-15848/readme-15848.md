---
title: "🚀 Tự động lấy và phân tích đánh giá sản phẩm Taobao, Tmall với JustOneAPI trên n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động trích xuất, xử lý và lưu trữ dữ liệu đánh giá sản phẩm từ Taobao và Tmall sử dụng JustOneAPI một cách nhanh chóng."
slug: "lay-danh-gia-san-pham-taobao-tmall-justoneapi-n8n"
tags: [n8n, automation, taobao, tmall, justoneapi, market-research, e-commerce]
keywords: [n8n workflow, tự động hóa taobao, lấy review taobao, justoneapi, nghiên cứu thị trường e-commerce]
---

# 🚀 Tự động lấy và phân tích đánh giá sản phẩm Taobao, Tmall với JustOneAPI

Các sếp đang kinh doanh hàng nội địa Trung Quốc, làm nghiên cứu thị trường (Market Research) hay phân tích đối thủ chắc chắn hiểu rõ nỗi khổ: Việc copy thủ công hàng trăm, hàng nghìn bình luận (reviews) từ Taobao và Tmall để phân tích tâm lý khách hàng cực kỳ tốn thời gian, dễ bỏ sót và mỏi tay.

Đừng lo nữa! Bài viết này sẽ hướng dẫn các sếp cách "lên đồ" một workflow n8n cực xịn sò, tự động hóa 100% quy trình gọi API lấy toàn bộ đánh giá sản phẩm từ Taobao/Tmall thông qua **JustOneAPI**, xử lý dữ liệu gọn gàng và lưu trữ lại chỉ trong một nốt nhạc. Không cần code phức tạp, tự động hóa hoàn toàn!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 95% thời gian:** Không cần copy-paste thủ công hàng nghìn dòng review từ Taobao, Tmall.
- **Dữ liệu sạch & chuẩn hóa:** Tự động lọc, xử lý và cấu trúc hóa dữ liệu đánh giá thông qua JavaScript/Python trong n8n.
- **Hỗ trợ nghiên cứu thị trường:** Dễ dàng tổng hợp feedback của khách hàng để cải thiện sản phẩm hoặc làm content marketing.
- **Linh hoạt mở rộng:** Dễ dàng kết nối tiếp với Google Sheets, Notion hoặc các mô hình AI (OpenAI, Claude) để phân tích cảm xúc (Sentiment Analysis).
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Hệ thống n8n đang hoạt động (Cloud hoặc Self-hosted).
- Tài khoản và API Key tại **JustOneAPI** (dịch vụ cung cấp API trích xuất dữ liệu Taobao/Tmall).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần tạo một workflow mới trên n8n, sau đó copy toàn bộ mã JSON của workflow này (hoặc tải file từ nguồn cấp) và dán trực tiếp vào giao diện n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này bao gồm 6 nodes chính được sắp xếp theo một luồng logic mượt mà:

- **Manual Execution Trigger (`manualTrigger`):** 
  - Node khởi chạy thủ công. Các sếp có thể thay thế bằng *Schedule Trigger* nếu muốn tự động lấy dữ liệu định kỳ theo ngày/tuần.
- **Set API and Review Parameters (`set`):** 
  - Nơi cấu hình các tham số đầu vào quan trọng như: `API Key` của JustOneAPI, `Product ID` (Item ID của sản phẩm Taobao/Tmall cần lấy review), và số trang cần cào.
- **Fetch Taobao/Tmall Reviews via API (`httpRequest`):** 
  - Node thực hiện gọi API đến endpoint của JustOneAPI. Các sếp cần đảm bảo URL endpoint, Method (GET/POST) và Header (chứa API Key) được điền chính xác theo tài liệu của JustOneAPI.
- **Store Raw Review Data (`set`):** 
  - Lưu lại toàn bộ phản hồi dạng thô (Raw JSON response) trả về từ API để phục vụ cho việc gỡ lỗi (debugging) khi cần thiết.
- **Process Review Data (`code`):** 
  - Sử dụng node Code để trích xuất các trường thông tin quan trọng từ JSON thô (như nội dung review, tên tài khoản, thời gian, hình ảnh đánh giá, số sao...) và định dạng lại thành cấu trúc chuẩn.
- **Store Final Reviews (`set`):** 
  - Lưu trữ kết quả cuối cùng đã qua xử lý, sẵn sàng để đẩy sang Google Sheets, Database hoặc Notion.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để test chạy thử với dữ liệu mẫu xem API có trả về kết quả chuẩn chỉnh không.
- Sau khi test thành công, bật nút **Active** để chính thức đưa workflow vào hoạt động.

### ✍️ Mẹo & gợi ý nâng cao
Để workflow trở thành một "trợ lý nghiên cứu sản phẩm" thực thụ, các sếp có thể mở rộng thêm:
1. **Đẩy dữ liệu vào Google Sheets / Airtable:** Thêm node Google Sheets để tự động lưu danh sách review vào bảng tính theo dõi.
2. **Tích hợp AI phân tích cảm xúc (Sentiment Analysis):** Nối thêm OpenAI/Claude node để tự động phân tích xem khách hàng đang khen hay chê điểm nào nhiều nhất trên sản phẩm đó.
3. **Gửi báo cáo qua Telegram / Slack:** Thiết lập thông báo tự động tổng hợp số lượng review tốt/xấu gửi về nhóm chat mỗi khi quét xong.

### 📌 Kết luận
Việc nghiên cứu đối thủ và phân tích sản phẩm trên Taobao/Tmall chưa bao giờ dễ dàng đến thế khi kết hợp sức mạnh của n8n và JustOneAPI. Hãy triển khai ngay hôm nay để tối ưu hóa quy trình làm việc và bứt phá doanh thu cho cửa hàng của các sếp!