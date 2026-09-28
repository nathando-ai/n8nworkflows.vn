---
title: "🚀 Xây dựng ứng dụng tìm kiếm công thức nấu ăn tự động với n8n và API Ninjas"
description: "Hướng dẫn tạo ứng dụng tra cứu công thức nấu ăn tương tác thông qua Form và API Ninjas bằng n8n, giúp tiết kiệm thời gian và tự động hóa quy trình đơn giản."
slug: "tim-kiem-cong-thuc-nau-an-tu-dong-voi-n8n-api-ninjas"
tags: [n8n, automation, no-code, api-ninjas, productivity]
keywords: [n8n workflow, tim kiem cong thuc nau an, tu dong hoa n8n, api ninjas, form trigger n8n]
---

# 🚀 Xây dựng ứng dụng tìm kiếm công thức nấu ăn tự động với n8n và API Ninjas

Các sếp có bao giờ cảm thấy bối rối mỗi khi đến giờ nấu ăn mà không biết hôm nay phải làm món gì với những nguyên liệu đang có sẵn trong tủ lạnh? Việc tra cứu thủ công trên Google đôi khi mất thời gian lọc quảng cáo và tìm kiếm công thức chuẩn. 

Hôm nay, tui xin giới thiệu một workflow n8n cực kỳ gọn nhẹ nhưng vô cùng thú vị do **Milan Vasarhelyi (SmoothWork)** thiết kế. Workflow này giúp các sếp tạo ra một giao diện Form tương tác để nhập tên món ăn hoặc nguyên liệu, sau đó tự động gọi API để trả về công thức chi tiết ngay lập tức mà không cần viết một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tạo ứng dụng mini ngay trong n8n:** Tận dụng tính năng Form Trigger và Form Response để tạo trang web tương tác thu nhỏ.
- **Tự động hóa hoàn toàn:** Chỉ mất chưa đầy 2 giây từ lúc nhập nguyên liệu đến khi nhận được tên món, nguyên liệu và hướng dẫn nấu ăn chi tiết.
- **Tiết kiệm thời gian:** Không cần phải lướt web tìm kiếm thủ công, mọi thứ hiển thị trực quan ngay trên màn hình trình duyệt.
- **Dễ dàng mở rộng:** Có thể tích hợp thêm gửi email, lưu trữ vào Google Sheets hoặc gửi qua Telegram/Slack tùy ý.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản n8n:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **API Key từ API Ninjas:** Đăng ký tài khoản miễn phí tại [API Ninjas](https://api-ninjas.com/) để lấy khóa xác thực (API Key) cho dịch vụ Recipe API.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp chỉ cần copy đoạn mã JSON của workflow này, vào giao diện n8n Editor, chọn **New Workflow** -> Bấm tổ hợp phím `Ctrl + V` (hoặc `Cmd + V`) để dán trực tiếp lên canvas.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 3 node chính, các sếp cần chú ý cấu hình các phần sau:

- **Form Trigger - Recipe Finder (`formTrigger`):** Node này đóng vai trò là giao diện đầu vào. Các sếp có thể mở node này để xem cấu hình form, đảm bảo có trường `query` để người dùng nhập tên món ăn hoặc nguyên liệu. Sau khi active, n8n sẽ cung cấp một đường link URL công khai để truy cập form.
- **Fetch Recipe from API Ninjas (`httpRequest`):** Node này dùng để gọi dữ liệu từ API Ninjas. 
  - Thiết lập phương thức `GET` trỏ tới Endpoint của API Ninjas Recipe.
  - Cần tạo **Credentials** loại `httpHeaderAuth` với tên Header (ví dụ: `X-Api-Key`) và giá trị là API Key mà các sếp lấy từ trang API Ninjas.
  - Thêm tham số truy vấn (Query Parameter) truyền từ giá trị người dùng nhập ở Form (`query`).
- **Show Recipe Result (`form` - operation: completion):** Node này chịu trách nhiệm hiển thị kết quả trả về từ API (bao gồm Tiêu đề món ăn, Nguyên liệu, và Hướng dẫn thực hiện) thành một định dạng văn bản dễ đọc trực tiếp trên trang web của form.

#### 3. Kích hoạt ⚡️
- Bấm nút **Test workflow** và điền thử một nguyên liệu (ví dụ: *chicken pasta*) vào trang Form test để kiểm tra xem API có trả về kết quả chính xác không.
- Sau khi test thành công, bật công tắc **Active** ở góc trên bên phải để đưa ứng dụng vào hoạt động chính thức.

### ✍️ Mẹo & gợi ý nâng cao
Để ứng dụng "xịn xò" hơn nữa, các sếp hoàn toàn có thể mở rộng workflow này bằng cách:
1. **Lưu lịch sử tìm kiếm:** Thêm một node Google Sheets hoặc Airtable để lưu lại các món ăn mà người dùng đã tra cứu nhằm phân tích sở thích.
2. **Gửi kết quả qua Email/Telegram:** Tích hợp thêm node gửi email hoặc nhắn tin Telegram để người dùng có thể lưu công thức mang vào bếp xem trên điện thoại.
3. **Tích hợp AI:** Kết hợp thêm OpenAI/Claude Node để dịch công thức sang tiếng Việt chuẩn xác và hấp dẫn hơn trước khi trả về form hiển thị.

### 📌 Kết luận
Workflow "Find Recipes Using API Ninjas" là một ví dụ tuyệt vời cho thấy sức mạnh của n8n trong việc tạo ra các ứng dụng micro-tool nội bộ chỉ trong vòng 5 phút. Hãy tự tay thiết lập ngay hôm nay để có một trợ lý nấu ăn thông minh cho riêng mình hoặc đội ngũ nhé!