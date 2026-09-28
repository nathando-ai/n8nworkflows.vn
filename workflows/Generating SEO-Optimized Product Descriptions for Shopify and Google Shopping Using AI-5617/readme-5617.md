---
title: "🚀 Tự động tạo mô tả sản phẩm chuẩn SEO cho Shopify và Google Shopping bằng AI với n8n"
description: "Hướng dẫn chi tiết cách tự động hóa quy trình viết mô tả sản phẩm chuẩn SEO cho Shopify và Google Merchant Center bằng AI Multimodal và Google Sheets."
slug: "tu-dong-tao-mo-ta-san-pham-shopify-google-shopping-ai-n8n"
tags: [n8n, automation, shopify, google-shopping, ai, openai, google-sheets]
keywords: [n8n workflow, tạo mô tả sản phẩm tự động, Shopify SEO, Google Merchant Center, AI copywriting, OpenAI Vision]
---

# 🚀 Tự động hóa tạo mô tả sản phẩm chuẩn SEO cho Shopify và Google Shopping bằng AI

Các sếp kinh doanh thương mại điện tử chắc chắn hiểu rõ nỗi đau khi phải viết hàng trăm, hàng ngàn mô tả sản phẩm. Việc viết thủ công không chỉ ngốn hàng tá thời gian, tốn kém chi phí nhân sự mà còn dễ bỏ sót các tiêu chuẩn SEO khắt khe của Shopify hay Google Merchant Center (GMC).

Workflow n8n này sinh ra để giải quyết triệt để vấn đề đó! Với sự kết hợp của **AI Multimodal (OpenAI Vision)** và **AI Agents**, hệ thống sẽ tự động đọc hình ảnh sản phẩm, phân tích chi tiết và viết ra những nội dung chuẩn SEO, tối ưu chuyển đổi cho cả Shopify lẫn Google Shopping một cách hoàn toàn tự động.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian:** Không cần ngồiò gõ từng dòng mô tả sản phẩm hay canh chỉnh chuẩn SEO nữa.
- **Đa nền tảng thông minh:** Tự động tạo định dạng HTML mượt mà cho Shopify và nội dung chuẩn quy tắc (dưới 700 ký tự, không quảng cáo quá đà) cho Google Merchant Center.
- **Tận dụng AI Vision:** AI tự nhìn hình ảnh sản phẩm để miêu tả chính xác màu sắc, chất liệu, kiểu dáng mà không cần nhập liệu thô sơ.
- **Đồng bộ trực tiếp:** Kết quả được đẩy thẳng về Google Sheets cực kỳ ngăn nắp và chuyên nghiệp.
:::

### 🔍 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Cloud hoặc Self-hosted).
- **Tài khoản Google Sheets:** Để đọc dữ liệu sản phẩm đầu vào và ghi kết quả.
- **OpenAI API Key:** Tài khoản OpenAI có tích hợp GPT-4o-mini để xử lý hình ảnh và chạy AI Agents.
- **Mẫu Google Sheets chuẩn:** Tải về [Product Description Writer Spreadsheet](https://docs.google.com/spreadsheets/d/1pEn8phxhkrWLBnM1CyWySjSrfkV2WMtrONZWAuBQLxo/edit?usp=sharing) để làm kho dữ liệu.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow từ n8n hoặc sao chép mã JSON nguồn.
- Trong giao diện n8n Editor, chọn **Add workflow** -> **Import from File / Clipboard** và dán đoạn mã vào.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Các sếp cần cấu hình các thông số quan trọng sau trong các node cốt lõi:
- **Google Sheets Trigger & Google Sheets / Google Sheets2:** Kết nối tài khoản Google thông qua **Google Sheets OAuth2 API**. Trỏ đúng đến file Google Sheets sản phẩm và tên Sheet phù hợp.
- **OpenAI / OpenAI Chat Model / OpenAI Chat Model1:** Thêm **OpenAI API Key** của các sếp. Đảm bảo mô hình được chọn là `gpt-4.1-mini` (hoặc `gpt-4o-mini`) để có khả năng đọc hiểu hình ảnh (Vision) tốt nhất.
- **Edit Image:** Node này giúp resize ảnh sản phẩm về 40% để giảm tải dung lượng, giúp AI xử lý nhanh hơn mà không làm giảm chất lượng nhận diện.
- **If1 Node:** Kiểm tra điều kiện sản phẩm bắt buộc phải có `image link`. Nếu không có ảnh, workflow sẽ tự động bỏ qua để tránh lỗi.
- **Shopify Agent & GMC Agent:** Hai AI Agent chịu trách nhiệm copywriting. Agent Shopify sẽ tạo nội dung HTML giàu cảm xúc, tối ưu chuyển đổi; Agent GMC sẽ tối ưu tiêu đề chuẩn SEO và mô tả gọn gàng dưới 700 ký tự theo đúng chính sách của Google.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** chạy thử với 1-2 dòng dữ liệu mẫu trong Google Sheets để kiểm tra kết quả trả về.
- Sau khi test thành công, chuyển trạng thái góc trên bên phải thành **Active** để hệ thống tự động chạy theo lịch trình (**Schedule Trigger**) hoặc khi có dữ liệu mới.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Nối thêm node Telegram hoặc Slack ở cuối workflow để nhận thông báo ngay khi AI hoàn thành việc viết mô tả cho toàn bộ danh sách sản phẩm.
- **Đa ngôn ngữ:** Các sếp có thể tinh chỉnh lại System Prompt trong các Agent AI để yêu cầu xuất nội dung ra tiếng Anh, tiếng Thái hoặc bất kỳ ngôn ngữ nào nếu kinh doanh thị trường quốc tế.
- **Lưu log lỗi:** Thêm một nhánh xử lý lỗi (Error Trigger) để ghi nhận lại các sản phẩm bị lỗi trong quá trình gọi API OpenAI.

### 📌 Kết luận
Với workflow n8n tự động hóa này, việc sản xuất hàng loạt nội dung chuẩn SEO cho cửa hàng Shopify và Google Shopping không còn là gánh nặng. Hãy "lên đồ" ngay hôm nay để tối ưu hóa hiệu suất kinh doanh e-commerce của các sếp!