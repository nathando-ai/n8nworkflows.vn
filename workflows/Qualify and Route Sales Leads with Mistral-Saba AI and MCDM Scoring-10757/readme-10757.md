---
title: "🚀 Tự Động Hóa Xác Minh & Phân Loại Lead Sales với AI Mistral-Saba + MCDM Scoring (Không Cần Code)"
description: "Workflow tự động hóa 100% không code giúp doanh nghiệp tự động phân loại, đánh giá chất lượng lead và phân phối cho đội ngũ bán hàng phù hợp, giảm 90% công việc thủ công trong quản lý lead. Kết quả: Tăng hiệu quả bán hàng, rút ngắn chu kỳ bán hàng và tối ưu hóa nguồn lực."
slug: "tieu-dong-hoa-xac-minh-phan-loai-lead-sales-ai-mistral-saba"
tags: [n8n, automation, lead-generation, ai-summarization, sales-automation, no-code]
keywords: [n8n workflow lead sales, tự động hóa phân loại lead, AI Mistral-Saba, MCDM scoring, routing lead, tự động hóa bán hàng]
---

# 🚀 **Tự Động Hóa Xác Minh & Phân Loại Lead Sales với AI Mistral-Saba + MCDM Scoring**

## 🔍 **Nỗi Đau Của Doanh Nghiệp Khi Quản Lý Lead Thủ Công**
Các sếp đang phải mất **giờ đồng hồ hàng ngày** để:
- **Lọc và đánh giá** hàng trăm lead từ nhiều nguồn (website, email, mạng xã hội, CRM).
- **Phân loại lead** theo kích thước doanh nghiệp (Enterprise, Mid-Market, SMB) và tính chất tương tác.
- **Giao lead cho đội ngũ bán hàng** phù hợp, nhưng thường phải dựa vào kinh nghiệm chủ quan → dẫn đến **tỷ lệ chuyển đổi thấp** và **tốn thời gian** cho việc điều chỉnh.
- **Không có hệ thống tự động** để cập nhật và theo dõi hiệu suất của mỗi lead → khó đánh giá hiệu quả của chiến dịch marketing.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tự động hóa 100% quá trình** từ nhận lead đến phân loại và giao cho đội ngũ phù hợp.
✅ **Sử dụng AI Mistral-Saba** để đánh giá chất lượng lead với độ chính xác cao.
✅ **Áp dụng mô hình MCDM (Multi-Criteria Decision Making)** để phân loại lead theo tiêu chí khách hàng (kích thước, ngành nghề, hành vi mua hàng).
✅ **Cập nhật tự động vào CRM** và **báo cáo hiệu suất** trên dashboard, giúp các sếp **quản lý chiến dịch một cách thông minh**.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian** trong việc phân loại và giao lead thủ công.
- **Tăng tỷ lệ chuyển đổi** nhờ AI đánh giá lead chính xác hơn con người.
- **Phân phối lead tự động** cho đội ngũ bán hàng phù hợp (Enterprise, Mid-Market, SMB), giảm thời gian chờ và tăng hiệu quả bán hàng.
- **Báo cáo tự động** hiệu suất lead và KPI trên dashboard, giúp các sếp **quản lý chiến dịch một cách dữ liệu hóa**.
- **Hoạt động 24/7** mà không cần can thiệp của con người.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow này hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản và API Keys**:
   - **OpenRouter API** (để kết nối với mô hình AI Mistral-Saba).
   - **CRM** (Salesforce, HubSpot, hoặc CRM khác để cập nhật lead).
   - **Dữ liệu nguồn**:
     - Dữ liệu **đặc điểm khách hàng** (demographic data).
     - Dữ liệu **hành vi khách hàng** (behavioral data).
     - Dữ liệu **giao dịch** (transactional data).
   - **Tài khoản analytics** (Google Sheets, Tableau, hoặc dashboard khác để báo cáo KPI).

2. **Cấu hình cơ bản**:
   - **Lịch trình chạy workflow** (ví dụ: hàng ngày, hàng giờ).
   - **Thông tin cấu hình API** cho các node `httpRequest` (nếu fetch dữ liệu từ API bên thứ ba).
   - **Mô hình AI Mistral-Saba** đã được cấu hình trong OpenRouter.

