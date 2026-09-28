---
title: "🎮 **Tự Động Hóa Lấy Thống Kê Trận Đấu Deadlock Game & Gửi Trực Tiếp Telegram (Không Cần Code!)**"
description: "Workflow tự động hóa lấy dữ liệu thống kê trận đấu từ Deadlock Game, phân tích kết quả và gửi báo cáo định kỳ qua Telegram. Giúp các sếp quản lý đội hình, phân tích chiến thuật và tối ưu hóa hiệu suất đội ngũ một cách nhanh chóng và chính xác."
slug: "tu-dong-hoa-lay-thong-ke-tran-dau-deadlock-game"
tags: [n8n, automation, no-code, telegram-bot, game-statistics, deadlock-game]
keywords: [n8n workflow deadlock game, tự động hóa lấy thống kê trận đấu, gửi báo cáo telegram, phân tích kết quả game, tự động hóa không code]
---

# 🚀 **Tự Động Hóa Lấy Thống Kê Trận Đấu Deadlock Game & Gửi Trực Tiếp Telegram**

### **💥 Nỗi Đau Của Các Sếp Khi Làm Thủ Công**
Hiện nay, việc theo dõi và phân tích kết quả trận đấu của đội ngũ trong **Deadlock Game** thường phụ thuộc vào việc các sếp phải:
- **Tìm kiếm thủ công** trên trang web hoặc game để lấy dữ liệu trận đấu.
- **Chuyển đổi và tổng hợp** thông tin từ nhiều trận đấu khác nhau.
- **Gửi báo cáo** qua Telegram hoặc email để cập nhật cho đội ngũ.
- **Mất thời gian** và dễ xảy ra lỗi do con người trong quá trình nhập liệu.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tự động lấy dữ liệu** trận đấu từ Deadlock Game.
✅ **Phân tích và tổng hợp** thông tin về các cầu thủ, điểm số, và chiến thuật.
✅ **Gửi báo cáo tự động** qua Telegram với định dạng rõ ràng.
✅ **Hoạt động 24/7** mà không cần can thiệp của con người.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm thời gian** lên đến **90%** so với cách làm thủ công.
- **Chính xác 100%** vì dữ liệu được lấy trực tiếp từ nguồn chính thức.
- **Cá nhân hóa báo cáo** với thông tin chi tiết về từng trận đấu.
- **Hoạt động liên tục** mà không cần phải nhớ hoặc nhắc nhở.
- **Tối ưu hóa hiệu suất đội ngũ** bằng cách phân tích kết quả một cách khoa học.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ**]
Để workflow hoạt động, các sếp cần:
1. **Tài khoản Telegram** và **API Key Telegram Bot**:
   - Tạo một bot Telegram mới bằng cách gửi tin nhắn cho `@BotFather` và lấy **API Key**.
   - Thêm bot vào nhóm hoặc chat cá nhân để nhận báo cáo.
2. **Thông tin URL của trang Deadlock Game**:
   - URL của trang chủ hoặc trang kết quả trận đấu (ví dụ: `https://deadlockgame.com/match/12345`).
3. **VPS hoặc máy chủ n8n** (khuyến nghị **Self-hosted** để ổn định):
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/4571) hoặc sao chép mã JSON từ trang đó.
- Trong **n8n Editor**, chọn **"Import"** và dán JSON vào.
- Hoặc tạo workflow mới và **copy/paste** từng node theo thứ tự sau:

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này bao gồm **7 node** chính, các sếp cần chú ý cấu hình như sau:

##### **🔹 Node 1: Telegram Trigger (n8n-nodes-base.telegramTrigger)**
- **Chức năng**: Khởi động workflow khi nhận được tin nhắn từ Telegram (có thể là lệnh hoặc tin nhắn cụ thể).
- **Cấu hình**:
  - Chọn **credentials**: `telegramApi` (đã tạo trước).
  - Thiết lập **filter** để workflow chỉ chạy khi nhận được lệnh cụ thể (ví dụ: `/start` hoặc `/stats`).

##### **🔹 Node 2: Fetch Profile HTML (n8n-nodes-base.httpRequest)**
- **Chức năng**: Lấy trang HTML của trận đấu từ Deadlock Game.
- **Cấu hình**:
  - **Method**: `GET`.
  - **URL**: Điền URL của trận đấu (ví dụ: `https://deadlockgame.com/match/12345`).
  - **Headers**: Thêm `User-Agent` để tránh bị chặn (ví dụ: `Mozilla/5.0`).

