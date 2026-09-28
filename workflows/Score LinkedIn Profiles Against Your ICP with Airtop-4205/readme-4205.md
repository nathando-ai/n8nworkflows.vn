---
title: "🔍 **Tự Động Đánh Giá Profile LinkedIn So Sánh Với ICP Bằng Airtop (N8n) - Giúp Các Sếp Lọc Lead Chất Lượng Mà Không Cần Code**"
description: "Workflow này tự động phân tích và đánh giá profile LinkedIn của cá nhân so với Ideal Customer Profile (ICP) của doanh nghiệp, giúp các sếp nhanh chóng lọc ra lead phù hợp với tiêu chí AI, kỹ thuật và cấp bậc. Kết quả là một score chính xác (tối đa 100 điểm) cùng thông tin chi tiết về cá nhân, tiết kiệm thời gian và nâng cao hiệu quả marketing/sales."
slug: "tieu-dong-danh-gia-linkedin-so-sanh-voi-icp-bang-airtop"
tags: [n8n, automation, no-code, airtop, linkedin-lead-scoring, marketing-automation]
keywords: [n8n workflow linkedin, tự động hóa đánh giá lead, scoring icp linkedin, airtop n8n, tự động hóa marketing, lọc lead chất lượng]
---

# 🚀 **Tự Động Đánh Giá Profile LinkedIn So Sánh Với ICP Bằng Airtop (N8n)**

## **Nỗi Đau Của Các Sếp Khi Làm Thủ Công**
Các sếp marketing, sales hoặc team tuyển dụng thường phải mất **giờ đồng hồ** để:
- **Tìm kiếm và phân tích** hàng trăm profile LinkedIn để tìm lead phù hợp.
- **Đánh giá thủ công** tiêu chí như **sự quan tâm đến AI, trình độ kỹ thuật và cấp bậc** của từng cá nhân.
- **So sánh** với **Ideal Customer Profile (ICP)** của doanh nghiệp, dẫn đến **tỷ lệ chuyển đổi thấp** và **tốn nhiều thời gian**.

Workflow này **giải quyết tất cả** bằng cách **tự động hóa 100% quá trình đánh giá**, giúp các sếp:
✅ **Tiết kiệm 80% thời gian** so với cách làm thủ công.
✅ **Lọc ra lead phù hợp** với tiêu chí ICP của doanh nghiệp.
✅ **Nhận score chính xác** (tối đa 100 điểm) cho mỗi profile.
✅ **Cá nhân hóa tiếp cận** dựa trên dữ liệu được enrich.

---
### **🎯 Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tự động hóa đánh giá lead** trong vài giây thay vì nhiều giờ.
- **Score ICP chính xác** (tối đa 100 điểm) dựa trên **AI Interest, Technical Depth và Seniority Level**.
- **Dữ liệu enrich đầy đủ** (tên, chức vụ, công ty, số lượng kết nối, mô tả cá nhân, v.v.).
- **Kết nối với CRM/Salesforce** để tự động phân loại lead.
- **Tối ưu hóa chiến dịch marketing/sales** bằng cách tập trung vào lead có score cao.
:::

