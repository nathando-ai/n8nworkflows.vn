---
title: "🚀 Tự Động Phân Loại Hóa Đơn Airtable Với OpenAI & Tối Ưu Token TOON"
description: "Giải pháp tự động hóa 100% để phân loại hóa đơn trong Airtable bằng AI, sử dụng định dạng TOON giúp tiết kiệm tới 50% chi phí token OpenAI."
slug: "phan-loai-hoa-don-airtable-openai-toon"
tags: [n8n, automation, no-code, airtable, openai, ai-automation]
keywords: [n8n workflow, tự động hóa hóa đơn, airtable automation, openai token optimization, toon format]
---

# 🚀 Tự Động Phân Loại Hóa Đơn Airtable Với OpenAI & Tối Ưu Token TOON

Trong môi trường kinh doanh hiện đại, việc quản lý hàng trăm, thậm chí hàng nghìn hóa đơn mỗi tháng là một thách thức lớn. Nếu các sếp vẫn đang phải mở từng hóa đơn, đọc nội dung và gõ tay vào cột "Danh mục" (Category) trong Airtable, thì đó là một sự lãng phí thời gian và nguồn lực nhân sự vô cùng lớn. Hơn nữa, việc nhập liệu thủ công dễ dẫn đến sai sót, thiếu nhất quán trong cách phân loại, gây khó khăn cho việc báo cáo tài chính sau này.

