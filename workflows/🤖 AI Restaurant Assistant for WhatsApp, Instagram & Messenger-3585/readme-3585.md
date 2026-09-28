```yaml
---
title: "🤖 AI Restaurant Assistant cho WhatsApp, Instagram & Messenger - Tự động hóa hoàn toàn"
description: "Workflow n8n này giúp tự động hóa tương tác khách hàng trên các nền tảng tin nhắn phổ biến, tích hợp AI để xử lý đơn hàng, thanh toán và hỗ trợ khách hàng 24/7 mà không cần can thiệp thủ công."
slug: "ai-restaurant-assistant-whatsapp-instagram-messenger"
tags: [n8n, automation, ai, restaurant, customer-service]
keywords: [n8n workflow, tự động hóa nhà hàng, chatbot AI, xử lý đơn hàng tự động, tích hợp WhatsApp, Instagram Messenger]
---
```

# 🤖 AI Restaurant Assistant cho WhatsApp, Instagram & Messenger

[Đoạn mở đầu: Phân tích nỗi đau thực tế của doanh nghiệp/người dùng khi làm thủ công. Giới thiệu workflow như giải pháp tự động hóa 100% không cần code.]

Nhà hàng và quán ăn luôn phải đối mặt với thách thức lớn về quản lý đơn hàng và tương tác khách hàng. Với lượng khách hàng ngày càng tăng, việc xử lý từng yêu cầu một cách thủ công không chỉ tốn thời gian mà còn dễ gây lỗi và làm mất đi trải nghiệm khách hàng.

Workflow này mang đến giải pháp toàn diện cho các nhà hàng và quán ăn, giúp tự động hóa hoàn toàn quy trình tương tác với khách hàng trên các nền tảng tin nhắn phổ biến như WhatsApp, Instagram và Messenger. Bằng cách tích hợp công nghệ trí tuệ nhân tạo (AI), workflow này có thể xử lý đơn hàng, thanh toán và hỗ trợ khách hàng 24/7 mà không cần can thiệp thủ công.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- Tiết kiệm thời gian xử lý đơn hàng lên đến 80%
- Tăng trải nghiệm khách hàng với phản hồi tức thì
- Giảm thiểu lỗi trong quá trình xử lý đơn hàng
- Tự động hóa quy trình thanh toán và quản lý khách hàng
- Hỗ trợ khách hàng 24/7 mà không cần nhân viên trực tiếp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản OpenAI để sử dụng các tính năng AI
- Tài khoản Supabase để lưu trữ dữ liệu và lịch sử trò chuyện
- Tài khoản Google Drive để lưu trữ và quản lý tài liệu
- Tài khoản Evolution API để tích hợp với WhatsApp
- Tài khoản Asaas để xử lý thanh toán
- Tài khoản Mapbox để tính toán khoảng cách và địa chỉ
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Để import workflow này vào n8n, các sếp có thể làm theo các bước sau:

1. Truy cập vào trang web của n8n và đăng nhập vào tài khoản của mình.
2. Nhấp vào nút "Import" ở góc trên bên phải của màn hình.
3. Chọn tùy chọn "Import from URL" và nhập URL của workflow này.
4. Nhấp vào nút "Import" để bắt đầu quá trình import.

Hoặc, các sếp cũng có thể sao chép và dán JSON của workflow vào n8n Editor.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Phân tích cụ thể các node quan trọng cần cấu hình trong workflow:

