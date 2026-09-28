---
title: "🚀 Tự động giám sát số dư ví USDT ERC-20 và cảnh báo qua Telegram với n8n"
description: "Hướng dẫn cài đặt workflow n8n tự động kiểm tra số dư ví USDT ERC-20 qua Etherscan mỗi 5 phút và gửi thông báo biến động ngay lập tức qua Telegram."
slug: "giam-sat-so-du-usdt-erc-20-telegram-n8n"
tags: [n8n, automation, crypto, usdt, telegram, blockchain, etherscan]
keywords: [n8n workflow, giám sát ví usdt, check số dư ví erc20, cảnh báo telegram, tự động hóa crypto, etherscan api]
keywords: [n8n workflow, giam sat vi usdt, check so du vi erc20, canh bao telegram, tu dong hoa crypto, etherscan api]
---

# 🚀 Tự động giám sát số dư ví USDT ERC-20 và cảnh báo qua Telegram

Các sếp đang quản lý các quỹ crypto, tài sản số hay đơn giản là muốn theo dõi sát sao một địa chỉ ví USDT trên mạng Ethereum? Việc cứ phải vào Etherscan hay các ví điện tử để F5 kiểm tra số dư thủ công vừa mất thời gian, vừa dễ bỏ lỡ những biến động quan trọng (như tiền về hoặc tiền bị rút đi). 

Giải pháp là đây! Workflow n8n siêu gọn nhẹ này sẽ tự động hóa hoàn toàn việc kiểm tra số dư ví USDT ERC-20 định kỳ và hú còi cảnh báo qua Telegram ngay khi phát hiện sự thay đổi, giúp các sếp nắm quyền kiểm soát tài sản 24/7 mà không tốn một giọt mồ hôi.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Theo dõi tự động 24/7:** Không cần canh, hệ thống tự động kiểm tra số dư ví định kỳ (mặc định cứ 5 phút/lần).
- **Cảnh báo tức thì:** Nhận thông báo trực tiếp qua Telegram ngay lập tức khi số dư thay đổi (tăng hoặc giảm).
- **Bảo mật & Chủ động:** Sử dụng Etherscan API chính chủ, chạy trên n8n tự host hoàn toàn bảo mật thông tin ví.
- **Tùy biến linh hoạt:** Dễ dàng thay đổi địa chỉ ví, mốc thời gian kiểm tra hoặc thêm các điều kiện lọc số tiền giao dịch.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Một hệ thống n8n đang hoạt động (Self-hosted hoặc n8n Cloud).
- **Etherscan API Key:** Đăng ký tài khoản miễn phí trên [Etherscan](https://etherscan.io/) để lấy API Key gọi dữ liệu.
- **Telegram Bot Token:** Tạo một Bot thông qua `@BotFather` trên Telegram và lấy Token, đồng thời lấy Chat ID của sếp hoặc nhóm chat.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy đoạn JSON của workflow (hoặc tải từ kho lưu trữ n8n với ID `3330`) và paste trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này bao gồm 7 nodes chính được cấu hình mạch lạc. Các sếp cần tinh chỉnh các điểm sau:

- **`Check Balance Every 5 Minutes` (Node Cron):** Định thời gian chạy tự động. Mặc định là 5 phút/lần. Các sếp có thể đổi thành 1 phút hoặc 1 giờ tùy nhu cầu.
- **`userData` (Node Set):** Nơi khai báo thông tin cơ bản. Các sếp cần vào đây điền:
  - Địa chỉ ví Ethereum (ERC-20 Wallet Address) cần giám sát.
  - Etherscan API Key của các sếp.
- **`Fetch USDT Balance from Etherscan` (Node HTTP Request):** Node này sẽ gọi API của Etherscan để truy vấn số lượng token USDT (hợp đồng thông minh USDT ERC-20 chuẩn) tại địa chỉ ví đã cấu hình.
- **`balanceChecker` (Node Code):** Xử lý logic so sánh số dư mới lấy về với số dư cũ được lưu trong bộ nhớ tạm/lần chạy trước.
- **`Balance Changed?` (Node IF):** Bộ lọc rẽ nhánh. Nếu số dư thay đổi (`true`), workflow sẽ kích hoạt nhánh gửi tin nhắn báo động; nếu không đổi (`false`), workflow sẽ đi theo nhánh còn lại.
- **`Balance Changed.` & `Balance Not Changed.` (Node Telegram):** Kết nối với tài khoản Telegram của các sếp. Cần tạo Credentials loại `telegramApi` và dán Bot Token vào đây, sau đó cấu hình Chat ID để nhận tin nhắn.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Execute Workflow** để test thử lần đầu (nhớ cấu hình đúng ví và API key trước nhé).
- Kiểm tra xem Telegram đã nhận được tin nhắn báo cáo chưa.
- Nếu mọi thứ mượt mà, gạt công tắc sang **Active** để workflow tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Thay vì chỉ gửi Telegram cá nhân, các sếp có thể nhân bản node Telegram để bắn tin nhắn vào Group chat nội bộ công ty hoặc tích hợp thêm Slack.
- **Lưu lịch sử biến động:** Kết nối thêm node Google Sheets hoặc Airtable ngay sau nhánh `Balance Changed.` để ghi lại lịch sử mỗi khi ví có biến động số dư phục vụ việc đối soát sau này.
- **Cảnh báo ngưỡng (Threshold):** Tinh chỉnh node Code để chỉ bắn tin nhắn khi số tiền biến động vượt quá một mức nhất định (ví dụ > $1000), tránh bị spam bởi các giao dịch nhỏ lẻ.

### 📌 Kết luận
Việc giám sát tài sản crypto chưa bao giờ dễ dàng đến thế với sức mạnh của n8n. Chỉ với vài phút thiết lập, các sếp đã có ngay một "quản gia" blockchain túc trực 24/7, bảo vệ tài sản và thông báo mọi biến động tài chính ngay trên chiếc điện thoại của mình. Triển khai ngay thôi các sếp ơi!