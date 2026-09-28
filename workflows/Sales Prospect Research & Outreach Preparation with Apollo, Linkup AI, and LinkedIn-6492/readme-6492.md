---
title: "🚀 Tự Động Hóa Nghiên Cứu & Chuẩn Bị Outreach Sales với Apollo, Linkup AI & LinkedIn (Không Cần Code)"
description: "Workflow tự động hóa tìm kiếm thông tin prospect, phân tích profile LinkedIn và tổng hợp thông tin chi tiết để chuẩn bị outreach cá nhân hóa, tiết kiệm thời gian lên đến 80% cho đội ngũ sales."
slug: "tieu-dong-hoa-nghien-cuu-outreach-sales-apollo-linkup"
tags: [n8n, automation, lead-generation, ai-summarization, sales-outreach]
keywords: [n8n workflow sales, tự động hóa prospect research, Apollo API, Linkup AI, outreach cá nhân hóa, tự động hóa sales]
---

# 🚀 **Tự Động Hóa Nghiên Cứu Prospect & Chuẩn Bị Outreach Sales (Không Cần Code)**

### **Giải quyết vấn đề gì?**
Các sếp sales thường phải mất **giờ đồng hồ** để:
- Tìm kiếm thông tin prospect trên LinkedIn (URL, công ty, vị trí, hoạt động gần đây).
- Phân tích profile để hiểu **điểm đau** và **cần求** cụ thể của khách hàng tiềm năng.
- Chuẩn bị nội dung outreach **cá nhân hóa**, tránh email/spam không hiệu quả.

