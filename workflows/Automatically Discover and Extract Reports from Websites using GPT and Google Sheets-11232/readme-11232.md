---
title: "🤖 Tự Động Khám Phá & Trích Xuất Báo Cáo Từ Website Bằng AI + Google Sheets (N8N)"
description: "Workflow tự động hóa sử dụng GPT-5.1 và Google Sheets để quét, phân tích và trích xuất báo cáo mới nhất từ các trang web chuyên ngành, tiết kiệm thời gian cho các sếp lên đến 20 giờ/tháng. Kết quả được lưu trữ sẵn trên Google Sheets với định dạng chuẩn, dễ dàng chia sẻ và phân tích."
slug: "tieu-dong-kham-pha-trich-xuat-bao-cao-ai-google-sheets"
tags: [n8n, automation, ai-rag, google-sheets, market-research, no-code]
keywords: [tự động hóa n8n, trích xuất báo cáo từ website, ai gpt-5.1, google sheets tự động, market research automation, workflow n8n market research]
---

# 🚀 **Tự Động Khám Phá & Trích Xuất Báo Cáo Từ Website Bằng AI + Google Sheets (N8N)**

### **Giải pháp cho các sếp:**
Bạn đã từng phải tốn **hàng giờ** mỗi tuần để quét các trang web chuyên ngành (như Bloomberg, McKinsey, hoặc các tổ chức nghiên cứu) để tìm báo cáo mới nhất? Hay phải **lo lắng mất báo cáo quan trọng** vì quên kiểm tra thường xuyên? Workflow này sẽ **tự động hóa toàn bộ quy trình** với sự hỗ trợ của **GPT-5.1** và **Google Sheets**, giúp bạn:
✅ **Tiết kiệm 20+ giờ/tháng** so với cách làm thủ công.
✅ **Không bỏ lỡ bất kỳ báo cáo mới** nhờ việc quét tự động hàng ngày.
✅ **Lưu trữ và phân loại** báo cáo theo định dạng chuẩn (Markdown) trên Google Sheets.
✅ **Xác thực chất lượng** báo cáo trước khi lưu, tránh dữ liệu sai lệch.
✅ **Kết hợp với Slack/Email** để thông báo báo cáo mới (mẹo nâng cao).

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động **liên tục 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng. Đây là giải pháp **ổn định, an toàn và tiết kiệm chi phí** so với phiên bản cloud.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (Đảm bảo tốc độ cao, phù hợp cho AI)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%**: Không cần can thiệp thủ công, workflow chạy tự động hàng ngày (hoặc theo yêu cầu).
- **Chất lượng cao**: AI **GPT-5.1** phân tích và lọc báo cáo **chính xác**, loại bỏ những tài liệu không liên quan.
- **Lưu trữ thông minh**: Tất cả báo cáo được **ghi lại trên Google Sheets** với các cột: **Tên báo cáo, Link tải, Ngày phát hành, Nguồn, Trạng thái**.
- **Dễ dàng chia sẻ**: Dữ liệu được **sắp xếp theo định dạng Markdown**, có thể chia sẻ trực tiếp hoặc xuất sang PDF/DOCX.
- **Báo cáo lỗi**: Nếu không tìm thấy báo cáo, hệ thống sẽ **ghi log** để các sếp biết cần kiểm tra lại nguồn.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Google Sheets** (để lưu trữ danh sách nguồn và báo cáo).
2. **API Key OpenAI** (để sử dụng GPT-5.1).
3. **Danh sách các URL nguồn** (các trang web chuyên ngành bạn muốn theo dõi).
4. **Google Sheets với 3 tab chuẩn**:
   - **Tab "Report Sources"**: Danh sách URL các trang web cần quét (cột: `URL`, `Sheet Name`).
   - **Tab "Discovered Reports"**: Lưu báo cáo đã trích xuất (cột: `Report Name`, `Download Link`, `Date`, `Source`).
   - **Tab "Discovery Log"**: Ghi log khi không tìm thấy báo cáo (cột: `URL Checked`, `Timestamp`, `Status`).

