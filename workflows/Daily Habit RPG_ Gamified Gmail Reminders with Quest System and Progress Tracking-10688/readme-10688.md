---
title: "🎮 **Hệ Thống RPG Hàng Ngày: Nhắc Nhở Email Gamified Cho Thói Quen Hàng Ngày**"
description: "Tự động hóa việc theo dõi thói quen hàng ngày bằng hệ thống RPG hấp dẫn, gửi email động viên mỗi sáng với XP, cấp độ và nhiệm vụ cá nhân hóa. Giúp các sếp tăng cường sự tập trung và duy trì thói quen một cách vui vẻ!"
slug: "daily-habit-rpg-gamified-gmail-reminders"
tags: [n8n, automation, no-code, productivity, gamification, gmail]
keywords: [n8n workflow, tự động hóa thói quen, RPG hàng ngày, nhắc nhở email, gamify productivity, tự động hóa cá nhân]
---

# 🚀 **Tự Động Hóa Thói Quen Hàng Ngày Bằng Hệ Thống RPG: Nhắc Nhở Email Gamified**

### **Nỗi Đau Của Các Sếp**
Các sếp thường gặp khó khăn trong việc duy trì thói quen hàng ngày như tập thể dục, học tiếng Anh, hoặc làm việc hiệu quả. Thói quen dễ bị quên lãng, thiếu động lực, và việc theo dõi tiến độ thủ công tốn thời gian. **Workflow này giải quyết vấn đề này bằng cách biến thói quen thành một trò chơi RPG hấp dẫn**, với hệ thống XP, cấp độ, và nhiệm vụ cá nhân hóa, gửi qua email mỗi sáng để động viên và theo dõi tiến độ tự động.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa động viên hàng ngày**: Nhận email RPG động viên mỗi sáng, không cần nhớ nhắc.
- **Gamification tăng động lực**: XP, cấp độ, và nhiệm vụ cá nhân hóa giúp duy trì thói quen lâu dài.
- **Tiết kiệm thời gian**: Không cần theo dõi thủ công, hệ thống tự động cập nhật tiến độ.
- **Cá nhân hóa hoàn toàn**: Chỉ cần chỉnh sửa code trong nodes, workflow sẽ phản ánh thói quen riêng của các sếp.
- **Hoạt động liên tục**: Chạy tự động hàng ngày, không phụ thuộc vào sự can thiệp của con người.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
- **Tài khoản Gmail**: Để gửi email nhắc nhở (cần OAuth2).
- **n8n Instance**: Cloud hoặc self-hosted (khuyến nghị self-hosted để đảm bảo dữ liệu riêng tư).
- **Thời gian**: ~5 phút để cấu hình và kích hoạt workflow.
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/10688) hoặc copy/paste JSON từ canvas vào **n8n Editor**.
- **Cách import**:
  1. Mở n8n Editor.
  2. Nhấn **"Import"** → **"From JSON"**.
  3. Dán JSON và nhấn **"Import"**.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow gồm **8 nodes** chính, mỗi node có vai trò quan trọng. Dưới đây là hướng dẫn chi tiết:

##### **🕒 Node 1: Daily Morning Trigger (n8n-nodes-base.scheduleTrigger)**
- **Chức năng**: Khởi động workflow mỗi sáng (mặc định 6:00 AM).
- **Cách chỉnh**:
  - Nhấp đúp vào node → Thay đổi `triggerAtHour` (ví dụ: `7` để chạy lúc 7:00 AM).
  - Lưu và kích hoạt workflow.

##### **🎮 Node 2: Initialize Player Stats (n8n-nodes-base.code)**
- **Chức năng**: Khởi tạo thống kê người chơi (XP, cấp độ, chuỗi thành công).
- **Lưu ý**:
  - Trong code, các sếp có thể thay đổi `playerStats` để phù hợp với mục tiêu cá nhân.
  - Ví dụ: `level: 1`, `xp: 0`, `streak: 0`.

##### **🏆 Node 3: Generate Daily Quests (n8n-nodes-base.code)**
- **Chức năng**: Tạo nhiệm vụ hàng ngày dựa trên ngày trong tuần (thứ 2: tập thể dục, thứ 7: học tiếng Anh...).
- **Cách chỉnh**:
  - Mở code và chỉnh `questDatabase` để thêm/bỏ nhiệm vụ.
  - Ví dụ:
    ```json
    "questDatabase": {
      "monday": ["Set 3 goals for the week"],
      "tuesday": ["Read 10 pages of a book"],
      "wednesday": ["Do 20 push-ups"],
      ...
    }
    ```

