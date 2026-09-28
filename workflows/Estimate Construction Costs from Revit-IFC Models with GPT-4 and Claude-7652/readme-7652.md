---
title: "🚀 Tự động tính toán chi phí xây dựng từ mô hình Revit và IFC bằng AI (GPT-4 & Claude)"
description: "Hướng dẫn xây dựng hệ thống tự động hóa n8n giúp trích xuất dữ liệu từ Revit/IFC, phân loại vật liệu bằng AI và xuất báo cáo dự toán chi phí chi tiết dưới dạng Excel và HTML."
slug: "u-d-ng-t-h-a-t-nh-to-n-chi-ph-x-y-d-ng-revit-ifc-ai"
tags: [n8n, automation, no-code, artificial-intelligence, revit, ifc, construction, ai-agent]
keywords: [n8n workflow, tính toán chi phí xây dựng, Revit IFC automation, OpenAI Claude AI, DataDrivenConstruction, quản lý dự án BIM]
---

# 🚀 Tự động tính toán chi phí xây dựng từ mô hình Revit và IFC với AI (GPT-4 & Claude)

Trong ngành xây dựng và kiến trúc (AEC), việc bóc tách khối lượng và lập dự toán chi phí từ các mô hình BIM (Revit, IFC) thường tốn rất nhiều thời gian thủ công, dễ sai sót khi phải xử lý hàng ngàn cấu kiện, chủng loại vật liệu và tra cứu đơn giá. 

Bài viết này sẽ hướng dẫn các sếp triển khai một siêu workflow n8n cực kỳ mạnh mẽ (được phát triển bởi *Artem Boiko* từ *DataDrivenConstruction.io*). Workflow này tự động hóa toàn bộ quy trình: từ việc chuyển đổi file mô hình, phân loại cấu kiện bằng AI, phân tích vật liệu chuyên sâu cho đến việc xuất báo cáo chi phí chuyên nghiệp dạng Excel và HTML trực quan!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 với các file mô hình Revit/IFC dung lượng lớn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Chuyển đổi mô hình 3D/IFC/Revit thành dữ liệu bảng tính mà không cần thao tác thủ công.
- **AI thông minh:** Sử dụng OpenAI (GPT-3.5/GPT-4) và Anthropic Claude để phân loại cấu kiện, nhận diện vật liệu theo tiêu chuẩn quốc tế (EU/DE/US) và dự toán giá thị trường.
- **Báo cáo chuyên nghiệp:** Tự động tạo file Excel đa sheet (Tóm tắt, Chi tiết) và báo cáo HTML trực quan kèm biểu đồ phân phối chi phí.
- **Tiết kiệm thời gian:** Giảm từ vài ngày bóc tách khối lượng thủ công xuống chỉ còn vài phút chạy automation.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance:** Đã cài đặt n8n (Khuyên dùng Self-hosted để xử lý file nặng).
- **Công cụ chuyển đổi:** `DDC_Converter_Revit` (hoặc `RvtExporter.exe`) để trích xuất file Revit sang Excel.
- **API Keys:** 
  - OpenAI API Key (cho các node `AI Classify Categories1`, `AI Analyze All Headers`, `OpenAI Chat Model`).
  - Anthropic API Key (cho model Claude Opus trong `AI Agent Enhanced`).
  - (Tùy chọn) xAI Grok API Key nếu muốn thay đổi mô hình LLM.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Tải file JSON của workflow hoặc copy trực tiếp mã nguồn workflow từ n8n template (`7652`), sau đó dán vào n8n Editor của các sếp.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow gồm 47 nodes được chia thành các block chức năng rõ ràng. Các sếp cần chú ý cấu hình các điểm sau:

- **Node `Setup - Define file paths`**: Đây là nơi quan trọng nhất để khai báo đường dẫn:
  - Đường dẫn tới bộ chuyển đổi (`RvtExporter.exe`).
  - Đường dẫn tới file dự án Revit/IFC (`.rvt` hoặc `.ifc`).
  - Tham số gom nhóm (`group_by`, ví dụ: `'Type Name'`, `'IfcType'`).
  - Quốc gia tính toán chi phí (ví dụ: `'Germany'`, `'Brazil'`, `'Vietnam'`...).
- **Cấu hình Credentials**:
  - Gắn kết nối API Key cho các node **OpenAI Chat Model** và **Anthropic Chat Model1** (Claude Opus).
- **Kiểm tra Conversion Block**:
  - Node `Check - Does Excel file exist?1` và `Extract - Run converter1` sẽ kiểm tra xem dữ liệu đã được xuất ra Excel chưa. Nếu chưa, hệ thống sẽ tự động gọi lệnh trích xuất từ file Revit.

#### 3. Kích hoạt ⚡️
- Nhấn **Execute Workflow** (hoặc dùng trigger thủ công `When clicking ‘Execute workflow’`) với một dự án mẫu để kiểm tra toàn bộ luồng chạy từ trích xuất, phân loại AI, đến tạo file Excel/HTML.
- Sau khi test thành công, bật nút **Active** để sẵn sàng sử dụng.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp thông báo:** Thêm node Telegram hoặc Slack vào cuối chuỗi (sau khi tạo file Excel/HTML thành công) để gửi file báo cáo trực tiếp vào nhóm dự án ngay khi tính toán xong.
- **Lưu trữ Cloud:** Kết nối node Google Drive hoặc OneDrive để tự động lưu các file Excel báo cáo chi phí và file HTML lên mây, giúp đội ngũ kỹ sư dễ dàng truy cập.
- **Mở rộng AI:** Thử nghiệm thay đổi giữa GPT-4o và Claude 3.5 Sonnet/Opus để tối ưu hóa độ chính xác khi dự toán đơn giá vật liệu theo khu vực địa lý cụ thể.

### 📌 Kết luận
Workflow tự động hóa tính toán chi phí xây dựng từ Revit/IFC bằng AI này là một "vũ khí tối tân" giúp các kỹ sư QS (Quantity Surveyor) và nhà quản lý dự án BIM tiết kiệm hàng tá thời gian. Hãy triển khai ngay lên hệ thống n8n của các sếp để tối ưu hóa quy trình làm việc ngay hôm nay!