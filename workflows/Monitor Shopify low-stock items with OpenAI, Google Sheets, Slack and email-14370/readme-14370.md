---
title: "🚀 Tự động giám sát tồn kho Shopify sắp hết với OpenAI, Google Sheets, Slack và Email"
description: "Hướng dẫn xây dựng workflow n8n tự động kiểm tra tồn kho Shopify mỗi 5 giờ, dùng AI viết thông báo, lưu lịch sử vào Google Sheets và gửi cảnh báo thông minh qua Slack/Email."
slug: "tu-dong-giam-sat-ton-kho-shopify-openai-google-sheets-slack"
tags: [n8n, automation, shopify, openai, google-sheets, slack]
keywords: [n8n workflow, shopify low stock alert, tu dong hoa ton kho, openai n8n, quan ly ton kho shopify]
---

# 🚀 Tự động giám sát tồn kho Shopify sắp hết với OpenAI, Google Sheets, Slack và Email

Các sếp đang kinh doanh trên Shopify có bao giờ rơi vào cảnh sản phẩm "cháy hàng" mà quên nhập thêm, hay nhân viên kho bỏ sót các mặt hàng sắp cạn kho vì phải kiểm tra thủ công hàng ngày? Việc để khách đặt hàng rồi mới phát hiện hết hàng sẽ làm giảm nghiêm trọng trải nghiệm khách hàng và uy tín cửa hàng.

Giải pháp là đây! Workflow n8n này sẽ tự động hóa toàn bộ quy trình: từ việc quét kho Shopify định kỳ, lọc ra các sản phẩm sắp hết, nhờ AI (OpenAI) viết thông điệp cảnh báo chuyên nghiệp, đồng bộ dữ liệu vào Google Sheets để tracking, phân loại mức độ ưu tiên và bắn thông báo ngay lập tức qua Slack/Email cho các sếp. Hoàn toàn tự động 100%, không tốn một phút làm tay!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Không bao giờ bỏ lỡ hàng tồn:** Hệ thống tự quét kho mỗi 5 giờ một lần, bắt trọn mọi sản phẩm có lượng tồn kho dưới ngưỡng an toàn (<= 10 sản phẩm).
- **Cảnh báo thông minh bằng AI:** Sử dụng OpenAI (GPT-4o-mini) để soạn thảo thông báo chi tiết, rõ ràng kèm theo SKU, tên sản phẩm và số lượng tồn.
- **Quản lý tập trung trên Google Sheets:** Tự động kiểm tra bản ghi cũ, tự động thêm mới hoặc cập nhật dòng hiện có mà không bị trùng lặp dữ liệu (duplicate).
- **Phân loại ưu tiên & Điều hướng thông minh:** Phân chia rõ ràng mức độ (High, Medium, Low) để team xử lý đúng việc, đúng trọng tâm qua Slack và Email.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Trước khi "lên đồ", các sếp cần chuẩn bị sẵn các tài khoản và kết nối sau:
- **Tài khoản n8n** (Cloud hoặc Self-hosted).
- **Shopify Account**: Lấy Shopify Access Token/API Credentials để n8n đọc dữ liệu sản phẩm.
- **OpenAI API Key**: Dùng cho node AI tạo nội dung cảnh báo.
- **Google Sheets**: Tạo sẵn một file Google Sheet để lưu log cảnh báo tồn kho.
- **Slack Workspace & Gmail Account**: Nơi nhận các thông báo cảnh báo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã JSON của workflow này từ nguồn gốc, sau đó vào giao diện n8n Editor, chọn **Add workflow** -> Click vào dấu ba chấm (...) ở góc trên bên phải -> Chọn **Import from File / Clipboard** và dán đoạn JSON vào là xong.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import thành công, các sếp cần cấu hình lại các node sau cho khớp với hệ thống của mình:
- **Trigger in Schedule time**: Mặc định chạy mỗi 5 giờ. Các sếp có thể đổi tần suất chạy tùy theo nhu cầu thực tế của cửa hàng.
- **Fetch Products (Shopify)**: Chọn `credentials` là tài khoản Shopify Access Token của các sếp để hệ thống có quyền đọc danh sách sản phẩm.
- **AI text genrator (OpenAI)** & **Genrate Alert Message (ChainLLM)**: Kết nối OpenAI API Key và chọn model mong muốn (khuyến nghị `gpt-4.1-mini` hoặc `gpt-4o-mini` cho tốc độ nhanh và chi phí tối ưu).
- **Check existing records**, **Add product alert to sheet**, **Update existing alert in sheet (Google Sheets)**: Kết nối tài khoản Google Sheets OAuth2, chọn đúng file Sheet và Sheet Name dùng để tracking tồn kho.
- **Send slack alert (Slack)** & **Notify team (Gmail)**: Kết nối Slack Workspace (chọn kênh nhận thông báo như `#inventory-alerts`) và cấu hình tài khoản Gmail gửi mail nội bộ nếu cần.

#### 3. Kích hoạt ⚡️
- Bấm nút **Execute Workflow** chạy thử với dữ liệu mẫu để kiểm tra xem các node đã kết nối mượt mà chưa.
- Kiểm tra lại Google Sheets, Slack và Gmail xem đã nhận được dữ liệu/thông báo chính xác chưa.
- Nếu mọi thứ xanh mướt, bật nút **Active** ở góc trên bên phải để hệ thống tự động chạy ngầm 24/7.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh nhận tin:** Ngoài Slack và Gmail, các sếp có thể gắn thêm node Telegram hoặc Zalo ZNS để bắn tin nhắn trực tiếp vào điện thoại cho quản lý kho.
- **Tùy chỉnh ngưỡng tồn kho:** Tại node **Check low stock** (If node), các sếp có thể thay đổi con số `10` thành bất kỳ hạn mức tồn kho nào phù hợp với quy mô kinh doanh của sản phẩm (ví dụ: sản phẩm bán chạy để ngưỡng 20, sản phẩm chậm đi thì để 5).
- **Lưu lịch sử báo cáo tuần:** Thiết lập thêm một nhánh phụ vào mỗi thứ Hai hàng đầu để tổng hợp toàn bộ dữ liệu từ Google Sheets và gửi báo cáo tổng quan tình hình kho hàng cho sếp lớn.

### 📌 Kết luận
Việc tự động hóa giám sát tồn kho Shopify giúp các sếp tiết kiệm hàng chục giờ kiểm kê thủ công mỗi tháng, loại bỏ hoàn toàn rủi ro sót đơn do hết hàng và tối ưu hóa chuỗi cung ứng. Hãy áp dụng ngay workflow này vào hệ thống của các sếp để vận hành cửa hàng chuyên nghiệp hơn!