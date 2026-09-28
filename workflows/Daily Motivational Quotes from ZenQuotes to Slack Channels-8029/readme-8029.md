---
title: "🚀 Tự động gửi câu nói truyền động lực mỗi ngày từ ZenQuotes lên Slack với n8n"
description: "Xây dựng hệ thống tự động lấy câu nói truyền cảm hứng ngẫu nhiên từ ZenQuotes và gửi vào Slack channel vào 8h sáng mỗi ngày, giúp làm mới năng lượng đội ngũ."
slug: "tu-dong-gui-cau-noi-truyen-dong-luc-zenquotes-slack"
tags: [n8n, automation, slack, zenquotes, productivity, api]
keywords: [n8n workflow, zenquotes api, slack automation, tu dong hoa n8n, tao dong luc lam viec]
keywords: [n8n workflow, zenquotes api, slack automation, tu dong hoa n8n, tao dong luc lam viec]
---

# 🚀 Tự động gửi câu nói truyền động lực mỗi ngày từ ZenQuotes lên Slack

Các sếp có bao giờ cảm thấy đội ngũ nhân sự của mình cần một nguồn năng lượng tích cực, một chút "vitamin M" (motivation) vào đầu mỗi ngày làm việc không? Việc phải thủ công đi tìm kiếm và đăng những câu nói hay (quotes) lên kênh Slack chung mỗi sáng vừa tốn thời gian, vừa dễ bị quên lãng.

Đừng lo, bài toán này sẽ được giải quyết gọn gàng với workflow n8n tự động hóa 100%. Hệ thống sẽ tự động gọi API lấy một câu nói truyền cảm hứng ngẫu nhiên từ ZenQuotes, format lại thật bắt mắt và bắn thẳng lên kênh Slack của công ty vào đúng 8 giờ sáng hàng ngày. Hoàn toàn không tốn một xu phí API và không cần viết code phức tạp!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Chạy ngầm 24/7, không cần con người nhúng tay vào mỗi sáng.
- **Tăng tinh thần đội ngũ:** Cung cấp nguồn cảm hứng tích cực, khởi đầu ngày mới năng suất cho toàn bộ team trên Slack.
- **Tiết kiệm chi phí:** Sử dụng ZenQuotes.io hoàn toàn miễn phí, không yêu cầu API Key rườm rà.
- **Tùy biến linh hoạt:** Dễ dàng thay đổi thời gian kích hoạt hoặc định dạng tin nhắn theo văn hóa công ty.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Slack Workspace:** Quyền Admin hoặc quyền cài đặt App để tạo Slack App tích hợp.
- **ZenQuotes API:** Không cần tài khoản hay API key, sử dụng trực tiếp qua HTTP Request node.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow này về máy, sau đó truy cập vào giao diện n8n của các sếp, chọn **Add workflow** -> **Import from File** và chọn file JSON vừa tải. Hoặc đơn giản là copy toàn bộ mã JSON và dán trực tiếp vào màn hình n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 4 nodes chính, các sếp cần chú ý cấu hình các điểm sau:

- **Daily 8AM Trigger (`cron`):** 
  - Node này mặc định được cấu hình chạy vào 8:00 sáng mỗi ngày theo múi giờ `America/New_York`. 
  - Các sếp nhớ vào cài đặt Workflow Settings hoặc chỉnh trực tiếp trong node để đổi sang múi giờ Việt Nam (`Asia/Ho_Chi_Minh`) cho đúng giờ làm việc nhé!

- **Fetch Random Quote (`httpRequest`):**
  - Node này kết nối tới `https://zenquotes.io/api/random` để lấy dữ liệu. Không cần điền API key gì cả, cứ để nguyên và test thử để xem nó trả về câu quote nào.

- **Format Quote for Slack (`code`):**
  - Node Javascript này chịu trách nhiệm bóc tách dữ liệu JSON thô từ ZenQuotes và format lại thành một chuỗi thông điệp đẹp mắt, sẵn sàng gửi lên Slack (bao gồm nội dung câu nói và tên tác giả).

- **Send to Slack (`slack`):**
  - **Connect Slack App:** Các sếp cần tạo một Slack App tại `api.slack.com`, thêm các OAuth scopes gồm `chat:write` và `channels:read`, sau đó cài đặt app vào Workspace của mình.
  - **Credentials:** Tạo Slack Credential trong n8n bằng Bot User OAuth Token vừa lấy được.
  - **Channel:** Cập nhật lại tên kênh nhận thông báo trong node này (mặc định là `#general`, các sếp có thể đổi thành `#random`, `#wellness` hoặc kênh riêng của team).

#### 3. Kích hoạt ⚡️
- Bấm nút **Execute Workflow** để chạy thử nghiệm thủ công xem Slack có nhận được tin nhắn hay không.
- Nếu mọi thứ mượt mà, hãy gạt công tắc **Active** ở góc trên cùng bên phải để workflow chính thức tự động chạy ngầm hàng ngày.

### ✍️ Mẹo & gợi ý nâng cao
- **Đa dạng hóa kênh:** Các sếp có thể nhân bản node Slack để gửi cùng một câu quote lên nhiều kênh khác nhau (Ví dụ: Kênh chung công ty, kênh riêng của phòng Dev, phòng Sales...).
- **Tích hợp AI dịch thuật:** Thêm một node AI (như OpenAI hoặc Claude) sau bước lấy quote để dịch câu nói tiếng Anh sang tiếng Việt cực kỳ mượt mà trước khi đẩy lên Slack.
- **Lưu trữ lịch sử:** Kết nối thêm một node Google Sheets để lưu lại danh sách những câu quote đã được gửi, tránh bị lặp lại trong tuần.

### 📌 Kết luận
Một workflow cực kỳ đơn giản, nhanh gọn nhưng lại mang lại giá trị tinh thần lớn cho văn hóa doanh nghiệp. Hãy "lên đồ" ngay cho hệ thống n8n của các sếp và tạo bất ngờ cho anh em đồng nghiệp vào sáng mai nhé!