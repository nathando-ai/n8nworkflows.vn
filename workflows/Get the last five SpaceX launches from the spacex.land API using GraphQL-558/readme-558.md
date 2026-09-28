---
title: "🚀 Tự động lấy thông tin 5 lần phóng tên lửa SpaceX gần nhất với GraphQL và n8n"
description: "Hướng dẫn cách sử dụng n8n kết hợp GraphQL để truy xuất dữ liệu thời gian thực từ API SpaceX, giúp bạn tự động hóa việc lấy thông tin các sự kiện phóng tên lửa một cách nhanh chóng."
slug: "lay-thong-tin-spacex-bang-graphql-trong-n8n"
tags: [n8n, automation, no-code, graphql, spacex, api]
keywords: [n8n workflow, graphql trong n8n, gọi api spacex, tự động hóa n8n, api integration]
---

# 🚀 Tự động lấy thông tin 5 lần phóng tên lửa SpaceX gần nhất qua GraphQL

Các sếp có bao giờ cần tích hợp dữ liệu từ một nguồn bên thứ ba sử dụng **GraphQL** nhưng lại ngại việc viết code phức tạp chưa? Việc gọi API theo cách thủ công vừa tốn thời gian, vừa khó kiểm soát dữ liệu trả về, đặc biệt khi cần lọc chính xác các thông tin như các lần phóng tên lửa mới nhất của SpaceX. 

Với workflow n8n này, các sếp sẽ sở hữu một giải pháp tự động hóa 100% không cần code (no-code), giúp kết nối trực tiếp với GraphQL API của SpaceX và lấy ra chính xác 5 lần phóng gần đây nhất chỉ trong tích tắc!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian:** Không cần viết mã lệnh phức tạp để gọi GraphQL, chỉ cần cấu hình trực quan trong n8n.
- **Dữ liệu chính xác:** Lọc đúng thông tin 5 lần phóng tên lửa SpaceX gần nhất (tên, ngày phóng, trạng thái...) mà không bị nhiễu dữ liệu thừa.
- **Linh hoạt tích hợp:** Dữ liệu thu về có thể dễ dàng chuyển tiếp sang Google Sheets, Telegram, Slack hoặc gửi email thông báo.
- **Hoạt động linh hoạt:** Có thể kích hoạt thủ công (Manual Trigger) hoặc chuyển đổi sang Cron/Webhook để chạy tự động định kỳ.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Hệ thống n8n:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **GraphQL Endpoint:** Sử dụng sẵn public API của SpaceX (`https://spacex-production.up.railway.app/` hoặc tương tự tùy cấu hình). Không yêu cầu API Key phức tạp.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể tạo một workflow mới trong n8n, sau đó copy đoạn JSON của workflow (hoặc tải file JSON từ thư viện n8n) và dán trực tiếp vào giao diện n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này cực kỳ gọn nhẹ với chỉ 2 nodes chính:
- **Node `On clicking 'execute'` (Manual Trigger):** Dùng để kích hoạt chạy thử bằng tay. Các sếp có thể thay thế node này bằng *Schedule Trigger* nếu muốn n8n tự động lấy dữ liệu theo giờ/ngày.
- **Node `GraphQL`:** 
  - Cấu hình URL endpoint của SpaceX GraphQL API.
  - Viết câu truy vấn (Query) GraphQL để lấy giới hạn 5 lần phóng (`limit: 5`). Ví dụ cấu trúc query cơ bản:
    ```graphql
    {
      launchesPast(limit: 5) {
        mission_name
        launch_date_utc
        rocket {
          rocket_name
        }
      }
    }
    ```
  - Kiểm tra lại kết quả trả về bằng cách nhấn nút **Test step** trong n8n để đảm bảo dữ liệu hiển thị chính xác.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** để kiểm tra dữ liệu trả về từ API SpaceX.
- Sau khi kiểm tra mọi thứ hoạt động trơn tru, hãy bật công tắc **Active** ở góc trên bên phải để workflow sẵn sàng vận hành.

### ✍️ Mẹo & gợi ý nâng cao
Để mở rộng workflow này cho các chiến dịch thực tế, các sếp có thể:
1. **Gửi thông báo về Telegram/Slack:** Thêm một node Telegram sau node GraphQL để bắn tin nhắn mỗi khi có dữ liệu phóng tên lửa mới.
2. **Lưu trữ tự động:** Kết nối thêm node **Google Sheets** hoặc **Airtable** để lưu lại danh sách các lần phóng vào bảng quản lý.
3. **Chạy định kỳ:** Thay thế Manual Trigger bằng *Schedule Trigger* (ví dụ: chạy vào thứ Hai hàng tuần) để cập nhật thông tin tự động mà không cần can thiệp thủ công.

### 📌 Kết luận
Một workflow siêu gọn nhẹ nhưng cực kỳ mạnh mẽ để làm quen với việc gọi GraphQL API trong n8n. Hãy áp dụng ngay vào hệ thống của các sếp để tối ưu hóa việc thu thập và xử lý dữ liệu từ các nguồn bên ngoài!