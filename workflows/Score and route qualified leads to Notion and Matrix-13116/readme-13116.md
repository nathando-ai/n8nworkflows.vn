---
title: "🚀 Tự Động Hóa Xếp Loại & Phân Loại Lead Tiềm Năng Sang Notion + Matrix (AI + No-Code)"
description: "Workflow tự động hóa lấy dữ liệu lead mới từ API, enrich bằng Clearbit, tính điểm lead (score), phân loại và gửi thông báo ngay cho đội bán hàng qua Matrix. Giúp các sếp tiết kiệm 10+ giờ/tuần và tăng hiệu quả chuyển đổi lead 30%."
slug: "tieu-dong-hoa-xep-loai-lead-notion-matrix"
tags: [n8n, automation, lead-generation, ai-summarization, notion, matrix, no-code, clearbit, crm]
keywords: [n8n workflow lead generation, tự động hóa xếp hạng lead, enrich lead bằng clearbit, gửi thông báo lead qua matrix, notion crm tự động, tự động hóa bán hàng no-code]
---

# 🚀 **Tự Động Hóa Xếp Loại & Phân Loại Lead Tiềm Năng Sang Notion + Matrix**

## **🔥 Nỗi Đau Của Các Sếp Trong Quá Trình Xử Lý Lead**
Hàng ngày, các sếp phải:
- **Làm thủ công** theo dõi hàng chục lead mới từ form đăng ký, email, hoặc API.
- **Tốn thời gian** để enrich dữ liệu (tìm thông tin công ty, vị trí, số lượng nhân viên,...) bằng cách tra cứu Google hoặc API như Clearbit.
- **Không biết lead nào thực sự tiềm năng** vì thiếu tiêu chí khách hàng lý tưởng (ICP) rõ ràng.
- **Mất lead hot** vì không thông báo kịp thời cho đội bán hàng.
- **Lưu trữ rối loạn** dữ liệu lead trong nhiều nơi (Excel, Google Sheets, Notion), khó theo dõi và phân tích.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Lấy lead mới** từ API form đăng ký.
✅ **Enrich dữ liệu** bằng Clearbit (tìm thông tin công ty, vị trí, số lượng nhân viên,...).
✅ **Xếp hạng lead** (score 0-100) dựa trên tiêu chí ICP của bạn.
✅ **Phân loại lead** thành **tiềm năng (score ≥ 75)** và **không tiềm năng**.
✅ **Gửi thông báo ngay** cho đội bán hàng qua Matrix (hoặc Slack) khi có lead hot.
✅ **Lưu lead vào Notion** với trạng thái rõ ràng (Qualified/Disqualified) để theo dõi lâu dài.

---
### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tuần** không phải làm thủ công enrich và phân loại lead.
- **Tăng hiệu quả chuyển đổi lead** 30%+ vì chỉ tập trung vào lead tiềm năng (score cao).
- **Đội bán hàng nhận thông báo ngay** khi có lead hot qua Matrix/Slack (không phải chờ email).
- **Dữ liệu lead được quản lý chuyên nghiệp** trong Notion với trạng thái, điểm số, và lịch sử.
- **Hoạt động 24/7** mà không cần can thiệp của con người.
:::

---
### 🔧 **Yêu Cầu Cần Thiết**
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản API Leads**:
   - URL API của hệ thống form đăng ký (ví dụ: API của Typeform, Jotform, hoặc API nội bộ).
   - Credential API (Token, Key, hoặc Header Auth) để kết nối với API này.
