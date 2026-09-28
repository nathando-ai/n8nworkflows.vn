---
title: "🚀 Tự động trích xuất thông tin Amazon Best Seller điện tử với Bright Data và Google Gemini"
description: "Hướng dẫn xây dựng workflow n8n tự động cào dữ liệu sản phẩm bán chạy nhất trên Amazon bằng Bright Data và cấu trúc hóa dữ liệu thông minh với Google Gemini AI."
slug: "trich-xuat-amazon-best-seller-bright-data-google-gemini"
tags: [n8n, automation, ai, scraping, bright-data, google-gemini, e-commerce]
keywords: [n8n workflow, cào dữ liệu amazon, bright data, google gemini ai, trích xuất dữ liệu cấu trúc, tự động hóa e-commerce]
---

# 🚀 Tự động trích xuất thông tin Amazon Best Seller điện tử với Bright Data và Google Gemini

Các sếp có đang mất hàng giờ liền để copy, paste hoặc thủ công thu thập dữ liệu sản phẩm bán chạy (Best Sellers) trên Amazon nhằm nghiên cứu thị trường, phân tích đối thủ cạnh tranh hay tìm nguồn hàng dropshipping? Việc này không chỉ tẻ nhạt, mất thời gian mà còn dễ gặp rỗi khi Amazon chặn IP hoặc thay đổi giao diện liên tục.

Giải pháp ở đây là gì? Workflow n8n tự động hóa 100% kết hợp sức mạnh cào dữ liệu chuyên nghiệp từ **Bright Data** và khả năng phân tích, cấu trúc hóa dữ liệu cực đỉnh của **Google Gemini AI**. Các sếp chỉ cần bấm nút hoặc đặt lịch chạy, toàn bộ thông tin sản phẩm điện tử hot nhất sẽ được bóc tách gọn gàng, sẵn sàng phục vụ cho các chiến dịch kinh doanh.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Bỏ qua hoàn toàn thao tác cào dữ liệu thủ công, tiết kiệm 95% thời gian nghiên cứu thị trường.
- **Dữ liệu chuẩn cấu trúc:** Biến các trang HTML thô cồng kềnh thành JSON hoặc bảng dữ liệu sạch sẽ, rõ ràng (tên sản phẩm, giá, đánh giá,...) nhờ Google Gemini.
- **Vượt rào cản chống bot:** Sử dụng hạ tầng proxy/scraping chuyên nghiệp của Bright Data giúp hạn chế tối đa việc bị Amazon chặn IP.
- **Linh hoạt tích hợp:** Dễ dàng chuyển tiếp dữ liệu đã trích xuất đến Google Sheets, Slack, Database hoặc hệ thống CRM thông qua Webhook.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một instance n8n đang hoạt động.
- Tài khoản **Bright Data** (để lấy API/Zone cấu hình cào dữ liệu Amazon).
- API Key của **Google Gemini** (Google AI Studio) để chạy mô hình AI trích xuất thông tin.
- Endpoint Webhook (tùy chọn) nếu các sếp muốn bắn dữ liệu sang hệ thống khác.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này từ n8n.io (Link gốc: [Workflow 3681](https://n8n.io/workflows/3681)), sau đó paste trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để workflow chạy trơn tru, các sếp nhớ cấu hình kỹ các node trọng điểm sau:

- **Set Amazon URL with the Bright Data Zone (`set`):**
  - Cập nhật lại đường dẫn URL Amazon Best Seller kèm theo thông tin Zone/API của tài khoản Bright Data của các sếp.
- **HTTP Request to fetch the Amazon Best Seller Products (`httpRequest`):**
  - Kiểm tra lại phần Credentials (`httpHeaderAuth`) để đảm bảo kết nối xác thực với Bright Data hoạt động chính xác.
- **Google Gemini Chat Model (`lmChatGoogleGemini`):**
  - Thêm Google Palm/Gemini API Credentials. 
  - Workflow sử dụng mô hình Google Gemini Flash Exp (hoặc các model tương đương) để phân tích ngữ nghĩa và trích xuất thông tin.
- **Webhook Notifier for structured data extractor (`httpRequest`):**
  - Cập nhật lại URL Webhook nhận dữ liệu cấu trúc (nếu các sếp muốn đẩy dữ liệu này sang Make, Zapier, Google Sheets hoặc custom server của mình).

#### 3. Kích hoạt ⚡️
- Bấm nút **‘Test workflow’** ở node `When clicking ‘Test workflow’` để chạy thử nghiệm xem dữ liệu trả về từ Bright Data và Gemini có chính xác không.
- Sau khi test thành công, bật trạng thái **Active** để workflow sẵn sàng hoạt động tự động theo lịch trình (nếu cài đặt Trigger định kỳ).

### ✍️ Mẹo & gợi ý nâng cao
- **Lưu trữ tự động:** Thay vì dùng Webhook Notifier, các sếp có thể nối thêm node **Google Sheets** hoặc **Airtable** để lưu trữ danh sách sản phẩm Best Seller thành file báo cáo mỗi ngày.
- **Cảnh báo qua Slack/Telegram:** Thêm nhánh điều kiện để nếu phát hiện sản phẩm có mức giảm giá sâu hoặc đánh giá đột biến, n8n sẽ bắn tin nhắn thông báo ngay về group chat cho đội ngũ Product/Sales.
- **Mở rộng danh mục:** Không chỉ hàng điện tử (Electronics), các sếp có thể thay đổi URL Bright Data để cào bất kỳ ngành hàng nào khác trên Amazon (Thời trang, Gia dụng, Sách...).

### 📌 Kết luận
Việc nghiên cứu sản phẩm bán chạy trên Amazon chưa bao giờ dễ dàng đến thế khi kết hợp sức mạnh cào dữ liệu thông minh và AI. Hãy triển khai ngay workflow này lên hệ thống n8n của các sếp để tối ưu hóa quy trình kinh nghiệm E-commerce ngay hôm nay!