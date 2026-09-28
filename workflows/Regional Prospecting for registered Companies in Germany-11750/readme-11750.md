---
title: "🔍 Tự Động Tìm Kiếm & Lọc Doanh Nghiệp Chất Lượng Cao Tại Đức (B2B Marketing) - N8N"
description: "Workflow tự động hóa tìm kiếm, đánh giá và phân loại doanh nghiệp đăng ký tại các khu vực cụ thể ở Đức bằng API Implisense (Handelsregister), giúp các sếp tiết kiệm thời gian lên tới 80% trong quá trình lead generation B2B."
slug: "tieu-diem-doi-nghiep-chat-luong-tai-deuc"
tags: [n8n, automation, lead-generation, b2b-marketing, api-integration]
keywords: [tự động hóa tìm kiếm doanh nghiệp Đức, n8n workflow lead generation, api handelsregister, tự động hóa b2b marketing, tìm kiếm doanh nghiệp theo khu vực]
---

# 🚀 **Tự Động Tìm Kiếm & Lọc Doanh Nghiệp Chất Lượng Cao Tại Đức (B2B Marketing)**

Hiện nay, các sếp trong lĩnh vực **B2B marketing/sales** thường phải mất **giờ đồng hồ** để tìm kiếm, lọc và đánh giá danh sách doanh nghiệp đăng ký tại Đức theo khu vực, ngành nghề và tiêu chí chất lượng. Quá trình này không chỉ tốn thời gian mà còn dễ gặp **lỗi nhân sự** (con người mệt mỏi, thiếu chính xác) và **thiếu tính liên tục** (không hoạt động 24/7).

**Workflow này giải quyết vấn đề đó bằng cách:**
✅ **Tự động hóa toàn bộ quy trình** từ tìm kiếm đến đánh giá chất lượng doanh nghiệp.
✅ **Sử dụng API Implisense (Handelsregister)** để lấy dữ liệu **2.5 triệu doanh nghiệp** tại Đức.
✅ **Phân loại tự động** doanh nghiệp thành **chất lượng cao** (score ≥15) và **chất lượng trung bình** (score <15).
✅ **Kết nối với CRM/Database** để lưu trữ và sử dụng ngay trong hệ thống bán hàng.

---
### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian lên tới 80%** so với cách làm thủ công.
- **Chất lượng lead cao hơn** với tiêu chí đánh giá khách quan (website, địa chỉ đầy đủ, hoạt động).
- **Hoạt động liên tục 24/7** mà không cần can thiệp của con người.
- **Dữ liệu sạch và không trùng lặp** nhờ hệ thống vetting tự động.
- **Kết nối dễ dàng với CRM** (HubSpot, Salesforce, Zoho) hoặc cơ sở dữ liệu riêng.
:::

