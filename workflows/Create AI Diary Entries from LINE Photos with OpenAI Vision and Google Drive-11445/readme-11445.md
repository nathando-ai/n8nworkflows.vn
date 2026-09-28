---
title: "📸 Tự Động Hóa Sách Nhật Ký AI Từ Ảnh LINE Với OpenAI Vision & Google Drive - Không Cần Code!"
description: "Workflow này tự động chuyển đổi mọi ảnh gửi qua LINE thành nhật ký AI ngắn gọn, lưu trữ sẵn trên Google Drive với cấu trúc thư mục logic (KidsDiary/YYYY/MM). Giúp các bậc phụ huynh theo dõi kỷ niệm bé yêu một cách dễ dàng, tiết kiệm thời gian và không cần viết tay."
slug: "tieu-dong-hoa-sach-nhat-ky-ai-tu-anh-line"
tags: [n8n, automation, no-code, openai, google-drive, line-bot, ai-multimodal]
keywords: [tự động hóa nhật ký trẻ em, workflow n8n line, openai vision tự động hóa, lưu ảnh google drive tự động, nhật ký AI từ ảnh]
---

# 🚀 **Tự Động Hóa Sách Nhật Ký AI Từ Ảnh LINE Với OpenAI Vision & Google Drive**

### **Giải pháp hoàn hảo cho các bậc phụ huynh muốn ghi lại kỷ niệm bé yêu một cách tự động, không cần viết tay!**

Hãy tưởng tượng: Bé yêu gửi một ảnh đẹp qua LINE, và chỉ trong vài giây, hệ thống đã tự động:
✅ **Tạo nhật ký AI ngắn gọn** (với OpenAI Vision) mô tả ảnh đó.
✅ **Lưu ảnh và nhật ký** vào Google Drive với cấu trúc thư mục logic (`KidsDiary/YYYY/MM`).
✅ **Gửi xác nhận** về LINE cho bạn biết đã lưu thành công.

