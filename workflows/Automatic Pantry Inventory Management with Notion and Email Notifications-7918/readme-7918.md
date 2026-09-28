---
title: "🛒 **Tự Động Hóa Quản Lý Hàng Tồn Kho Pantry Với Notion + Thông Báo Email Hàng Ngày (Không Cần Code!)**"
description: "Workflow này tự động cập nhật danh sách mua sắm hàng ngày từ Notion, so sánh với tồn kho hiện tại, và gửi email thông báo chi tiết. Giúp tiết kiệm thời gian lên tới 80% cho việc quản lý nhà bếp!"
slug: "tu-dong-hoa-quan-ly-hang-ton-kho-pantry-notion-email"
tags: [n8n, automation, notion, email-notification, personal-productivity, no-code]
keywords: [n8n workflow quản lý nhà bếp, tự động hóa danh sách mua sắm, Notion + email tự động, quản lý tồn kho hàng ngày, tiết kiệm thời gian nhà bếp]
---

# 🚀 **Tự Động Hóa Quản Lý Hàng Tồn Kho Pantry Với Notion + Email Hàng Ngày**

### **Nỗi Đau Của Các Sếp: Quản Lý Nhà Bếp Làm Mất Thời Gian & Đa Dư Hàng Hóa**
Bạn có bao giờ đứng trước tủ bếp, mở ra thấy **nửa tủ đầy hàng nhưng vẫn phải mua lại** vì quên? Hoặc phải **ghi chép danh sách mua sắm bằng tay**, sau đó quên bỏ vào túi? Hay thậm chí **mua thừa** vì không biết chính xác đã có bao nhiêu trong tủ?

