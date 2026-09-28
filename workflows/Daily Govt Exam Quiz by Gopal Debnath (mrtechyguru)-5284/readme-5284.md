---
title: "📚 **Tự Động Hóa Bài Thi Hàng Ngày Cho Sinh Viên - Từ Google Sheets Đến Email, Telegram & SMS (Không Cần Code!)**"
description: "Workflow tự động hóa gửi bài thi hàng ngày từ Google Sheets đến sinh viên qua Email, Telegram và SMS, tiết kiệm thời gian cho giáo viên và đảm bảo thông tin chính xác. Đáp ứng nhu cầu học tập 24/7 cho sinh viên."
slug: "tieu-dong-hoa-bai-thi-hang-ngay-cho-sinh-vien"
tags: [n8n, automation, no-code, ai, google-sheets, telegram, email, twilio, cron-job]
keywords: [n8n workflow tự động hóa bài thi, gửi bài thi qua email telegram sms, tự động hóa giáo dục, cron job n8n, google sheets n8n]
---

# 🚀 **Tự Động Hóa Bài Thi Hàng Ngày Cho Sinh Viên - Từ Google Sheets Đến Email, Telegram & SMS**

Hãy tưởng tượng một ngày bạn là giáo viên, phải viết bài thi hàng ngày, sao chép vào Google Sheets, sau đó gửi cho từng sinh viên qua Email, Telegram và SMS. **Thời gian bị lãng phí, dễ xảy ra lỗi nhân sự, và sinh viên không nhận được thông tin kịp thời!**

Workflow này **giải quyết tất cả những vấn đề trên** bằng cách tự động hóa **tất cả quy trình** chỉ với một lần cấu hình. Bằng cách kết nối **Google Sheets** (nơi bạn lưu trữ bài thi), **n8n** sẽ:
✅ **Lấy bài thi tự động** từ Google Sheets mỗi ngày (hoặc theo lịch bạn đặt).
✅ **Chuyển đổi và định dạng** bài thi thành dạng phù hợp.
✅ **Gửi bài thi đến sinh viên** qua **Email, Telegram và SMS** (thông qua Twilio).
✅ **Hoạt động 24/7** mà không cần bạn can thiệp.

Không cần viết một dòng code nào, chỉ cần **cài đặt và chạy** là xong!

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm thời gian**: Không cần sao chép bài thi vào từng kênh thông tin.
- **Chính xác 100%**: Tránh sai sót khi gửi thông tin qua nhiều kênh.
- **Tương tác đa kênh**: Sinh viên nhận được bài thi qua **Email, Telegram và SMS** (tùy chọn).
- **Hoạt động tự động**: Bài thi được gửi **mỗi ngày** (hoặc theo lịch bạn thiết lập) mà không cần can thiệp.
- **Dễ dàng mở rộng**: Thêm sinh viên, thay đổi nội dung bài thi chỉ cần chỉnh sửa trên Google Sheets.
:::

---

### 🔧 **Yêu cầu cần thiết**
:::info[**CHUẨN BỊ**]
Để workflow này hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Google Sheets** (để lưu trữ bài thi hàng ngày).
2. **Tài khoản Email** (để gửi bài thi qua Email, cần **SMTP credentials**).
3. **Tài khoản Telegram** (để gửi bài thi qua Telegram, cần **Telegram Bot Token**).
4. **Tài khoản Twilio** (để gửi SMS, cần **Twilio Account SID và Auth Token**).
5. **Tài khoản n8n Self-hosted** (để chạy workflow 24/7).