- **Variaveis**: Node này được sử dụng để lưu trữ các biến toàn cục trong workflow.
- **Data&Hora**: Node này được sử dụng để lấy ngày và giờ hiện tại.
- **Converter Img**: Node này được sử dụng để chuyển đổi hình ảnh.
- **Maps**: Node này được sử dụng để ánh xạ dữ liệu.
- **TranscAudio**: Node này được sử dụng để chuyển đổi âm thanh.
- **MsgType**: Node này được sử dụng để xác định loại tin nhắn.
- **Aguarda**: Node này được sử dụng để chờ đợi một khoảng thời gian.
- **CalculoTime**: Node này được sử dụng để tính toán thời gian.
- **JSONhistorico1**: Node này được sử dụng để lưu trữ lịch sử trò chuyện.
- **Prompt**: Node này được sử dụng để lưu trữ các prompt cho AI.
- **Converte PDF**: Node này được sử dụng để chuyển đổi tệp PDF.
- **Extract PDF**: Node này được sử dụng để trích xuất văn bản từ tệp PDF.
- **Maps5**: Node này được sử dụng để ánh xạ dữ liệu.
- **Calculator**: Node này được sử dụng để tính toán.
- **Modelo IA**: Node này được sử dụng để tương tác với AI.
- **OpenAI2**: Node này được sử dụng để tương tác với AI.
- **Segmentos**: Node này được sử dụng để phân đoạn dữ liệu.
- **1,2s**: Node này được sử dụng để chờ đợi một khoảng thời gian.
- **Loop Over Items1**: Node này được sử dụng để lặp qua các mục.
- **no.op2**: Node này được sử dụng để không thực hiện bất kỳ hành động nào.
- **OutputParser**: Node này được sử dụng để phân tích đầu ra.
- **JSONhistorico**: Node này được sử dụng để lưu trữ lịch sử trò chuyện.
- **Filtro Reset**: Node này được sử dụng để lọc dữ liệu.
- **JSONhistorico2**: Node này được sử dụng để lưu trữ lịch sử trò chuyện.
- **Interferencia**: Node này được sử dụng để xử lý xung đột.
- **Desbloqueia IA**: Node này được sử dụng để mở khóa AI.
- **Bloquear IA**: Node này được sử dụng để khóa AI.
- **Desbloquear IA**: Node này được sử dụng để mở khóa AI.
- **SalvaHistorico1**: Node này được sử dụng để lưu trữ lịch sử trò chuyện.
- **Add Timeout**: Node này được sử dụng để thêm thời gian chờ.
- **Busca Timeout**: Node này được sử dụng để tìm kiếm thời gian chờ.
- **SalvaHistorico**: Node này được sử dụng để lưu trữ lịch sử trò chuyện.
- **Postgres Memory**: Node này được sử dụng để lưu trữ dữ liệu trong cơ sở dữ liệu PostgreSQL.
- **WH Asaas**: Node này được sử dụng để tương tác với API Asaas.
- **Response Asaas**: Node này được sử dụng để xử lý phản hồi từ API Asaas.
- **get_consumer**: Node này được sử dụng để lấy thông tin khách hàng.
- **up_consumer**: Node này được sử dụng để cập nhật thông tin khách hàng.
- **Criar Cliente**: Node này được sử dụng để tạo khách hàng mới.
- **Criar Cobrança**: Node này được sử dụng để tạo hóa đơn mới.
- **Add Link**: Node này được sử dụng để thêm liên kết.
- **PhoneID**: Node này được sử dụng để phân tích số điện thoại.
- **Sem Dados**: Node này được sử dụng để xử lý trường hợp không có dữ liệu.
- **Asaas Erro**: Node này được sử dụng để xử lý lỗi từ API Asaas.
- **Asaas Erro1**: Node này được sử dụng để xử lý lỗi từ API Asaas.
- **Asaas Erro2**: Node này được sử dụng để xử lý lỗi từ API Asaas.
- **checar_cpf**: Node này được sử dụng để kiểm tra số CPF.
- **START**: Node này được sử dụng để bắt đầu workflow.
- **up_dados**: Node này được sử dụng để cập nhật dữ liệu.
- **Img Instagram**: Node này được sử dụng để xử lý hình ảnh trên Instagram.
- **Img WhatsApp**: Node này được sử dụng để xử lý hình ảnh trên WhatsApp.
- **Maps6**: Node này được sử dụng để ánh xạ dữ liệu.
- **Convert File Wp**: Node này được sử dụng để chuyển đổi tệp trên WhatsApp.
- **Add Response**: Node này được sử dụng để thêm phản hồi.
- **Filter WhatsApp**: Node này được sử dụng để lọc dữ liệu trên WhatsApp.
- **Reply Message Insta**: Node này được sử dụng để trả lời tin nhắn trên Instagram.
- **Reply Message Wp**: Node này được sử dụng để trả lời tin nhắn trên WhatsApp.
- **Fixed Credentials**: Node này được sử dụng để lưu trữ thông tin đăng nhập cố định.
- **Get Reply Insta**: Node này được sử dụng để lấy phản hồi từ Instagram.
- **Message Markup Wp**: Node này được sử dụng để đánh dấu tin nhắn trên WhatsApp.
- **No Marking**: Node này được sử dụng để không đánh dấu tin nhắn.
- **Message Markup Insta**: Node này được sử dụng để đánh dấu tin nhắn trên Instagram.
- **Response Refined**: Node này được sử dụng để tinh chỉnh phản hồi.
- **Filter Insta&Face**: Node này được sử dụng để lọc dữ liệu trên Instagram và Facebook.
- **Get Reply Facebook**: Node này được sử dụng để lấy phản hồi từ Facebook.
- **Channel**: Node này được sử dụng để xác định kênh.
- **Message Markup Face**: Node này được sử dụng để đánh dấu tin nhắn trên Facebook.
- **Block IA**: Node này được sử dụng để khóa AI.
- **MapTextHuman**: Node này được sử dụng để ánh xạ văn bản từ con người.
- **Lead Search**: Node này được sử dụng để tìm kiếm khách hàng tiềm năng.
- **Lead Found**: Node này được sử dụng để xử lý trường hợp tìm thấy khách hàng tiềm năng.
- **Waiting**: Node này được sử dụng để chờ đợi.
- **Register New Lead**: Node này được sử dụng để đăng ký khách hàng tiềm năng mới.
- **Text Wrap**: Node này được sử dụng để bọc văn bản.
- **Send Instagram**: Node này được sử dụng để gửi tin nhắn trên Instagram.
- **Send Facebook**: Node này được sử dụng để gửi tin nhắn trên Facebook.
- **Get Audio WpAPI**: Node này được sử dụng để lấy âm thanh từ API WhatsApp.
- **Send Evolution**: Node này được sử dụng để gửi tin nhắn thông qua Evolution API.
- **Send WhatsApp**: Node này được sử dụng để gửi tin nhắn trên WhatsApp.
- **Bloqueio de IA**: Node này được sử dụng để khóa AI.
- **Best Agent AI**: Node này được sử dụng để chọn AI tốt nhất.
- **Respond to Webhook**: Node này được sử dụng để xử lý webhook.
- **Send via Evolution**: Node này được sử dụng để gửi tin nhắn thông qua Evolution API.
- **Send via Instagram**: Node này được sử dụng để gửi tin nhắn trên Instagram.
- **Send via Face**: Node này được sử dụng để gửi tin nhắn trên Facebook.
- **Send via WAAPI**: Node này được sử dụng để gửi tin nhắn thông qua API WhatsApp.
- **reagir_waapi**: Node này được sử dụng để phản hồi thông qua API WhatsApp.
- **origem**: Node này được sử dụng để xác định nguồn gốc.
- **FromMe WhatsApp**: Node này được sử dụng để xác định tin nhắn từ mình trên WhatsApp.
- **FromMe Insta&Face&Wp**: Node này được sử dụng để xác định tin nhắn từ mình trên Instagram, Facebook và WhatsApp.
- **FromMe Insta&Face**: Node này được sử dụng để xác định tin nhắn từ mình trên Instagram và Facebook.
- **reagir_evo**: Node này được sử dụng để phản hồi thông qua Evolution API.
- **update_name**: Node này được sử dụng để cập nhật tên.
- **create_payment**: Node này được sử dụng để tạo thanh toán.
- **n8n**: Node này được sử dụng để tương tác với n8n.
- **n8n1**: Node này được sử dụng để tương tác với n8n.
- **No Operation1**: Node này được sử dụng để không thực hiện bất kỳ hành động nào.
- **Start Deletion**: Node này được sử dụng để bắt đầu quá trình xóa.
- **Down Audio WpAPI**: Node này được sử dụng để tải xuống âm thanh từ API WhatsApp.
- **Down Audio Insta&Face**: Node này được sử dụng để tải xuống âm thanh từ Instagram và Facebook.
- **MapAudioEvo**: Node này được sử dụng để ánh xạ âm thanh thông qua Evolution API.
- **Down Img Insta&Face**: Node này được sử dụng để tải xuống hình ảnh từ Instagram và Facebook.
- **Code4**: Node này được sử dụng để thực thi mã.
- **Code Resposta**: Node này được sử dụng để thực thi mã phản hồi.
- **Se Erro**: Node này được sử dụng để xử lý lỗi.
- **Response Address Sucess**: Node này được sử dụng để xử lý địa chỉ thành công.
- **Response Address Error**: Node này được sử dụng để xử lý lỗi địa chỉ.
- **Mapbox Cliente**: Node này được sử dụng để tương tác với Mapbox.
- **Mapbox Distancia**: Node này được sử dụng để tính toán khoảng cách trên Mapbox.
- **Apontamentos**: Node này được sử dụng để lưu trữ các ghi chú.
- **TriggerMapbox**: Node này được sử dụng để kích hoạt Mapbox.
- **CalculateDelivery**: Node này được sử dụng để tính toán thời gian giao hàng.
- **CPF exist**: Node này được sử dụng để kiểm tra sự tồn tại của CPF.
- **RespondCPF2**: Node này được sử dụng để xử lý phản hồi CPF.
- **RespondCPF3**: Node này được sử dụng để xử lý phản hồi CPF.
- **checar_cep**: Node này được sử dụng để kiểm tra mã bưu điện.
- **send_img_wp**: Node này được sử dụng để gửi hình ảnh trên WhatsApp.
- **send_img_evo**: Node này được sử dụng để gửi hình ảnh thông qua Evolution API.
- **Send Images**: Node này được sử dụng để gửi hình ảnh.
- **Evolution Imagem**: Node này được sử dụng để xử lý hình ảnh thông qua Evolution API.
- **Set Field Evo**: Node này được sử dụng để đặt trường trong Evolution API.
- **Response Img**: Node này được sử dụng để xử lý phản hồi hình ảnh.
- **Response Img Erro**: Node này được sử dụng để xử lý lỗi hình ảnh.
- **Wait**: Node này được sử dụng để chờ đợi.
- **AI Agent Products**: Node này được sử dụng để tương tác với AI để xử lý sản phẩm.
- **Model20**: Node này được sử dụng để tương tác với AI.
- **Calculator1**: Node này được sử dụng để tính toán.
- **Check Bebidas**: Node này được sử dụng để kiểm tra đồ uống.
- **consulta_bebidas**: Node này được sử dụng để truy vấn đồ uống.
- **Respond Bebida**: Node này được sử dụng để xử lý phản hồi đồ uống.
- **Checa CEP**: Node này được sử dụng để kiểm tra