##### **💬 Node 4: Fetch Daily Quote (n8n-nodes-base.httpRequest)**
- **Chức năng**: Lấy câu động viên từ API miễn phí (không cần API key).
- **Lưu ý**:
  - Nếu API thất bại, hệ thống sẽ tự động sử dụng câu động viên mặc định.

##### **📊 Node 5: Process Game Stats (n8n-nodes-base.code)**
- **Chức năng**: Tính toán cấp độ, XP, và thành tích (D → SSS).
- **Cách chỉnh**:
  - Các sếp có thể thay đổi logic tính toán trong code để phù hợp với hệ thống điểm riêng.

##### **✉️ Node 6: Create Email Template (n8n-nodes-base.code)**
- **Chức năng**: Tạo mẫu email HTML động với:
  - Thống kê người chơi (cấp độ, XP).
  - Danh sách nhiệm vụ hàng ngày.
  - Thành tích và động viên.
- **Lưu ý**:
  - Mẫu email có thiết kế responsive, hoạt động trên mọi thiết bị.

##### **📧 Node 7: Send Quest Email (n8n-nodes-base.gmail)**
- **BẮT BUỘC phải cấu hình**:
  1. Nhấn **"Create New"** trong phần **Credentials**.
  2. Chọn **Gmail** và đăng nhập với OAuth2.
  3. Điền **email nhận** (của chính các sếp hoặc đồng nghiệp).
  4. **Test run** trước khi kích hoạt:
     - Nhấn **"Execute Workflow"** để kiểm tra email đã gửi đúng không.
  5. Kích hoạt workflow khi đã kiểm tra xong.

##### **📝 Node 8: Log Execution Stats (n8n-nodes-base.code)**
- **Chức năng**: Ghi log tiến độ chạy (có thể kết nối với Google Sheets hoặc cơ sở dữ liệu).
- **Lưu ý**:
  - Nếu muốn lưu lịch sử, các sếp có thể kết nối với **Google Sheets** hoặc **database** bằng node `n8n-nodes-base.googleSheets`.

---

#### **3. Kích Hoạt ⚡️**
1. **Test run** với dữ liệu mẫu:
   - Nhấn **"Execute Workflow"** để kiểm tra email đã gửi đúng.
2. **Bật Active workflow**:
   - Nhấn nút **"Activate"** ở góc trên bên phải.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[CÁCH LÀM NÊN HIỂU]
- **Kết hợp với Slack/Telegram**: Thay vì email, các sếp có thể gửi thông báo qua Slack hoặc Telegram bằng node `n8n-nodes-base.slack` hoặc `n8n-nodes-base.telegram`.
- **Lưu log vào Google Sheets**: Kết nối node `Log Execution Stats` với `n8n-nodes-base.googleSheets` để theo dõi tiến độ dài hạn.
- **Thêm nhiệm vụ tùy chỉnh**: Chỉnh sửa `questDatabase` trong node `Generate Daily Quests` để thêm nhiệm vụ mới (ví dụ: "Học 1 bài hát mới").
- **Báo cáo tuần/Tháng**: Sử dụng node `n8n-nodes-base.date` để gửi báo cáo tổng hợp định kỳ.
- **Thay đổi thời gian chạy**: Để workflow chạy vào giờ khác (ví dụ: 8:00 AM), chỉnh `triggerAtHour` trong node `Daily Morning Trigger`.
:::

---

### 📌 **Kết Luận**
Workflow **Daily Habit RPG** không chỉ giúp các sếp tự động hóa việc nhắc nhở thói quen hàng ngày mà còn **gamify quá trình**, biến nó thành một trò chơi thú vị. Với chỉ **5 phút cấu hình**, các sếp sẽ nhận được email động viên mỗi sáng, theo dõi tiến độ cá nhân hóa, và duy trì thói quen một cách hiệu quả.

**Hãy áp dụng ngay và biến thói quen của mình thành một RPG hấp dẫn!** 🎮✨

---
**🔗 [Tải workflow nguyên bản](https://n8n.io/workflows/10688) | [Hướng dẫn chi tiết trên n8n.io](https://n8n.io/workflows/10688)**