**Lưu ý**:
- **Google Sheets**: Bạn cần tạo một **Sheet** có cấu trúc phù hợp (các cột như `Sinh viên`, `Email`, `Số điện thoại`, `Nội dung bài thi`).
- **Twilio**: Đăng ký tài khoản [Twilio](https://www.twilio.com/) và lấy **Account SID** và **Auth Token**.
- **Telegram Bot**: Tạo một bot Telegram và lấy **Token** từ [@BotFather](https://t.me/BotFather).
- **SMTP**: Nếu gửi Email qua Gmail, cần **App Password** (nếu sử dụng 2FA).

---
:::info[**Gợi ý hạ tầng cho n8n**]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Bước 1: Tải workflow từ [đây](https://n8n.io/workflows/5284) (hoặc copy JSON từ link trên).
Bước 2: Mở **n8n Editor** và nhấn **Import** → Dán JSON vào và nhấn **Import**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này có **6 node chính**, các sếp cần cấu hình như sau:

##### **🔹 Node 1: Daily Trigger (n8n-nodes-base.cron)**
- **Cấu hình**:
  - **Schedule**: Chọn thời gian gửi bài thi (ví dụ: `0 8 * * *` để gửi lúc 8h sáng hàng ngày).
  - **Time Zone**: Chọn múi giờ phù hợp (ví dụ: `Asia/Ho_Chi_Minh`).
  - **Active**: Bật để kích hoạt lịch trình.

##### **🔹 Node 2: Fetch Question (n8n-nodes-base.googleSheets)**
- **Cấu hình**:
  - **Credentials**: Chọn `googleApi` (đã cấu hình trước).
  - **Operation**: Chọn `Get rows`.
  - **Sheet Name**: Nhập tên Sheet chứa bài thi (ví dụ: `BaiThiHangNgay`).
  - **Range**: Nhập phạm vi dữ liệu (ví dụ: `Sheet1!A1:D100`).
  - **Output**: Chọn `json` để lấy dữ liệu dưới dạng JSON.

##### **🔹 Node 3: Format Quiz (n8n-nodes-base.function)**
- **Cấu hình**:
  - **JavaScript Code**: Sử dụng mã sau để định dạng bài thi:
    ```javascript
    return {
      json: {
        email: item.email,
        telegram: item.telegram,
        sms: item.sms,
        content: `Bài thi ngày ${new Date().toLocaleDateString()}:\n\n${item.content}`
      }
    };
    ```
  - **Lưu ý**:
    - `item.email`, `item.telegram`, `item.sms` là các cột trong Google Sheets chứa thông tin liên lạc của sinh viên.
    - `item.content` là nội dung bài thi.

##### **🔹 Node 4: Send Email (n8n-nodes-base.emailSend)**
- **Cấu hình**:
  - **Credentials**: Chọn `smtp` (đã cấu hình trước).
  - **From**: Nhập Email gửi (ví dụ: `giaovien@trungtam.edu.vn`).
  - **To**: Sử dụng `{{$json.email}}` để lấy Email từ dữ liệu.
  - **Subject**: Nhập tiêu đề Email (ví dụ: `Bài thi ngày {{ $node["Fetch Question"].json[0].date }}`).
  - **Body**: Nhập nội dung Email (ví dụ: `{{$json.content}}`).

##### **🔹 Node 5: Send to Telegram (n8n-nodes-base.telegram)**
- **Cấu hình**:
  - **Credentials**: Chọn `telegramApi` (đã cấu hình trước).
  - **Chat ID**: Sử dụng `{{$json.telegram}}` để lấy ID Chat của sinh viên.
  - **Text**: Nhập nội dung bài thi (ví dụ: `{{$json.content}}`).

##### **🔹 Node 6: Send via Twilio (n8n-nodes-base.twilio)**
- **Cấu hình**:
  - **Credentials**: Chọn `twilioApi` (đã cấu hình trước).
  - **To**: Sử dụng `{{$json.sms}}` để lấy số điện thoại của sinh viên.
  - **From**: Nhập số Twilio của bạn (ví dụ: `+1234567890`).
  - **Body**: Nhập nội dung SMS (ví dụ: `Bài thi ngày {{ $node["Fetch Question"].json[0].date }}: {{$json.content}}`).

#### **3. Kích hoạt ⚡️**
- **Test Run**: Nhấn **Run Once** để kiểm tra workflow với dữ liệu mẫu.
- **Active Workflow**: Sau khi kiểm tra thành công, nhấn **Active** để bật workflow.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Thêm Logs**: Sử dụng **n8n-nodes-base.set** để lưu lịch sử gửi bài thi vào Google Sheets hoặc một bảng dữ liệu khác.
2. **Gửi Báo Cáo**: Thêm một node **n8n-nodes-base.emailSend** để gửi báo cáo tổng hợp cho giáo viên về số lượng bài thi đã gửi.
3. **Kết hợp với Slack**: Thêm node **n8n-nodes-base.slack** để thông báo khi workflow gặp lỗi.
4. **Tùy chỉnh Nội Dung**: Sử dụng **n8n-nodes-base.function** để thêm header/footer vào bài thi.
5. **Lưu Trữ Bài Thi**: Sử dụng **n8n-nodes-base.googleDrive** để lưu bài thi đã gửi vào Google Drive.

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các giáo viên khỏi việc sao chép bài thi vào nhiều kênh thông tin. Bằng cách **tự động hóa gửi bài thi qua Email, Telegram và SMS**, sinh viên sẽ nhận được thông tin **kịp thời và chính xác**, trong khi bạn chỉ cần **cập nhật một lần trên Google Sheets**.

**Hãy áp dụng ngay workflow này và làm việc hiệu quả hơn!** 🚀

---
**💡 Lưu ý cuối cùng**:
- Nếu gặp lỗi, hãy kiểm tra **credentials** của các node (Google Sheets, SMTP, Telegram, Twilio).
- Để workflow hoạt động 24/7, **cài đặt n8n trên VPS** (không dùng phiên bản miễn phí trên cloud).
- **Mở rộng** workflow bằng cách thêm node khác như **Google Drive, Slack, hoặc Discord**!