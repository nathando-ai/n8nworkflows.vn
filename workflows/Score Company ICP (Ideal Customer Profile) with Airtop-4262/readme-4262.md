---
title: "🔍 **Tự Động Hóa Đánh Giá ICP (Ideal Customer Profile) Cho Doanh Nghiệp Bằng LinkedIn - Không Cần Code!**"
description: "Workflow này tự động phân tích hồ sơ LinkedIn của công ty, tính điểm ICP dựa trên tiêu chí AI, kỹ thuật, quy mô nhân sự và vị trí địa lý - giúp các sếp lọc leads B2B chất lượng, tiết kiệm thời gian và tối ưu chiến lược bán hàng. Kết quả là một báo cáo chi tiết với điểm số và lý do cụ thể cho từng tiêu chí."
slug: "tieu-dong-hoa-danh-gia-icp-company-bang-linkedin"
tags: [n8n, automation, sales, airtop, icp-scoring, no-code, linkedin-automation]
keywords: [tự động hóa icp, scoring leads b2b, airtop n8n, đánh giá doanh nghiệp trên linkedin, tự động hóa bán hàng, workflow icp]
---

# **🚀 Tự Động Hóa Đánh Giá ICP (Ideal Customer Profile) Cho Doanh Nghiệp Bằng LinkedIn - Không Cần Code!**

### **💡 Giải Pháp Cho Nỗi Đau Của Các Sếp**
Bạn đã bao giờ phải:
- **Lọc thủ công** hàng trăm hồ sơ LinkedIn để tìm ra khách hàng tiềm năng phù hợp?
- **Mất thời gian** phân tích chi tiết về quy mô nhân sự, ngành nghề, hoặc mức độ tập trung vào AI/tech của mỗi công ty?
- **Không biết** cách ưu tiên outreach cho những lead có khả năng chuyển đổi cao nhất?

Workflow này **tự động hóa toàn bộ quá trình** bằng cách:
✅ **Trích xuất dữ liệu** từ LinkedIn (thông tin về nhân sự, ngành nghề, dịch vụ, vị trí địa lý).
✅ **Đánh giá điểm ICP** dựa trên tiêu chí **AI, kỹ thuật, quy mô nhân sự, và vị trí địa lý**.
✅ **Cung cấp báo cáo chi tiết** với điểm số và lý do cụ thể cho từng tiêu chí.
✅ **Hoàn toàn không cần code**, chỉ cần **n8n + Airtop** để hoạt động 24/7.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này chạy **ổn định 24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS riêng.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đủ sức mạnh cho workflow này)
:::

---

### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần phân tích thủ công hàng trăm hồ sơ LinkedIn.
- **Chính xác cao**: Dữ liệu trích xuất tự động từ LinkedIn, giảm sai sót con người.
- **Cá nhân hóa ICP**: Đánh giá dựa trên tiêu chí **AI, kỹ thuật, quy mô nhân sự, và vị trí** phù hợp với chiến lược bán hàng của doanh nghiệp.
- **Hoạt động liên tục**: Workflow chạy **24/7** mà không cần can thiệp.
- **Dễ dàng tích hợp**: Kết quả có thể **push vào CRM** (HubSpot, Salesforce) hoặc **gửi qua Slack/Email** để báo cáo.
:::

---

