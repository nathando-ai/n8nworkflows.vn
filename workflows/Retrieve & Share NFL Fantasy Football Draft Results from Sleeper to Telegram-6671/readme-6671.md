---
title: "🏈 **Tự Động Hóa Lấy Kết Quả Draft NFL Fantasy Football từ Sleeper sang Telegram (Không Cần Code!)**"
description: "Workflow này giúp các sếp NFL Fantasy Football nhanh chóng tra cứu kết quả draft của đội bóng Sleeper chỉ bằng cách nhập tên tài khoản vào Telegram Bot. Tiết kiệm thời gian, tránh thủ công, và cập nhật kết quả 24/7."
slug: "tu-dong-hoa-lay-ket-qua-draft-nfl-sleeper-sang-telegram"
tags: [n8n, automation, no-code, fantasy-football, telegram-bot]
keywords: [n8n workflow NFL, tự động hóa Sleeper, tra cứu draft fantasy football, Telegram Bot NFL, không cần code]
---

# 🚀 **Tra Cứu & Chia Sẻ Kết Quả Draft NFL Fantasy Football từ Sleeper sang Telegram**

### **Nỗi Đau Của Các Sếp NFL Fantasy Football**
Hàng ngày, các sếp phải:
- **Tra cứu thủ công** kết quả draft của đội bóng Sleeper trên ứng dụng.
- **Ghi chép lại** thông tin về các cầu thủ được chọn (vị trí, đội bóng, điểm số).
- **Chia sẻ kết quả** với đồng đội qua Telegram/Slack, dễ bị lỗi hoặc quên.
- **Phải nhớ** tên tài khoản Sleeper chính xác (thường là chữ hoa/chữ thường) để tránh kết quả sai.

**Workflow này giải quyết tất cả!** Chỉ cần nhập **tên tài khoản Sleeper** vào Telegram Bot, hệ thống sẽ tự động:
✅ **Lấy dữ liệu draft** từ Sleeper (API).
✅ **Trích xuất thông tin** về các cầu thủ được chọn (vị trí, đội bóng, điểm số).
✅ **Gửi kết quả** ngay lập tức qua Telegram với định dạng dễ đọc.
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần tra cứu thủ công trên Sleeper.
- **Chính xác 100%**: Tránh sai sót do nhập liệu hoặc nhớ sai tên tài khoản.
- **Cập nhật tức thì**: Kết quả draft được gửi ngay khi có yêu cầu.
- **Dễ chia sẻ**: Gửi kết quả cho đồng đội qua Telegram một cách nhanh chóng.
- **Hoạt động liên tục**: Workflow chạy tự động, không phụ thuộc vào giờ làm việc.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Sleeper**:
   - Đăng ký và tham gia **một league draft NFL Fantasy Football** (nếu có nhiều league, workflow sẽ lấy league gần nhất).
   - **Lưu ý**: Tên tài khoản Sleeper **phải chính xác** (chữ hoa/chữ thường), nếu sai sẽ không có kết quả.

