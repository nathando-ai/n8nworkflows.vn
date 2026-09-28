---
title: "🔍 **Tự Động Hóa Đánh Giá ICP (Ideal Customer Profile) Cho LinkedIn - Airtop + n8n (Không Cần Code!)""
description: "Workflow này tự động phân tích hồ sơ LinkedIn của cá nhân, tính điểm ICP dựa trên sự quan tâm về AI, trình độ kỹ thuật và cấp bậc, giúp các sếp lọc và ưu tiên leads chất lượng cao chỉ trong vài giây. Kết quả: Tiết kiệm 10+ giờ/tháng, tăng hiệu quả bán hàng 30%!"
slug: "tieu-dong-hoa-danh-gia-icp-linkedin-airtop-n8n"
tags: [n8n, automation, sales, airtop, linkedin-scraping, icp-scoring]
keywords: [tự động hóa n8n, đánh giá icp linkedin, airtop automation, scoring leads, tự động hóa bán hàng, không cần code]
---

# 🚀 **Tự Động Hóa Đánh Giá ICP LinkedIn - Airtop + n8n: Lọc Leads Chất Lượng Mà Không Cần Code!**

### **Nỗi Đau Của Các Sếp Trong Bán Hàng**
Các sếp thường phải mất **từ 5-10 giờ/tuần** để:
- **Thủ công** tìm kiếm và phân tích hồ sơ LinkedIn của leads.
- **Đánh giá** xem họ có phù hợp với ICP (Ideal Customer Profile) của doanh nghiệp không.
- **Lọc bỏ** những hồ sơ không tương xứng, lãng phí thời gian cho những người không có tiềm năng.
- **Không có tiêu chí khách quan** để ưu tiên leads, dẫn đến việc bỏ lỡ cơ hội bán hàng với khách hàng tiềm năng.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Trích xuất** thông tin chi tiết từ LinkedIn (tên, chức vụ, công ty, trình độ kỹ thuật, sự quan tâm về AI, cấp bậc).
✅ **Đánh giá ICP** dựa trên hệ thống điểm số khách quan (AI Interest, Technical Depth, Seniority Level).
✅ **Trả về kết quả** dưới dạng JSON, giúp các sếp **lọc leads nhanh chóng** và tập trung vào những người có tiềm năng cao nhất.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS. Với chi phí thấp, hiệu suất cao:
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172) (Đảm bảo tốc độ nhanh, không lag)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không còn phải thủ công phân tích từng hồ sơ (giảm **10+ giờ/tháng**).
- **Đánh giá chính xác**: Sử dụng hệ thống điểm số khách quan để lọc leads **phù hợp với ICP**.
- **Tăng hiệu quả bán hàng**: Ưu tiên tiếp cận những khách hàng **có tiềm năng cao nhất** (tăng **30% doanh số**).
- **Hoạt động liên tục**: Workflow chạy tự động **24/7**, không phụ thuộc vào giờ làm việc.
- **Dữ liệu chi tiết**: Nhận thông tin **toàn diện** từ LinkedIn (tên, chức vụ, công ty, trình độ kỹ thuật, số lượng kết nối, mô tả cá nhân...).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản Airtop** (đăng ký tại [portal.airtop.ai](https://portal.airtop.ai/browser-profiles)).
2. **Profile Airtop kết nối LinkedIn**:
   - Cài đặt **browser profile** trong Airtop và **đăng nhập LinkedIn** để trích xuất dữ liệu.
   - **Lưu ý**: Profile này **không thể chia sẻ** với người khác (do vấn đề bảo mật).
3. **API Key Airtop**:
   - Tạo tại [Airtop Dashboard](https://portal.airtop.ai/) và thêm vào **credentials** của n8n.
4. **Danh sách URL LinkedIn** của leads (hoặc một form để nhập URL).
5. **(Tùy chọn)** Một **form nhập liệu** (ví dụ trên Notion, Google Form) để tự động trigger workflow khi có mới leads.

---
:::note[LƯU Ý QUAN TRỌNG]
- **Không cần skill code**: Workflow này **100% không cần viết mã**, chỉ cần cấu hình các node.
- **Không vi phạm chính sách LinkedIn**: Airtop hoạt động như một **người dùng thực** (không scrape dữ liệu một cách tự động vi phạm T&C).
- **Độ chính xác cao**: Dữ liệu trích xuất gần như **100% chính xác** (do Airtop sử dụng AI + browser automation).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có **2 cách** để import workflow này:

**Cách 1: Import từ file JSON**
1. Tải workflow từ [n8n.io/workflows/4258](https://n8n.io/workflows/4258) (chọn **Download JSON**).
2. Trên **n8n Editor**, nhấn **Import** → Chọn file JSON vừa tải.
3. **Xác nhận** và workflow sẽ xuất hiện trên canvas.

**Cách 2: Copy/Paste JSON**
1. Copy toàn bộ mã JSON từ [n8n.io/workflows/4258](https://n8n.io/workflows/4258).
2. Trên **n8n Editor**, nhấn **Import** → Chọn **Paste JSON**.
3. **Xác nhận** và workflow sẽ được tạo.

---
#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Sau khi import, các sếp **phải cấu hình** các node sau để workflow hoạt động:

##### **A. Node "On form submission" (Trigger)**
- **Chức năng**: Nhận input từ form (ví dụ: Google Form, Notion, hoặc input trực tiếp).
- **Cấu hình**:
  - Nếu sử dụng **form ngoài**, kết nối với **webhook** hoặc **form trigger** của n8n.
  - Nếu **không có form**, có thể **bỏ qua** và sử dụng **node "When Executed by Another Workflow"** (nếu muốn gọi từ workflow khác).

##### **B. Node "When Executed by Another Workflow" (Trigger)**
- **Chức năng**: Cho phép workflow này được **gọi từ workflow khác** (nếu cần).
- **Cấu hình**:
  - Nếu **không cần**, có thể **xóa node này** và chỉ giữ lại **form trigger**.

##### **C. Node "Parameters" (Set)**
- **Chức năng**: Đảm bảo dữ liệu truyền vào node Airtop có định dạng đúng.
- **Cấu hình**:
  - **Không cần chỉnh sửa** (n8n tự động xử lý).
  - **Lưu ý**: Nếu input từ form, **đảm bảo field tên là "LinkedIn Profile URL"** (hoặc chỉnh sửa trong node này).

##### **D. Node "Edit Fields" (Set)**
- **Chức năng**: Sửa đổi và chuẩn hóa dữ liệu trước khi truyền vào Airtop.
- **Cấu hình**:
  - **Không cần chỉnh sửa** (n8n tự động xử lý).
  - **Lưu ý**: Nếu muốn **thêm/bỏ field**, chỉnh sửa tại đây.

##### **E. Node "Calculate ICP PersonScoring" (Airtop - QUAN TRỌNG NHẤT!)**
- **Chức năng**: **Cốt lõi** của workflow - trích xuất và tính điểm ICP.
- **Cấu hình BẮT BUỘC**:
  1. **Credentials**:
     - Chọn **airtopApi** (đã cấu hình trước khi import).
  2. **Key Parameters**:
     - **Operation**: Để là **"query"** (không cần đổi).
     - **Resource**: Để là **"extraction"** (không cần đổi).
     - **Prompt**: **CẦN CHỈNH SỬA** theo **ICP của doanh nghiệp**!
        - **Mẫu prompt mặc định**:
          ```plaintext
          Please extract the following information from the LinkedIn profile page:

          1. **Full Name**: Extract the full name of the individual.
          2. **Current or Most Recent Job Title**: Identify the job title next to the logo of the current or last employer.
          3a. **Current or Most Recent Employer**: Extract the name of the company.
          3b. **Company LinkedIn URL**: Extract the LinkedIn URL of the company.
          4. **Location**: Extract the location (city, country).
          5. **Number of Connections**: Extract the number of connections.
          6. **Number of Followers**: Extract the number of followers.
          7. **About Section**: Extract the content of the "About" section.
          8. **AI Interest Level**: Classify the person's interest in AI as:
             - Beginner (5 points)
             - Intermediate (10 points)
             - Advanced (25 points)
             - Expert (35 points)
          9. **Technical Depth**: Classify the technical depth as:
             - Basic (5 points)
             - Intermediate (15 points)
             - Advanced (25 points)
             - Expert (35 points)
          10. **Seniority Level**: Classify the seniority level as:
              - Junior (5 points)
              - Mid-level (15 points)
              - Senior (25 points)
              - Executive (30 points)

          Return the extracted data in JSON format with the following structure:
          {
              "full_name": "...",
              "job_title": "...",
              "employer": "...",
              "company_linkedin_url": "...",
              "location": "...",
              "connections": "...",
              "followers": "...",
              "about_section": "...",
              "ai_interest": "...",
              "technical_depth": "...",
              "seniority_level": "...",
              "icp_score": "..."
          }
          ```
        - **Cách chỉnh sửa**:
          - **Thêm/bỏ điểm số** cho các tiêu chí (ví dụ: nếu **AI Interest** quan trọng hơn, tăng điểm từ 5→10 cho Beginner).
          - **Thêm tiêu chí mới** (ví dụ: "Industry Fit" với điểm số từ 0-10).
          - **Đảm bảo format JSON** như trên để workflow trả về dữ liệu chuẩn.

  3. **Test Run**:
     - Nhập **1 URL LinkedIn** vào input (ví dụ: `https://linkedin.com/in/janedoe`).
     - Nhấn **Run Workflow** để kiểm tra kết quả.
     - **Nếu lỗi**, kiểm tra:
       - **Prompt có hợp lệ không?** (Không có lỗi cú pháp JSON).
       - **Airtop Profile có đăng nhập LinkedIn thành công không?** (Kiểm tra tại [portal.airtop.ai](https://portal.airtop.ai/)).
       - **API Key có đúng không?** (Kiểm tra tại n8n Credentials).

##### **F. Node "Set" (Parameters & Edit Fields)**
- **Chức năng**: Chuẩn hóa dữ liệu trước khi xuất.
- **Cấu hình**:
  - **Không cần chỉnh sửa** (n8n tự động xử lý).
  - **Lưu ý**: Nếu muốn **thêm field** vào output, chỉnh sửa tại đây.

---
#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Nhập **1-2 URL LinkedIn** vào input (ví dụ: `https://linkedin.com/in/nguyenvana`).
   - Nhấn **Run Workflow** để kiểm tra kết quả.
   - **Kiểm tra output**:
     - Dữ liệu trích xuất có đầy đủ không?
     - Điểm ICP có hợp lý không?
     - **Nếu có lỗi**, quay lại **node Airtop** và chỉnh sửa prompt.

2. **Bật Active**:
   - Sau khi test thành công, nhấn **Active** để workflow chạy tự động khi có input.

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**

#### **1. Kết Nối Với CRM (Salesforce, HubSpot, Notion)**
- **Mục đích**: Tự động **cập nhật điểm ICP** vào CRM khi có mới leads.
- **Cách làm**:
  - Thêm **node Salesforce/HubSpot/Notion** sau node Airtop.
  - **Cấu hình**:
    - **Credentials**: Thêm API Key của CRM.
    - **Action**: "Create Record" (tạo mới lead với điểm ICP).
    - **Field Mapping**: Liên kết `icp_score` từ Airtop với field `ICP_Score` trong CRM.

#### **2. Batch Processing (Xử Lý Batch Leads)**
- **Mục đích**: Đánh giá **nhiều leads một lúc** thay vì một một.
- **Cách làm**:
  - Sử dụng **node "List CSV/Excel"** (n8n-nodes-base.listCSV) để đọc danh sách URL từ file.
  - **Cấu hình**:
    - File CSV có **1 cột là "LinkedIn URL"**.
    - **Loop** qua từng URL và truyền vào workflow này.

#### **3. Gửi Kết Quả Sang Slack/Telegram**
- **Mục đích**: **Báo cáo tự động** điểm ICP cho team.
- **Cách làm**:
  - Thêm **node Slack/Telegram** sau node Airtop.
  - **Cấu hình**:
    - **Credentials**: Thêm token Slack/Telegram.
    - **Message**: Tạo tin nhắn mẫu như:
      ```plaintext
      📊 **ICP Score Report**
      - **Name**: {{ $json["full_name"] }}
      - **Job Title**: {{ $json["job_title"] }}
      - **Company**: {{ $json["employer"] }}
      - **ICP Score**: {{ $json["icp_score"] }}/95
      - **Action**: [Xem hồ sơ]({{ $json["company_linkedin_url"] }})
      ```

#### **4. Lưu Log & Báo Cáo Định Kỳ**
- **Mục đích**: **Đánh giá hiệu quả** của leads trong thời gian.
- **Cách làm**:
  - Thêm **node "Set" (Log)** để lưu dữ liệu vào **Google Sheets/Notion**.
  - **Cấu hình**:
    - **Credentials**: Thêm API Key của Google Sheets.
    - **Action**: "Create Row" (tạo dòng mới với dữ liệu ICP).
    - **Schedule**: Sử dụng **n8n-nodes-base.schedule** để chạy hàng ngày/tuần.

#### **5. Tối Ưu H