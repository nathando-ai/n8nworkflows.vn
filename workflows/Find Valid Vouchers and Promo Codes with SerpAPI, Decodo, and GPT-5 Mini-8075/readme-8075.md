---
title: "🚀 Tìm kiếm mã giảm giá và voucher tự động với AI, SerpAPI và Decodo trong n8n"
description: "Hướng dẫn xây dựng workflow n8n sử dụng AI Agent kết hợp SerpAPI và Decodo để tự động săn và lọc mã giảm giá, voucher hoạt động tốt nhất cho bất kỳ trang web nào."
slug: "tim-kiem-ma-giam-gia-voucher-tu-dong-n8n-ai"
tags: [n8n, automation, no-code, ai-agent, serpapi, decodo, azure-openai]
keywords: [n8n workflow, săn mã giảm giá tự động, serpapi n8n, decodo scraper, ai agent voucher, azure openai n8n]
---

# 🚀 Tự động hóa tìm kiếm mã giảm giá và Voucher với AI Agent cực đỉnh

Các sếp có bao giờ mất hàng giờ đồng hồ lướt web, thử từng mã giảm giá "treo đầu dê bán thịt chó" mà không mã nào xài được khi mua sắm online không? Việc này cực kỳ mất thời gian và bực bội!

Hôm nay, em xin giới thiệu một giải pháp tự động hóa 100% không cần code bằng **n8n**: Workflow **"Find Valid Vouchers and Promo Codes with SerpAPI, Decodo, and GPT-5 Mini"** do tác giả *Khaisa Studio* phát triển. Trợ lý AI thông minh sẽ thay các sếp lùng sục khắp internet, cào dữ liệu và chắt lọc ra những chiếc mã giảm giá xịn sò và còn hoạt động tốt nhất!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian:** Không cần phải mất công tìm kiếm thủ công qua hàng chục trang web tổng hợp voucher rác.
- **Độ chính xác cao:** AI Agent kết hợp công cụ cào dữ liệu thông minh sẽ kiểm tra và lọc ra các mã mới nhất, còn hạn sử dụng.
- **Tương tác trực quan:** Nhắn tin trực tiếp qua giao diện chat để yêu cầu tìm mã cho bất kỳ thương hiệu, sản phẩm nào các sếp muốn.
- **Hoạt động linh hoạt:** Tích hợp bộ nhớ chat (Memory Buffer Window) giúp cuộc trò chuyện mạch lạc, dễ dàng tra cứu nối tiếp.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow này "lên đồ" mượt mà, các sếp cần chuẩn bị sẵn các tài khoản và API Key sau:
1. **SerpAPI:** Dùng để tìm kiếm thông tin mã giảm giá trên Google.
2. **Azure OpenAI (hoặc OpenAI tương đương):** Cung cấp mô hình ngôn ngữ (GPT-5 Mini / GPT-4o) làm "não" cho AI Agent.
3. **Decodo:** Dùng làm công cụ cào dữ liệu web (Scrapper) để bóc tách thông tin chi tiết từ các trang web voucher.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Các sếp tải file JSON của workflow (hoặc copy trực tiếp từ nguồn n8n.io/8075).
- Trong giao diện n8n Editor, chọn **Add workflow** > **Import from File** (hoặc nhấn `Ctrl+V` để paste trực tiếp vào màn hình canvas).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 6 nodes chính hoạt động nhịp nhàng với nhau. Các sếp cần cấu hình kỹ các phần sau:

- **Node `Message` (Chat Trigger):** Điểm khởi đầu cho phép các sếp nhập câu hỏi/yêu cầu tìm mã giảm giá. Không cần chỉnh sửa nhiều, giữ nguyên mặc định.
- **Node `Promo Seeker Agent` (Agent):** Trung tâm điều phối của workflow. Node này kết nối với Chat Model, Memory và các Tools để xử lý yêu cầu.
- **Node `Gpt 5 Mini` (Azure OpenAI API):**
  - Cần tạo credentials loại **Azure OpenAI API**.
  - Điền **API Key** và **Endpoint URL** lấy từ Azure Portal của các sếp.
  - Cấu hình thông số model là `gpt5mini` (hoặc model phù hợp theo tài khoản của các sếp).
- **Node `SerpAPI` (Tool SerpApi):**
  - Đăng ký tài khoản tại [SerpAPI](https://serpapi.com/) để lấy **API Key**.
  - Tạo credentials **SerpAPI** trong n8n và dán khóa vào.
- **Node `Decodo Scrapper` (Decodo Tool):**
  - Đăng ký tài khoản tại [Decodo](https://decodo.com/) để lấy **API Key** từ cài đặt tài khoản.
  - Tạo credentials **Decodo API** trong n8n và kết nối vào node này.
- **Node `Chat Memory` (Memory Buffer Window):** Giúp lưu giữ ngữ cảnh hội thoại, để AI nhớ các câu hỏi trước đó (ví dụ: "Tìm mã Shopee trước" -> "Còn mã cho Tiki thì sao?"). Giữ nguyên cấu hình mặc định.

#### 3. Kích hoạt ⚡️
- Nhấn nút **Chat with node** hoặc mở giao diện Chat Trigger để test thử bằng một câu lệnh đơn giản (Ví dụ: *"Tìm mã giảm giá Shopee mới nhất hôm nay"*).
- Kiểm tra xem AI có gọi SerpAPI và Decodo Scrapper để trả về kết quả chính xác không.
- Sau khi test ngon lành, gạt công tắc sang **Active** để chính thức đưa trợ lý vào hoạt động!

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp kênh chat nội bộ:** Thay vì chỉ chat trên giao diện n8n, các sếp có thể thay thế node `Chat Trigger` bằng **Telegram Trigger** hoặc **Slack Trigger** để săn voucher ngay trên app chat công việc.
- **Lưu lịch sử vào Google Sheets:** Nối thêm một nhánh phụ để lưu lại các mã giảm giá ngon ăn tìm được vào bảng tính Google Sheets nhằm chia sẻ cho đồng đội hoặc người thân cùng dùng.
- **Thông báo tự động:** Kết hợp thêm node gửi email hoặc tin nhắn Zalo/Telegram cá nhân mỗi khi có chiến dịch flash sale lớn cần tìm mã gấp.

### 📌 Kết luận
Với workflow tự động hóa này, việc săn sale và tìm voucher tiết kiệm chưa bao giờ dễ dàng đến thế. Hãy cài đặt ngay hôm nay để tối ưu hóa thời gian và chi phí mua sắm của các sếp nhé! Chúc các sếp thao tác thành công!