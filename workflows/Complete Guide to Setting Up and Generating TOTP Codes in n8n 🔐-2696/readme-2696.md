---
title: "🚀 Hướng Dẫn Đầy Đủ Cài Đặt & Tạo Mã TOTP trong n8n 🔐"
description: "Tự động sinh mã OTP (TOTP) trong n8n chỉ với 2 node, không cần viết code, giúp bảo mật tài khoản và tích hợp 2FA vào workflow."
slug: "huong-dan-cai-dat-va-tao-ma-totp-trong-n8n"
tags: [n8n, automation, no-code, security, two-factor-authentication]
keywords: [n8n workflow, tự động hóa, TOTP, mã xác thực, two-factor authentication]
---

# 🚀 Hướng Dẫn Đầy Đủ Cài Đặt & Tạo Mã TOTP trong n8n 🔐

Bạn có bao giờ phải gõ mã OTP (One‑Time Password) mỗi khi đăng nhập vào các dịch vụ quan trọng?  
Việc này không chỉ tốn thời gian mà còn dễ gây lỗi khi nhập sai, đặc biệt khi phải làm việc trên nhiều tài khoản cùng lúc.  

**Workflow này** sẽ giải quyết hoàn toàn vấn đề đó: chỉ với **2 node** trong n8n, bạn có thể **tự động sinh mã TOTP** (Time‑Based One‑Time Password) và đưa chúng vào bất kỳ quy trình nào – không cần viết một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không còn phải mở app OTP mỗi lần, mã được sinh tự động.
- **Độ chính xác 100 %**: Mã luôn đúng thời gian, giảm rủi ro nhập sai.
- **Tích hợp liền mạch**: Dùng mã TOTP trong các workflow khác (email, Slack, API…) mà không cần can thiệp thủ công.
- **Hoạt động liên tục 24/7**: Khi n8n chạy trên VPS, mã luôn sẵn sàng cho mọi yêu cầu.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n** (self‑hosted hoặc cloud) với quyền tạo workflow.  
- **Credential “totpApi”**: chứa **Secret Key** (được cung cấp khi bạn bật 2FA trên dịch vụ mục tiêu).  
- **Node “Manual Trigger”** để khởi chạy thử nghiệm (có sẵn trong workflow).  
- Không cần bất kỳ dịch vụ bên ngoài nào khác.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập link gốc: <https://n8n.io/workflows/2696>.  
2. Nhấn **“Export” → “Download JSON”** để lưu file `totp-workflow.json`.  
3. Trong n8n Editor, chọn **“Import” → “From File”**, tải lên file vừa tải về.  
4. Hoặc **copy toàn bộ JSON** và dán vào **“Import → From Clipboard”**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Mô tả | Cấu hình cần chỉnh |
|------|------|-------------------|
| **When clicking ‘Test workflow’** (Manual Trigger) | Dùng để kích hoạt workflow thủ công, giúp bạn kiểm tra mã TOTP ngay lập tức. | Không cần thay đổi, chỉ nhấn **“Execute Workflow”** khi muốn test. |
| **TOTP** | Node sinh mã OTP dựa trên chuẩn RFC 6238. | - **Credentials**: chọn `totpApi` (hoặc tạo mới).<br>- **Secret**: dán **Secret Key** của dịch vụ (ví dụ: `JBSWY3DPEHPK3PXP`).<br>- **Algorithm**: mặc định `SHA1` (có thể để mặc định).<br>- **Digits**: `6` (hoặc `8` tùy dịch vụ).<br>- **Period**: `30` giây (mặc định). |
| **Output** | Node sẽ trả về trường `code` chứa mã OTP hiện tại. | Bạn có thể dùng `{{ $json["code"] }}` trong các node tiếp theo (email, Slack, HTTP Request…). |

> **Lưu ý:** Nếu secret key có ký tự đặc biệt, hãy chắc chắn không có khoảng trắng thừa khi dán vào trường Secret.

#### 3. Kích hoạt ⚡️
1. **Test run**: Nhấn **“Execute Workflow”** trên node Manual Trigger, kiểm tra giá trị `code` trong phần Output.  
2. Nếu mã đúng, **bật “Active”** (nút chuyển đổi ở góc trên bên phải) để workflow luôn sẵn sàng khi được gọi từ các workflow khác hoặc webhook.  

### ✍️ Mẹo & gợi ý nâng cao
- **Kết hợp Slack/Telegram**: Thêm một node Slack hoặc Telegram ngay sau node TOTP để gửi mã OTP trực tiếp tới thiết bị di động của bạn.  
- **Lưu log**: Dùng node “Write Binary File” hoặc “Google Sheets” để ghi lại mỗi lần sinh mã, tiện cho audit hoặc debug.  
- **Trigger tự động**: Thay Manual Trigger bằng **Cron** (ví dụ: mỗi 30 giây) để tự động sinh và gửi mã tới email/điện thoại.  
- **Bảo mật**: Đặt credential `totpApi` ở mức **“Read‑Only”** và chỉ chia sẻ quyền truy cập cho các workflow thực sự cần.

### 📌 Kết luận
Với chỉ **2 node** đơn giản, các sếp đã có thể **tự động sinh mã TOTP** cho mọi dịch vụ hỗ trợ 2FA, giảm thiểu lỗi nhập và tăng tốc độ làm việc. Hãy import ngay workflow này, cấu hình secret key, và bắt đầu tích hợp vào các quy trình tự động của mình – bảo mật và hiệu quả trong tầm tay! 🚀