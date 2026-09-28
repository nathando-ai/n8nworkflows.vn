---
title: "🚀 Tự động hóa báo cáo lộ trình sản phẩm cạnh tranh với Gemini và Olostep trong n8n"
description: "Xây dựng phòng R&D tự động giúp phân tích đối thủ, xu hướng thị trường và tạo báo cáo chiến lược sản phẩm chuyên nghiệp gửi thẳng vào Google Drive và email."
slug: "tu-dong-hoa-bao-cao-lo-trinh-san-pham-gemini-olostep"
tags: [n8n, automation, ai, google-drive, gemini, olostep, product-management]
keywords: [n8n workflow, tu dong hoa lo trinh san pham, gemini flash, olostep scrape, google drive automation]
keywords: [n8n workflow, tự động hóa, phân tích đối thủ, product roadmap, ai automation]
---

# 🚀 Tự động hóa báo cáo lộ trình sản phẩm cạnh tranh với Gemini và Olostep

Chào các sếp! Việc đoán mò tính năng nào nên làm tiếp theo hay ngồi thủ công lướt web soi đối thủ đang làm tốn rất nhiều thời gian của Product Manager và Founder. Workflow **Competitive Roadmap & Trend Arbitrage** này sinh ra để đóng vai trò như một phòng R&D tự động hóa 100%. 

Hệ thống sẽ so sánh năng lực sản phẩm hiện tại của các sếp với dữ liệu thị trường thời gian thực, các bản cập nhật của đối thủ và xu hướng vĩ mô để tìm ra các cơ hội "White Space" (Khoảng trống thị trường) — những tính năng giá trị cao mà chưa ai làm. Nhờ sức mạnh của **Gemini 2.5 Flash** và **Olostep**, mọi dữ liệu thô được chuyển hóa thành một "Báo cáo Tình báo Chiến lược" hoàn chỉnh với các đề xuất hành động cụ thể.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian nghiên cứu:** Không còn phải tự tay tổng hợp báo cáo thị trường và soi tính năng đối thủ.
- **Chiến lược dựa trên dữ liệu thật:** AI phân tích sâu các khoảng trống thị trường (Gap Analysis) và xu hướng vĩ mô thông qua Olostep và Gemini.
- **Báo cáo chuyên nghiệp tự động:** Tự động tạo Google Docs chuẩn chỉnh, chia sẻ quyền và gửi link trực tiếp qua email cho các bên liên quan.
- **Hoạt động liên tục 24/7:** Kích hoạt mọi lúc qua Web Form đơn giản mỗi khi cần nghiên cứu ngách sản phẩm mới.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow chạy mượt mà, các sếp cần chuẩn bị sẵn:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Google Gemini API Key**: Dành cho các node phân tích chiến lược và biên tập báo cáo.
- **Olostep API**: Dành cho việc cào dữ liệu web, xu hướng thị trường và tính năng đối thủ.
- **Google Drive Credentials (OAuth2)**: Dành cho việc tạo, chuyển đổi, chia sẻ và xóa file HTML tạm thời.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần tải file JSON của workflow này, vào giao diện n8n chọn **Add workflow** -> **Import from File** (hoặc copy toàn bộ JSON và dán trực tiếp vào Editor).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 11 nodes được thiết kế mạch lạc. Các sếp cần chú ý cấu hình kỹ các điểm sau:
- **On form submission**: Node này tạo một Form đầu vào. Các sếp chạy thử để lấy link form thu thập dữ liệu (Ngành nghề, Đối thủ hàng đầu, và Danh sách tính năng hiện tại của sếp).
- **Research (Olostep API)**: Kết nối tài khoản Olostep để hệ thống tự động cào các xu hướng ngành, tính năng mới của đối thủ và nỗi đau của khách hàng.
- **Analyze and compare research data**, **Product strategist**, **Report editor (Google Gemini)**: Chọn đúng credentials `googlePalmApi` và kiểm tra kỹ các câu lệnh Prompt (đã được tối ưu sẵn) để đảm bảo AI phân tích đúng trọng tâm sản phẩm của các sếp.
- **Transfer HTML to Doc**, **Share link & email**, **Upload html file**, **Delete html file**: Kết nối tài khoản Google Drive OAuth2. Đảm bảo cấu hình đúng email nhận thông báo trong node **Share link & email**.

#### 3. Kích hoạt ⚡️
- Điền thử một vài thông tin mẫu vào Form đầu vào và bấm **Execute Workflow** để kiểm tra toàn bộ luồng chạy.
- Kiểm tra email xem Google Docs đã được tạo và chia sẻ thành công chưa.
- Sau khi test ngon lành, hãy gạt công tắc **Active** góc trên cùng bên phải để đưa workflow vào hoạt động chính thức.

### ✍️ Mẹo & gợi ý nâng cao
- **Đa dạng hóa đối thủ:** Nhân bản node **Research** để cào dữ liệu từ nhiều đối thủ cùng lúc, giúp góc nhìn thị trường toàn diện hơn.
- **Tích hợp khung chiến lược riêng:** Tùy chỉnh prompt trong node Gemini để áp dụng các mô hình chiến lược quen thuộc như SWOT, Blue Ocean Strategy hoặc Jobs-to-be-Done (JTBD).
- **Tự động hóa Backlog:** Kết hợp nối tiếp workflow này với **Jira**, **Linear**, hoặc **Productboard** để tự động đẩy các tính năng "Catch-Up" hoặc "Leapfrog" trực tiếp vào danh sách công việc của đội ngũ engineering.

### 📌 Kết luận
Workflow **Competitive Roadmap & Trend Arbitrage** là trợ thủ đắc lực giúp các Product Manager và Founder nắm thế chủ động trên thị trường mà không cần tốn hàng tuần nghiên cứu thủ công. Hãy triển khai ngay hôm nay để tối ưu hóa quy trình R&D của doanh nghiệp các sếp nhé!