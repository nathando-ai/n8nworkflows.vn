---
title: "🚀 Tạo file llms.txt chuẩn AI từ dữ liệu crawl website bằng Screaming Frog tự động trên n8n"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa việc chuyển đổi file CSV crawl từ Screaming Frog thành file llms.txt tối ưu hóa cho AI và LLM."
slug: "tao-file-llms-txt-tu-screaming-frog-voi-n8n"
tags: [n8n, automation, ai, screaming-frog, seo, llms-txt]
keywords: [n8n workflow, llms.txt, screaming frog, seo automation, ai optimization, openAI gpt-4o-mini]
---

# 🚀 Tạo file llms.txt chuẩn AI từ dữ liệu crawl website bằng Screaming Frog

Các sếp có bao giờ đau đầu khi muốn tối ưu hóa website của mình cho các mô hình ngôn ngữ lớn (LLM) như ChatGPT, Claude chưa? Việc tạo một file chuẩn `llms.txt` thủ công cho các website lớn thực sự là một cơn ác mộng tốn thời gian. 

Workflow n8n này sẽ giúp các sếp tự động hóa 100% quá trình biến file CSV crawl từ **Screaming Frog** thành một file `llms.txt` hoàn chỉnh, chuẩn chỉnh để AI dễ dàng đọc hiểu và thu thập dữ liệu từ website của bạn. Không cần code phức tạp, chỉ vài thao tác kéo thả!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn**: Biến file CSV cồng kềnh thành file `llms.txt` gọn gàng, chuẩn cấu trúc chỉ trong vài giây.
- **Tối ưu hóa cho AI/LLM**: Giúp các con bot AI crawl và Index nội dung website chính xác, nâng cao hiệu quả SEO thế hệ mới.
- **Lọc thông minh**: Dễ dàng lọc bỏ các URL rác, trang lỗi (404) hoặc trang không cần thiết dựa trên bộ lọc HTTP status hoặc AI Text Classifier.
- **Tùy biến linh hoạt**: Cho phép thêm mô tả, tên website, tiêu đề tùy ý vào file xuất ra.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Phần mềm Screaming Frog SEO Spider**: Dùng để crawl dữ liệu website.
- **Tài khoản n8n**: Đã kích hoạt (Self-hosted hoặc Cloud).
- **OpenAI API Key**: (Tùy chọn) Nếu các sếp muốn kích hoạt node *Text Classifier* để AI lọc thông minh nội dung chất lượng cao.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này, vào giao diện n8n chọn **New Workflow** -> **Import from JSON** và dán vào là xong.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 12 nodes được thiết kế mạch lạc. Các sếp cần chú ý các điểm sau:

- **Form - Screaming frog internal_html.csv upload** (`formTrigger`): 
  - Khi test, form sẽ yêu cầu nhập Tên website, Mô tả ngắn và tải lên file CSV (khuyến nghị dùng `internal_html.csv` từ Screaming Frog).
- **Extract data from Screaming Frog file** (`extractFromFile`): 
  - Node này tự động đọc file Excel/CSV. Đảm bảo cấu hình đúng định dạng file đầu vào.
- **Set useful fields** (`set`): 
  - Thiết lập 7 trường khóa chính (`url`, `title`, `description`, `status`, `indexability`, `content_type`, `word_count`). 
  - *Lưu ý:* Nếu các sếp dùng Screaming Frog bằng tiếng Pháp, Ý, Đức hay Tây Ban Nha, workflow vẫn tự tương thích tốt!
- **Filter URLs** (`filter`): 
  - Lọc sẵn các URL có `status` = 200, `indexability` = indexable và `content_type` chứa `text/html`. Các sếp có thể tùy chỉnh thêm điều kiện lọc theo số lượng từ (word count) hoặc thư mục URL.
- **Text Classifier** (`textClassifier` & `OpenAI Chat Model`): 
  - 🚫 **Mặc định đang tắt (Deactivated)**. Các sếp có thể bật lên nếu muốn dùng AI (GPT-4o-mini) phân loại thông minh các trang chất lượng cao. Cần cấu hình **OpenAI API Key** trong credentials của node *OpenAI Chat Model*.
- **Generate llms.txt file** (`convertToFile`): 
  - Xuất dữ liệu thành file text định dạng chuẩn.
- **upload file anywhere** (`noOp`): 
  - Mặc định node này là No-Op (chỉ để tải trực tiếp từ n8n UI). Các sếp nên thay thế node này bằng **Google Drive** hoặc **OneDrive** node để tự động lưu file `llms.txt` thẳng lên cloud folder.

#### 3. Kích hoạt ⚡️
- Bấm **"Test Workflow"**, điền thông tin vào form, tải lên file CSV từ Screaming Frog và nhấn Submit để chạy thử nghiệm.
- Kiểm tra kết quả ở node cuối cùng và tải file về, hoặc bật **Active** để sử dụng lâu dài.

### ✍️ Mẹo & gợi ý nâng cao
- **Tự động hóa lưu trữ**: Thay thế node `upload file anywhere` bằng node Google Drive để tự động ghi đè file `llms.txt` mới nhất lên hosting hoặc Google Drive mỗi khi crawl lại website.
- **Thông báo qua Telegram/Slack**: Thêm node thông báo khi quá trình tạo file `llms.txt` hoàn tất để các sếp nắm tiến độ.
- **Xử lý website lớn**: Đối với các website có hàng trăm nghìn URL, nên bổ sung node *Loop Over Items* để tránh quá tải giới hạn API và timeout của n8n.

### 📌 Kết luận
Việc tối ưu website cho AI không còn là xu hướng tương lai mà đã là hiện tại. Với workflow n8n này, các sếp có thể tiết kiệm hàng giờ đồng hồ mỗi khi cập nhật cấu trúc website cho các LLM. Triển khai ngay hôm nay để đón đầu xu hướng AI SEO!