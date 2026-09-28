---
title: "🚀 Tự Động Hóa X402 Payment Processor Blockchain Với 1Shot API (Không Cần Code)"
description: "Workflow này giúp các sếp xây dựng một hệ thống thanh toán blockchain tự động hóa 100% trên nền tảng n8n, hỗ trợ xác thực và thanh toán giao dịch trên chuỗi (verify/settle) với API 1Shot. Giảm thiểu thời gian phát triển từ tháng thành giờ, tối ưu chi phí và tăng tính chính xác cho giao dịch crypto."
slug: "tieu-dong-hoa-x402-payment-processor-blockchain"
tags: [n8n, blockchain, crypto-trading, 1shot-api, tự động hóa thanh toán, no-code]
keywords: [n8n workflow blockchain, tự động hóa thanh toán crypto, x402 payment processor, 1shot api n8n, thanh toán blockchain tự động]
---

# 🚀 **Xây Dựng Hệ Thống Thanh Toán Blockchain Tự Động Hóa Với X402 & 1Shot API**

## **Nỗi Đau Của Các Sếp Trong Thanh Toán Blockchain**
Hiện nay, việc xây dựng một **hệ thống thanh toán blockchain** đòi hỏi kiến thức sâu về smart contract, API integration và quản lý giao dịch 24/7. Các sếp phải:
- **Tốn thời gian** để phát triển và kiểm tra logic xác thực (`verify`) và thanh toán (`settle`).
- **Lo ngại lỗi giao dịch** do thiếu cơ chế tự động hóa, dẫn đến mất mát tài sản.
- **Phải quản lý nhiều API keys** và cấu hình phức tạp cho từng mạng blockchain.
- **Không có giải pháp no-code** để tích hợp thanh toán blockchain một cách dễ dàng.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tự động hóa toàn bộ quy trình** từ xác thực (`/verify`) đến thanh toán (`/settle`) trên blockchain.
✅ **Hỗ trợ nhiều mạng** (Ethereum, Base Sepolia, Polygon,...) chỉ với một cấu hình.
✅ **Kiểm tra và trả lỗi chi tiết** khi giao dịch không hợp lệ.
✅ **Không cần viết code** – chỉ cần cấu hình và chạy!

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian phát triển** so với viết từ đầu bằng Solidity.
- **Tăng tính chính xác** với logic xác thực tự động (`verify`) trước khi thanh toán.
- **Hỗ trợ nhiều mạng blockchain** (Ethereum, Base, Polygon,...) chỉ với một API.
- **Giao dịch 24/7** mà không cần can thiệp thủ công.
- **Giảm rủi ro lỗi giao dịch** nhờ kiểm tra payload trước khi submit.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản 1Shot API** (đăng ký tại [1Shot API](https://1shotapi.dev/)) và **API Key/Secret/Business ID**.
2. **N8n Self-Hosted** (không dùng phiên bản cloud để đảm bảo bảo mật).
3. **Danh sách token hỗ trợ** (cấu hình trong node `Lookup Payment Configs`).
4. **Danh sách mạng blockchain hỗ trợ** (cấu hình trong node `Supported Networks Config`).
5. **Môi trường phát triển** (Postman/curl để test API).
:::

---

## 🚀 **Cách Import & Cấu Hình Workflow**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/7364](https://n8n.io/workflows/7364) hoặc copy toàn bộ JSON dưới đây vào **n8n Editor**.
- **Nhấn "Import"** và chọn **Self-Hosted n8n** làm môi trường.

```json
// (Dữ liệu JSON đầy đủ sẽ được cung cấp sau khi import từ link trên)
```

### **2. Các Bước Cấu Hình BẮT BUỘC**
Workflow gồm **20 node** với các chức năng chính sau. Các sếp **phải chỉnh** các phần sau:

#### **A. Cấu Hình Credentials 1Shot API**
- Mở node **`Simulate Payment`** hoặc **`1Shot API Submit & Wait`**.
- Nhấn **`Credential to connect with`** → Chọn **`oneShotOAuth2Api`** (nếu chưa có, tạo mới).
- Điền:
  - **API Key** (từ tài khoản 1Shot API).
  - **Secret** (từ tài khoản 1Shot API).
  - **Business ID** (từ tài khoản 1Shot API).

#### **B. Cấu Hình Token Hỗ Trợ (Lookup Payment Configs)**
- Mở node **`Lookup Payment Configs`** (node **Code**).
- Sửa phần `config` để thêm **token và smart contract** bạn muốn hỗ trợ:
  ```javascript
  const config = {
    tokens: {
      "USDC": {
        contract: "0x036CbD53842c5426634e7929541eC2318f3dCF7e", // Ví dụ USDC trên Base Sepolia
        decimals: 6,
        symbol: "USDC"
      },
      "ETH": {
        contract: "0x0000000000000000000000000000000000000000", // Ví dụ ETH
        decimals: 18,
        symbol: "ETH"
      }
    }
  };
  return { json: config };
  ```

#### **C. Cấu Hình Mạng Blockchain Hỗ Trợ (Supported Networks Config)**
- Mở node **`Supported Networks Config`** (node **Code**).
- Sửa phần `networks` để thêm **mạng blockchain** bạn muốn hỗ trợ:
  ```javascript
  const networks = [
    { scheme: "ethereum", network: "base-sepolia" },
    { scheme: "polygon", network: "mumbai" },
    { scheme: "arbitrum", network: "goerli" }
  ];
  return { json: { kinds: networks } };
  ```

#### **D. Test Webhook Endpoints**
Workflow có **3 endpoint chính**:
1. **`/verify`** → Xác thực giao dịch trước khi thanh toán.
2. **`/settle`** → Thực hiện thanh toán trên blockchain.
3. **`/supported`** → Trả về danh sách mạng blockchain hỗ trợ.

**Test với curl (ví dụ):**
```bash
# Test endpoint /verify
curl -X POST \
  http://[your-n8n-domain]/webhook/verify \
  -H "Content-Type: application/json" \
  -d '{
    "x402Version": 1,
    "paymentHeader": "eyJ4NDAyVmVyc2lvbiI6IjEiLCJzY2hlbWUiOiJleGFjdCIsIm5ldHdvcmsiOiJiYXNlLXNlcG9saWEiLCJwYXlsb2FkIjp7ImF1dGhvcml6YXRpb24iOnsiZnJvbSI6IjB4NTU2ODBDNkI2OUQ1OThDMEI0MkY5M0NENTNERkYzRDIwZTA2OWI1YiIsInRvIjoiMHg5ZkVhZDhCMTlDMDQ0QzJmNDA0ZGFjMzhCOTI1RWExNkFEYWEyOTU0IiwidmFsdWUiOiIxMDAwMDAiLCJ2YWxpZEFmdGVyIjoiMTc1NTEzMjk4NCIsInZhbGlkQmVmb3JlIjoiMTc1NTEzMzE2NCIsIm5vbmNlIjoiMHgxNjRjZjNjMDFlMzgwOTk4MTdmYzNkM2I5YTlkYjYzZGNiYTFjNWMwZDExOGU4ZThhNjIwODAwNmQ5M2U1ODYyIn0sInNpZ25hdHVyZSI6IjB4YjdlNzMxMjViY2QxNDU2MTJlZThkZWY1MDQ1M2I3YzhmMWY1NjQzZmYzZDRlMjcxMWVkNTdiNGRhNjY3NDRhMjdmM2Q1YWRmY2EyMDA4MDI4M2YxODVmODQ0YWJiYWI0YjczYWM2N2JjZDU0NmJiM2ViZDc3M2RlYzczODFlNGUxYyJ9fQ==",
    "paymentRequirements": {
      "scheme": "exact",
      "network": "base-sepolia",
      "maxAmountRequired": "5000000",
      "resource": "https://n8n.1shotapi.dev/webhook/gas-station",
      "description": "Swap stablecoins for gas tokens",
      "mimeType": "",
      "payTo": "0x9fEad8B19C044C2f404dac38B925Ea16ADaa2954",
      "maxTimeoutSeconds": 150,
      "asset": "0x036CbD53842c5426634e7929541eC2318f3dCF7e",
      "extra": {
        "name": "USD Coin",
        "version": "version"
      }
    }
  }'
```

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết nối với Slack/Telegram** để thông báo kết quả giao dịch:
   - Sử dụng node **`n8n-nodes-slack`** hoặc **`n8n-nodes-telegram`** sau node **`Settlement Response`** để gửi thông báo khi thanh toán thành công/thất bại.
2. **Lưu log giao dịch** vào Google Sheets/Notion:
   - Thêm node **`n8n-nodes-google-sheets`** sau node **`Verify Response`** để ghi lại lịch sử giao dịch.
3. **Tự động gửi báo cáo định kỳ** (hàng ngày/tuần):
   - Sử dụng node **`n8n-nodes-email`** hoặc **`n8n-nodes-slack`** để gửi tổng hợp giao dịch.
4. **Cấu hình rate limiting** để tránh bị blacklist:
   - Thêm node **`n8n-nodes-base.set`** trước webhook để kiểm soát số lượng request.

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa thanh toán blockchain **không cần viết code**. Bằng cách cấu hình đơn giản, các sếp có thể:
✔ **Xác thực và thanh toán giao dịch** một cách tự động.
✔ **Hỗ trợ nhiều mạng blockchain** với một cấu hình.
✔ **Giảm thời gian phát triển** từ tháng thành giờ.

**🚀 Hãy áp dụng ngay và bắt đầu tự động hóa thanh toán blockchain của bạn!**

---
:::note[LƯU Ý CUỐI CUNG]
- **Không dùng phiên bản n8n cloud** để đảm bảo bảo mật API keys.
- **Test kỹ với dữ liệu mẫu** trước khi deploy sản xuất.
- **Cập nhật token và mạng blockchain** khi có thay đổi.
:::

---
**🔗 [Tải workflow từ n8n.io](https://n8n.io/workflows/7364)**
**📌 [Hướng dẫn cài n8n Self-Hosted](https://docs.n8n.io/hosting/installation/)**