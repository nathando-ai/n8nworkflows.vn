---
title: "🚀 Chuyển Đổi Blueprint Make.com thành Workflow n8n với Azure OpenAI & Google Sheets"
description: "Tự động chuyển các blueprint của Make.com sang workflow n8n, lưu trữ chi tiết vào Google Sheets và tối ưu hoá bằng Azure OpenAI."
slug: "chuyen-doi-blueprint-make-com-n8n-azure-openai-google-sheets"
tags: [n8n, automation, no-code, azure-openai, google-sheets]
keywords: [n8n workflow, tự động hóa, Azure OpenAI, Google Sheets, chuyển đổi blueprint]
---

# 🚀 Chuyển Đổi Blueprint Make.com thành Workflow n8n với Azure OpenAI & Google Sheets

Doanh nghiệp ngày càng phụ thuộc vào các nền tảng tự động hoá như Make.com để thiết kế quy trình. Tuy nhiên, khi muốn di chuyển sang môi trường **n8n** – một nền tảng mã nguồn mở, tự host và linh hoạt hơn – việc **sao chép thủ công** từng bước, từng trigger, từng action trở nên cực kỳ mất thời gian và dễ gây lỗi.  

**Workflow này** sẽ tự động **đọc blueprint (JSON) của Make.com**, **phân tích nội dung bằng Azure OpenAI**, và **ghi lại cấu trúc chi tiết** vào một bảng Google Sheets, đồng thời tạo ra một workflow n8n sẵn sàng chạy. Tất cả chỉ trong vài cú click, không cần viết một dòng code nào.

:::info[Gợi ý hạ tầng cho n8n]  
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]  
- **Tiết kiệm 80% thời gian** so với việc copy‑paste thủ công.  
- **Độ chính xác 100%**: Azure OpenAI giúp hiểu đúng cấu trúc và tham số của blueprint.  
- **Tự động lưu lịch sử**: Mỗi lần chuyển đổi đều được ghi lại trong Google Sheets để tra cứu.  
- **Sẵn sàng triển khai**: Workflow n8n được tạo ra ngay, chỉ cần bật chạy.  
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]  
- **Tài khoản n8n** (self‑hosted hoặc n8n.cloud).  
- **API Key Azure OpenAI** (đăng ký tại Azure Portal, bật dịch vụ `Azure OpenAI`).  
- **Google Cloud Project** với **Google Sheets API** và **Google Drive API** được bật, kèm **OAuth 2.0 credentials** (JSON).  
- **Google Sheet** (đã tạo) để lưu kết quả, cùng với **Google Drive folder** (nếu muốn lưu file blueprint).  
- **Make.com Blueprint** ở dạng JSON (có thể tải từ Make.com > Scenarios > Export).  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập **n8n Editor** → **Import** → **Upload JSON** và chọn file `Convert-Make-Blueprint-to-n8n.json` (được cung cấp trong phần tải xuống).  
2. Hoặc **Copy/Paste** nội dung JSON vào ô **Import from Clipboard**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Vai trò | Cấu hình cần chỉnh |
|------|---------|--------------------|
| **Manual Trigger** | Bắt đầu workflow, cho phép upload blueprint. | Không cần thay đổi. |
| **Extract From File** | Đọc nội dung JSON của blueprint từ Google Drive (nếu lưu). | Chọn **Google Drive Credential**, nhập **File ID** hoặc **Folder Path**. |
| **Code** (Node) | Tiền xử lý: chuyển JSON thành chuỗi sạch, loại bỏ comment. | Không thay đổi, nhưng có thể tùy chỉnh nếu blueprint có định dạng đặc biệt. |
| **If** | Kiểm tra xem blueprint có chứa trường `actions` không. | Điều kiện: `{{$json["actions"] !== undefined}}`. |
| **@n8n/n8n-nodes-langchain.lmChatAzureOpenAi** | Gửi nội dung blueprint tới Azure OpenAI để “dịch” thành mô tả workflow n8n. | - Chọn **Azure OpenAI Credential**.<br>- **Model**: `gpt-4o` (hoặc model hiện có).<br>- **Prompt**: `Bạn là một chuyên gia n8n. Hãy chuyển đổi blueprint Make.com dưới đây thành workflow n8n chi tiết, bao gồm các node, trigger, và các tham số cần thiết.` |
| **@n8n/n8n-nodes-langchain.agent** | Tạo ra các node n8n dựa trên output của Azure OpenAI. | - Chọn **Same Azure OpenAI Credential**.<br>- **Agent Prompt**: `Dựa trên mô tả ở trên, tạo một workflow n8n JSON hợp lệ.` |
| **Google Sheets** | Ghi lại bản tóm tắt, link workflow, và trạng thái. | - Chọn **Google Sheets Credential**.<br>- **Spreadsheet ID** và **Sheet Name** (ví dụ: `Blueprint_Conversion`). |
| **Google Drive** (tùy chọn) | Lưu file JSON của workflow n8n đã tạo. | - Chọn **Google Drive Credential**.<br>- Đặt **Folder ID** nơi lưu. |
| **Sticky Note** | Ghi chú hướng dẫn cho người dùng cuối. | Không cần chỉnh, chỉ để hiển thị thông tin. |

> **Lưu ý:**  
> - Đảm bảo **Azure OpenAI** và **Google** credentials đều ở trạng thái **Active**.  
> - Kiểm tra **quota** của Azure OpenAI để tránh lỗi “Rate limit exceeded”.  
> - Nếu muốn lưu blueprint trên Google Drive, tạo một folder riêng và cung cấp **Folder ID** trong node `Extract From File`.

#### 3. Kích hoạt ⚡️
1. **Test run**: Nhấn **Execute Workflow** → tải lên một file blueprint mẫu → kiểm tra kết quả trong Google Sheet.  
2. Nếu mọi thứ ổn, bật **Active** (toggle ở góc phải) để workflow chạy tự động mỗi khi có file mới được đưa vào Google Drive hoặc khi trigger manual được kích hoạt.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp Slack/Telegram**: Thêm node **Slack** hoặc **Telegram** để gửi thông báo khi chuyển đổi thành công hoặc thất bại.  
- **Lưu log chi tiết**: Dùng node **Write Binary File** để lưu log JSON của Azure OpenAI vào Google Drive, giúp debug nhanh.  
- **Báo cáo định kỳ**: Kết hợp **Cron** + **Google Sheets** để tổng hợp số lượng blueprint đã chuyển đổi trong tuần/tháng và gửi email báo cáo.  
- **Mở rộng sang các nền tảng khác**: Thay `@n8n/n8n-nodes-langchain.lmChatAzureOpenAi` bằng **OpenAI** hoặc **Anthropic** nếu muốn so sánh kết quả.

### 📌 Kết luận
Với workflow này, các sếp có thể **tự động hoá 100% quá trình chuyển đổi blueprint Make.com sang n8n**, giảm thiểu lỗi thủ công, tăng tốc độ triển khai và luôn có bản ghi chi tiết trên Google Sheets. Hãy **import ngay**, cấu hình các credentials cần thiết, và để n8n làm việc thay bạn! 🚀