---
title: "🚀 Tự Động Hóa Tạo & Quản Lý Token ERC-20 Với Telegram Bot & 1Shot API (Không Cần Code)"
description: "Workflow này giúp các sếp tự động tạo ví EVM miễn phí cho người dùng, quản lý token ERC-20 và thực hiện giao dịch thông qua Telegram Bot. Giúp tiết kiệm thời gian, tăng trải nghiệm người dùng và mở rộng khả năng tự động hóa trong lĩnh vực crypto."
slug: "tieu-dong-hoa-tao-quan-ly-token-erc-20-telegram-bot-1shot-api"
tags: [n8n, automation, crypto, telegram-bot, 1shot-api, no-code, blockchain, erc-20]
keywords: [n8n workflow crypto, tự động hóa token ERC-20, Telegram bot quản lý ví, 1Shot API tự động hóa, tự động hóa giao dịch blockchain, tạo ví EVM không code]
---

# 🚀 Tự Động Hóa Tạo & Quản Lý Token ERC-20 Với Telegram Bot & 1Shot API

## 🔍 Giới Thiệu: Giải Pháp Tự Động Hóa Crypto Cho Doanh Nghiệp

Hiện nay, việc quản lý token ERC-20 và tạo ví EVM cho người dùng thủ công là một quá trình tốn thời gian, dễ sai sót và khó mở rộng. Các sếp thường phải:
- Tạo ví EVM thủ công cho từng người dùng.
- Quản lý danh sách token và giao dịch một cách rời rạc.
- Theo dõi trạng thái ví và giao dịch thông qua nhiều công cụ khác nhau.
- Cập nhật thông tin cho người dùng một cách không đồng bộ.

Workflow này **giải quyết tất cả những vấn đề trên bằng cách tự động hóa toàn bộ quy trình** thông qua một Telegram Bot kết nối với **1Shot API** và **n8n**. Các sếp chỉ cần cài đặt một lần và người dùng có thể:
✅ Tạo ví EVM miễn phí chỉ với một lệnh `/start`.
✅ Quản lý token ERC-20 một cách dễ dàng.
✅ Gửi và nhận token thông qua giao diện Telegram thân thiện.
✅ Theo dõi trạng thái ví và giao dịch 24/7.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động tạo ví và quản lý token cho hàng ngàn người dùng chỉ với một bot.
- **Trải nghiệm người dùng cao**: Người dùng có thể tương tác với ví của mình qua Telegram, không cần kiến thức kỹ thuật.
- **An toàn và minh bạch**: Sử dụng **1Shot API** (cơ sở trên MetaMask Smart Wallets) để quản lý ví không cần bảo mật mật khẩu.
- **Hoạt động liên tục**: Workflow chạy 24/7 trên VPS, không phụ thuộc vào thời gian làm việc của nhân viên.
- **Mở rộng dễ dàng**: Thêm chức năng mới như giao dịch tự động, cảnh báo giá token, hoặc tích hợp với các dịch vụ khác (Slack, Email, CRM).
:::

---