---
---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Bước 1**: Tải file JSON từ [n8n.io/workflows/10757](https://n8n.io/workflows/10757) hoặc sao chép mã JSON từ trang này.
- **Bước 2**: Mở **n8n Editor** (trên máy chủ self-hosted hoặc n8n.cloud).
- **Bước 3**: Nhấn **Import Workflow** và dán JSON vào.
- **Bước 4**: Chọn **Create Workflow** để tạo workflow mới.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này gồm **20 node** với các chức năng chính sau. Các sếp cần chú ý cấu hình các node sau:

##### **A. Cấu Hình API và Credentials**
1. **`OpenRouter Chat Model` (Mistral-Saba)**
   - **Credentials**: Đăng ký và thêm `openRouterApi` vào n8n.
     - API Key: Lấy từ [OpenRouter](https://openrouter.ai/).
     - Model: Chọn `mistralai/mistral-saba`.
   - **Key Parameters**:
     - `model`: `mistralai/mistral-saba`.
     - `temperature`: 0.7 (có thể điều chỉnh theo nhu cầu).

2. **`Fetch Demographic Data`, `Fetch Behavioral Data`, `Fetch Transactional Data`**
   - Các node này sử dụng `httpRequest` để lấy dữ liệu từ API bên thứ ba.
   - **Lưu ý**:
     - Đảm bảo URL API là chính xác và có quyền truy cập.
     - Nếu dữ liệu từ API yêu cầu **authentication**, thêm `Authorization` header với token API.

3. **`Assign to Enterprise Sales Team`, `Assign to Mid-Market Team`, `Assign to SMB Team`, `Send to Nurture Campaign`**
   - Các node này gửi lead đến các đội ngũ hoặc chiến dịch cụ thể.
   - **Lưu ý**:
     - Đảm bảo URL API của CRM hoặc hệ thống nội bộ là chính xác.
     - Thêm thông tin **payload** (dữ liệu gửi đi) như:
       ```json
       {
         "lead_id": "{{ $node["Merge Lead Data Sources"].json["lead_id"] }}",
         "team": "Enterprise",
         "reason": "High potential based on AI scoring"
       }
       ```

4. **`Update CRM with Lead Scores`**
   - Node này cập nhật điểm số lead vào CRM.
   - **Lưu ý**:
     - Thay đổi `url` và `headers` phù hợp với API của CRM (ví dụ: Salesforce, HubSpot).
     - Đảm bảo trường `lead_score` và `routing_reason` được cập nhật chính xác.

##### **B. Cấu Hình MCDM Scoring Engine (AHP-TOPSIS)**
- Node này sử dụng **mô hình AHP-TOPSIS** để đánh giá lead dựa trên nhiều tiêu chí.
- **Lưu ý**:
  - Node này sử dụng **JavaScript code** trong `code` node.
  - Các sếp có thể **tùy chỉnh trọng số** cho các tiêu chí (ví dụ: kích thước doanh nghiệp, ngành nghề, hành vi mua hàng) trong phần `MCDM Scoring Engine`.
  - **Mẫu code tham khảo** (có thể chỉnh sửa trong node `MCDM Scoring Engine`):
    ```javascript
    // Dữ liệu đầu vào từ node trước
    const leadData = $input.all();
    const criteriaWeights = {
      companySize: 0.4,
      industry: 0.3,
      behavioralScore: 0.2,
      transactionalScore: 0.1
    };

    // Áp dụng mô hình AHP-TOPSIS
    const scores = leadData.map(lead => {
      // Tính điểm tổng hợp dựa trên trọng số
      const totalScore = (lead.companySize * criteriaWeights.companySize) +
                         (lead.industry * criteriaWeights.industry) +
                         (lead.behavioralScore * criteriaWeights.behavioralScore) +
                         (lead.transactionalScore * criteriaWeights.transactionalScore);
      return { ...lead, score: totalScore };
    });

    return { json: { leads: scores } };
    ```

##### **C. Cấu Hình AI Lead Qualification Agent**
- Node này sử dụng **LangChain Agent** để đánh giá lead với mô hình AI Mistral-Saba.
- **Lưu ý**:
  - Đảm bảo **prompt** trong node `AI Lead Qualification Agent` là rõ ràng và cụ thể.
  - **Mẫu prompt tham khảo**:
    ```
    Analyze the lead data and assign a quality score (0-100) based on:
    1. Company size (Enterprise: 90-100, Mid-Market: 70-89, SMB: 50-69).
    2. Industry relevance (0-100).
    3. Behavioral engagement (0-100).
    4. Transactional history (0-100).
    Return the score and reasoning.
    ```

##### **D. Cấu Hình Schedule Trigger**
- Node này chạy workflow theo **lịch trình tự động**.
- **Lưu ý**:
  - Thiết lập **thời gian chạy** phù hợp (ví dụ: hàng ngày lúc 8h sáng).
  - Nếu muốn chạy **ngay lập tức**, chọn `Manual Trigger` và kích hoạt thủ công.

---

#### **3. Kích Hoạt ⚡️**
- **Bước 1**: Chạy **test run** với dữ liệu mẫu để kiểm tra workflow.
  - Sử dụng **mock data** (dữ liệu giả) để test các node như `Fetch Demographic Data`, `AI Lead Qualification Agent`, và `Route by Lead Quality`.
- **Bước 2**: Kiểm tra **log** trong n8n để đảm bảo không có lỗi.
- **Bước 3**: Bật **Active workflow** để chạy tự động theo lịch trình.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết Nối với Slack/Telegram**
   - Thêm node `slack` hoặc `telegram` để **báo cáo kết quả** mỗi khi lead được phân loại.
   - Ví dụ: Gửi thông báo khi lead được giao cho đội ngũ Enterprise.

2. **Lưu Log và Audit Trail**
   - Sử dụng node `httpRequest` để lưu **log** vào Google Sheets hoặc database.
   - Cấu hình node `Log KPIs to Analytics Dashboard` để **theo dõi hiệu suất** của mỗi lead.

3. **Tùy Chỉnh Routing Rules**
   - Các sếp có thể **cập nhật trọng số** trong `MCDM Scoring Engine` để ưu tiên lead theo tiêu chí riêng.
   - Ví dụ: Nếu doanh nghiệp muốn ưu tiên lead từ ngành **tech**, tăng trọng số cho tiêu chí `industry`.

4. **Báo Cáo Hiệu Suất Định Kỳ**
   - Sử dụng node `Calculate Performance KPIs` để tính toán **tỷ lệ chuyển đổi**, **thời gian phản hồi**, và **tỷ lệ lead chất lượng**.
   - Cập nhật báo cáo vào **Google Data Studio** hoặc **Tableau** để theo dõi hiệu suất dài hạn.

5. **Kết Nối với CRM Bên Ngoài**
   - Nếu sử dụng **Salesforce** hoặc **HubSpot**, các sếp có thể **cập nhật lead** vào CRM tự động.
   - Ví dụ: Cập nhật trường `Lead_Score__c` trong Salesforce.

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các doanh nghiệp muốn **tự động hóa quá trình phân loại và giao lead** một cách chính xác và hiệu quả. Với sự hỗ trợ của **AI Mistral-Saba** và **mô hình MCDM**, các sếp không chỉ tiết kiệm **thời gian và công sức** mà còn **tăng tỷ lệ chuyển đổi** và **tối ưu hóa nguồn lực bán hàng**.

**Hành động ngay hôm nay:**
1. **Cài đặt n8n trên VPS** để chạy workflow 24/7 (không phụ thuộc vào internet).
2. **Import workflow** và cấu hình các API cần thiết.
3. **Chạy test run** và theo dõi kết quả.
4. **Bật workflow** và bắt đầu tự động hóa bán hàng của mình!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**Chia sẻ và đặt câu hỏi:**
Nếu các sếp có bất kỳ thắc mắc hoặc cần hỗ trợ trong quá trình cấu hình, hãy để lại bình luận dưới đây hoặc liên hệ với cộng đồng n8n trên [Discord](https://n8n.io/discord). Chúc các sếp thành công với workflow tự động hóa lead của mình! 🚀