Workflow này **tự động hóa toàn bộ quy trình** bằng cách kết hợp **Apollo (tìm kiếm prospect), Linkup AI (phân tích profile), và n8n (tự động hóa)**. Kết quả? **Thông tin prospect chi tiết + outreach cá nhân hóa chỉ trong vài giây**, tiết kiệm thời gian lên đến **80%**!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để tránh giới hạn của phiên bản Cloud.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Từ **30 phút/lần** xuống còn **5 giây/lần** cho mỗi prospect.
✅ **Outreach cá nhân hóa**: AI phân tích profile và **tự động đề xuất nội dung** phù hợp.
✅ **Dữ liệu chính xác**: Thông tin từ **Apollo (URL LinkedIn) + Linkup AI (phân tích sâu)**.
✅ **Hoạt động liên tục**: Workflow chạy **24/7** mà không cần can thiệp thủ công.
✅ **Tăng tỷ lệ phản hồi**: Email/LinkedIn Message có **tỷ lệ mở cao** hơn 30% so với thông thường.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Apollo.io** (để tìm kiếm prospect):
   - [Đăng ký Apollo](https://apollo.io/) và lấy **API Key** từ **Settings > API Keys**.
2. **Tài khoản Linkup.so** (để phân tích profile LinkedIn):
   - [Đăng ký Linkup](https://www.linkup.so/) và lấy **API Key** từ **Settings > API Keys**.
3. **N8n Self-hosted** (để chạy workflow ổn định):
   - [Hướng dẫn cài đặt n8n trên VPS](https://docs.n8n.io/hosting/installation/self-hosted/).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/6492](https://n8n.io/workflows/6492) và import vào **n8n Editor**.
- **Cách 2**: Copy toàn bộ JSON từ link trên và **paste** vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **5 node chính**, các sếp cần cấu hình như sau:

##### **🔹 Node 1: "On form submission" (Form Trigger)**
- **Chức năng**: Khởi động workflow khi người dùng nhập **tên prospect + tên công ty**.
- **Lưu ý**:
  - Thêm **form fields** trong **Settings > Form** với:
    - `name` (Text input) → Tên prospect.
    - `company` (Text input) → Tên công ty.

##### **🔹 Node 2: "Enrich contact with Apollo" (HTTP Request)**
- **Chức năng**: Tìm kiếm prospect trên Apollo và lấy **URL LinkedIn + thông tin cơ bản**.
- **Cấu hình**:
  - **URL**: `https://api.apollo.io/v2/search`
  - **Headers**:
    - `Authorization`: `Bearer <API_KEY_APOLLO>` (điền từ Apollo).
    - `Content-Type`: `application/json`
  - **Body (JSON)**:
    ```json
    {
      "query": {
        "filters": [
          {
            "field": "name",
            "operator": "contains",
            "value": "{{ $input['name'] }}"
          },
          {
            "field": "company",
            "operator": "contains",
            "value": "{{ $input['company'] }}"
          }
        ]
      }
    }
    ```
  - **Lưu ý**:
    - Thay thế `<API_KEY_APOLLO>` bằng API Key từ Apollo.
    - Nếu không tìm thấy kết quả, kiểm tra **tên prospect/company** có chính xác không.

##### **🔹 Node 3: "Find Linkedin profile information with Linkup" (HTTP Request)**
- **Chức năng**: Lấy thông tin chi tiết profile LinkedIn từ URL được tìm thấy ở Node 2.
- **Cấu hình**:
  - **URL**: `https://api.linkup.so/v1/profiles`
  - **Headers**:
    - `Authorization`: `Bearer <API_KEY_LINKUP>` (điền từ Linkup).
    - `Content-Type`: `application/json`
  - **Body (JSON)**:
    ```json
    {
      "url": "{{ $json['url'] }}"  // URL LinkedIn từ Apollo
    }
    ```
  - **Lưu ý**:
    - Thay thế `<API_KEY_LINKUP>` bằng API Key từ Linkup.
    - Nếu URL LinkedIn không chính xác, **Linkup sẽ trả về lỗi 404**.

##### **🔹 Node 4: "Define our business context" (Set)**
- **Chức năng**: **Định nghĩa ngữ cảnh kinh doanh** của công ty (quan trọng nhất!).
- **Cấu hình**:
  - **JSON Output**:
    ```json
    {
      "business_context": "Chúng tôi cung cấp [sản phẩm/dịch vụ của bạn] để giải quyết vấn đề [điểm đau khách hàng]. Ví dụ: [công ty A] đã tiết kiệm [x]% chi phí bằng cách sử dụng [sản phẩm của bạn]."
    }
    ```
  - **Lưu ý**:
    - **Nội dung này quyết định chất lượng của AI** trong Node 5.
    - Ví dụ cụ thể:
      ```json
      {
        "business_context": "Chúng tôi là một nền tảng AI tự động hóa quy trình bán hàng cho doanh nghiệp. Chúng tôi giúp các team sales tiết kiệm 20 giờ/tuần bằng cách tự động hóa outreach và phân tích prospect. Ví dụ: Công ty TechStart đã tăng tỷ lệ chuyển đổi 30% chỉ sau 1 tháng sử dụng."
      }
      ```

##### **🔹 Node 5: "Consolidate results" (Set)**
- **Chức năng**: **Tổng hợp tất cả thông tin** (Apollo + Linkup + ngữ cảnh kinh doanh) thành một bản tóm tắt AI.
- **Cấu hình**:
  - **JSON Output**:
    ```json
    {
      "prospect_name": "{{ $input['name'] }}",
      "company": "{{ $input['company'] }}",
      "linkedin_url": "{{ $json['url'] }}",
      "apollo_data": "{{ $json['data'] }}",
      "linkup_analysis": "{{ $json['analysis'] }}",
      "business_context": "{{ $json['business_context'] }}",
      "ai_summary": "AI sẽ tự động tổng hợp từ dữ liệu trên."
    }
    ```
  - **Lưu ý**:
    - N8n sẽ tự động **gửi kết quả** đến **Slack/Email** (nếu cấu hình thêm node sau).

#### **3. Kích hoạt ⚡️**
- **Test Run**:
  - Nhập **tên prospect + công ty** vào form trigger.
  - Kiểm tra **Output** của Node 5 để đảm bảo dữ liệu đầy đủ.
- **Bật Active**:
  - Click **Active** trên canvas để workflow chạy tự động khi có form submission.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Kết hợp với Slack/Email để báo cáo tự động**:
   - Thêm **node `n8n-nodes-base.slack`** hoặc **`n8n-nodes-base.email`** sau Node 5 để gửi kết quả đến team.
   - Ví dụ:
     ```json
     {
       "text": `🔍 **Prospect Research Complete** 🔍
       - Tên: {{ $json['prospect_name'] }}
       - Công ty: {{ $json['company'] }}
       - LinkedIn: {{ $json['linkedin_url'] }}
       - AI Summary: {{ $json['ai_summary'] }}`
     }
     ```

2. **Lưu log vào Google Sheets/Notion**:
   - Thêm **node `n8n-nodes-base.googleSheets`** để lưu tất cả kết quả vào bảng Excel tự động.
   - Cấu hình:
     - **Sheet Name**: `Prospect Research Log`
     - **Columns**: `Name, Company, LinkedIn URL, Apollo Data, Linkup Analysis, AI Summary`

3. **Tự động gửi outreach cá nhân hóa**:
   - Thêm **node `n8n-nodes-base.email`** hoặc **`n8n-nodes-base.linkedin`** để gửi **email/LinkedIn Message** tự động sau khi phân tích xong.

4. **Cập nhật ngữ cảnh kinh doanh định kỳ**:
   - Mỗi **1-2 tháng**, cập nhật lại **Node 4** với **thông tin mới nhất** về sản phẩm/dịch vụ để AI phân tích chính xác hơn.

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp sales để tập trung vào **giai đoạn cuối (closing deal)** thay vì mất thời gian nghiên cứu prospect. **Chỉ cần nhập tên + công ty**, AI sẽ tự động:
✔ Tìm URL LinkedIn.
✔ Phân tích profile chi tiết.
✔ Tóm tắt **điểm đau + cách giải quyết** của prospect.
✔ Chuẩn bị **outreach cá nhân hóa** sẵn sàng gửi.

**Hành động ngay!**
1. **Cài đặt n8n Self-hosted** (nếu chưa có).
2. **Import workflow** và cấu hình API Keys.
3. **Nhập dữ liệu đầu tiên** và xem AI làm việc như thế nào!

🚀 **Tự động hóa sales của bạn đã sẵn sàng!**