### **🔧 Yêu Cầu Cần Thiết**
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản Airtop** (để trích xuất dữ liệu LinkedIn):
   - [Đăng ký Airtop](https://portal.airtop.ai/) (miễn phí cho thử nghiệm).
   - **Cài đặt Airtop Profile** và **authenticate với LinkedIn** (cần tài khoản LinkedIn cá nhân).
   - **Tạo API Key** tại [Airtop API Keys](https://portal.airtop.ai/api-keys).

2. **Workflow n8n** (self-hosted hoặc dùng n8n.cloud):
   - Nếu dùng **n8n.cloud**, cần **mua gói premium** để chạy workflow liên tục.

3. **Dữ liệu đầu vào**:
   - **LinkedIn URL của công ty** (ví dụ: `https://www.linkedin.com/company/google/`).
   - **Tiêu chí ICP** (có thể điều chỉnh trong `prompt` của Airtop).

---

### **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có **2 cách** để import workflow này:
- **Tải file JSON** từ [n8n.io/workflows/4262](https://n8n.io/workflows/4262) và **import vào n8n Editor**.
- **Copy toàn bộ JSON** từ link trên và **dán vào n8n Editor** (tab `Import`).

:::note[Lưu ý]
- **Không cần chỉnh sửa** toàn bộ workflow, chỉ cần **cấu hình các node quan trọng** như hướng dẫn dưới đây.
- Nếu dùng **n8n.cloud**, cần **bật "Active"** sau khi import.
:::

---

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này có **6 node chính**, nhưng **các node quan trọng** cần cấu hình là:

##### **🔹 Node "Calculate ICP" (Airtop)**
- **Credentials**:
  - Chọn **`airtopApi`** (đã tạo trong n8n khi setup Airtop).
- **Key Parameters**:
  - **`operation`**: Để là `query` (không cần chỉnh).
  - **`resource`**: Để là `extraction` (không cần chỉnh).
  - **`prompt`**:
    ```plaintext
    Task: Analyze the company's LinkedIn profile and calculate a score based on the criteria below.

    Information Source: Use data from the company's LinkedIn profile, including the About section, Employee count, Industry, Headquarters, Services, and any keywords or descriptions provided.

    ## Scoring Criteria
    | Category       | Classification | Points |
    |----------------|----------------|--------|
    | AI Focus        | Low            | 5      |
    |                | Medium         | 10     |
    |                | High           | 25     |
    | Technical Level | Basic          | 5      |
    |                | Intermediate   | 15     |
    |                | Advanced       | 25     |
    |                | Expert         | 35     |
    | Employee Count  | 0–9            | 5      |
    |                | 10–150         | 25     |
    |                | 150+           | 30     |
    | Agency Status   | Not Automation Agency | 0 |
    |                | Automation Agency | 20 |
    | Geography       | Outside US/Europe | 0 |
    |                | US/Europe Based | 10 |

    Provide a structured JSON response with:
    - Total ICP score (0-100)
    - Breakdown by category (AI Focus, Technical Level, etc.)
    - Justification for each score.
    ```
    - **Lưu ý**: Nếu muốn **điều chỉnh tiêu chí**, chỉ cần **sửa phần `Scoring Criteria`** trong `prompt`.

##### **🔹 Node "Unify params" & "Parse to JSON" (Set)**
- **Không cần chỉnh** (n8n tự động xử lý dữ liệu đầu vào và chuyển đổi sang JSON).

##### **🔹 Node "When Executed by Another Workflow" (Execute Workflow Trigger)**
- **Không cần chỉnh** (dùng để **kích hoạt workflow từ bên ngoài**, ví dụ từ một form hoặc workflow khác).

##### **🔹 Node "Flat json" (Set)**
- **Không cần chỉnh** (n8n tự động **biến JSON thành dạng phẳng** để dễ dàng lưu hoặc push vào CRM).

---

#### **3. Kích Hoạt ⚡️**
Sau khi cấu hình xong:
1. **Test Run** với **1 LinkedIn URL mẫu** (ví dụ: `https://www.linkedin.com/company/microsoft/`).
2. **Kiểm tra kết quả**:
   - N8n sẽ trả về **1 JSON** với:
     ```json
     {
       "total_icp_score": 85,
       "ai_focus": { "score": 25, "justification": "..." },
       "technical_level": { "score": 35, "justification": "..." },
       "employee_count": { "score": 25, "justification": "..." },
       ...
     }
     ```
3. **Bật "Active"** để workflow chạy liên tục.

---

### **✍️ Mẹo & Gợi Ý Nâng Cao**
#### **1. Tích Hợp Với Form (Để Nhập LinkedIn URL)**
- Sử dụng **node `formTrigger`** để tạo **form nhập LinkedIn URL**.
- **Cách làm**:
  - Tạo **1 form** trong n8n với **1 trường input** (type `text`, placeholder: `Nhập LinkedIn URL của công ty`).
  - Kết nối **form này với node `On form submission`** trong workflow.
  - **Kết quả**: Các sếp có thể **nhập URL và nhận kết quả ICP ngay lập tức**.

#### **2. Push Kết Quả Vào CRM (HubSpot/Salesforce)**
- Sau khi workflow trả về **JSON**, các sếp có thể:
  - **Push vào HubSpot** (sử dụng node `HubSpot`).
  - **Push vào Salesforce** (sử dụng node `Salesforce`).
  - **Gửi qua Email/Slack** (sử dụng node `Email` hoặc `Slack`).

#### **3. Lưu Log & Báo Cáo Định Kỳ**
- Sử dụng **node `Set`** để lưu kết quả vào **Google Sheets** hoặc **Notion**.
- **Cách làm**:
  - Tạo **1 sheet/đơn vị lưu trữ** trong Google Sheets/Notion.
  - Sử dụng **node `Google Sheets`** để ghi dữ liệu.
  - **Kết quả**: Các sếp có **báo cáo ICP định kỳ** để phân tích.

#### **4. Điều Chỉnh Tiêu Chí ICP**
- Nếu **tiêu chí ICP** của doanh nghiệp khác (ví dụ: ưu tiên **công ty ở Việt Nam** hơn **US/Europe**), chỉ cần **sửa phần `prompt`** trong node `Calculate ICP`:
  ```plaintext
  | Geography       | Outside Vietnam | 0 |
  |                | Vietnam Based   | 20 |
  ```

---

### **📌 Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi việc **phân tích thủ công hàng trăm hồ sơ LinkedIn**, đồng thời **cung cấp dữ liệu ICP chính xác** để ưu tiên outreach cho những lead **có khả năng chuyển đổi cao nhất**.

**Hành động ngay**:
1. **Setup Airtop** và **n8n**.
2. **Import workflow** và **cấu hình node `Calculate ICP`**.
3. **Test với 1-2 LinkedIn URL** và **bắt đầu tự động hóa ICP**!

---
**🚀 Cần hỗ trợ?** Hãy để lại **comment** bên dưới hoặc liên hệ **Airtop** qua [đây](https://portal.airtop.ai/support). Chúc các sếp **tự động hóa thành công**! 💪