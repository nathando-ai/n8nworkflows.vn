---
title: "🤖 Tự Động Gửi Tin Tức AI MIT Vào Discord Mỗi Ngày (Không Trùng Lặp) - Deduplication 100%"
description: "Workflow tự động hóa lấy tin tức AI mới nhất từ MIT News, lọc ra những bài viết trong 24h, loại bỏ trùng lặp và gửi trực tiếp vào Discord mỗi sáng. Giúp các sếp tiết kiệm thời gian theo dõi tin tức hàng ngày và tránh spam."
slug: "tieu-dong-gui-tin-tuc-ai-mit-vao-discord"
tags: [n8n, automation, no-code, discord, rss-feed, deduplication, ai-news]
keywords: [n8n workflow tự động, gửi tin tức AI vào Discord, loại bỏ tin trùng lặp, tự động hóa tin tức hàng ngày, RSS feed MIT]
---

# 🚀 **Tự Động Gửi Tin Tức AI MIT Vào Discord Mỗi Ngày (Không Trùng Lặp)**

## **🔥 Nỗi Đau Của Các Sếp**
Bạn có phải là một nhà nghiên cứu, nhà phát triển AI, hoặc thành viên trong một nhóm công nghệ phải theo dõi liên tục các tin tức mới nhất về AI từ các nguồn uy tín như **MIT Technology Review**? Thì việc này không chỉ tốn thời gian mà còn dễ bị **trùng lặp tin tức** khi phải kiểm tra lại những bài đã đọc trước đó.

Với **workflow này**, các sếp sẽ:
✅ **Tự động lấy tin tức AI mới nhất** từ MIT News mỗi sáng.
✅ **Lọc ra những bài viết trong 24h** để đảm bảo tin tức mới nhất.
✅ **Loại bỏ trùng lặp 100%** bằng cách sử dụng **Data Table** của n8n.
✅ **Gửi tin tức vào Discord** một cách tự động, giúp nhóm không bỏ lỡ bất kỳ tin tức quan trọng nào.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không phải thủ công tìm kiếm và lọc tin tức hàng ngày.
- **Tin tức mới nhất**: Chỉ nhận những bài viết trong **24h**, không bị lỡ tin.
- **Không trùng lặp**: Hệ thống tự động kiểm tra và loại bỏ tin đã gửi trước đó.
- **Tích hợp Discord**: Tin tức được gửi trực tiếp vào kênh Discord của nhóm, dễ dàng theo dõi.
- **Hoạt động tự động**: Workflow chạy **mỗi ngày lúc 9h sáng** (có thể điều chỉnh).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Discord** và **Webhook URL** (để nhận tin tức tự động).
2. **n8n Self-hosted** (không dùng Cloud để đảm bảo ổn định 24/7).
3. **Thời gian ~5 phút** để cấu hình Data Table và kết nối các node.
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/11210](https://n8n.io/workflows/11210) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ link trên và **paste** vào **Import Workflow** trong n8n.

:::note[LƯU Ý]
- **Không chỉnh sửa JSON** nếu chưa hiểu rõ cấu trúc, chỉ cần import và chạy thử.
- Nếu dùng **n8n Cloud**, workflow có thể không hoạt động ổn định do giới hạn tài nguyên.
:::

---

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **8 node**, các sếp cần chú ý đến các bước sau:

##### **📌 Bước 1: Tạo Data Table (Trước Khi Import)**
- Mở **Data Tables** trong n8n Dashboard.
- Tạo một bảng mới tên **`mit_ai_news_sent`** với **4 cột**:
  - `creator` (String) → Để theo dõi người tạo (có thể bỏ trống).
  - `title` (String) → Tiêu đề bài viết.
  - `link` (String) → Link bài viết.
  - `pubDate` (Date) → Ngày đăng bài.

##### **📌 Bước 2: Kết Nối Data Table Vào Node "Avoid Duplicated Articles"**
- Mở node **"Avoid Duplicated Articles"** (loại `dataTable`).
- Chọn **`mit_ai_news_sent`** là Data Table để lưu trữ lịch sử tin tức đã gửi.

##### **📌 Bước 3: Cấu Hình Node "MIT AI Articles" (Discord Webhook)**
- Mở node **"MIT AI Articles"** (loại `discord`).
- Chọn **credentials** là `discordWebhookApi`.
- Điền **Webhook URL** từ Discord vào trường `Webhook URL`.
- **Thiết kế tin nhắn** (có thể chỉnh sửa template):
  ```json
  {
    "content": "📢 **Tin tức AI mới nhất từ MIT ({{ $json["title"] }})**\n\n{{ $json["link"] }}\n\n*Đăng ngày: {{ $json["pubDate"] }}*"
  }
  ```

##### **📌 Bước 4: Chỉnh Schedule Trigger (Nếu Cần)**
- Mở node **"Scheduled Daily Trigger"** (loại `scheduleTrigger`).
- **Thời gian mặc định**: 9h sáng (UTC).
- **Điều chỉnh theo múi giờ** của các sếp bằng cách nhấp đúp vào node và chọn **timezone** phù hợp.

##### **📌 Bước 5: Test Run & Bật Workflow**
- **Chạy thử (Test Run)** với dữ liệu mẫu để kiểm tra:
  - Tin tức có được lấy đúng không?
  - Có trùng lặp không?
  - Discord có nhận được tin nhắn không?
- **Bật Active** workflow sau khi kiểm tra thành công.

---

#### **3. Kích Hoạt ⚡️**
- **Test Run**: Chạy workflow một lần để đảm bảo tất cả node hoạt động.
- **Bật Active**: Sau khi kiểm tra, bật **Active** để workflow chạy tự động hàng ngày.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[CÁCH TIẾP CẬN THÊM]
1. **Thêm RSS Feed khác**:
   - Thay đổi URL trong node **"mit-artificial-intelligence (articles)"** (loại `rssFeedRead`) bằng RSS của **TechCrunch, Wired, ou AI Newsletter**.
2. **Lọc tin tức theo từ khóa**:
   - Thêm node **`If`** sau node **`Filter 24h`** để chỉ lấy tin tức chứa từ khóa như **"AI", "Machine Learning", "Deep Learning"**.
3. **Gửi tin tức qua Telegram/Email**:
   - Thay node **Discord** bằng **Telegram Bot** hoặc **Email** (n8n có node hỗ trợ).
4. **Lưu log tin tức**:
   - Thêm node **`Set`** để lưu thêm thông tin như **người nhận**, **thời gian gửi** vào Data Table.
5. **Báo cáo định kỳ**:
   - Thêm node **`ScheduleTrigger`** khác để gửi **tóm tắt tuần** về tin tức AI.
:::

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp cần theo dõi tin tức AI hàng ngày mà không bị **trùng lặp, tốn thời gian và mất tập trung**. Với **tự động hóa 100%**, các sếp chỉ cần **cấu hình một lần** và **quên đi việc theo dõi tin tức thủ công**.

👉 **Hãy import ngay và bắt đầu tự động hóa tin tức AI của mình!** 🚀

---
:::note[CHÚ Ý CUỐI CUNG]
- **N8n Self-hosted** là lựa chọn tối ưu để workflow hoạt động ổn định 24/7.
- **Nếu cần hỗ trợ**, các sếp có thể liên hệ với **Vasyl Pavlyuchok** (tác giả workflow) qua [LinkedIn](https://www.linkedin.com/in/vasyl-pavlyuchok/) hoặc [Email](mailto:vasyl@techbooster.io).
:::

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::