Workflow này **giải quyết tất cả** bằng cách:
✅ **Tự động cập nhật tồn kho** từ Notion (hoặc Google Sheets) mỗi ngày.
✅ **So sánh với danh sách "Cần mua"** và tạo danh sách mua sắm mới.
✅ **Gửi email thông báo** chi tiết hàng ngày (hoặc theo lịch) để bạn không quên.
✅ **Không cần code**, chỉ cần **cài đặt 1 lần** và workflow hoạt động **một mình** 24/7.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS. Với VPS TinoHost, các sếp có thể:
👉 [Đăng ký VPS n8n](https://tino.vn/vps-n8n?affid=388) với **mã giảm giá VPSN8N** (giảm tới 39%).
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (đủ sức mạnh cho workflow này).
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian** quản lý nhà bếp (không cần ghi chép tay).
- **Tránh mua thừa/đa dư** bằng cách theo dõi tồn kho chính xác.
- **Danh sách mua sắm tự động** cập nhật theo thực tế.
- **Email thông báo hàng ngày** (hoặc theo lịch) để không quên.
- **Hoạt động liên tục** mà không cần can thiệp của con người.
- **Dễ dàng mở rộng** cho nhiều người dùng trong gia đình.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản Notion** (để lưu trữ danh sách hàng tồn kho và danh sách "Cần mua").
✔ **Email** (để gửi thông báo hàng ngày).
✔ **API Key của Notion** (để workflow có thể đọc/viết vào Notion).
✔ **Thời gian** (~30 phút để cấu hình lần đầu).

---
:::info[CHUẨN BỊ NOTION]
Workflow này **không cần cấu hình Notion phức tạp**. Các sếp chỉ cần:
1. **Tạo 2 bảng Notion**:
   - **Bảng "Pantry Items"** (lưu danh sách hàng tồn kho, ví dụ: "Gạo", "Đường", "Trứng").
   - **Bảng "To Buy"** (lưu danh sách hàng cần mua, ví dụ: "Bánh mì", "Sữa").
2. **Chia sẻ bảng với n8n** bằng cách:
   - Mở bảng Notion → **Settings & Sharing** → **Add a person/integration** → **Copy Integration Token**.
   - Dán **Integration Token** vào **User Config** trong workflow.
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể **import workflow** từ file JSON hoặc **copy/paste JSON** vào n8n Editor:
- **Tải workflow gốc** từ [đây](https://n8n.io/workflows/7918) (chọn **Export JSON**).
- **Trên n8n Editor**:
  - Nhấn **Import** → **Paste JSON** → **Import**.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này có **9 node**, nhưng chỉ **3 node quan trọng** cần cấu hình kỹ:

##### **A. Node "User Config" (n8n-nodes-base.set)**
- **Chức năng**: Cấu hình các tham số chung như **Integration Token của Notion**, **Email gửi thông báo**, và **Lịch trình Cron**.
- **Cách chỉnh**:
  - Mở node → **Add Property** → Điền:
    ```json
    {
      "notionIntegrationToken": "YOUR_NOTION_INTEGRATION_TOKEN",
      "emailTo": "email_cua_ban@gmail.com",
      "cronSchedule": "0 8 * * *" // Gửi email lúc 8h sáng hàng ngày
    }
    ```
  - **Lưu ý**:
    - **notionIntegrationToken**: Lấy từ **Settings & Sharing** của bảng Notion (hướng dẫn ở trên).
    - **cronSchedule**: Thay đổi thời gian gửi email theo nhu cầu (ví dụ: `"0 16 * * *"` để gửi lúc 4h chiều).

##### **B. Node "Get Pantry Items" & "Get Existing To Buy" (n8n-nodes-base.notion)**
- **Chức năng**: Lấy dữ liệu từ Notion về **hàng tồn kho** và **danh sách cần mua**.
- **Cách chỉnh**:
  - Mở node → **Credentials** → Chọn **notionIntegrationToken** (đã cấu hình ở trên).
  - **Query**:
    - **Get Pantry Items**:
      ```json
      {
        "filter": {
          "property": "Status",
          "status": {
            "equals": "In Pantry"
          }
        }
      }
      ```
    - **Get Existing To Buy**:
      ```json
      {
        "filter": {
          "property": "Status",
          "status": {
            "equals": "To Buy"
          }
        }
      }
      ```
  - **Lưu ý**:
    - Đảm bảo **cột "Status"** trong Notion có giá trị **"In Pantry"** và **"To Buy"**.

##### **C. Node "Compose Email" (n8n-nodes-base.function)**
- **Chức năng**: Xây dựng nội dung email từ dữ liệu tồn kho và danh sách cần mua.
- **Cách chỉnh**:
  - Mở node → **Edit Function** → Sử dụng **JavaScript template** mặc định (không cần chỉnh sửa nếu đã import từ file JSON).
  - **Lưu ý**:
    - Nếu muốn **thay đổi định dạng email**, các sếp có thể mở node này và chỉnh sửa **template HTML** trong **Compose Email**.

##### **D. Node "Send Email" (n8n-nodes-base.emailSend)**
- **Chức năng**: Gửi email thông báo hàng ngày.
- **Cách chỉnh**:
  - Mở node → **Credentials** → Chọn **SMTP** (nếu chưa có, thêm mới).
  - **Config SMTP**:
    - **Host**: `smtp.gmail.com` (hoặc SMTP của nhà cung cấp email khác).
    - **Port**: `587`.
    - **Username**: Email của bạn.
    - **Password**: **App Password** (nếu dùng Gmail, tạo tại [My Account > Security > App Passwords](https://myaccount.google.com/apppasswords)).
  - **Lưu ý**:
    - **Không dùng mật khẩu chính của Gmail** (Google không cho phép).

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Nhấn **Run Workflow** để kiểm tra.
  - Kiểm tra **email** và **Notion** để đảm bảo dữ liệu đúng.
- **Bật Active**:
  - Sau khi test thành công, nhấn **Active** để workflow chạy tự động.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Thêm Slack/Telegram Notifications**:
   - Sử dụng **node Slack** hoặc **Telegram Bot** để gửi thông báo ngay khi workflow chạy.
   - Cách thêm:
     - Import **node Slack** hoặc **Telegram** vào workflow.
     - Gửi thông báo cùng với email.

2. **Lưu Log Lịch Sử**:
   - Sử dụng **node Sticky Note** (đã có trong workflow) để lưu **lịch sử các lần chạy**.
   - Cách mở:
     - Mở **Sticky Note** → **View Notes** để xem log.

3. **Gửi Báo Cáo Tuần/Tháng**:
   - Thay đổi **cronSchedule** để gửi báo cáo định kỳ (ví dụ: `"0 9 * * 0"` để gửi thứ 7 hàng tuần).
   - **Tăng cường nội dung email** bằng **AI** (nếu muốn):
     - Sử dụng **node LLM** (n8n-nodes-base.llm) để tổng hợp báo cáo chi tiết.

4. **Chia Sẻ Cho Gia Đình**:
   - **Chia sẻ bảng Notion** cho người khác trong gia đình.
   - **Cấu hình email chung** để tất cả thành viên nhận thông báo.

---

### 📌 **Kết Luận: Tự Động Hóa Nhà Bếp Bằng Một Click!**
Workflow này **giải phóng thời gian** của các sếp khỏi việc **ghi chép danh sách mua sắm bằng tay** và **quên mua hàng**. Với **Notion + Email tự động**, bạn sẽ:
✔ **Tiết kiệm 80% thời gian** quản lý nhà bếp.
✔ **Tránh mua thừa/đa dư** bằng cách theo dõi tồn kho chính xác.
✔ **Không bao giờ quên** mua hàng nhờ email thông báo hàng ngày.

**Hành động ngay!**
1. **Import workflow** từ [đây](https://n8n.io/workflows/7918).
2. **Cấu hình Notion và email** theo hướng dẫn.
3. **Bật Active** và **nghỉ ngơi** – workflow sẽ làm việc thay bạn!

---
**💡 Mẹo cuối**: Nếu gặp vấn đề, hãy **check log** trong **Sticky Note** hoặc **email debug** từ n8n. Các sếp có thể **tạo issue** trên [GitHub n8n](https://github.com/n8n-io/n8n) nếu cần hỗ trợ kỹ thuật!