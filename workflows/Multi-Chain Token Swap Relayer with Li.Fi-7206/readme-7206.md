---
title: "🚀 Xây dựng Multi-Chain Token Swap Relayer tự động với Li.Fi và n8n"
description: "Hướng dẫn cấu hình workflow n8n tích hợp Li.Fi và 1Shot API giúp monetization các lệnh swap token ERC-20 sang native gas trên hơn 100 EVM blockchains."
slug: "multi-chain-token-swap-relayer-li-fi-n8n"
tags: [n8n, automation, crypto, li-fi, 1shot-api, web3, token-swap]
keywords: [n8n workflow, multi-chain swap, li.fi protocol, 1shot api, crypto automation, x402 payment]
---

# 🚀 Xây dựng Multi-Chain Token Swap Relayer tự động với Li.Fi và n8n

Các sếp trong lĩnh vực Web3 và Crypto thường gặp khó khăn khi muốn xây dựng hệ thống tự động hóa thu phí (monetization) hoặc hỗ trợ người dùng swap token ERC-20 sang native gas token trên nhiều mạng lưới blockchain khác nhau (EVM chains). Việc này đòi hỏi tích hợp phức tạp giữa các giao thức định tuyến (router), xử lý chữ ký và relay giao dịch.

Giải pháp ư? Workflow n8n **"Multi-Chain Token Swap Relayer with Li.Fi"** do *1Shot API* phát triển sẽ giúp các sếp tự động hóa toàn bộ quy trình này một cách mượt mà thông qua API, kết hợp giao thức thanh toán x402 và Li.Fi protocol.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow xử lý các giao dịch Web3 và chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Đa chuỗi (Multi-chain):** Hỗ trợ swap token sang native gas token trên hơn 100 EVM blockchains thông qua Li.Fi.
- **Tự động hóa thanh toán:** Tích hợp xác thực thanh toán x402 qua header `X-Payment` được mã hóa Base64 an toàn.
- **Mô phỏng & Thực thi thông minh:** Sử dụng 1Shot API để simulate giao dịch trước khi submit chính thức lên blockchain, hạn chế tối đa lỗi phí gas.
- **Phản hồi tức thì:** Webhook trả về kết quả 200 OK khi giao dịch thành công hoặc mã lỗi chi tiết khi có sự cố.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Self-hosted hoặc Cloud).
- **1Shot API Account:** Tài khoản 1Shot API và thông tin xác thực OAuth2 (`oneShotOAuth2Api`).
- **Li.Fi Protocol:** Endpoint hoặc cấu hình API liên quan đến Li.Fi (được tích hợp sẵn trong HTTP Request).
- **Cấu hình thanh toán:** Danh sách token hỗ trợ, Chain ID, Token Name, Version và Contract Method ID từ 1Shot Gas Station (`callDiamondWithEIP3009SignatureToNative`).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow từ nguồn cung cấp (hoặc copy toàn bộ JSON workflow).
- Trong giao diện n8n Editor, chọn **Add workflow** -> **Import from File** (hoặc dán trực tiếp JSON vào màn hình làm việc).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Để hệ thống hoạt động chính xác với cấu hình của các sếp, hãy chú ý các node quan trọng sau:

- **Webhook (`Webhook`):** 
  - Đường dẫn mặc định được thiết lập là `=gas-station` với phương thức `POST`. Các sếp có thể thay đổi đường dẫn phù hợp với hệ thống của mình.
- **Xác thực & Giải mã (`Decode & Validate X-Payment`, `Check for presence of X-HEADER`):** 
  - Kiểm tra sự tồn tại và tính hợp lệ của Header `x-payment` được gửi kèm trong request HTTP.
- **Cấu hình thanh toán (`Lookup Payment Configs`):** 
  - **CỰC KỲ QUAN TRỌNG:** Các sếp phải chỉnh sửa node Code này để khai báo chính xác các token muốn hỗ trợ swap, bao gồm:
    1. Địa chỉ token (Token Address)
    2. EVM Chain ID
    3. Tên token (`name`)
    4. Phiên bản token (`version`)
    5. Import phương thức `callDiamondWithEIP3009SignatureToNative` vào tài khoản business 1Shot API và cập nhật `contractMethodId`.
- **Lấy báo giá Li.Fi (`Fetch Li.Fi Quote`):** 
  - Node HTTP Request này gọi tới Li.Fi API để tìm route và quote tối ưu chuyển đổi token của người dùng sang native gas token.
- **Mô phỏng & Thực thi (`Simulate Payment`, `1Shot API Submit & Wait`):** 
  - Yêu cầu cấu hình credentials **1Shot OAuth2 API** (`oneShotOAuth2Api`) để thực hiện các thao tác simulate và submit giao dịch lên blockchain.

#### 3. Test & Kích hoạt ⚡️
- Sử dụng lệnh `curl` mẫu dưới đây để test thử endpoint Webhook (nhớ thay đổi URL webhook và payload x-payment tương ứng):
```sh
curl -X POST \
  https://your-n8n-instance.com/webhook/gas-station \
  -H "x-payment: YOUR-BASE64-ENCODED-PAYMENT-PAYLOAD" \
  -H "User-Agent: CustomUserAgent/1.0" \
  -H "Accept: application/json" \
  -H "Content-Type: application/json" \
  -d '{
    "fromChain": "43114",
    "fromToken": "0x9702230A8Ea53601f5cD2dc00fDBc13d4dF4A8c7",
    "fromAmount": "1000000",
    "fromAddress": "0x55680c6b69d598c0b42f93cd53dff3d20e069b5b",
    "toChain": "43114"
  }'
```
- Kiểm tra kết quả trả về (`Response: 200 - Payment Successful`).
- Bật công tắc **Active** để đưa workflow vào vận hành chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo Telegram/Slack:** Thêm node Telegram/Slack sau node `Response: 200 - Payment Successful` để nhận cảnh báo ngay lập tức khi có giao dịch swap/thanh toán thành công.
- **Lưu lịch sử giao dịch:** Kết nối thêm node Google Sheets hoặc cơ sở dữ liệu (PostgreSQL/Supabase) để lưu lại log chi tiết các request, ví dụ, địa chỉ ví, token nguồn và trạng thái giao dịch phục vụ việc tra cứu sau này.
- **Quản lý lỗi tự động:** Tinh chỉnh các nhánh `Respond to Webhook` lỗi để trả về thông báo chi tiết (như số dư không đủ, sai địa chỉ token) giúp client dễ dàng xử lý phía giao diện người dùng (UI).

### 📌 Kết luận
Workflow **Multi-Chain Token Swap Relayer with Li.Fi** là một công cụ cực kỳ mạnh mẽ giúp các nhà phát triển và dự án Web3 dễ dàng tích hợp tính năng swap token đa chuỗi và thu phí tự động mà không cần viết smart contract phức tạp từ đầu. Hãy áp dụng ngay vào hệ thống của các sếp để tối ưu hóa quy trình on-chain!