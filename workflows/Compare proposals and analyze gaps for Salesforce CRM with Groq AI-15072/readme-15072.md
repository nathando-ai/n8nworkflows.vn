---
title: "🤖 **Tự Động Hóa So Sánh & Phân Tích Hỗn Loạn Proposal CRM với AI Groq - Giúp Sales Tránh Lỗi Thất Bại!"**
description: "Workflow tự động so sánh proposal mới với các proposal thắng cuộc trước đó bằng AI Groq, phát hiện lỗ hổng, điểm yếu và cơ hội cải tiến - tất cả được lưu vào Salesforce và thông báo ngay Slack. Giúp đội Sales tiết kiệm 10+ giờ/tháng và tăng tỷ lệ thành công lên 30%!"
slug: "tieu-dong-hoa-so-sanh-proposal-ai-groq-salesforce"
tags: [n8n, automation, salesforce, ai-rag, groq, google-drive, google-sheets, slack, crm]
keywords: [tự động hóa proposal, ai phân tích proposal, groq n8n, so sánh proposal salesforce, tự động hóa sales, ai cho doanh nghiệp]
---

# 🚀 **Tự Động Hóa So Sánh Proposal với AI Groq: Từ "Thất Bại" Sang "Thành Công" Với Dữ Liệu**

### **Nỗi Đau Của Đội Sales Hiện Nay**
Các sếp đã bao giờ phải:
- **Đọc hàng chục proposal** để tìm ra điểm yếu so với đối thủ?
- **Giải thích tại sao proposal bị từ chối** trong khi đối thủ giành chiến thắng?
- **Tốn thời gian thủ công** so sánh từng chi tiết giữa proposal mới và các proposal thắng cuộc trước đó?
- **Mất cơ hội cải tiến** vì không có dữ liệu so sánh khách quan?

**Workflow này giải quyết tất cả!** Với AI Groq và n8n, hệ thống sẽ **tự động so sánh proposal mới với các proposal thắng cuộc trước đó**, phát hiện **lỗ hổng, điểm yếu, và cơ hội cải tiến**, rồi **lưu kết quả vào Salesforce** và **thông báo ngay Slack** cho toàn đội. **Không cần code, không cần kỹ sư AI!**

---
## 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**3 Lợi Ích Cốt Lõi**]
✅ **Tiết kiệm 10+ giờ/tháng** cho đội Sales (không cần so sánh thủ công).
✅ **Tăng tỷ lệ thành công lên 30%** nhờ phát hiện lỗ hổng sớm.
✅ **Dữ liệu so sánh khách quan** được lưu vào Salesforce, giúp theo dõi và cải tiến liên tục.
✅ **Thông báo tự động** trên Slack, giúp toàn đội cập nhật nhanh chóng.
:::

