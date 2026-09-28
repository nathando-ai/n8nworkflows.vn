---
title: "🚀 Tự động hóa ghi nhật ký giao dịch Interactive Brokers (IBKR) vào Google Sheets"
description: "Hướng dẫn xây dựng workflow n8n tự động lấy báo cáo giao dịch hàng ngày từ Interactive Brokers (IBKR), xử lý file XML và cập nhật trực tiếp vào Google Sheets."
slug: "tu-dong-hoa-nhat-ky-giao-dich-ibkr-google-sheets-n8n"
tags: [n8n, automation, trading, ibkr, google-sheets, finance]
keywords: [n8n workflow, IBKR trade journal, tự động hóa giao dịch, Interactive Brokers Google Sheets, n8n flex query]
---

# 🚀 Tự động hóa ghi nhật ký giao dịch Interactive Brokers (IBKR vào Google Sheets)

Các sếp làm trong lĩnh vực tài chính hoặc trader giao dịch trên **Interactive Brokers (IBKR)** chắc chắn hiểu rõ nỗi khổ: Việc ghi chép, tổng hợp nhật ký giao dịch (Trade Journal) hàng ngày bằng tay cực kỳ mất thời gian, dễ sai sót và tốn công sức đối chiếu. 

Giải pháp gì để tự động hóa 100% công đoạn này? Workflow n8n dưới đây sẽ tự động yêu cầu báo cáo Flex Report từ IBKR mỗi ngày, phân tích dữ liệu và đồng bộ thẳng vào Google Sheets mà không cần các sếp phải động tay vào bất kỳ dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Chạy định kỳ hàng ngày, không cần thao tác thủ công xuất file báo cáo từ sàn.
- **Dữ liệu thời gian thực & chính xác:** Các trường dữ liệu quan trọng như ngày giao dịch, mã cổ phiếu/crypto, khối lượng, giá, tỷ giá... được chuẩn hóa chính xác.
- **Chống trùng lặp thông minh:** Sử dụng `tradeID` làm khóa định danh giúp tự động cập nhật hoặc thêm mới dòng, không lo bị nhân đôi dữ liệu.
- **Tiết kiệm thời gian phân tích:** Tập trung vào chiến lược giao dịch thay vì tốn thời gian nhập liệu Excel.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản Interactive Brokers (IBKR):** Đã cấu hình Flex Query và lấy được Token/Query ID.
- **Tài khoản Google:** Đã chuẩn bị sẵn một Google Sheet để làm nhật ký giao dịch.
- **Hệ thống n8n:** Đã cài đặt sẵn sàng (Self-hosted hoặc n8n Cloud).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow (hoặc tải file từ nguồn cấp) và paste trực tiếp vào n8n Editor của mình. Workflow gồm 9 nodes chính hoạt động mượt mà theo dây chuyền.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống chạy trơn tru, các sếp cần cấu hình chính xác các node sau:

- **Daily Schedule Trigger:** Thiết lập mốc thời gian chạy workflow tự động mỗi ngày (mặc định là `08:00` sáng).
- **1. Request Flex Report & 3. Download Report (HTTP Request nodes):** 
  - Thêm hoặc xác thực thông tin token/tham số truy vấn Flex Query của IBKR.
  - Các sếp cần tạo Flex Query trên trang quản trị của IBKR để lấy `Query ID` và `Token`.
- **Wait 10 Seconds:** Node này đảm bảo hệ thống IBKR có đủ thời gian chuẩn bị và xuất file báo cáo XML. Các sếp có thể tăng thời gian chờ nếu dữ liệu lớn.
- **4. Convert XML to JSON:** Chuyển đổi toàn bộ báo cáo XML thô từ sàn thành định dạng JSON để n8n dễ dàng xử lý.
- **6. Format Trade Fields (Set node):** Chuẩn hóa các trường dữ liệu quan trọng trước khi ghi nhận như: `tradeDate`, `symbol`, `quantity`, `buySell`, `tradeID`, `price`, `money`, `currency`, `fxRateToBase`.
- **7. Save to Google Sheet (Google Sheets node):**
  - **Google Sheets OAuth2 API:** Kết nối tài khoản Google của các sếp.
  - **Google Sheet ID:** Thay thế `YOUR_GOOGLE_SHEET_ID` bằng ID thực tế của file Google Sheet nhật ký giao dịch.
  - **Operation:** Chọn `appendOrUpdate` và cấu hình cột đối chiếu (matching column) là `tradeID` để tránh trùng lặp dữ liệu khi chạy lại báo cáo.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** để test thủ công một lần, kiểm tra xem dữ liệu từ IBKR đã đổ vào Google Sheets chuẩn chỉnh chưa.
- Sau khi test thành công, bật công tắc **Active** ở góc trên cùng bên phải để workflow tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Nhận thông báo qua Telegram/Slack:** Thêm một node Telegram hoặc Slack ở cuối workflow để bắn tin nhắn báo cáo nhanh (Ví dụ: *"Đã đồng bộ thành công X giao dịch mới vào nhật ký hôm nay!"*).
- **Lưu log lỗi:** Kết nối nhánh lỗi (Error Trigger) để nếu tài khoản IBKR lỗi API hoặc Google Sheets quá tải, hệ thống sẽ gửi cảnh báo ngay cho các sếp.
- **Dashboard trực quan:** Kết nối Google Sheet vừa tạo với Google Looker Studio để vẽ biểu đồ PnL (Lợi nhuận/Thua lỗ) theo ngày/tuần/tháng cực kỳ chuyên nghiệp.

### 📌 Kết luận
Việc quản lý tài chính và giao dịch đòi hỏi sự chính xác tuyệt đối và dữ liệu phải luôn cập nhật. Với workflow n8n tích hợp giữa Interactive Brokers và Google Sheets này, các sếp đã tiết kiệm được hàng giờ đồng hồ nhập liệu thủ công mỗi tuần. Lên đồ và tự động hóa ngay thôi nào các sếp!