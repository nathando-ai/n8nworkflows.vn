---
title: "🚀 Tạo công thức nấu ăn tự động từ ảnh tủ lạnh bằng GPT-4 Vision & Telegram trong n8n"
description: "Hướng dẫn xây dựng trợ lý nấu ăn AI trên Telegram: chụp ảnh tủ lạnh hoặc nhắn nguyên liệu, AI tự động quét và gợi ý thực đơn chi tiết 100% tự động."
slug: "tao-cong-thuc-nau-an-tu-dong-tu-anh-tu-lanh-telegram-gpt4"
tags: [n8n, automation, no-code, ai-agent, telegram, openrouter, gpt-4-vision]
keywords: [n8n workflow, tao cong thuc nau an ai, telegram bot ai, gpt-4 vision, tu dong hoa n8n, openrouter api]
---

# 🚀 Trợ lý nấu ăn AI thông minh: Biến ảnh tủ lạnh thành công thức món ngon qua Telegram

Các sếp có bao giờ rơi vào cảnh mở tủ lạnh ra nhìn một đống nguyên liệu "còn gì nấu nấy" nhưng chẳng biết nấu món gì chưa? Việc nghĩ thực đơn mỗi ngày vừa tốn thời gian, vừa dễ lãng phí thực phẩm. 

Đừng lo, bài viết này sẽ hướng dẫn các sếp triển khai một workflow n8n cực kỳ xịn sò được thiết kế bởi **Yusuke Yamamoto**. Workflow này cho phép các sếp (hoặc khách hàng) chỉ cần **chụp ảnh tủ lạnh gửi vào Telegram** (hoặc nhắn tên nguyên liệu), AI sẽ tự động phân tích và trả về ngay 3 công thức nấu ăn chi tiết, chuẩn đầu bếp mà không cần viết một dòng code nào!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Nhận diện hình ảnh đỉnh cao**: Dùng GPT-4 Vision để "nhìn" và đọc tên các nguyên liệu có trong ảnh chụp tủ lạnh hoặc kệ bếp.
- **Linh hoạt đầu vào**: Hỗ trợ cả 2 hình thức: Gửi ảnh (Vision AI) hoặc nhắn tin chữ thủ công (Text input).
- **Công thức chuẩn đầu bếp**: AI đóng vai trò chef chuyên nghiệp, sáng tạo 3 món ăn chi tiết, có định mức và hướng dẫn rõ ràng.
- **Phản hồi tức thì qua Telegram**: Giao diện trả về cực kỳ bắt mắt, nhiều emoji, dễ đọc ngay trên điện thoại.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance**: Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Telegram Bot Token**: Tạo bot thông qua `@BotFather` trên Telegram để nhận trigger và gửi tin nhắn.
- **OpenRouter API Key**: Tài khoản OpenRouter để sử dụng các mô hình AI đỉnh cao (`openai/gpt-4-vision-preview` và `openai/gpt-4o-mini`) với chi phí tối ưu.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể sử dụng file JSON của workflow này, copy mã JSON từ n8n và paste trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm 12 nodes được chia thành 4 giai đoạn rõ rệt. Các sếp cần cấu hình chính xác các điểm sau:

- **Telegram Trigger**: 
  - Kết nối với `Telegram Bot Credentials` của các sếp.
  - Node này sẽ lắng nghe sự kiện người dùng gửi tin nhắn hoặc hình ảnh tới Bot.

- **Check Input Type (IF Node)**: 
  - Node này đóng vai trò phân luồng thông minh. Nó kiểm tra xem tin nhắn có chứa text không. Nếu không (nghĩa là gửi ảnh), nó sẽ đẩy sang nhánh **AI Vision Agent** phía trên.

- **OpenAI Vision Model & OpenAI Recipe Model (lmChatOpenRouter)**:
  - Cấu hình credentials với `OpenRouter API`.
  - Node `AI Vision Vision` sử dụng model: `openai/gpt-4-vision-preview` để quét ảnh nguyên liệu.
  - Node `Recipe Generator` sử dụng model: `openai/gpt-4o-mini` để viết công thức tiết kiệm và nhanh chóng.

- **Ingredient Parser & Recipe Parser (Output Parser Structured)**:
  - Các node này ép kiểu dữ liệu đầu ra của AI về dạng JSON chuẩn (có cấu trúc rõ ràng gồm tên món, độ khó, nguyên liệu, cách làm...), giúp các bước sau xử lý mượt mà, không sợ lỗi định dạng.

- **Send a text message (Telegram)**:
  - Kết nối lại với `Telegram Bot Credentials` để gửi chuỗi kết quả đã được format đẹp mắt (`Format Response`) về đúng chat ID của người dùng.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và gửi một bức ảnh tủ lạnh (hoặc nhắn "thịt bò, khoai tây") vào Bot Telegram của các sếp để test thực tế.
- Nếu mọi thứ trả về ngon nghẻ, hãy bật công tắc **Active** góc trên cùng bên phải để bot chạy 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Lưu lịch sử món ăn**: Nối thêm node **Google Sheets** hoặc **Notion** sau bước `Format Response` để lưu lại những món ăn đã nấu, giúp theo dõi dinh dưỡng hàng tuần.
- **Tích hợp thêm thông báo nhóm**: Thêm node **Slack** hoặc **Discord** nếu muốn chia sẻ thực phẩm/món ăn vui vẻ với các thành viên trong gia đình hoặc văn phòng.
- **Tối ưu chi phí AI**: Có thể thay thế các model OpenRouter bằng các model open-source chạy qua Ollama nếu các sếp tự host phần cứng riêng.

### 📌 Kết luận
Chỉ với vài bước cấu hình đơn giản trên n8n, các sếp đã sở hữu ngay một trợ lý AI nấu ăn cá nhân cực kỳ thông minh ngay trên Telegram. Triển khai ngay để cuộc sống bếp núc trở nên thú vị và bớt đau đầu mỗi khi mở tủ lạnh nhé các sếp!