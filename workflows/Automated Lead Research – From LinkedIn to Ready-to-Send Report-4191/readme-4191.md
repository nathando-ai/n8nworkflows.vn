---
title: "🚀 Tự Động Hoá Nghiên Cứu Lead Từ LinkedIn Đến Báo Cáo Sẵn Sàng Gửi – Không Cần Code!"
description: "Workflow này tự động tra cứu thông tin chi tiết của lead từ LinkedIn, phân tích bằng AI (OpenAI + Perplexity), và tạo báo cáo định dạng Google Docs/Sheets sẵn sàng gửi cho team Sales. Giúp các sếp tiết kiệm **50% thời gian nghiên cứu lead** và nâng cao chất lượng tương tác."
slug: "tieu-dong-hoa-nghien-cuu-lead-tu-linkedin-den-bao-cao-san-sang"
tags: [n8n, automation, sales, ai, linkedin, google-sheets, google-docs, openai, perplexity]
keywords: [tự động hóa lead research, n8n workflow linkedin, phân tích lead bằng ai, báo cáo sales tự động, tự động hóa sales marketing]
---

# 🚀 **Tự Động Hoá Nghiên Cứu Lead Từ LinkedIn Đến Báo Cáo Sẵn Sàng Gửi**

Hiện nay, các sếp Sales phải mất **giờ đồng hồ** để tra cứu thông tin chi tiết của lead trên LinkedIn, phân tích hành vi, nghiên cứu đối thủ, và cuối cùng viết báo cáo để gửi cho khách hàng tiềm năng. Quá trình này không chỉ tốn thời gian mà còn dễ bị lỗi nhân sự (con người quên hoặc sai sót). **Workflow này giải quyết tất cả vấn đề đó bằng cách tự động hóa toàn bộ quy trình từ A đến Z – chỉ cần nhập thông tin lead, AI sẽ làm tất cả!**

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 50% thời gian nghiên cứu lead**: AI tự động tra cứu thông tin chi tiết từ LinkedIn và Perplexity.
- **Báo cáo cá nhân hóa**: Dữ liệu được phân tích và tổng hợp thành báo cáo định dạng Google Docs/Sheets, sẵn sàng gửi cho khách hàng.
- **Nâng cao chất lượng tương tác**: AI phân tích hành vi, ngành nghề, và đối thủ của lead để team Sales có chiến lược phù hợp.
- **Hoạt động 24/7**: Workflow chạy tự động khi có lead mới, không cần can thiệp thủ công.
- **Tích hợp AI hiện đại**: Sử dụng OpenAI (ChatGPT) và Perplexity để tra cứu thông tin chính xác và sâu sắc.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản LinkedIn**:
   - **Tài khoản cá nhân** (để tra cứu thông tin cá nhân của lead).
   - **Tài khoản công ty** (để tra cứu thông tin công ty của lead).
   - **API Access Token** của LinkedIn (cần đăng ký tại [LinkedIn Developer Portal](https://www.linkedin.com/developers/)).
2. **Tài khoản Google**:
   - **Google Sheets** (để lưu trữ dữ liệu lead và báo cáo).
   - **Google Docs** (để tạo báo cáo cuối cùng).
   - **Service Account Email** (để quyền truy cập vào Google Sheets/Docs).
3. **API Keys**:
   - **OpenAI API Key** (để sử dụng ChatGPT và AI phân tích).
   - **Perplexity API Key** (để tra cứu thông tin từ Perplexity).
4. **Dữ liệu đầu vào**:
   - Danh sách lead (có thể là email, tên, hoặc liên kết LinkedIn) trong **Google Sheets** (cột `Lead Data`).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/4191](https://n8n.io/workflows/4191) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ link trên và paste vào **Import Workflow** trong n8n Editor.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **28 node** và có **3 phần chính**:
- **Phần 1: Tra cứu thông tin lead từ LinkedIn** (API GET/POST).
- **Phần 2: Phân tích bằng AI** (OpenAI + Perplexity).
- **Phần 3: Tạo báo cáo tự động** (Google Docs/Sheets).

##### **A. Cấu hình API LinkedIn**
- **Node**: `Personal LinkedIn Account GET` và `Company LinkedIn Account GET`.
  - **Tham số cần điền**:
    - `Authorization`: `Bearer <API_ACCESS_TOKEN>` (đăng ký tại [LinkedIn Developer Portal](https://www.linkedin.com/developers/)).
    - **Headers**:
      - `X-Restli-Protocol-Version`: `2.0.0`
      - `Content-Type`: `application/json`
    - **URL mẫu**:
      - Cá nhân: `https://api.linkedin.com/v2/people/{id}?projection=(basicProfile)`
      - Công ty: `https://api.linkedin.com/v2/companies/{id}?projection=(basic)`

##### **B. Cấu hình AI (OpenAI & Perplexity)**
- **Node**: `OpenAI Chat Model`, `Perplexity Search`.
  - **Tham số cần điền**:
    - **OpenAI**:
      - `API Key`: Nhập từ [OpenAI Dashboard](https://platform.openai.com/account/api-keys).
      - **Model**: Chọn `gpt-3.5-turbo` (hoặc `gpt-4` nếu có).
    - **Perplexity**:
      - `API Key`: Nhập từ [Perplexity API](https://www.perplexity.ai/api).
      - **Prompt mẫu** (cần chỉnh sửa theo yêu cầu):
        ```json
        "Analyze the following LinkedIn profile and provide insights on industry trends, potential pain points, and competitive landscape."
        ```

##### **C. Cấu hình Google Sheets & Docs**
- **Node**: `Get All Data`, `Add to sheets`, `Create doc`, `Add report to doc`.
  - **Tham số cần điền**:
    - **Google Sheets**:
      - `Spreadsheet ID`: Tìm trong URL của file Sheets (vd: `1AbCdeFgHiJkLmNoPqRsTuVwXyZ`).
      - `Sheet Name`: Tên sheet chứa dữ liệu lead (vd: `Lead Data`).
    - **Google Docs**:
      - `File ID`: Tạo một file Docs mới và copy `File ID` từ URL.
      - **Permissions**: Cấp quyền cho **Service Account Email** (đăng ký tại [Google Cloud Console](https://console.cloud.google.com/)).

##### **D. Cấu hình Trigger Manual**
- **Node**: `When clicking ‘Test workflow’`.
  - **Lưu ý**: Workflow sẽ chạy khi nhấn nút **Test** hoặc khi có dữ liệu mới trong Google Sheets (cột `Lead Data`).

---

#### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Nhấn **Test** và nhập **1 lead mẫu** (email, tên, hoặc liên kết LinkedIn) vào Google Sheets.
   - Kiểm tra kết quả trong **Google Docs** (báo cáo tự động tạo).
2. **Bật Active**:
   - Sau khi test thành công, chuyển workflow sang **Active**.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tích hợp Slack/Telegram**:
   - Thêm node **Slack Webhook** hoặc **Telegram Bot** để thông báo khi báo cáo hoàn thành.
2. **Lưu log hoạt động**:
   - Sử dụng node **Sticky Note** để ghi lại lịch sử hoạt động của workflow.
3. **Gửi báo cáo định kỳ**:
   - Kết hợp với **Google Calendar API** để tự động gửi báo cáo cho team Sales hàng tuần.
4. **Cải thiện prompt AI**:
   - Chỉnh sửa **prompt** trong node `Analyst of prospect` để phù hợp với ngành nghề của lead (vd: Tech, Finance, Healthcare).

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp Sales để tập trung vào việc bán hàng thay vì nghiên cứu lead. Bằng cách tự động hóa toàn bộ quy trình từ tra cứu LinkedIn đến tạo báo cáo AI, các sếp sẽ:
✅ **Tiết kiệm 50% thời gian**.
✅ **Nâng cao chất lượng tương tác**.
✅ **Hoạt động 24/7** mà không cần can thiệp thủ công.

**Hãy import workflow ngay hôm nay và bắt đầu tự động hóa Sales của mình!** 🚀

---
**Ghi chú cuối cùng**:
- Nếu gặp lỗi API, kiểm tra lại **các permission** của tài khoản LinkedIn và Google.
- Để tối ưu hóa, các sếp có thể **tùy chỉnh prompt AI** theo ngành nghề cụ thể của lead.