2. **Tài khoản Clearbit**:
   - API Key của [Clearbit](https://clearbit.com/) để enrich dữ liệu lead (tìm thông tin công ty, vị trí, số lượng nhân viên,...).
3. **Tài khoản Notion**:
   - Database Notion đã tạo với các property cần thiết:
     - `Name` (Tên lead)
     - `Email` (Email lead)
     - `Company` (Công ty)
     - `Score` (Điểm lead)
     - `Status` (Trạng thái: Qualified/Disqualified)
   - Credential Notion để kết nối với database.
4. **Tài khoản Matrix/Slack** (lựa chọn):
   - Credential Matrix hoặc Slack để gửi thông báo khi có lead tiềm năng.
   - ID phòng chat (Room ID) trong Matrix hoặc Channel ID trong Slack.

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/13116](https://n8n.io/workflows/13116) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ link trên và paste vào **Import Workflow** trong n8n.
- **Cách 3**: Sử dụng plugin **n8n Browser Extension** để import trực tiếp từ trang workflow.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **16 node** với logic phức tạp. Dưới đây là hướng dẫn chi tiết để cấu hình:

##### **A. Cấu Hình API Leads (Fetch New Leads)**
- **Node**: `Fetch New Leads` (HTTP Request)
  - **Method**: POST hoặc GET (tùy thuộc vào API của bạn).
  - **URL**: Điền URL API của hệ thống form đăng ký (ví dụ: `https://api.typform.com/forms/YOUR_FORM_ID/submissions`).
  - **Headers**:
    - `Authorization`: Điền `Bearer YOUR_API_KEY` (nếu API yêu cầu).
    - `Content-Type`: `application/json`.
  - **Body (nếu cần)**: Nếu API yêu cầu payload, điền theo yêu cầu của API.
  - **Response Format**: API phải trả về **mảng JSON** với các trường tối thiểu:
    ```json
    [
      {
        "email": "lead@example.com",
        "name": "Lead Name",
        "company": "Company Name"  // (không bắt buộc, sẽ được enrich sau)
      }
    ]
    ```

##### **B. Cấu Hình Clearbit Enrichment**
- **Node**: `Clearbit Enrichment` (HTTP Request)
  - **Method**: POST.
  - **URL**: `https://company.clearbit.com/v2/companies/enrich?token=YOUR_CLEARBIT_API_KEY`.
  - **Headers**:
    - `Authorization`: `Bearer YOUR_CLEARBIT_API_KEY`.
    - `Content-Type`: `application/json`.
  - **Body**: Sử dụng **Dynamic Content** từ node trước (`Fetch New Leads`) để truyền email lead:
    ```json
    {
      "emails": ["{{ $json["email"] }}"]
    }
    ```
  - **Response Handling**: Clearbit trả về dữ liệu enrich như:
    ```json
    {
      "company": {
        "name": "Company Name",
        "size": 50,  // Số lượng nhân viên
        "funding": 5000000,  // Vốn đầu tư (nếu có)
        "alexa_rank": 10000  // Thứ hạng Alexa
      }
    }
    ```

##### **C. Cấu Hình Notion Database**
- **Node**: `Notion – Create Qualified Lead Page` và `Notion – Archive Disqualified Lead`
  - **Credential Notion**: Thêm credential Notion trong n8n với quyền **Write**.
  - **Database ID**: Tìm ID của database Notion trong URL:
    ```
    https://www.notion.so/workspace/YOUR_WORKSPACE_ID/database/YOUR_DATABASE_ID
    ```
    Điền `YOUR_DATABASE_ID` vào **Database ID** trong node Notion.
  - **Properties Mapping**:
    | Property trong Notion | Field trong Workflow |
    |-----------------------|----------------------|
    | Name                  | `{{ $node["Set – Lead Basics"].json["name"] }}` |
    | Email                 | `{{ $node["Set – Lead Basics"].json["email"] }}` |
    | Company               | `{{ $node["Merge – Combine Lead & Enrichment"].json["company"]["name"] }}` |
    | Score                 | `{{ $node["Code – Calculate Lead Score"].json["score"] }}` |
    | Status                | `Qualified` (hoặc `Disqualified`) |

##### **D. Cấu Hình Matrix/Slack Notification**
- **Node**: `Matrix Notify – New Qualified Lead`
  - **Credential Matrix/Slack**: Thêm credential vào n8n.
  - **Room ID/Channel ID**: Điền ID phòng chat trong Matrix hoặc Channel ID trong Slack.
  - **Message Template**: Sử dụng **Dynamic Content** trong node `Code – Build Matrix Message` để tự động tạo thông báo:
    ```markdown
    🚀 **New Qualified Lead Alert!** 🚀
    **Name**: {{ $node["Set – Lead Basics"].json["name"] }}
    **Email**: {{ $node["Set – Lead Basics"].json["email"] }}
    **Company**: {{ $node["Merge – Combine Lead & Enrichment"].json["company"]["name"] }}
    **Score**: {{ $node["Code – Calculate Lead Score"].json["score"] }}/100
    **Notion Page**: [View in Notion](https://www.notion.so/YOUR_DATABASE_ID?page={{ $node["Set – Build Notion Props"].json["title"] }})
    ```

##### **E. Cấu Hình Scoring Logic (Code Node)**
- **Node**: `Code – Calculate Lead Score`
  - Mở node này và chỉnh sửa logic tính điểm. Dưới đây là ví dụ cơ bản (sử dụng JavaScript):
    ```javascript
    // Điểm tối đa là 100
    let score = 0;

    // Tính điểm dựa trên số lượng nhân viên (Clearbit)
    if ($input.all().company.size) {
      if ($input.all().company.size > 100) score += 30;
      else if ($input.all().company.size > 50) score += 20;
      else if ($input.all().company.size > 10) score += 10;
    }

    // Tính điểm dựa trên vốn đầu tư (nếu có)
    if ($input.all().company.funding) {
      if ($input.all().company.funding > 5000000) score += 20;
      else if ($input.all().company.funding > 1000000) score += 10;
    }

    // Tính điểm dựa trên vị trí (CEO, CTO, Founder)
    const role = $input.all().job_title.toLowerCase();
    if (role.includes("ceo") || role.includes("cto") || role.includes("founder")) {
      score += 20;
    }

    // Đảm bảo điểm không quá 100
    score = Math.min(score, 100);

    // Xác định lead có tiềm năng không
    const isQualified = score >= 75;

    return {
      score: score,
      qualified: isQualified
    };
    ```
  - **Lưu ý**: Các sếp có thể điều chỉnh trọng số (ví dụ: tăng điểm cho công ty có vốn lớn hơn) để phù hợp với ICP của mình.

##### **F. Cấu Hình Batching & Rate-Limit**
- **Node**: `Split In Batches` và `Wait 1 s (Rate-limit)`
  - `Split In Batches`: Đặt **Batch Size = 1** để xử lý lead một lúc (tránh quá tải API).
  - `Wait 1 s`: Giúp tránh bị rate-limiting khi gọi API Clearbit hoặc Notion.

---

#### **3. Kích Hoạt Workflow ⚡️**
1. **Test Run**:
   - Chạy **Manual Execution** với dữ liệu mẫu để kiểm tra logic.
   - Kiểm tra:
     - Lead có được enrich không?
     - Điểm score có hợp lý không?
     - Thông báo Matrix/Slack có được gửi không?
     - Lead có được lưu vào Notion không?
2. **Bật Active**:
   - Sau khi kiểm tra thành công, bật **Active** để workflow chạy tự động theo lịch.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết hợp với Slack thay vì Matrix**:
   - Thay node `Matrix Notify` bằng node `Slack Webhook` và cấu hình tương tự.
2. **Lưu log hoạt động**:
   - Thêm node `Sticky Note` hoặc `Google Sheets` để ghi lại lịch sử lead đã xử lý.
3. **Gửi báo cáo định kỳ**:
   - Sử dụng node `Schedule Trigger` (tháng) kết hợp với node `Notion` để tạo báo cáo tổng hợp lead.
4. **Tự động gắn tag trong Notion**:
   - Sử dụng node `Notion` với property `Tags` để tự động gắn tag `Hot Lead` cho lead score ≥ 90.
5. **Kết hợp với AI Chatbot**:
   - Sử dụng node `n8n-nodes-base.llm` (nếu có) để tự động phân tích lead và đề xuất hành động tiếp theo.

---
### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** để tự động hóa quá trình xử lý lead từ đầu đến cuối, giúp các sếp:
✔ **Tiết kiệm thời gian** và tập trung vào việc bán hàng chứ không phải làm thủ công.
✔ **Tăng hiệu quả** với lead tiềm năng được phân loại chính xác.
✔ **Cung cấp thông tin kịp thời** cho đội bán hàng qua Matrix/Slack.
✔ **Quản lý lead chuyên nghiệp** trong Notion với dữ liệu đầy đủ và dễ theo dõi.

**Hành động ngay hôm nay!**
1. **Cài đặt n8n Self-hosted** trên VPS để workflow chạy 24/7 (không phụ thuộc vào n8n.io).
2. **Import workflow** và cấu hình theo hướng dẫn trên.
3. **Bật Active** và bắt đầu tự động hóa lead của mình!

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**Chia sẻ và đặt câu hỏi!** Nếu các sếp có bất kỳ thắc mắc hoặc muốn tùy chỉnh workflow, hãy để lại comment bên dưới. Chúng tôi sẽ hỗ trợ miễn phí! 🚀