---
### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản RapidAPI** (miễn phí):
   - Đăng ký tại [RapidAPI](https://rapidapi.com/) và lấy **x-rapidapi-key**.
   - **Ghi chú:** Nếu không có API key, workflow sẽ **không hoạt động**.
2. **Tham số tìm kiếm (cấu hình sau khi import):**
   - `query`: Từ khóa tìm kiếm (ví dụ: `"software OR it"`).
   - `regionCode`: Mã khu vực (ví dụ: `"de-10"` cho Berlin).
   - `industryCode`: Mã ngành NACE (ví dụ: `"J62"` cho phần mềm).
   - `pageSize`: Số kết quả tối đa (1-1000).
3. **(Tùy chọn) Nguồn kết nối CRM/Database:**
   - Nếu muốn lưu kết quả vào CRM (HubSpot, Salesforce) hoặc cơ sở dữ liệu, cần **API key** hoặc **credentials** tương ứng.
:::

---
### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/11750](https://n8n.io/workflows/11750) và import vào **n8n Editor**.
- **Cách 2:** Copy toàn bộ JSON từ link trên và **paste** vào **Import Workflow** trong n8n.
- **Lưu ý:** Nếu import từ file, **không cần chỉnh sửa** cấu trúc workflow, chỉ cần **cấu hình các node quan trọng** sau.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow gồm **3 giai đoạn chính** (Init, Search, Vetting). Dưới đây là **các node cần cấu hình kỹ lưỡng**:

##### **🔹 Phase 1: Init (Khởi tạo)**
- **Node "Authorization" (type: set):**
  - **Tham số cần điền:**
    - `headers.x-rapidapi-key`: Dán **API key** từ RapidAPI vào đây.
    - **Lưu ý:** Nếu không điền, API sẽ **không trả về kết quả**.

##### **🔹 Phase 2: Search (Tìm kiếm)**
- **Node "Implisense Search" (type: httpRequest):**
  - **URL:** `https://implisense.p.rapidapi.com/search`
  - **Headers:**
    - `x-rapidapi-key`: Điền từ **Node "Authorization"**.
    - `x-rapidapi-host`: `implisense.p.rapidapi.com`.
  - **Body (JSON):**
    ```json
    {
      "query": "{{ $node["Prepare Search Input"].json["query"] }}",
      "regionCode": "{{ $node["Prepare Search Input"].json["regionCode"] }}",
      "industryCode": "{{ $node["Prepare Search Input"].json["industryCode"] }}",
      "pageSize": "{{ $node["Prepare Search Input"].json["pageSize"] }}"
    }
    ```
  - **Lưu ý:** Nếu không cấu hình **Node "Prepare Search Input"**, workflow sẽ **không tìm kiếm được**.

- **Node "Prepare Search Input" (type: set):**
  - **Tham số mặc định:**
    ```json
    {
      "query": "software OR it",
      "regionCode": "de-10",
      "industryCode": "J62",
      "pageSize": 100
    }
    ```
  - **Cách chỉnh:**
    - **Thay đổi `query`** theo từ khóa tìm kiếm (ví dụ: `"finance"`, `"healthcare"`).
    - **Thay đổi `regionCode`** theo mã khu vực (danh sách [mã ZIP Đức](https://www.postleitzahlen-vorwahl.de/)).
    - **Thay đổi `industryCode`** theo [mã NACE](https://ec.europa.eu/eurostat/web/nuts/industry/industry-classification-nace-revision-2).

##### **🔹 Phase 3: Vetting (Đánh giá chất lượng)**
- **Node "Validate Input" (type: code):**
  - **Mục đích:** Kiểm tra đầu vào có hợp lệ không.
  - **Không cần chỉnh sửa** (n8n tự động kiểm tra).

- **Node "Normalize & Score Results" (type: code):**
  - **Mục đích:** Đánh giá điểm số cho mỗi doanh nghiệp dựa trên tiêu chí:
    - Có website không?
    - Địa chỉ đầy đủ không?
    - Hoạt động (active) không?
  - **Không cần chỉnh sửa** (n8n tự động tính điểm).

- **Node "Sort by Relevance" (type: code):**
  - **Mục đích:** Sắp xếp danh sách theo **điểm số cao nhất**.
  - **Không cần chỉnh sửa**.

- **Node "High Quality Leads?" (type: if):**
  - **Tiêu chí:**
    - **Chất lượng cao:** `score >= 15`.
    - **Chất lượng trung bình:** `score < 15`.
  - **Không cần chỉnh sửa** (n8n tự động phân loại).

- **Node "Prepare High Quality Payload" & "Prepare Medium Quality Payload" (type: set):**
  - **Mục đích:** Chuẩn bị dữ liệu để **lưu vào CRM/Database**.
  - **Cách chỉnh:**
    - Nếu muốn **lưu vào CRM** (ví dụ: HubSpot), thêm **Node HTTP Request** sau "Merge & Log Results" với:
      - **URL:** API endpoint của CRM.
      - **Headers:** `Authorization: Bearer {{ $node["Authorization"].json["apiKey"] }}`.
      - **Body:** Dữ liệu từ `{{ $json }}`.

- **Node "Merge & Log Results" (type: code):**
  - **Mục đích:** Gộp kết quả **chất lượng cao** và **trung bình** thành một danh sách duy nhất.
  - **Không cần chỉnh sửa**.

- **Node "Generate Summary Report" (type: set):**
  - **Mục đích:** Tạo **báo cáo tổng hợp** (số lượng lead, điểm trung bình, khu vực, ngành nghề).
  - **Cách sử dụng:**
    - Có thể **gửi báo cáo qua Email** (n8n-nodes-base.email) hoặc **Slack** (n8n-nodes-base.slack).
    - **Ví dụ cấu hình Email:**
      ```json
      {
        "to": "team@doanhnghiep.com",
        "subject": "Báo cáo lead Đức - {{ $node["Generate Summary Report"].json["regionCode"] }}",
        "text": "Tổng số lead: {{ $node["Generate Summary Report"].json["totalLeads"] }}\n\n- Chất lượng cao: {{ $node["Generate Summary Report"].json["highQuality"] }}\n- Chất lượng trung bình: {{ $node["Generate Summary Report"].json["mediumQuality"] }}"
      }
      ```

#### **3. Kích hoạt ⚡️**
- **Bước 1:** **Test Run** với dữ liệu mẫu:
  - Nhấn **Run Workflow** và kiểm tra kết quả ở **Node "Merge & Log Results"**.
  - **Nếu có lỗi API**, kiểm tra lại **x-rapidapi-key** và **headers**.
- **Bước 2:** **Bật Active** workflow.
- **Bước 3 (tùy chọn):** **Lên lịch tự động** (n8n-nodes-base.schedule) để chạy hàng ngày/tuần.

---
### ✍️ **Mẹo & gợi ý nâng cao**
:::info[CÁC Ý TƯỞNG MỞ RỘNG]
1. **Kết nối với Slack/Telegram:**
   - Sau **Node "Generate Summary Report"**, thêm **Node Slack/Telegram** để thông báo kết quả tự động.
   - **Ví dụ:**
     ```json
     {
       "text": "🚀 Đã tìm kiếm lead Đức - {{ $node["Generate Summary Report"].json["regionCode"] }}!\n- Tổng lead: {{ $node["Generate Summary Report"].json["totalLeads"] }}"
     }
     ```

2. **Lưu log vào cơ sở dữ liệu:**
   - Sử dụng **Node Database (PostgreSQL/MySQL)** để lưu lịch sử tìm kiếm.
   - **Cách cấu hình:**
     - Thêm **Node Database** sau "Merge & Log Results".
     - **Query:**
       ```sql
       INSERT INTO lead_search_history (region, industry, total_leads, timestamp)
       VALUES ('{{ $node["Generate Summary Report"].json["regionCode"] }}', '{{ $node["Generate Summary Report"].json["industryCode"] }}', {{ $node["Generate Summary Report"].json["totalLeads"] }}, NOW());
       ```

3. **Tự động gửi báo cáo định kỳ:**
   - Sử dụng **Node Schedule** để chạy workflow hàng tuần.
   - **Ví dụ:**
     - **Cron:** `0 0 * * 1` (Chạy thứ 2 hàng tuần).
     - **Node Email** để gửi báo cáo tự động.

4. **Tăng cường tính cá nhân hóa:**
   - Sau khi **phân loại lead**, thêm **Node LLM (n8n-nodes-base.llm)** để tự động viết **email cold outreach** cho lead chất lượng cao.
   - **Ví dụ Prompt:**
     ```
     Tôi là một chuyên gia B2B marketing. Viết một email cold outreach ngắn gọn (5-6 câu) để giới thiệu sản phẩm [Tên Sản Phẩm] cho công ty [Tên Công Ty] tại Đức. Email phải:
     - Giới thiệu ngắn gọn về sản phẩm.
     - Nêu lợi ích cụ thể cho ngành [Ngành Nghề].
     - Kết thúc bằng một call-to-action rõ ràng (ví dụ: "Hãy liên hệ với tôi để biết thêm chi tiết").
     ```

5. **Duy trì danh sách lead sạch:**
   - Thêm **Node Set** sau "Merge & Log Results" để **xóa trùng lặp** bằng ID công ty.
   - **Cách sử dụng:**
     ```json
     {
       "uniqueLeads": "{{ $node["Merge & Log Results"].json | uniqueBy('companyId') }}"
     }
     ```
:::

---
### 📌 **Kết luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp trong **B2B marketing/sales** muốn:
✔ **Tự động hóa tìm kiếm lead** tại Đức mà không cần code.
✔ **Lọc và đánh giá chất lượng** doanh nghiệp một cách khách quan.
✔ **Kết nối với CRM/Database** để sử dụng ngay trong hệ thống bán hàng.

**Hành động ngay hôm nay:**
1. **Import workflow** và cấu hình **API key**.
2. **Chỉnh sửa tham số tìm kiếm** theo nhu cầu.
3. **Kết nối với CRM** hoặc **lưu log** để bắt đầu tự động hóa!

**🎁 Mã giảm giá VPS cho n8n (Self-hosted):**
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**).
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).
:::

**Chúc các sếp thành công với chiến dịch B2B marketing mới!** 🚀