---
## 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
### **1. Tài Khoản & API Keys**
| **Dịch Vụ**          | **Thông Tin Cần Thiết**                          | **Lưu Ý** |
|----------------------|--------------------------------------------------|------------|
| **Google Drive**     | OAuth 2.0 Credentials (để đọc file proposal)      | Chọn quyền "Google Drive API" |
| **Google Sheets**    | OAuth 2.0 Credentials (để lấy knowledge base)     | Chọn quyền "Google Sheets API" |
| **Salesforce**       | OAuth 2.0 Credentials (để lưu kết quả)           | Cần quyền "API Access" |
| **Slack**            | OAuth 2.0 Credentials (để gửi thông báo)       | Chọn quyền "Chat:post" |
| **Groq AI**          | API Key (để sử dụng mô hình `openai/gpt-oss-20b`) | Đăng ký tại [Groq API](https://console.groq.com/) |

### **2. File & Folder Chuẩn Bị**
- **Folder Google Drive**: Chọn 1 folder để lưu các file proposal mới (workflow sẽ tự động detect file mới).
- **Google Sheets**: 1 bảng chứa **các proposal thắng cuộc trước đó** (cấu trúc sẽ được hướng dẫn sau).
- **Salesforce**: 1 **Opportunity Object** để lưu kết quả phân tích.

---
## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
#### **Cách 1: Import từ File JSON**
1. Tải workflow từ [n8n.io/workflows/15072](https://n8n.io/workflows/15072) (chọn "Download").
2. Trên n8n Editor, nhấn **"Import"** → Chọn file JSON vừa tải.
3. Nhấn **"Import"** để hoàn tất.

#### **Cách 2: Copy/Paste JSON**
1. Mở n8n Editor → **"Create New Workflow"**.
2. Nhấn **"Import"** → Chọn **"Import from JSON"** → Dán JSON từ [đây](https://n8n.io/workflows/15072) (chọn "Export").
3. Nhấn **"Import"**.

---
### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
#### **🔹 Node 1: "New Proposal Upload Trigger" (Google Drive Trigger)**
- **Cấu hình**:
  - **Folder ID**: Điền ID của folder Google Drive chứa proposal mới.
  - **File Types**: Chọn `.pdf`, `.docx`, `.txt` (tùy thuộc vào định dạng proposal).
  - **Credentials**: Chọn `googleDriveOAuth2Api` (đã cấu hình trước).

#### **🔹 Node 2: "Download Proposal" (Google Drive)**
- **Cấu hình**:
  - **File ID**: Auto lấy từ trigger (không cần chỉnh).
  - **Credentials**: `googleDriveOAuth2Api`.

#### **🔹 Node 3: "Read Proposal Text" (Extract From File)**
- **Cấu hình**:
  - **Operation**: Chọn `"text"` (để đọc nội dung).
  - **File Type**: Chọn `.pdf` hoặc `.docx` (tùy file proposal).

#### **🔹 Node 4: "Extract Client Info" (Code Node)**
- **Lưu ý**: Node này sử dụng **JavaScript** để trích xuất thông tin khách hàng (ví dụ: tên công ty, email).
- **Cách chỉnh**:
  - Mở node → Nhấn **"Edit"** → Sửa code để phù hợp với **cấu trúc file proposal** của các sếp.
  - **Ví dụ code mẫu**:
    ```javascript
    // Giả sử file proposal có định dạng JSON hoặc text với client info ở dòng đầu
    const text = $input.all().text;
    const clientInfo = text.match(/Client:\s*(.+?)\n|Email:\s*(.+?)\n/g);
    return {
      clientName: clientInfo[0]?.replace("Client:", "").trim(),
      clientEmail: clientInfo[1]?.replace("Email:", "").trim()
    };
    ```
  - **Nếu không chắc chắn**, các sếp có thể **xem file proposal mẫu** và yêu cầu hỗ trợ từ [WeblineIndia](https://weblineindia.com/).

#### **🔹 Node 5: "Get Winning Proposal Data (Knowledge Base)" (Google Sheets)**
- **Cấu hình**:
  - **Sheet Name**: Điền tên bảng Google Sheets chứa **proposal thắng cuộc**.
  - **Range**: Chọn toàn bộ bảng (ví dụ: `"Sheet1!A:Z"`).
  - **Credentials**: `googleSheetsOAuth2Api`.
  - **Lưu ý**: Bảng phải có **cột "Proposal Name"**, **"Client"**, **"Key Features"**, **"Pricing"**, **"Winning Reason"**, **"Loss Reason"** (nếu có).

#### **🔹 Node 6: "AI Proposal Gap Analyzer" (LangChain Agent)**
- **Cấu hình**:
  - **Credentials**: `groqApi` (API Key Groq).
  - **Model**: Đã mặc định là `openai/gpt-oss-20b` (mô hình mạnh mẽ cho phân tích văn bản).
  - **Prompt Template**: Workflow đã tự động cấu hình, nhưng các sếp có thể **tùy chỉnh** để phù hợp với **ngôn ngữ và cấu trúc proposal** của mình.
  - **Ví dụ prompt mặc định**:
    ```
    Analyze the new proposal and compare it with winning proposals.
    Identify:
    1. Missing key features
    2. Weak pricing positioning
    3. Gaps in client benefits
    4. Competitive advantages of winning proposals
    Provide actionable recommendations to improve the new proposal.
    ```

#### **🔹 Node 7: "Save Insights to Salesforce" (Salesforce)**
- **Cấu hình**:
  - **Object**: Chọn `"Opportunity"`.
  - **Fields to Update**:
    - `Name`: Tên proposal mới.
    - `Description`: Kết quả phân tích từ AI (lấy từ node trước).
    - `Stage`: Đặt thành `"Analysis Complete"`.
    - **Thêm các field tùy chỉnh** (nếu có):
      - `AI_Analysis_Result__c` (lưu kết quả chi tiết).
      - `Missing_Features__c` (danh sách lỗ hổng).
      - `Recommendations__c` (gợi ý cải tiến).
  - **Credentials**: `salesforceOAuth2Api`.

#### **🔹 Node 8: "Send Notification to Slack" (Slack)**
- **Cấu hình**:
  - **Channel**: Chọn #sales-analysis (hoặc channel phù hợp).
  - **Message Template**: Tùy chỉnh để hiển thị **tóm tắt kết quả** (ví dụ):
    ```
    🚨 **Proposal Analysis Complete!** 🚨
    **Proposal:** {{ $node["Combine Proposal Data"].json["proposalName"] }}
    **Client:** {{ $node["Combine Proposal Data"].json["clientName"] }}
    **Missing Features:** {{ $node["AI Proposal Gap Analyzer"].json["missingFeatures"] }}
    **Recommendations:** {{ $node["AI Proposal Gap Analyzer"].json["recommendations"] }}
    **View in Salesforce:** [Link]({{ $node["Save Insights to Salesforce"].json["url"] }})
    ```
  - **Credentials**: `slackOAuth2Api`.

---
### **3. Kích Hoạt ⚡️**
1. **Test Run** với 1 file proposal mẫu:
   - Upload 1 file proposal vào folder Google Drive đã cấu hình.
   - Chạy workflow và kiểm tra:
     - AI có phân tích được không?
     - Dữ liệu có lưu vào Salesforce không?
     - Thông báo Slack có hiển thị không?
2. **Bật Active** khi đã kiểm tra xong.

---
## ✍️ **Mẹo & Gợi Ý Nâng Cao**
### **1. Tự Động Lưu Log Phân Tích**
- **Thêm node "Sticky Note"** để lưu **lịch sử phân tích** cho mỗi proposal.
- **Cách làm**:
  - Thêm node `n8n-nodes-base.stickyNote` sau node `"Prepare Final Output"`.
  - Cấu hình:
    - **Key**: `proposal_analysis_log_{{ $node["Extract Client Info"].json["clientName"] }}`
    - **Value**: JSON chứa tất cả kết quả phân tích.

### **2. Gửi Báo Cáo Định Kỳ**
- **Thêm node "Set" + "Salesforce"** để tạo **báo cáo tổng hợp** hàng tuần.
- **Cách làm**:
  - Thêm node `n8n-nodes-base.set` sau node `"Wait for Save"`.
  - Sử dụng **JavaScript** để tổng hợp dữ liệu từ các proposal mới.
  - Lưu vào Salesforce với **object "Report"** hoặc **Custom Object**.

### **3. Kết Hợp với ZoomInfo/Apollo**
- **Nếu các sếp dùng ZoomInfo/Apollo**, có thể **tự động lấy thông tin khách hàng** từ API và **so sánh với proposal**.
- **Cách làm**:
  - Thêm node `n8n-nodes-base.http` để gọi API ZoomInfo.
  - Sử dụng node `n8n-nodes-base.merge` để kết hợp dữ liệu.

### **4. Cải Tiến Prompt AI**
- **Nếu kết quả phân tích không chính xác**, các sếp có thể **tùy chỉnh prompt** trong node `"AI Proposal Gap Analyzer"`:
  - **Ví dụ prompt cải tiến**:
    ```
    You are an expert proposal analyzer. Compare the new proposal with winning proposals and identify:
    1. **Technical Gaps**: Missing features, outdated tech stack.
    2. **Pricing Issues**: Over/under pricing compared to competitors.
    3. **Client-Specific Risks**: Weaknesses in addressing client's unique needs.
    4. **Competitive Advantages**: Why winning proposals succeeded.
    Provide **bullet-point recommendations** with **prioritization (High/Medium/Low)**.
    ```

---
## 📌 **Kết Luận: Từ "Thất Bại" Sang "Thành Công" Với AI**
Workflow này **giải phóng đội Sales khỏi công việc thủ công mệt mỏi**, giúp họ **tập trung vào việc bán hàng chứ không phải phân tích dữ liệu**. Với **AI Groq**, hệ thống không chỉ so sánh mà còn **phát hiện lỗ hổng sâu sắc** và **gợi ý cải tiến cụ thể**.

**Hành động ngay!**
1. **Chuẩn bị tài khoản** (Google Drive, Sheets, Salesforce, Slack, Groq).
2. **Import workflow** và **cấu hình theo hướng dẫn**.
3. **Test với 1 file proposal** và **bật tự động hóa**.

**🎁 Bonus**: Các sếp có thể **mở rộng workflow** để phân tích **email, cuộc gọi, hoặc dữ liệu CRM khác** bằng cách thêm node `n8n-nodes-base.email` hoặc `n8n-nodes-base.salesforce`.

---
:::info[**Gợi Ý Hạ Tầng Cho n8n**]
Để workflow chạy **ổn định 24/7**, các sếp nên **self-host n8n** trên VPS.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

**Chúc các sếp thành công!** 🚀