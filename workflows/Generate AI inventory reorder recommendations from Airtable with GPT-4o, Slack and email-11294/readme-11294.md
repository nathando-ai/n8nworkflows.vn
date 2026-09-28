---
title: "🚀 Tự động hóa gợi ý đặt hàng tồn kho thông minh từ Airtable với GPT-4o, Slack và Email"
description: "Hướng dẫn xây dựng workflow n8n tự động lấy dữ liệu kho từ Airtable, dùng AI GPT-4o tối ưu hóa mức tồn kho, gửi báo cáo qua Gmail/Slack và đồng bộ dữ liệu sang Notion, Asana."
slug: "tu-dong-hoa-goi-y-dat-hang-ton-kho-n8n-gpt4o-airtable"
tags: [n8n, automation, ai-agent, airtable, gpt-4o, slack, gmail]
keywords: [n8n workflow, tự động hóa kho hàng, gpt-4o inventory, airtable n8n, quản lý tồn kho ai]
---

# 🚀 Tự động hóa gợi ý đặt hàng tồn kho thông minh từ Airtable với GPT-4o, Slack và Email

Việc quản lý kho thủ công bằng tay thường gặp nhiều rủi ro: sai sót dữ liệu đầu vào, không tính toán kịp thời điểm đặt hàng (reorder point), dẫn đến tình trạng đứt gãy chuỗi cung ứng hoặc tồn kho quá mức. Workflow này ra đời nhằm giải quyết triệt để bài toán đó bằng cách tự động hóa 100% quy trình từ khâu trích xuất, kiểm tra tính hợp lệ, tối ưu hóa bằng trí tuệ nhân tạo (GPT-4o) cho đến việc thông báo đa kênh (Slack, Gmail) và đồng bộ lưu trữ (Notion, Asana).

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa thông minh:** Tận dụng sức mạnh của GPT-4o (Azure OpenAI) để tính toán điểm đặt hàng lại, mức tồn kho an toàn và đánh giá sức khỏe kho hàng không cần can thiệp thủ công.
- **Xử lý dữ liệu sạch:** Tự động lọc các dòng lỗi cấu trúc và ghi log vào Google Sheets để tiện kiểm toán (audit).
- **Cảnh báo đa kênh:** Gửi báo cáo chuyên nghiệp qua Gmail cho quản lý và thông báo ngắn gọn, trực quan (kèm emoji 🟢 ⚠️ 🔴) qua Slack cho đội ngũ vận hành.
- **Đồng bộ hóa toàn diện:** Tự động lưu quyết định thương mại vào Notion Database và tạo task trực tiếp trên Asana để xử lý các mặt hàng sắp hết.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động trơn tru, các sếp cần chuẩn bị sẵn các tài khoản và credentials sau trong n8n:
- **Airtable Account:** Chứa bảng dữ liệu kho hàng (Inventory source).
- **Azure OpenAI Account:** API Key cấu hình cho các model GPT-4o.
- **Google Sheets:** File Google Sheet để ghi log các dòng dữ liệu không hợp lệ.
- **Slack Workspace:** Bot/App được cấp quyền gửi tin nhắn thông báo cho Ops team.
- **Gmail Account:** Tài khoản Google kết nối qua OAuth2 để gửi email tổng kết cho manager.
- **Notion & Asana Accounts:** Tài khoản để đồng bộ hóa bản ghi tồn kho và tạo task giao việc tự động.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp có thể sử dụng file JSON của workflow này, copy và paste trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình lại các node cốt lõi sau cho khớp với hệ thống của công ty:
- **Fetch Inventory Records from Airtable:** Chọn credential `airtableTokenApi`, điền chính xác `Base ID` và `Table Name` chứa dữ liệu kho của sếp.
- **Configure GPT-4o Models (Azure OpenAI):** Thiết lập `azureOpenAiApi` credentials và đảm bảo tham số model được trỏ đúng đến `gpt-4o`.
- **Log Invalid Inventory Rows to Google Sheet:** Trỏ tới file Google Sheets cấu hình sẵn, kết nối bằng `googleSheetsOAuth2Api` để ghi nhận các SKU lỗi cấu trúc.
- **Notify Operations Team on Slack & Email Inventory Summary to Manager:** Chọn đúng kênh Slack (hoặc user ID) và điền địa chỉ email người nhận cho Gmail.
- **Log Trade Decision to Notion & Create Asana Task:** Liên kết Notion Database ID và cấu hình Asana Workspace để hệ thống tự động tạo tác vụ khi kho đạt ngưỡng cảnh báo.

#### 3. Kích hoạt ⚡️
- Chạy thử thủ công bằng nút `When clicking ‘Execute workflow’` để kiểm tra toàn bộ luồng dữ liệu (Data flow).
- Sau khi test thành công không báo lỗi, gạt công tắc sang **Active** để hệ thống tự động vận hành.

### ✍️ Mẹo & gợi ý nâng cao
- **Mở rộng kênh thông báo:** Có thể bổ sung node Telegram hoặc Microsoft Teams bên cạnh Slack để đa dạng hóa kênh nhận tin cho đội vận hành.
- **Lưu lịch sử chạy (Logging):** Thêm một node Google Sheets ở cuối luồng để lưu lại toàn bộ kết quả AI trả về nhằm phân tích xu hướng tiêu thụ hàng hóa theo tuần/tháng.
- **Lập lịch tự động (Cron):** Thay thế node `manualTrigger` bằng `Schedule Trigger` để hệ thống tự động chạy quy trình kiểm tra kho hàng vào mỗi sáng thứ Hai hàng tuần.

### 📌 Kết luận
Workflow tích hợp AI và tự động hóa đa nền tảng này giúp giải phóng hoàn toàn thời gian kiểm đếm, tính toán thủ công của đội ngũ quản lý kho. Hãy "lên đồ" ngay cho hệ thống n8n của các sếp để tối ưu hóa chuỗi cung ứng một cách thông minh nhất!