---
### **🔧 Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ TRƯỚC KHI SỬ DỤNG**]
Để workflow hoạt động, các sếp cần:
1. **Tài khoản Airtop** (đăng ký tại [portal.airtop.ai](https://portal.airtop.ai/browser-profiles)) với **profile LinkedIn được kết nối**.
2. **API Key Airtop** (cấu hình trong n8n dưới **Credentials** → **Airtop API**).
3. **Danh sách URL profile LinkedIn** (cần nhập vào form hoặc truyền từ workflow khác).
4. **(Tùy chọn) Form nhập liệu** (để người dùng nhập URL profile LinkedIn).
:::

---
## **🚀 Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/4205](https://n8n.io/workflows/4205) hoặc copy/paste JSON vào **n8n Editor**.
- **Nhấn "Import"** và chọn **Create New Workflow**.

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này có **5 node chính**, nhưng **hai node quan trọng nhất** cần cấu hình kỹ:

#### **🔹 Node "Calculate ICP PersonScoring" (Airtop)**
- **Loại node:** `airtop`
- **Credentials:** Chọn **airtopApi** (đã cấu hình trước).
- **Key Parameters:**
  - **Operation:** `query`
  - **Resource:** `extraction`
  - **Prompt:** **CẦN CHỈNH SỬA** theo tiêu chí ICP của doanh nghiệp.
    *Ví dụ:*
    ```plaintext
    Please extract and score the following information from the LinkedIn profile page based on Ideal Customer Profile (ICP) criteria:

    1. **Full Name** (Extract the full name)
    2. **Current/Most Recent Job Title** (Identify the job title)
    3. **Current/Most Recent Employer** (Extract the company name)
    4. **AI Interest Level** (Score from 1-4: 1=Beginner, 2=Intermediate, 3=Advanced, 4=Expert)
    5. **Technical Depth** (Score from 1-4: 1=Basic, 2=Intermediate, 3=Advanced, 4=Expert)
    6. **Seniority Level** (Score from 1-4: 1=Junior, 2=Mid-Level, 3=Senior, 4=Executive)

    **Scoring System:**
    - AI Interest: Beginner (5), Intermediate (10), Advanced (25), Expert (35)
    - Technical Depth: Basic (5), Intermediate (15), Advanced (25), Expert (35)
    - Seniority Level: Junior (5), Mid-Level (15), Senior (25), Executive (30)
    ```
  - **Output Format:** Yêu cầu Airtop trả về **JSON** với các trường:
    ```json
    {
      "fullName": "John Doe",
      "jobTitle": "AI Engineer",
      "employer": "TechCorp",
      "aiInterestScore": 35,
      "technicalDepthScore": 30,
      "seniorityScore": 25,
      "totalICPScore": 90,
      "linkedinProfileUrl": "https://linkedin.com/in/johndoe"
    }
    ```

#### **🔹 Node "On form submission" (Form Trigger)**
- **Loại node:** `formTrigger`
- **Cấu hình:**
  - **Fields:**
    - `linkedinProfileUrl` (type: `text`, required: `true`)
  - **Example:**
    ```json
    {
      "linkedinProfileUrl": "https://linkedin.com/in/janedoe"
    }
    ```
  - **Nếu không dùng form**, có thể **bỏ node này** và truyền dữ liệu từ **Execute Workflow Trigger**.

#### **🔹 Node "When Executed by Another Workflow" (Execute Workflow Trigger)**
- **Loại node:** `executeWorkflowTrigger`
- **Sử dụng khi:**
  - Workflow này được **kích hoạt từ một workflow khác** (ví dụ: từ CRM hoặc danh sách lead).
  - **Input Example:**
    ```json
    {
      "linkedinProfileUrl": "https://linkedin.com/in/someone"
    }
    ```

#### **🔹 Node "Parameters" & "Edit Fields" (Set)**
- **Loại node:** `set`
- **Chỉnh sửa tên biến** để đảm bảo **tương thích** với Airtop.
  - Ví dụ:
    - `linkedinProfileUrl` → `profileUrl`
    - `airtopProfile` → `airtopCredentials`

---
### **3. Kích Hoạt ⚡️ Workflow**
1. **Test Run** với **URL profile mẫu** (ví dụ: `https://linkedin.com/in/janedoe`).
2. **Kiểm tra output** trong **Execution View** để đảm bảo:
   - Dữ liệu được **extract** chính xác.
   - **Score ICP** được tính toán đúng.
3. **Bật Active** workflow.

---
## **✍️ Mẹo & Gợi Ý Nâng Cao**
:::note[**CÁCH SỬ DỤNG HIỆU QUẢ NHẤT**]
1. **Kết nối với CRM/Salesforce**
   - Sau khi workflow hoàn thành, **gửi kết quả** đến **Salesforce, HubSpot hoặc Notion** để tự động cập nhật lead.
   - **Node sử dụng:** `n8n-nodes-base.salesforce` hoặc `n8n-nodes-base.notion`.

2. **Batch Processing (Xử lý Batch)**
   - **Tải danh sách URL** từ **Excel/Google Sheets** và **chạy song song** nhiều profile.
   - **Node sử dụng:** `n8n-nodes-base.googleSheets` + `n8n-nodes-base.loop`.

3. **Gửi Báo Cáo Định Kỳ**
   - **Tự động gửi email** (với **Slack/Telegram**) báo cáo **top 10 lead có score cao nhất**.
   - **Node sử dụng:** `n8n-nodes-base.email` + `n8n-nodes-base.slack`.

4. **Tối ưu hóa Prompt Airtop**
   - **Nếu score không chính xác**, hãy **cập nhật lại prompt** trong node Airtop để phù hợp với **ICP mới nhất** của doanh nghiệp.
   - **Ví dụ:**
     ```plaintext
     "Nếu người dùng có từ khóa 'AI', 'Machine Learning', 'Deep Learning' trong mô tả, tăng điểm AI Interest lên 40 điểm."
     ```
:::

---
## **📌 Kết Luận**
Workflow này **giúp các sếp tự động hóa quá trình đánh giá lead LinkedIn**, tiết kiệm **thời gian và nâng cao hiệu quả marketing/sales**. **Không cần code**, chỉ cần **cấu hình Airtop và nhập tiêu chí ICP**, workflow sẽ **tự động enrich và scoring** profile.

👉 **Hãy áp dụng ngay** và **tận hưởng lợi ích của tự động hóa** trong việc lọc lead chất lượng!

---
### **🔗 Tài Liệu Tham Khảo**
- [Airtop Documentation](https://docs.airtop.ai/)
- [n8n Airtop Node Guide](https://docs.n8n.io/integrations/builtIn/nodes/airtop/)
- [Cách Cài Đặt n8n Self-Hosted](https://docs.n8n.io/hosting/self-hosted/)

:::info[**Gợi Ý Hạ Tầng Cho n8n**]
Để workflow **chạy ổn định 24/7**, các sếp nên **cài n8n trên VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::