---
:::note[Lưu ý quan trọng]
- **Không cần kỹ năng code**: Workflow đã được thiết kế sẵn, chỉ cần cấu hình các tham số.
- **GPT-5.1**: Nếu không có API Key, có thể thay thế bằng **GPT-4** (tốc độ chậm hơn nhưng vẫn hiệu quả).
- **Limiter API**: Nếu sử dụng phiên bản free OpenAI, lưu ý **giá trị credit** để không bị ngắt workflow.
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có **2 cách** để import workflow này:
- **Tải file JSON** từ [n8n.io/workflows/11232](https://n8n.io/workflows/11232) và import vào **n8n Editor**.
- **Copy/Paste JSON** từ file vào **n8n Editor** (tab `Import/Export`).

**Hướng dẫn chi tiết:**
1. Mở **n8n Editor** (trang chủ của n8n).
2. Nhấn **`Import`** (góc trên bên phải).
3. Chọn **`From JSON`** và dán nội dung JSON từ file.
4. Nhấn **`Import`** để hoàn tất.

---

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Sau khi import, các sếp **phải cấu hình** các node sau để workflow hoạt động:

##### **A. Cấu hình Google Sheets**
1. **Tạo credentials**:
   - Vào **Settings > Credentials > Add Credentials**.
   - Chọn **Google Sheets OAuth2 API**.
   - Đăng nhập Google và cấp quyền cho n8n.
   - **Ghi lại ID credentials** (sẽ dùng sau).

2. **Cấu hình các node Google Sheets**:
   - **Node "Read Active Sources"**:
     - **Credentials**: Chọn `googleSheetsOAuth2Api` (đã tạo ở trên).
     - **Sheet Name**: Nhập tên tab **"Report Sources"**.
     - **Range**: `Sheet1!A:B` (giả sử cột A là URL, cột B là tên tab).
   - **Node "Save Discovered Report"**:
     - **Credentials**: Chọn `googleSheetsOAuth2Api`.
     - **Sheet Name**: Nhập tên tab **"Discovered Reports"**.
   - **Node "Log No Report Found"**:
     - **Credentials**: Chọn `googleSheetsOAuth2Api`.
     - **Sheet Name**: Nhập tên tab **"Discovery Log"**.

##### **B. Cấu hình OpenAI (GPT-5.1)**
1. **Tạo credentials OpenAI**:
   - Vào **Settings > Credentials > Add Credentials**.
   - Chọn **OpenAI API**.
   - Nhập **API Key** từ tài khoản OpenAI của bạn.
   - **Ghi lại ID credentials**.

2. **Cấu hình node "OpenAI GPT-5.1"**:
   - **Credentials**: Chọn `openAiApi` (đã tạo).
   - **Model**: Đảm bảo chọn `gpt-5.1` (nếu không có, chọn `gpt-4` làm thay thế).

##### **C. Cấu hình Trigger**
Workflow có **3 cách kích hoạt**:
1. **Manual Trigger** (nhấn nút "Run" thủ công).
2. **Schedule Trigger** (chạy hàng ngày, ví dụ 8h sáng).
3. **Called by Another Workflow** (nếu kết hợp với workflow khác).

**Cách cấu hình Schedule Trigger**:
- Mở node **"Schedule (Daily)"**.
- Chọn **`Daily`** và thiết lập giờ chạy (ví dụ: **8:00 AM**).

##### **D. Cấu hình AI Agent**
Node **"AI Report Discovery Agent"** là **cốt lõi** của workflow. Các sếp **không cần chỉnh sửa code**, nhưng nên kiểm tra:
- **Prompt**: Nếu muốn thay đổi logic AI, có thể chỉnh sửa trong **node "agent"**.
- **Output Parser**: Đảm bảo **Structured Output Parser** trả về dữ liệu đúng định dạng (ví dụ: JSON với các trường `reportName`, `downloadLink`, `isValid`).

##### **E. Node "Validate & Normalize Output" (Code)**
Node này **xác thực** báo cáo trước khi lưu. Các sếp **không cần chỉnh sửa**, nhưng có thể mở ra xem logic:
```javascript
// Logic mặc định: Kiểm tra link download và định dạng
return {
  json: {
    ...node.input,
    isValid: node.input.json?.downloadLink?.includes("pdf") || node.input.json?.downloadLink?.includes("docx")
  }
};
```

---

#### **3. Kích hoạt ⚡️**
1. **Test Run** (kiểm tra với 1-2 URL mẫu):
   - Chọn **Manual Trigger** và nhấn **Run**.
   - Kiểm tra **Google Sheets** xem có báo cáo mới được lưu không.
2. **Bật Active**:
   - Sau khi test thành công, chuyển **Workflow Status** từ **Inactive** sang **Active**.
   - Nếu dùng **Schedule Trigger**, workflow sẽ chạy tự động hàng ngày.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết hợp với Slack/Email để thông báo báo cáo mới**:
   - Thêm **node Slack** hoặc **node Email** sau node **"Save Discovered Report"**.
   - Ví dụ: Khi lưu báo cáo thành công, gửi tin nhắn Slack với nội dung:
     ```
     📄 Báo cáo mới được phát hiện: [Tên báo cáo]
     🔗 Link tải: [Download Link]
     📅 Ngày phát hành: [Date]
     ```

2. **Lưu log vào Google Drive**:
   - Thay vì chỉ ghi log trên Sheets, có thể **ghi vào Google Drive** với định dạng Excel/PPT.

3. **Tăng tốc độ với Batch Processing**:
   - Nếu có **hàng trăm URL**, sử dụng **node "Split in Batches"** để chia nhỏ và xử lý đồng thời.

4. **Tự động xuất báo cáo định kỳ**:
   - Sử dụng **node "Schedule Trigger"** kết hợp với **node "Google Drive"** để xuất báo cáo thành PDF hàng tuần.

5. **Sử dụng AI để tổng hợp báo cáo**:
   - Sau khi trích xuất, có thể **gửi dữ liệu vào node LLM** để tổng hợp thành báo cáo ngắn gọn.

---

### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp cần **tự động hóa việc tìm kiếm báo cáo từ website**, tiết kiệm thời gian và đảm bảo **không bỏ lỡ bất kỳ thông tin quan trọng nào**. Với **cấu hình đơn giản** và **sử dụng AI GPT-5.1**, bạn có thể **quét hàng trăm trang web** chỉ trong vài giây mỗi ngày.

**Hành động ngay hôm nay:**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Bật Schedule Trigger** để workflow chạy tự động.
3. **Kiểm tra Google Sheets** sau mỗi lần chạy để xem kết quả.

👉 **[Tải workflow ngay](https://n8n.io/workflows/11232)** và bắt đầu tự động hóa việc nghiên cứu thị trường của bạn!

---
**Chia sẻ ý kiến:**
Các sếp có thể **cập nhật hoặc mở rộng** workflow này bằng cách:
- Thêm **nhiều nguồn website** hơn.
- **Tích hợp với Notion** để lưu trữ báo cáo.
- **Sử dụng AI để phân tích nội dung** báo cáo.

Hãy **like và share** nếu bài viết hữu ích! 🚀