## 🔧 Yêu cầu cần thiết

Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Telegram Bot**:
   - Tạo bot thông qua [BotFather](https://t.me/BotFather) và lấy **API Token**.
   - **Không cho phép sử dụng trong nhóm** (do chat ID trong nhóm có thể thay đổi).

2. **Tài khoản 1Shot API**:
   - Đăng ký tại [1Shot API](https://1shotapi.com) và lấy **API Key & Secret**.
   - Cài đặt **Token Factory** của 1Shot API để tạo token ERC-20. Các sếp có thể [clone repo](https://github.com/1Shot-API/1Shot-Token-Factory) và tùy chỉnh smart contract.

3. **Bảng dữ liệu (Data Tables)**:
   - **User Table**: Các cột cần thiết là `chatid`, `wallet`, và `walletid`.
   - **Token Table**: Các cột cần thiết là `wallet`, `token`, `name`, và `chatid`.

4. **N8n Workflow**:
   - Cài đặt n8n trên VPS hoặc sử dụng phiên bản cloud (nếu không muốn tự host).

---

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Truy cập [n8n Editor](https://n8n.io/editor).
2. Nhấp vào **Import** và chọn file JSON đã tải xuống từ [link gốc](https://n8n.io/workflows/11264).
   *Hoặc* copy toàn bộ JSON từ [đây](https://n8n.io/workflows/11264) và dán vào **Import from JSON** trong Editor.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

#### **A. Cấu hình Telegram Bot**
- **Node "Telegram Trigger"**:
  - Điền **API Token** từ BotFather vào `telegramApi` credentials.
  - Chọn **Chat Type**: `Private` (do không cho phép sử dụng trong nhóm).
  - Đặt **Trigger**: `/start` (hoặc tùy chỉnh theo nhu cầu).

- **Node "Send Action Keyboard Options"**:
  - Cấu hình **Inline Keyboard** để người dùng có thể chọn các tùy chọn như:
    - "Tạo Token Mới"
    - "Xem Token Của Tôi"
    - "Gửi Token"
    - "Kiểm Tra Ví"

#### **B. Cấu hình 1Shot API**
- **Node "Create a User Wallet"**:
  - Điền **API Key & Secret** vào `oneShotOAuth2Api` credentials.
  - Chọn **Resource**: `wallets` và **Operation**: `create`.

- **Node "Deploy User Token"**:
  - Đảm bảo **Token Factory** đã được cài đặt trong tài khoản 1Shot API.
  - Đặt **Method**: `deployToken` (đối với tạo token mới).

- **Node "Send Token"**:
  - Đặt **Method**: `mint` (đối với gửi token).

#### **C. Cấu hình Data Tables**
- **Node "Check for Existing User"**:
  - Kết nối với **User Table** và chọn `chatid` làm key để kiểm tra người dùng đã tồn tại hay chưa.

- **Node "Record User Wallet"**:
  - Thêm dữ liệu mới vào **User Table** với các cột: `chatid`, `wallet`, và `walletid`.

- **Node "Record New Token"**:
  - Thêm dữ liệu mới vào **Token Table** với các cột: `wallet`, `token`, `name`, và `chatid`.

#### **D. Cấu hình Telegram Message**
- **Node "Get the name of the token"**, **"Get the token Symbol"**, **"Max Supply"**:
  - Sử dụng `operation: "sendAndWait"` để yêu cầu người dùng nhập thông tin qua Telegram.
  - Ví dụ: Bot sẽ gửi tin nhắn `"Nhập tên token:"` và chờ người dùng trả lời.

- **Node "Reply with TX Hash"**:
  - Sau khi giao dịch thành công, bot sẽ trả về **hash giao dịch** cho người dùng.

---

### 3. Kích hoạt ⚡️
1. **Test Run**:
   - Chạy workflow với dữ liệu mẫu để kiểm tra các bước:
     - Tạo ví mới.
     - Tạo token mới.
     - Gửi token.
   - Đảm bảo tất cả các node hoạt động như mong đợi.

2. **Bật Active**:
   - Sau khi kiểm tra xong, chuyển workflow sang **Active**.

---

## ✍️ Mẹo & gợi ý nâng cao

### 1. Tích hợp với Slack/Telegram Group (Nếu cần)
- Sử dụng **node Telegram** để gửi thông báo về **Slack** hoặc **Telegram Group** khi có sự kiện quan trọng (ví dụ: giao dịch thành công, token mới được tạo).
- Cài đặt **Slack Webhook** hoặc **Telegram Bot** mới để gửi thông báo.

### 2. Lưu Log Giao Dịch
- Thêm **node "Set"** hoặc **node "Sticky Note"** để lưu log giao dịch vào một bảng dữ liệu riêng.
- Ví dụ: Bảng `Transaction Log` với các cột: `wallet`, `token`, `amount`, `txHash`, `status`.

### 3. Gửi Báo Cáo Định Kỳ
- Sử dụng **node "Schedule"** để gửi báo cáo tuần/Tháng về:
  - Số lượng ví được tạo.
  - Tổng giá trị token được gửi.
  - Số lượng giao dịch thành công/thất bại.

### 4. Cập Nhật Token Tự Động
- Thêm chức năng **cập nhật max supply** hoặc **chỉnh sửa thông tin token** thông qua Telegram Bot.

### 5. Tích Hợp với CRM
- Gửi thông tin ví và giao dịch vào **CRM** (ví dụ: HubSpot, Zoho) để theo dõi hành vi người dùng.

---

## 📌 Kết luận

Workflow này là **giải pháp hoàn hảo** cho các sếp muốn tự động hóa quản lý token ERC-20 và tạo ví EVM một cách dễ dàng, không cần code. Với **Telegram Bot** và **1Shot API**, các sếp có thể:
✔ Tạo ví cho người dùng chỉ với một lệnh `/start`.
✔ Quản lý token và giao dịch một cách tự động.
✔ Tăng trải nghiệm người dùng và tiết kiệm thời gian.

**Hãy áp dụng ngay workflow này và nâng cao hiệu suất quản lý crypto của doanh nghiệp!** 🚀

---
### 🔗 Tài liệu tham khảo
- [1Shot API - Token Factory](https://github.com/1Shot-API/1Shot-Token-Factory)
- [Tutorial YouTube](https://youtu.be/bKRvt2DuVKA)
- [n8n Workflow Gốc](https://n8n.io/workflows/11264)