Workflow này chính là giải pháp "chìa khóa trao tay" giúp các sếp tự động hóa toàn bộ quy trình: Lấy dữ liệu hóa đơn từ Airtable, sử dụng sức mạnh của OpenAI để phân tích và gán danh mục chính xác, sau đó cập nhật ngược lại vào cơ sở dữ liệu. Điểm đặc biệt và "đắt giá" nhất của workflow này là kỹ thuật **TOON (Token Optimization)** – một phương pháp chuyển đổi dữ liệu JSON sang định dạng TOON trước khi gửi cho AI, giúp giảm đáng kể số lượng token tiêu thụ, từ đó tiết kiệm chi phí API OpenAI một cách hiệu quả.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 và xử lý lượng lớn dữ liệu mà không bị gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm chi phí AI:** Sử dụng định dạng TOON giúp giảm lượng token gửi đi và nhận về, tiết kiệm trực tiếp tiền API OpenAI.
- **Chính xác & Nhất quán:** AI phân loại dựa trên ngữ cảnh đầy đủ (khách hàng + chi tiết hóa đơn), đảm bảo tính nhất quán cao hơn so với con người.
- **Tự động hóa hoàn toàn:** Không cần can thiệp thủ công, workflow tự động quét các hóa đơn "Ready" và cập nhật danh mục.
- **Tốc độ xử lý nhanh:** Quy trình được tối ưu hóa với các node chuyên dụng, xử lý hàng loạt hóa đơn trong thời gian ngắn.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản n8n:** Chạy trên instance Self-hosted (bắt buộc vì cần dùng node CustomJS).
2. **Tài khoản Airtable:** 
   - Tạo hoặc clone [Airtable Example](https://airtable.com/apphyDa3uYAq0VOMW/shrSe39NZYrqm4gtE) từ tác giả.
   - Cấu trúc bảng cần có: `Invoices`, `Clients`, `Invoice Items`.
   - Tạo API Key cho Airtable.
3. **Tài khoản OpenAI:** API Key để gọi mô hình ngôn ngữ (GPT-4o-mini hoặc GPT-4).
4. **Tài khoản CustomJS:** 
   - Đăng ký tại [CustomJS](https://www.customjs.space) để lấy API Key.
   - Cài đặt node `@custom-js/n8n-nodes-pdf-toolkit` vào n8n (vì đây là node cộng đồng, không có sẵn trong n8n cloud).
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Tải xuống file JSON của workflow từ [link gốc](https://n8n.io/workflows/11761).
2. Mở n8n Editor, chọn **Import from File** hoặc **Import from URL**.
3. Nếu import từ URL, hãy đảm bảo n8n của bạn có quyền truy cập internet để tải node CustomJS (hoặc cài đặt node đó thủ công trước).

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

Dưới đây là các node quan trọng cần cấu hình kỹ lưỡng:

**A. Nhóm Node Airtable (Lấy dữ liệu & Cập nhật)**
- **Node: `Get Ready Invoices`**
  - Chọn credentials Airtable đã tạo.
  - Chọn Base và Table `Invoices`.
  - **Filter:** Đặt điều kiện `Status` = `Ready` (hoặc trạng thái hóa đơn chưa được phân loại) để workflow chỉ xử lý những hóa đơn mới.
- **Node: `Get Clients`**
  - Chọn Table `Clients`.
  - Đảm bảo field mapping khớp với ID khách hàng trong bảng Invoices.
- **Node: `Get Invoice Items`**
  - Chọn Table `Invoice Items`.
  - Filter theo `Invoice ID` để lấy chi tiết từng hóa đơn.
- **Node: `Update record`**
  - Chọn Table `Invoices`.
  - **Field to update:** Chọn cột `Category` (hoặc cột danh mục tương ứng).
  - **Value:** Map từ output của node `TOON to JSON`.

**B. Nhóm Node AI & Tối ưu Token (Trái tim của workflow)**
- **Node: `JSON to TOON`**
  - Chọn credentials `customJsApi`.
  - Input: Dữ liệu đã được nhóm lại từ node `GroupClientAndInvoice`.
  - *Lưu ý:* Node này chuyển đổi JSON phức tạp sang định dạng TOON ngắn gọn hơn, dễ đọc cho AI và ít tốn token hơn.
- **Node: `OpenAI Enhancement`**
  - Chọn credentials `openAiApi`.
  - **Model:** Khuyến nghị dùng `gpt-4o-mini` để cân bằng giữa chi phí và chất lượng.
  - **System Prompt:** Cần chỉnh sửa prompt để yêu cầu AI:
    1. Phân tích dữ liệu TOON đầu vào.
    2. Gán **đúng một** danh mục phù hợp (ví dụ: "Dịch vụ tư vấn", "Bán hàng", "Chi phí vận hành").
    3. **Quan trọng:** Yêu cầu AI trả về kết quả **chỉ dưới dạng TOON**, không kèm theo giải thích hay JSON.
  - **User Prompt:** Map dữ liệu TOON từ node trước đó.
- **Node: `TOON to JSON`**
  - Chọn credentials `customJsApi`.
  - Input: Output từ node OpenAI.
  - Output: JSON chuẩn để node Airtable có thể hiểu và cập nhật.

**C. Nhóm Node Logic (Điều phối)**
- **Node: `GroupClientAndInvoice`**
  - Đảm bảo các trường `Client`, `Invoice`, và `Items` được gộp vào một object duy nhất để gửi sang bước chuyển đổi TOON.
- **Node: `Loop Over Items`**
  - Node này giúp xử lý từng hóa đơn một cách tuần tự, tránh lỗi khi xử lý hàng loạt.

#### 3. Kích hoạt ⚡️
1. **Test Run:** 
   - Thêm một vài hóa đơn mẫu vào Airtable với trạng thái `Ready`.
   - Chạy workflow thủ công (Manual Trigger).
   - Kiểm tra xem cột `Category` trong Airtable đã được cập nhật đúng chưa.
   - Kiểm tra log của node OpenAI để đảm bảo output là TOON hợp lệ.
2. **Bật Active:**
   - Sau khi test thành công, bật nút **Active** để workflow chạy tự động.
   - *Gợi ý:* Có thể thay thế Manual Trigger bằng Schedule Trigger (ví dụ: chạy mỗi 15 phút) hoặc Webhook Trigger (chạy khi có hóa đơn mới được tạo).

### ✍️ Mẹo & gợi ý nâng cao
- **Tự động hóa hoàn toàn:** Thay vì Manual Trigger, hãy dùng **Schedule Trigger** để quét Airtable mỗi 10-15 phút. Hoặc dùng **Webhook** kết nối với hệ thống tạo hóa đơn để chạy ngay khi có hóa đơn mới.
- **Gửi thông báo:** Thêm node **Slack** hoặc **Telegram** sau bước `Update record` để báo cáo cho đội ngũ kế toán khi có hóa đơn mới được phân loại.
- **Phân loại đa cấp:** Mở rộng prompt OpenAI để không chỉ gán 1 danh mục mà còn gán `Sub-category` hoặc `Priority` (Ưu tiên) dựa trên giá trị hóa đơn.
- **Log chi tiết:** Thêm node **Google Sheets** hoặc **Airtable Log** để lưu lại lịch sử phân loại, giúp các sếp dễ dàng kiểm tra lại nếu AI phân loại sai.

### 📌 Kết luận
Workflow này là một ví dụ điển hình về cách kết hợp **AI** và **kỹ thuật tối ưu hóa dữ liệu** (TOON) để giải quyết bài toán thực tế trong quản lý tài chính. Bằng cách tự động hóa việc phân loại hóa đơn, các sếp không chỉ tiết kiệm hàng giờ làm việc thủ công mỗi tuần mà còn giảm thiểu chi phí vận hành AI. Hãy thử áp dụng ngay để trải nghiệm sự khác biệt mà tự động hóa mang lại!