---
title: "🚀 Tự Động Xác Minh & Phân Loại Lead B2B với AI (ProspectPro + Web RAG + GPT-4) - Không Cần Code"
description: "Workflow tự động hóa hoàn toàn để phân tích, đánh giá và phân loại lead B2B dựa trên dữ liệu website, thông tin công ty và trí tuệ nhân tạo GPT-4. Giúp các sếp tiết kiệm 80% thời gian trong quá trình xác minh lead, đồng thời tăng độ chính xác lên 95% so với cách làm thủ công."
slug: "tu-dong-xac-min-lead-b2b-voi-ai-prospectpro-web-rag-gpt-4"
tags: [n8n, automation, lead-generation, ai-summarization, prospectpro, web-rag, gpt-4]
keywords: [n8n workflow lead generation, tự động hóa xác minh lead B2B, ProspectPro AI, Web RAG với n8n, GPT-4 trong tự động hóa bán hàng]
---

# 🚀 **Tự Động Xác Minh & Phân Loại Lead B2B với AI (ProspectPro + Web RAG + GPT-4)**

### **Giải pháp hoàn toàn tự động hóa để các sếp:**
- **Tiết kiệm 80% thời gian** trong việc nghiên cứu lead thủ công.
- **Tăng độ chính xác lên 95%** bằng trí tuệ nhân tạo và dữ liệu website thực tế.
- **Phân loại lead** theo tiêu chí ICP (Ideal Customer Profile) một cách tự động.
- **Tránh trùng lặp** bằng cách đánh dầu tag tự động trong ProspectPro.
- **Hoạt động 24/7** mà không cần can thiệp của con người.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động ổn định và hiệu quả nhất, các sếp nên **self-host n8n** trên một VPS ổn định. Dưới đây là một số gợi ý:
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (Đảm bảo tốc độ xử lý nhanh cho AI)
:::

---

## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Không cần nghiên cứu lead thủ công, tự động hóa toàn bộ quy trình từ tìm kiếm đến phân loại.
✅ **Độ chính xác cao**: Sử dụng **Web RAG** (Retrieval-Augmented Generation) để lấy dữ liệu website thực tế và **GPT-4** để phân tích chi tiết.
✅ **Phân loại tự động**: Lead được đánh tag "AutoQualified" hoặc "ManualQualification" dựa trên tiêu chí ICP.
✅ **Tránh trùng lặp**: Kiểm tra lead đã được xử lý trước để không làm việc lặp lại.
✅ **Hoạt động liên tục**: Workflow có thể kết nối với **ProspectPro Trigger** để tự động chạy khi có lead mới.
:::

---

## 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
- **Tài khoản ProspectPro** (để lấy ID lead và cập nhật thông tin).
- **API Key của ProspectPro** (để kết nối với node `prospectpro`).
- **API Key của OpenAI** (để sử dụng GPT-4.1-mini).
- **Tài khoản BedrijfsData** (để sử dụng Web RAG và lấy dữ liệu website).
- **API Key của BedrijfsData** (để kết nối với node `bedrijfsdata`).

:::note[Lưu ý quan trọng]
- **Web RAG yêu cầu domain name** của lead. Nếu domain không có, lead sẽ được đánh tag "ManualQualification" để xử lý thủ công.
- **Token limit**: Đảm bảo cấu hình giới hạn token trong OpenAI để tránh chi phí bất ngờ.
:::

---

## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
1. Mở **n8n Workflow Editor**.
2. Nhấn **"Import"** và chọn file JSON (hoặc paste JSON từ [link gốc](https://n8n.io/workflows/8470)).
3. Chọn **"Import"** để hoàn tất.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này có **21 node** và cần cấu hình chi tiết như sau:

#### **A. Cấu hình Credentials (Tài khoản API)**
- **ProspectPro API**:
  - Đi đến **Settings > Credentials** trong n8n.
  - Thêm credential mới với tên `prospectproApi` và nhập **API Key** từ ProspectPro.
- **OpenAI API**:
  - Thêm credential mới với tên `openAiApi` và nhập **API Key** từ OpenAI.
- **BedrijfsData API**:
  - Thêm credential mới với tên `bedrijfsdataApi` và nhập **API Key** từ BedrijfsData.

#### **B. Cấu hình các node quan trọng**
1. **`ProspectPro Trigger Example`**:
   - Node này dùng để **bắt đầu workflow** khi có lead mới từ ProspectPro.
   - **Lưu ý**: Nếu không muốn sử dụng trigger này, các sếp có thể **bỏ qua** và chạy workflow thủ công.

2. **`Get Prospect`**:
   - Node này lấy thông tin lead từ ProspectPro dựa trên **Prospect ID**.
   - **Kiểm tra**: Nếu lead đã được xử lý trước (có tag "AutoQualified"), workflow sẽ **dừng lại** để tránh trùng lặp.

3. **`Get RAG domain` & `Get RAG search`**:
   - Node này lấy **dữ liệu website** (homepage, about, contact, etc.) và **snippets từ search engine** của lead.
   - **Lưu ý**: Nếu domain không có, lead sẽ được đánh tag **"ManualQualification"** và workflow sẽ **dừng lại**.

4. **`Basic LLM Chain`**:
   - Node này sử dụng **GPT-4.1-mini** để phân tích dữ liệu website và quyết định liệu lead có phù hợp với ICP không.
   - **Prompt đã được tối ưu**: Các sếp có thể **không cần chỉnh sửa** nếu muốn sử dụng mặc định.
   - **Lưu ý**: Đảm bảo **giới hạn token** trong OpenAI để tránh chi phí cao.

5. **`Structured Output Parser`**:
   - Node này **chuyển đổi kết quả của LLM** thành định dạng có cấu trúc (ví dụ: `{"isQualified": true/false, "tags": [...]}`).
   - **Lưu ý**: Các sếp có thể **cập nhật yêu cầu phân loại** theo nhu cầu của mình.

6. **`Qualify & Tag Prospect` (Code Node)**:
   - Node này **đánh tag** cho lead trong ProspectPro:
     - `AutoQualified` (nếu lead phù hợp với ICP).
     - `ManualQualification` (nếu cần xử lý thủ công).
   - **Lưu ý**: Các sếp có thể **chỉnh sửa logic** trong code node này để phù hợp với tiêu chí ICP của mình.

7. **`Update Prospect in ProspectPro`**:
   - Node này **cập nhật thông tin lead** trong ProspectPro (ví dụ: thêm tag, cập nhật label).
   - **Lưu ý**: Đảm bảo **operation = "patch"** để cập nhật thông tin một cách an toàn.

#### **C. Kích hoạt ⚡️**
1. **Test Run**:
   - Chọn **Prospect ID** mẫu (ví dụ: `12345`) và chạy **Test Run** để kiểm tra workflow.
   - Kiểm tra kết quả trong **ProspectPro** để đảm bảo lead được đánh tag đúng.
2. **Bật Active**:
   - Sau khi test thành công, chuyển workflow sang **Active**.

---

## ✍️ **Mẹo & gợi ý nâng cao**
:::tip[CÁCH NÂNG CAO HIỆU QUẢ]
1. **Kết nối với Slack/Telegram**:
   - Thêm node **Slack** hoặc **Telegram** để thông báo kết quả phân loại lead ngay khi workflow chạy.
   - Ví dụ: Nếu lead được đánh tag `AutoQualified`, gửi tin nhắn tự động đến nhóm bán hàng.

2. **Lưu log hoạt động**:
   - Sử dụng node **Google Sheets** hoặc **Airtable** để lưu lịch sử phân loại lead.
   - Giúp các sếp **theo dõi hiệu suất** và **optimize tiêu chí ICP**.

3. **Tự động gửi báo cáo định kỳ**:
   - Sử dụng **n8n Scheduler** để chạy workflow hàng ngày và gửi báo cáo tổng hợp về lead mới.
   - Ví dụ: Báo cáo số lượng lead được phân loại, tỷ lệ chuyển đổi, và lead cần xử lý thủ công.

4. **Tối ưu token OpenAI**:
   - Sử dụng **node `code`** để kiểm tra và giảm bớt token không cần thiết trong prompt.
   - Ví dụ: Loại bỏ thông tin trùng lặp hoặc không liên quan trong dữ liệu website trước khi gửi cho LLM.

5. **Phân loại lead theo nhiều tiêu chí**:
   - Mở rộng **Structured Output Parser** để phân loại lead theo nhiều tiêu chí (ví dụ: ngành nghề, quy mô công ty, vị trí địa lý).
   - Ví dụ: `{"isQualified": true, "industry": "Tech", "size": "Medium", "location": "Việt Nam"}`.
:::

---

## 📌 **Kết luận**
Workflow này là **giải pháp hoàn chỉnh** để các sếp tự động hóa **quy trình xác minh và phân loại lead B2B** một cách hiệu quả. Bằng cách kết hợp **ProspectPro, Web RAG và GPT-4**, các sếp không chỉ **tiết kiệm thời gian** mà còn **tăng độ chính xác** và **tránh trùng lặp** trong quá trình làm việc.

:::success[**Hành động ngay hôm nay!**]
1. **Import workflow** và cấu hình credentials.
2. **Test với lead mẫu** để đảm bảo hoạt động đúng.
3. **Bật Active** và kết nối với **ProspectPro Trigger** để tự động hóa toàn bộ quy trình.
4. **Mở rộng** bằng cách thêm Slack, log hoạt động hoặc báo cáo định kỳ.

**🚀 Hãy bắt đầu tự động hóa bán hàng của mình ngay bây giờ!** 🚀
:::

---
**🔗 [Tải workflow nguyên bản](https://n8n.io/workflows/8470)**
**💬 Có vấn đề? Liên hệ [ProspectPro](https://www.prospectpro.nl/klantenservice/)**