**Không cần viết tay, không cần nhớ, chỉ cần chụp ảnh và quên!** Đây chính là sức mạnh của **tự động hóa no-code** với n8n.

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần viết nhật ký tay, hệ thống làm tất cả cho bạn.
- **Ghi lại kỷ niệm một cách logic**: Ảnh và nhật ký được lưu theo ngày/tháng, dễ dàng tìm kiếm sau này.
- **Cá nhân hóa tự động**: OpenAI Vision phân tích ảnh và tạo ra những câu nhật ký độc đáo, phù hợp với từng bức ảnh.
- **Hoạt động 24/7**: Workflow chạy tự động mỗi khi nhận được ảnh qua LINE, không cần can thiệp thủ công.
- **Dễ dàng chia sẻ**: Bạn có thể chia sẻ link Google Drive với gia đình hoặc bạn bè để cùng xem lại kỷ niệm.
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản LINE Developer**:
   - Đăng ký tại [LINE Developers](https://developers.line.biz/) để tạo **Channel ID** và **Channel Secret**.
   - Cài đặt **Webhook URL** của n8n (sau khi import workflow) vào LINE Developer Console.
   - Lấy **Access Token** của LINE để gọi API.

2. **Tài khoản Google Drive**:
   - Cài đặt **Google Drive API** và tạo **Service Account** với quyền chỉnh sửa thư mục `KidsDiary`.
   - Lấy **Client ID** và **Client Secret** từ [Google Cloud Console](https://console.cloud.google.com/).

3. **Tài khoản OpenAI**:
   - Đăng ký tại [OpenAI](https://platform.openai.com/) và lấy **API Key**.

4. **n8n Self-hosted**:
   - Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng** (Self-hosted).
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Tải file JSON** từ [n8n.io/workflows/11445](https://n8n.io/workflows/11445).
- Trong **n8n Editor**, chọn **Import** và chọn file JSON đã tải.
- Hoặc copy toàn bộ JSON và paste vào **Import Workflow** trong n8n.

---
### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**

#### **🔹 Step 1: LINE Webhook & API Setup**
- **LINE Webhook**:
  - Đặt **Path** = `line-webhook` (không đổi).
  - **HTTP Method** = `POST`.
  - Sau khi import, **copy URL Webhook** từ n8n và dán vào **LINE Developer Console** (trong phần **Webhook Configuration**).

- **Extract LINE Message Data**:
  - Node này tự động trích xuất `messageId` và `replyToken` từ payload LINE. **Không cần chỉnh sửa**.

- **Get Image from LINE**:
  - **Headers**:
    - `Authorization: Bearer <LINE_ACCESS_TOKEN>` (điền từ tài khoản LINE của bạn).
  - **URL**: `https://api.line.me/v2/bot/message/content?type=image&messageId={{$node["Extract LINE Message Data"].json["$.message.id"]}}`
    - **Lưu ý**: `$node["Extract LINE Message Data"].json["$.message.id"]` là biến tự động trích xuất từ node trước.

#### **🔹 Step 2: OpenAI Vision & Google Drive Setup**
- **OpenAI Vision - Generate Diary**:
  - **API Key**: Điền từ tài khoản OpenAI của bạn.
  - **Model**: Sử dụng `gpt-4-vision-preview` (hoặc model mới nhất).
  - **Prompt**:
    ```json
    "Analyze this image and generate a short Japanese diary entry (about 50 characters)."
    ```
  - **Image**: Chọn `{{$node["Get Image from LINE"].json["body"]}}` (ảnh đã tải từ LINE).

- **Prepare Folder Path**:
  - Node này tự động tạo đường dẫn `KidsDiary/YYYY/MM` dựa trên ngày hiện tại. **Không cần chỉnh sửa**.

- **Create Folder Structure**:
  - **Credentials**: Chọn **Google Drive** đã cấu hình trước.
  - **Folder Path**: `KidsDiary/{{$node["Prepare Folder Path"].json["path"]}}`
  - **Parent Folder ID**: Lấy từ **Google Drive API** (thường là `root` hoặc ID của thư mục cha).

#### **🔹 Step 3: Merge & Convert to File**
- **Merge**:
  - Kết hợp `{{$node["OpenAI Vision - Generate Diary"].json["choices"][0]["message"]["content"]}}` (nhật ký AI) với metadata ảnh.
  - **Lưu ý**: Đảm bảo `{{$node["Get Image from LINE"].json["body"]}}` (ảnh) và `{{$node["OpenAI Vision - Generate Diary"].json["choices"][0]["message"]["content"]}}` (nhật ký) được truyền vào node này.

- **Convert to File**:
  - **Operation**: `toText`.
  - **Text**: `{{$node["Merge"].json["text"]}}` (nhật ký AI).
  - **File Name**: `{{$node["Prepare Folder Path"].json["path"]}}/diary.txt`.

#### **🔹 Step 4: Upload Files & Reply to LINE**
- **Upload Photo to Drive**:
  - **Credentials**: Chọn **Google Drive**.
  - **File**: `{{$node["Get Image from LINE"].json["body"]}}`.
  - **File Name**: `{{$node["Prepare Folder Path"].json["path"]}}/photo_{{$node["Get Image from LINE"].json["$.message.id"]}}.jpg`.

- **Upload Photo to diary (new)**:
  - **Credentials**: Chọn **Google Drive**.
  - **File**: `{{$node["Convert to File"].json["file"]}}` (file `.txt` nhật ký).
  - **File Name**: `{{$node["Prepare Folder Path"].json["path"]}}/diary.txt`.

- **Reply to LINE**:
  - **Headers**:
    - `Authorization: Bearer <LINE_ACCESS_TOKEN>`.
  - **URL**: `https://api.line.me/v2/bot/message/push`
  - **Body**:
    ```json
    {
      "to": "{{$node["Extract LINE Message Data"].json["$.replyToken"]}}",
      "messages": [
        {
          "type": "text",
          "text": "📸 Ảnh và nhật ký đã được lưu thành công vào Google Drive!"
        }
      ]
    }
    ```

---
### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Gửi một ảnh qua LINE Webhook (có thể test bằng Postman hoặc tool như [RequestBin](https://requestbin.com/)).
   - Kiểm tra **Google Drive** xem ảnh và file `.txt` nhật ký đã được lưu không.
   - Kiểm tra **LINE** xem có nhận được tin nhắn xác nhận không.

2. **Bật Active Workflow**:
   - Trong **n8n Editor**, chọn workflow và bật **Active**.

---
## ✍️ **Mẹo & gợi ý nâng cao**
:::tip[NÂNG CAO THÊM TÍNH NĂNG]
- **Gửi báo cáo định kỳ**: Sử dụng **n8n-nodes-base.email** hoặc **Slack** để gửi email/báo cáo hàng tuần về các nhật ký mới được tạo.
- **Lưu log chi tiết**: Sử dụng **n8n-nodes-base.stickyNote** để ghi lại thông tin debug (ví dụ: lỗi OpenAI, lỗi Google Drive).
- **Kết hợp với Telegram**: Thay vì LINE, các sếp có thể sử dụng **Telegram Bot** để nhận ảnh và tự động lưu nhật ký.
- **Tùy chỉnh nhật ký**: Thay đổi **prompt** trong OpenAI để nhật ký phù hợp với ngôn ngữ hoặc phong cách riêng.
- **Xóa ảnh sau khi lưu**: Sử dụng **n8n-nodes-base.httpRequest** để gọi API LINE xóa ảnh sau khi đã lưu nhật ký (nếu không muốn ảnh chiếm dung lượng).
:::

---
## 📌 **Kết luận**
Workflow này không chỉ **tiết kiệm thời gian** mà còn **tạo ra những kỷ niệm đẹp** cho bé yêu một cách tự động. Với **OpenAI Vision**, mỗi ảnh đều được mô tả một cách độc đáo, trong khi **Google Drive** giúp bạn dễ dàng quản lý và tìm kiếm lại những khoảnh khắc quý giá.

**Hãy áp dụng ngay và bắt đầu ghi lại những kỷ niệm bé yêu một cách dễ dàng!** 🚀

---
### **🔗 Tài liệu tham khảo**
- [LINE Developers](https://developers.line.biz/)
- [Google Drive API](https://developers.google.com/drive/api/v3/quickstart/nodejs)
- [OpenAI API](https://platform.openai.com/docs/api-reference/introduction)
- [n8n Workflow gốc](https://n8n.io/workflows/11445)