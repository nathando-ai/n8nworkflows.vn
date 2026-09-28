---
title: "🚀 Tự Động Hoá Nghiên Cứu & Tóm Tắt Dữ Liệu Leads B2B Từ Google Sheets Sang Airtable Với AI (BrowserAct + LangChain)"
description: "Workflow tự động hóa hoàn toàn không cần code giúp các sếp tự động scrap thông tin chi tiết từ trang web của các công ty B2B, tổng hợp và phân tích bằng AI, sau đó lưu trữ vào Airtable với định dạng chuẩn CRM. Giúp tiết kiệm thời gian lên đến 80% trong quá trình nghiên cứu thị trường và quản lý leads."
slug: "tu-dong-hoa-nghien-cuu-leads-b2b-google-sheets-airtable"
tags: [n8n, automation, no-code, ai-summarization, browseract, airtable, google-sheets, langchain, b2b-marketing]
keywords: [n8n workflow b2b, tự động hóa nghiên cứu thị trường, ai tổng hợp dữ liệu, airtable crm, browseract scrap website, langchain n8n, tự động hóa leads b2b]
---

# 🚀 **Tự Động Hoá Nghiên Cứu & Tóm Tắt Dữ Liệu Leads B2B Từ Google Sheets Sang Airtable Với AI**

## **🔍 Nỗi Đau Của Các Sếp Trong Nghiên Cứu Thị Trường B2B**
Hàng ngày, các sếp và đội ngũ marketing phải:
- **Tìm kiếm thủ công** thông tin chi tiết về hàng trăm công ty tiềm năng (B2B leads) trên Google, LinkedIn hay trang web của họ.
- **Tóm tắt và phân tích** thông tin từ các trang web dài dòng, bài báo, và tài liệu PDF để rút ra thông tin quan trọng.
- **Ghi chép vào CRM** (Airtable, Salesforce...) một cách rườm rà, dễ bị lỗi và mất thời gian.
- **Cập nhật thường xuyên** để đảm bảo dữ liệu không lỗi thời.

Kết quả? **Thời gian nghiên cứu tăng gấp 3-5 lần**, chất lượng dữ liệu không đồng nhất, và quyết định marketing bị ảnh hưởng bởi thông tin không đầy đủ hoặc lỗi thời.

---
### **🎯 Giải Pháp: Workflow Tự Động Hoá AI-Powered**
Workflow này **tự động hóa toàn bộ quy trình** từ việc **scrap dữ liệu từ website** → **tóm tắt và phân tích bằng AI** → **lưu trữ vào Airtable** với định dạng chuẩn CRM. Các sếp chỉ cần:
✅ **Chỉnh sửa 1 file Google Sheets** với danh sách URL của các công ty B2B.
✅ **Nhận kết quả tự động** trong Airtable với thông tin chi tiết, tóm tắt AI, và đánh giá tiềm năng.
✅ **Cập nhật liên tục** mà không cần can thiệp thủ công.

---
## **🎯 Kết Quả Các Sếp Nhận Được**

:::tip[**3 Lợi Ích Cốt Lõi**]
- **Tiết kiệm thời gian lên đến 80%** trong nghiên cứu thị trường (so với cách làm thủ công).
- **Dữ liệu chính xác và đồng nhất** do AI tự động tóm tắt và phân loại thông tin từ nhiều nguồn.
- **CRM tự động cập nhật** với định dạng chuẩn (Name, Industry, Notes, Status, Contact Info...), giúp đội ngũ sales dễ dàng theo dõi và ưu tiên leads.
- **Hoạt động 24/7** mà không cần can thiệp của con người, giảm thiểu lỗi do con người gây ra.
:::

---

## **🔧 Yêu Cầu Cần Thiết**

:::info[**CHUẨN BỊ TRƯỚC KHI BẮT ĐẦU**]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản và API Keys:**
   - **BrowserAct** (để scrap dữ liệu từ website).
   - **OpenRouter** (API cho mô hình AI GPT-5 và Gemini).
   - **Google Sheets** (để lưu danh sách URL và dữ liệu đầu vào).
   - **Airtable** (để lưu kết quả cuối cùng).
   - **OAuth 2.0 Credentials** cho Google Sheets và Airtable.

2. **File Google Sheets chuẩn:**
   - Một sheet với **cột "Page URL"** chứa danh sách các trang web công ty B2B cần nghiên cứu.
   - Ví dụ:
     | Page URL               |
     |------------------------|
     | https://example.com    |
     | https://company2.com   |

3. **Airtable Base chuẩn:**
   - Tạo một **base** mới với các trường phù hợp với schema output (ví dụ: `Name`, `Industry`, `Notes`, `Status`, `Contact Email`, `Website`).
   - Workflow sẽ tự động tạo các record mới với định dạng này.

