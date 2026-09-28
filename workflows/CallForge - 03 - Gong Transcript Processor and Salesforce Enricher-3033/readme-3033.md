---
title: "🚀 **Tự Động Hóa Xử Lý Transcript Gong & Nâng Cao Dữ Liệu Salesforce – CallForge (AI Sales Call Processor)**"
description: "Workflow này tự động trích xuất thông tin quan trọng từ cuộc gọi Gong, phân loại nội dung theo người nói (Internal/External), và enrich dữ liệu bằng Salesforce để tối ưu hóa quy trình bán hàng. Giúp các sếp tiết kiệm **50% thời gian** trong phân tích cuộc gọi và nâng cao hiệu quả team sales."
slug: "tieu-dong-hoa-xu-ly-transcript-gong-salesforce"
tags: [n8n, automation, salesforce, ai, gong, no-code, sales, sales-automation]
keywords: [n8n workflow salesforce, tự động hóa cuộc gọi gong, enrich dữ liệu sales, phân tích cuộc gọi ai, sales automation no-code, xử lý transcript gong]
---

# 🚀 **CallForge: Tự Động Hóa Xử Lý Transcript Gong & Nâng Cao Dữ Liệu Salesforce**

### **Giải pháp AI cho Sales Team: Từ Transcript → Dữ Liệu Sẵn Sàng Cho AI**
Hiện nay, các sếp và đội ngũ sales phải mất **giờ đồng hồ** để thủ công phân tích transcript cuộc gọi từ Gong, tra cứu thông tin khách hàng trên Salesforce, và tổng hợp dữ liệu để báo cáo. **Workflow CallForge** tự động hóa toàn bộ quy trình này bằng cách:
✅ **Trích xuất và phân loại** nội dung cuộc gọi theo người nói (Internal/External).
✅ **Nâng cao dữ liệu** bằng thông tin từ Salesforce (Opportunity, Account, Email).
✅ **Tạo ra một "data blob" sẵn sàng** để đầu vào cho các mô hình AI (LLM) sau này.
✅ **Tiết kiệm 50% thời gian** so với cách làm thủ công.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS chuyên dụng:
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** – giảm tới **39%**)
👉 **[VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** – Đảm bảo tốc độ xử lý nhanh cho workflow AI.
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần thủ công phân tích transcript và tra cứu Salesforce.
- **Dữ liệu chính xác**: Trích xuất thông tin khách hàng (Email, Company, Location) từ Salesforce và API bên thứ ba.
- **Sẵn sàng cho AI**: Data được định dạng chuẩn để đầu vào cho các mô hình LLM (ChatGPT, LlamaIndex, etc.).
- **Hoạt động liên tục**: Workflow chạy tự động sau mỗi cuộc gọi mới từ Gong.
- **Cá nhân hóa**: Phân loại nội dung theo người nói (Internal/External) để phân tích chi tiết.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Gong**:
   - **API Key** của Gong để lấy transcript và chi tiết cuộc gọi.
   - **Headers Auth** (cấu hình trong node `httpRequest`).
2. **Tài khoản Salesforce**:
   - **Credentials OAuth2** (cấu hình trong node `salesforce`).
   - **Permissions** để truy cập `Opportunity` và `Account`.
3. **API Key (nếu cần mở rộng)**:
   - **People Data Labs** (để enrich dữ liệu địa lý, *nếu mở rộng phần Enrich Call Data*).

---
### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/3033](https://n8n.io/workflows/3033) hoặc copy JSON từ trang này.
- Mở **n8n Editor** → Nhấn **Import Workflow** → Dán JSON hoặc tải file `.json`.
- **Kích hoạt workflow** bằng cách bật nút **Active** ở góc trên phải.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **18 node** với logic phức tạp. Dưới đây là **các bước cấu hình quan trọng**:

##### **A. Cấu hình API Gong (2 node `httpRequest`)**
- **Node 1**: `Retrieve detailed call data`
  - **URL**: `https://api.gong.io/v1/calls/{callId}` (thay `{callId}` bằng ID cuộc gọi từ trigger).
  - **Headers**:
    ```json
    {
      "Authorization": "Bearer YOUR_GONG_API_KEY",
      "Content-Type": "application/json"
    }
    ```
- **Node 2**: `Get transcript`
  - **URL**: `https://api.gong.io/v1/calls/{callId}/transcript`
  - **Headers**: Giống như node trên.

##### **B. Phân loại người nói (2 node `code`)**
- **Node `Join Affiliation`** và **`Join conversation`**:
  - Logic trong node này **phân loại người nói** thành `Internal` (nhân viên sales) hoặc `External` (khách hàng).
  - **Mẫu code tham khảo** (sửa theo yêu cầu):
    ```javascript
    // Node "Join Affiliation"
    $input.all().forEach(item => {
      if (item.participant.email.includes("@yourcompany.com")) {
        item.affiliation = "Internal";
      } else {
        item.affiliation = "External";
      }
    });
    return $input.all();
    ```
  - **Lưu ý**: Cần thay `@yourcompany.com` bằng domain của team sales.

##### **C. Trích xuất dữ liệu Salesforce (2 node `salesforce`)**
- **Node `Get Opp Data`**:
  - **Operation**: `get`
  - **Resource**: `opportunity`
  - **Query**: Lấy `Opportunity` liên quan đến cuộc gọi (ví dụ: `AccountId` từ transcript).
- **Node `Get account data`**:
  - **Operation**: `get`
  - **Resource**: `account`
  - **Query**: Lấy thông tin `Account` từ `AccountId` trong `Opportunity`.

##### **D. Gộp và định dạng dữ liệu (5 node `merge`/`aggregate`)**
- **Node `Merge call and transcript Data`**: Gộp transcript và metadata cuộc gọi.
- **Node `Aggregate Gong Call Transcript`**: Tạo một chuỗi text liên tục từ transcript.
- **Node `Aggregate Salesforce data`**: Gộp dữ liệu `Opportunity` và `Account`.
- **Node `Merge Enriched Transcript Data`**: Kết hợp tất cả dữ liệu thành một "data blob" chuẩn cho AI.

##### **E. Lọc Email khách hàng (node `set`)**
- **Node `Get External Attendees Emails`**:
  - Trích xuất email của khách hàng (`External`) từ transcript.
  - **Mẫu code tham khảo**:
    ```javascript
    $input.all().forEach(item => {
      const emails = item.transcript.match(/[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}/g);
      item.externalEmails = emails || [];
    });
    return $input.all();
    ```

---

#### **3. Kích hoạt ⚡️**
- **Test run** với một cuộc gọi mẫu:
  1. Nhấn **Run Workflow** và chọn một cuộc gọi từ Gong.
  2. Kiểm tra **output** ở node cuối (`Merge Enriched Transcript Data`).
  3. Nếu dữ liệu hợp lý, **bật Active workflow**.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết hợp với Slack/Telegram**:
   - Thêm node `slack` hoặc `telegram` để báo cáo kết quả cuộc gọi ngay khi xử lý xong.
   - **Mẫu prompt Slack**:
     ```json
     {
       "text": "📞 Cuộc gọi mới từ Gong:\n- **Khách hàng**: {{externalEmails[0]}}\n- **Company**: {{account.Name}}\n- **Opportunity**: {{opportunity.Name}}\n- **Tóm tắt**: {{aggregatedTranscript}}"
     }
     ```

2. **Lưu log vào Google Sheets/Notion**:
   - Thêm node `googleSheets` hoặc `notion` để lưu dữ liệu đã enrich vào bảng tóm tắt.

3. **Sử dụng AI để phân tích sâu**:
   - Sau khi có `data blob`, các sếp có thể **đầu vào vào một workflow AI khác** (ví dụ: sử dụng `n8n-nodes-ai` để phân tích sentiment hoặc trích xuất intent).

4. **Tự động gửi báo cáo định kỳ**:
   - Sử dụng **node `setInterval`** (cài đặt từ `n8n-nodes-base`) để chạy workflow hàng ngày và gửi báo cáo email.

---

### 📌 **Kết luận**
**CallForge** là **công cụ tự động hóa mạnh mẽ** cho đội ngũ sales, giúp:
✔ **Tiết kiệm thời gian** trong phân tích cuộc gọi.
✔ **Nâng cao chất lượng dữ liệu** bằng Salesforce.
✔ **Sẵn sàng cho AI** để phân tích sâu hơn.

**Hành động ngay**:
1. **Import workflow** và cấu hình API.
2. **Test với một cuộc gọi mẫu**.
3. **Bật Active** và bắt đầu tự động hóa!

---
**💡 Lưu ý cuối cùng**:
- Nếu gặp vấn đề với **Salesforce API**, kiểm tra lại **credentials OAuth2** và **permissions**.
- Đối với **node `code`**, các sếp có thể **tùy chỉnh logic phân loại** theo yêu cầu cụ thể của team.

**Chúc các sếp thành công với CallForge!** 🚀