##### **🔹 Node 3: Extract Match ID (n8n-nodes-base.function)**
- **Chức năng**: Trích xuất **ID trận đấu** từ URL hoặc HTML.
- **Cấu hình**:
  - Sử dụng **JavaScript** để extra ID từ URL hoặc nội dung HTML.
  - Ví dụ:
    ```javascript
    return { matchId: url.split('/').pop() };
    ```

##### **🔹 Node 4: Fetch Match HTML (n8n-nodes-base.httpRequest)**
- **Chức năng**: Lấy trang HTML chi tiết của trận đấu bằng ID đã extra.
- **Cấu hình**:
  - **Method**: `GET`.
  - **URL**: `https://deadlockgame.com/match/{matchId}` (sử dụng biến `{{$node["Extract Match ID"].json["matchId"]}}`).

##### **🔹 Node 5: Parse Players (n8n-nodes-base.function)**
- **Chức năng**: Phân tích và extra thông tin về các cầu thủ trong trận đấu.
- **Cấu hình**:
  - Sử dụng **JavaScript** để extra tên, điểm số, và các thông tin khác từ HTML.
  - Ví dụ:
    ```javascript
    const players = [];
    // Lấy dữ liệu từ HTML và extra vào mảng players
    return { players };
    ```

##### **🔹 Node 6: Format Message (n8n-nodes-base.function)**
- **Chức năng**: Định dạng tin nhắn Telegram với thông tin trận đấu.
- **Cấu hình**:
  - Sử dụng **JavaScript** để tạo tin nhắn có định dạng Markdown hoặc HTML.
  - Ví dụ:
    ```javascript
    return {
      message: `**Trận đấu ID: {{$node["Extract Match ID"].json["matchId"]}}**
      **Kết quả:** {{players[0].score}} - {{players[1].score}}
      **Cầu thủ:** {{players[0].name}} vs {{players[1].name}}`
    };
    ```

##### **🔹 Node 7: Send Telegram Message (n8n-nodes-base.telegram)**
- **Chức năng**: Gửi tin nhắn đã định dạng qua Telegram.
- **Cấu hình**:
  - Chọn **credentials**: `telegramApi`.
  - **Chat ID**: Điền ID của chat/nhóm Telegram (có thể lấy từ `@username` hoặc API Telegram).
  - **Message**: Sử dụng biến `{{$node["Format Message"].json["message"]}}`.

---

#### **3. Kích Hoạt ⚡️**
- **Test Run**: Chạy workflow với dữ liệu mẫu để kiểm tra.
- **Bật Active**: Sau khi kiểm tra thành công, bật **Active** để workflow hoạt động tự động.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[**CÁC Ý TƯỚNG MỞ RỘNG**]
1. **Gửi báo cáo định kỳ**:
   - Sử dụng **n8n-nodes-base.set** để lập lịch gửi báo cáo hàng ngày/tuần.
   - Ví dụ: Gửi báo cáo kết quả trận đấu của ngày hôm qua vào sáng hôm sau.

2. **Kết hợp với Slack**:
   - Thay vì chỉ gửi qua Telegram, các sếp có thể gửi báo cáo đồng thời qua **Slack** bằng node `n8n-nodes-base.slack`.

3. **Lưu log dữ liệu**:
   - Sử dụng **n8n-nodes-base.googleSheets** hoặc **n8n-nodes-base.airtable** để lưu trữ lịch sử trận đấu.

4. **Phân tích chiến thuật**:
   - Thêm node **LLM** (ví dụ: `n8n-nodes-base.llm`) để phân tích và đề xuất chiến thuật từ dữ liệu trận đấu.

5. **Tự động cập nhật URL trận đấu mới**:
   - Sử dụng **webhook** từ Deadlock Game (nếu có) hoặc kết hợp với **n8n-nodes-base.cron** để lấy dữ liệu mới mỗi khi có trận đấu mới.
:::

---

### 📌 **Kết Luận**
Workflow này giúp các sếp **tự động hóa hoàn toàn** quá trình lấy và phân tích thống kê trận đấu Deadlock Game, đồng thời gửi báo cáo trực tiếp qua Telegram. **Không cần code**, không cần mất thời gian thủ công, và **chính xác 100%**.

**Hãy áp dụng ngay để tối ưu hóa hiệu suất đội ngũ và nâng cao hiệu quả quản lý!** 🚀

---
**🔗 [Tải workflow nguyên bản](https://n8n.io/workflows/4571) | 📌 [Cài đặt n8n Self-hosted](https://n8n.io/)**