4. **BrowserAct Template:**
   - Chọn **template "B2B Contact Research"** trong tài khoản BrowserAct của mình.
   - [Hướng dẫn cài đặt template](https://docs.browseract.com).

---
## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/13385](https://n8n.io/workflows/13385) (chọn "Export").
2. **Mở n8n Editor** (trên máy chủ self-hosted hoặc n8n.cloud).
3. Nhấn **"Import"** và chọn file JSON vừa tải.
4. Chọn **"Import"** để workflow xuất hiện trên canvas.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Copy toàn bộ mã JSON** từ [n8n.io/workflows/13385](https://n8n.io/workflows/13385) (chọn "Export" → "Copy JSON").
2. Trong n8n Editor, nhấn **"Import"** → **"Paste JSON"** và dán mã vào.
3. Chọn **"Import"** để workflow xuất hiện.

---

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**

Workflow này gồm **14 node** với các chức năng chính sau. Dưới đây là **các node quan trọng cần cấu hình kỹ**:

#### **🔹 Node "Manual Trigger" (Bắt đầu thủ công)**
- **Lưu ý:** Node này cho phép các sếp **khởi động workflow thủ công** khi cần.
- **Cách sử dụng:**
  - Nhấn nút **"Run"** trên node này để bắt đầu quá trình tự động hóa.

#### **🔹 Node "Retrieve Input Data" (Lấy dữ liệu từ Google Sheets)**
- **Cấu hình:**
  - **Credentials:** Chọn `googleSheetsOAuth2Api` (đã cấu hình trước).
  - **Sheet Name:** Điền tên sheet chứa danh sách URL (ví dụ: `"B2B Leads"`).
  - **Range:** Điền `"Page URL!A:A"` (giả sử cột URL ở cột A).
  - **Operation:** Chọn `"get"` để lấy dữ liệu.

#### **🔹 Node "Extract Target Page Data" (BrowserAct - Scrap website)**
- **Cấu hình:**
  - **Credentials:** Chọn `browserActApi`.
  - **Template:** Chọn `"B2B Contact Research"` (đã cài đặt trước).
  - **Input Data:** Liên kết với node `Retrieve Input Data` (URL từ Google Sheets).
  - **Lưu ý:**
    - Đảm bảo **API Key của BrowserAct** đã được cấu hình đúng.
    - Nếu gặp lỗi, kiểm tra [hướng dẫn kết nối n8n với BrowserAct](https://docs.browseract.com).

#### **🔹 Node "Analyze the Company Page" (AI Agent - Tóm tắt bằng LangChain)**
- **Cấu hình:**
  - **Credentials:** Chọn `openRouterApi`.
  - **Model:** Sử dụng `openai/gpt-5` (để phân tích chi tiết) và `google/gemini-3-flash-preview` (để tóm tắt nhanh).
  - **Prompt:** Workflow tự động cấu hình, nhưng các sếp có thể **cập nhật prompt** để phù hợp với nhu cầu phân tích cụ thể (ví dụ: yêu cầu AI chú trọng đến thông tin về sản phẩm, giá trị thị trường, hoặc đối thủ cạnh tranh).
  - **Lưu ý:**
    - Nếu mô hình AI trả về kết quả không chính xác, hãy **cập nhật prompt** trong node `lmChatOpenRouter` hoặc `agent`.

#### **🔹 Node "Aggregate" (Kết hợp dữ liệu)**
- **Cấu hình:**
  - **Operation:** Chọn `"aggregate"` để ghép tất cả dữ liệu scrap và phân tích từ các URL.
  - **Lưu ý:** Node này đảm bảo dữ liệu được **truyền liên tục** từ scrap → AI → Airtable.

#### **🔹 Node "Create a record" (Lưu vào Airtable)**
- **Cấu hình:**
  - **Credentials:** Chọn `airtableOAuth2Api`.
  - **Base ID:** Điền ID của Airtable Base (tìm trong URL của base, ví dụ: `app123abc` trong `https://airtable.com/app123abc`).
  - **Table Name:** Điền tên bảng (ví dụ: `"B2B Leads"`).
  - **Fields:** Đảm bảo các trường trong Airtable **khớp với schema** từ node `Structured Output Parser` (ví dụ: `Name`, `Industry`, `Notes`, `Status`).
  - **Lưu ý:**
    - Nếu Airtable không có trường nào, **tạo mới** trước khi chạy workflow.
    - Kiểm tra **định dạng JSON** trong node `Structured Output Parser` để đảm bảo dữ liệu truyền vào Airtable đúng định dạng.

#### **🔹 Node "Update Database" (Cập nhật Google Sheets)**
- **Cấu hình:**
  - **Credentials:** Chọn `googleSheetsOAuth2Api`.
  - **Sheet Name:** Điền tên sheet (ví dụ: `"B2B Leads"`).
  - **Range:** Điền `"Page URL!A:A"` (cột chứa URL).
  - **Operation:** Chọn `"update"` để ghi kết quả phân tích vào cột mới (ví dụ: `"Status"` hoặc `"Notes"`).
  - **Lưu ý:** Workflow sẽ tự động **cập nhật trạng thái** của mỗi lead (ví dụ: `"Đang phân tích"`, `"Hoàn thành"`, `"Không phù hợp"`).

---

### **3. Kích Hoạt Workflow ⚡️**
1. **Test Run (Chạy thử với dữ liệu mẫu):**
   - Chọn **1-2 URL** trong Google Sheets và chạy node `Manual Trigger`.
   - Kiểm tra:
     - Dữ liệu scrap từ BrowserAct có chính xác không?
     - AI có tóm tắt và phân tích đúng không?
     - Airtable có nhận được record mới không?

2. **Bật Active Workflow:**
   - Sau khi kiểm tra thành công, **bật chế độ Active** để workflow chạy tự động khi có sự kiện (nếu cần thiết).

---

## **✍️ Mẹo & Gợi Ý Nâng Cao**

### **1. Tối Ưu Hóa AI Cho Phù Hợp Với Doanh Nghiệp**
- **Cập nhật Prompt:**
  - Mở node `lmChatOpenRouter` hoặc `agent` và **sửa prompt** để AI tập trung vào thông tin quan trọng hơn (ví dụ: yêu cầu AI **so sánh công ty với đối thủ**, **đánh giá tiềm năng hợp tác**, hoặc **tóm tắt thông tin về sản phẩm chính**).
  - Ví dụ một **prompt nâng cao**:
    > *"Tôi là một chuyên gia marketing B2B. Tóm tắt thông tin chi tiết về công ty [NAME] từ trang web [URL]. Đặc biệt chú trọng đến:
    > - Sản phẩm/dịch vụ chính và giá trị độc đáo (USP).
    > - Thị trường mục tiêu và đối thủ cạnh tranh.
    > - Thông tin liên lạc của CEO/giám đốc bán hàng.
    > - Báo cáo tài chính gần nhất (nếu có).
    > Trả về kết quả dưới dạng JSON với các trường: `Name`, `Industry`, `MainProducts`, `TargetMarket`, `Competitors`, `ContactPerson`, `ContactEmail`, `Notes`."*

- **Thử nghiệm mô hình AI khác:**
  - Thay đổi mô hình từ `openai/gpt-5` sang `mistralai/mixtral-8x7b` (nếu OpenRouter hỗ trợ) để kiểm tra hiệu suất.

### **2. Tích Hợp Slack/Telegram Cho Báo Cáo Thực Tiempo**
- **Thêm node Slack/Telegram** sau node `Create a record` để **báo cáo kết quả mới** ngay khi có.
- **Cách làm:**
  1. Thêm node `n8n-nodes-slack.webhook` hoặc `n8n-nodes-telegram.bot`.
  2. Cấu hình **webhook URL** từ Slack/Telegram.
  3. Sử dụng **template thông báo** như:
     > *"🚀 **Lead mới được phân tích:**
     > - **Tên công ty:** {{ $node["Create a record"].json["Name"] }}
     > - **Ngành nghề:** {{ $node["Create a record"].json["Industry"] }}
     > - **Trạng thái:** {{ $node["Create a record"].json["Status"] }}
     > - **Link:** {{ $node["Create a record"].json["Website"] }}
     > - **Ghi chú:** {{ $node["Create a record"].json["Notes"] }}
     > *Xem chi tiết tại Airtable: [Link](https://airtable.com/...)*"*

### **3. Lưu Log & Theo Dõi Lỗi**
- **Thêm node `n8n-nodes-base.stickyNote`** để ghi log các lỗi hoặc tiến trình.
- **Cách làm:**
  1. Thêm node `StickyNote` sau node `Extract Target Page Data` và `Create a record`.
  2. Điền nội dung log như:
     > *"Scrap URL: {{ $node["Retrieve Input Data"].json["Page URL"] }}
     > - Trạng thái: {{ $node["Extract Target Page Data"].json["status"] }}
     > - Lỗi (nếu có): {{ $node["Extract Target Page Data"].json["error"] }}"*

### **4. Chạy Workflow Định Kỳ (Cron Job)**
- **Sử dụng node `n8n-nodes-base.schedule`** để chạy workflow **hàng ngày/tuần** thay vì thủ công.
- **Cách làm:**
  1. Thêm node `Schedule` vào đầu workflow.
  2. Cấu hình **thời gian chạy** (ví dụ: `0 0 * * *` để chạy hàng ngày lúc 00:00).
  3. Liên kết node `Schedule` với `Manual Trigger`.

### **5. Tự Động Xóa Dữ Liệu Lỗi Thời**
- **Thêm node `n8n-nodes-base.if`** để **xóa record trong Airtable** nếu dữ liệu quá cũ (ví dụ: >30