2. **Bot Telegram**:
   - Tạo **Bot Telegram** thông qua [@BotFather](https://t.me/BotFather) và lấy **API Token**.
   - Tạo **chatbot riêng** để nhận yêu cầu tra cứu (ví dụ: `@NFLDraftBot`).

3. **Credentials trong n8n**:
   - Thiết lập **Telegram API** trong **Credentials** của n8n (Token từ BotFather).
   - **Không cần API Sleeper** vì workflow sử dụng **HTTP Request** với URL công khai của Sleeper.

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/6671](https://n8n.io/workflows/6671) hoặc copy toàn bộ JSON từ trang này.
- Mở **n8n Editor** → Nhấn **Import Workflow** → Dán JSON hoặc chọn file JSON đã tải.
- **Kích hoạt workflow** sau khi import xong.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này gồm **8 node**, nhưng các sếp chỉ cần chú ý đến **3 node quan trọng**:

##### **A. Node "Send Message to Chatbot" (TelegramTrigger)**
- **Chức năng**: Node này nhận **yêu cầu tra cứu** từ Telegram.
- **Cấu hình**:
  - **Credentials**: Chọn `telegramApi` (đã thiết lập trước đó).
  - **Message**: Thiết lập **lệnh khởi động** (ví dụ: `/draft <tên_tài_khoản>`).
    *Ví dụ*: Nếu người dùng gửi `/draft johnny123`, workflow sẽ tra cứu league của `johnny123`.

##### **B. Node "Extract Username" (Code)**
- **Chức năng**: Trích xuất **tên tài khoản Sleeper** từ yêu cầu Telegram.
- **Cấu hình**:
  - **Code**: Sử dụng **JavaScript** để lấy tên từ message Telegram.
    ```javascript
    return { username: $input.all()[0].text.split(' ')[1] };
    ```
  - **Lưu ý**: Nếu muốn **hardcode username** (không dùng Telegram), chỉnh sửa node này để trả về tên cố định.

##### **C. Node "Get Drafts" (HTTP Request)**
- **Chức năng**: Lấy **danh sách league draft** của tài khoản Sleeper.
- **Cấu hình**:
  - **Method**: `GET`
  - **URL**: `https://api.sleeper.app/v1/user/<username>/leagues` (thay `<username>` bằng `$node["Extract Username"].json.username`).
  - **Headers**:
    ```
    Accept: application/json
    ```
  - **Lưu ý**: URL này **chỉ hoạt động cho năm 2024**. Nếu muốn dùng cho năm 2025, thay đổi URL thành:
    ```
    https://api.sleeper.app/v1/user/<username>/leagues/2025
    ```

##### **D. Node "Return Picked By results" (Code)**
- **Chức năng**: **Định dạng kết quả** thành thông điệp Telegram dễ đọc.
- **Cấu hình**:
  - **Code**: Sử dụng **JavaScript** để lọc và sắp xếp thông tin cầu thủ.
    ```javascript
    const draftPicks = $input.all()[0].json;
    const formattedMessage = draftPicks.map(pick => {
      return `🏈 ${pick.player.name} (${pick.player.position}) - ${pick.player.team} (${pick.player.points})`;
    }).join('\n');
    return { message: formattedMessage };
    ```
  - **Lưu ý**: Các sếp có thể **chỉnh sửa text** để phù hợp với phong cách cá nhân.

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Gửi **yêu cầu mẫu** từ Telegram (ví dụ: `/draft johnny123`).
  - Kiểm tra **log** trong n8n để đảm bảo workflow hoạt động.
- **Bật Active**:
  - Sau khi test thành công, **bật workflow** và chia sẻ Bot Telegram cho đồng đội.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Thêm Logo Sleeper**:
   - Trong node **"Send a text message"**, thêm **logo Sleeper** vào thông điệp để trông chuyên nghiệp hơn.
   ```markdown
   ![Sleeper Logo](https://www.sleeper.com/favicon.ico) **Kết quả Draft NFL Fantasy:**
   ```
2. **Lưu Log Kết Quả**:
   - Thêm **node StickyNote** để lưu **lịch sử tra cứu** (giúp theo dõi các league đã tra cứu).
3. **Chia Sẻ Kết Quả qua Slack**:
   - Thay thế node Telegram bằng **Slack Webhook** để chia sẻ kết quả trên Slack.
4. **Tự Động Gửi Báo Cáo Hàng Tuần**:
   - Sử dụng **node Schedule** để gửi **báo cáo tổng hợp** kết quả draft hàng tuần.

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp NFL Fantasy Football muốn:
✔ **Tiết kiệm thời gian** tra cứu kết quả draft.
✔ **Tránh sai sót** do nhập liệu thủ công.
✔ **Chia sẻ kết quả** một cách nhanh chóng và tự động.

**Hãy áp dụng ngay!** Import workflow, cấu hình Telegram Bot, và bắt đầu tra cứu kết quả chỉ trong vài phút.

---
**💡 Cần hỗ trợ?** Đăng ký **VPS n8n** từ TinoHost để workflow chạy ổn định 24/7:
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (Mã giảm giá: **VPSN8N**)