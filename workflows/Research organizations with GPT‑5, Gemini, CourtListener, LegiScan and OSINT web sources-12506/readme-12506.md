---
title: "🔍 **Tự Động Hoà AI: Nghiên Cứu Tổ Chức Sinh Vật & OSINT Với GPT-5, Gemini & 10 Nguồn Dữ Liệu Công Khai**"
description: "Workflow tự động hóa nghiên cứu tổ chức sinh vật và OSINT (Open-Source Intelligence) bằng AI tiên tiến như GPT-5, Gemini, và các nguồn dữ liệu công khai như CourtListener, LegiScan, Twitter, LinkedIn. Sản sinh báo cáo Markdown chính xác, tự động hóa 100% không cần code."
slug: "tieu-dong-hoa-nghien-cuu-toc-chuc-sinh-vat-gpt-5-gemini"
tags: [n8n, automation, ai-rag, osint, market-research, gpt-5, gemini, open-source]
keywords: [n8n workflow nghiên cứu tổ chức, tự động hóa osint, gpt-5 gemini tự động hóa, báo cáo tổ chức sinh vật, công cụ nghiên cứu công khai]
---

# 🚀 **Nghiên Cứu Tổ Chức Sinh Vật & OSINT Tự Động Hóa Với AI: Từ Dữ Liệu Công Khai Đến Báo Cáo Markdown**

## **🔥 Nỗi Đau Của Các Sếp Trong Nghiên Cứu Tổ Chức**
Bạn có bao giờ phải:
- **Tốn hàng giờ** để tra cứu thông tin từ nhiều nguồn khác nhau (CourtListener, LegiScan, LinkedIn, Twitter...)?
- **Lo ngại sai sót** khi tổng hợp dữ liệu từ nhiều nguồn không đồng nhất?
- **Không biết cách xác minh** tính chính xác của thông tin từ AI (như GPT-5 hay Gemini)?
- **Không có báo cáo tự động** để chia sẻ với ban lãnh đạo hoặc khách hàng?

Workflow này **giải quyết tất cả** bằng cách tự động hóa **nghiên cứu tổ chức sinh vật (animal advocacy)** và OSINT (Open-Source Intelligence) với **AI tiên tiến**, kết hợp **10+ nguồn dữ liệu công khai**, và **sản sinh báo cáo Markdown** hoàn chỉnh.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7** và **không bị gián đoạn**, các sếp nên cài đặt n8n trên **VPS riêng (Self-hosted)** với các tính năng tối ưu:
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đảm bảo tốc độ cao cho AI)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Từ **hàng giờ** xuống **vài phút** để hoàn thành nghiên cứu.
✅ **Chính xác cao**: AI **Gemini + GPT-5** kết hợp với **OSINT** để **xác minh và lọc bỏ thông tin sai lệch**.
✅ **Báo cáo tự động**: **Markdown sạch sẽ**, dễ chia sẻ và tích hợp vào **Slack, Notion, hoặc CRM**.
✅ **Hoạt động liên tục**: **Không cần can thiệp thủ công**, chạy **24/7** trên VPS.
✅ **Cá nhân hóa**: **Tùy chỉnh prompt** để phù hợp với mục tiêu nghiên cứu cụ thể.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
#### **1. API Keys & Credentials**
| **Dịch vụ**               | **API Key**               | **Mô tả**                                                                 |
|---------------------------|---------------------------|---------------------------------------------------------------------------|
| **OpenRouter**            | `openRouterApi`           | Để sử dụng **GPT-5, Gemini, và các mô hình AI khác**.                   |
| **Serper API**            | `serperApi`               | **Tìm kiếm web thực thời** (thay thế Google Custom Search).               |
| **LegiScan**              | `legiscanApi`             | **Tra cứu luật pháp, dự luật, và hoạt động chính trị**.                 |
| **CourtListener**         | `courtListenerApi`        | **Lấy dữ liệu tòa án liên bang** (tòa án Mỹ).                            |
| **OpenCorporates**        | `openCorporatesApi`       | **Thông tin công ty, cấu trúc tổ chức**.                               |
| **Jina AI**               | `jinaAiApi`               | **Trích xuất văn bản từ URL** (OSINT).                                   |
| **ScrapingDog**           | `scrapingDogApi`          | **Scraping LinkedIn, Twitter, Instagram** (để lấy thông tin cá nhân).   |
| **BuiltWith**             | `builtWithApi`            | **Phân tích công nghệ website** của tổ chức.                            |

#### **2. Các Dịch Vụ Khác**
- **Weaviate** (nếu muốn lưu trữ vector database cho **Open Paws**).
- **Webhook** (để kích hoạt workflow từ bên ngoài).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/12506](https://n8n.io/workflows/12506).
- **Mở n8n Editor** → **Import Workflow** → Chọn file JSON.
- **Hoặc copy/paste** JSON từ file vào **Create Workflow** → **Import JSON**.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này **phức tạp** với **53 node**, nhưng các sếp chỉ cần chú ý đến **các bước sau**:

##### **A. Cấu Hình Credentials (API Keys)**
- **OpenRouter**:
  - Đi đến **Credentials** → **Add New Credentials** → Chọn **OpenRouter API**.
  - Điền **API Key** từ [OpenRouter](https://openrouter.ai/).
  - **Lưu ý**: Các mô hình như **GPT-5** và **Gemini 2.5 Flash** sẽ tự động được chọn trong **keyParameters**.

- **Serper API**:
  - Thêm **Serper API Key** (mặc định dùng cho **Google Search Discovery**).

- **LegiScan**:
  - Thêm **API Key** từ [LegiScan](https://legiscan.com/).
  - **Credentials Type**: `httpQueryAuth`.

- **CourtListener**:
  - Thêm **API Key** từ [CourtListener](https://www.courtlistener.com/api/).
  - **Credentials Type**: `httpHeaderAuth`.

- **OpenCorporates**:
  - Thêm **API Key** từ [OpenCorporates](https://opencorporates.com/api).
  - **Credentials Type**: `httpQueryAuth`.

- **Jina AI**:
  - Thêm **API Key** từ [Jina AI](https://jina.ai/).
  - **Credentials Type**: `jinaAiApi`.

- **ScrapingDog**:
  - Thêm **API Key** từ [ScrapingDog](https://www.scrapingdog.com/).
  - **Credentials Type**: `httpQueryAuth`.

##### **B. Cấu Hình Webhook (Nếu Kích Hoạt Từ Ngoài)**
- Node **"Trigger organization research (Webhook)"** sẽ **chờ đợi request POST** từ bên ngoài.
- **Path**: `/org-osint` (được định nghĩa trong node **webhook**).
- **HTTP Method**: `POST`.
- **Lưu ý**: Nếu không cần kích hoạt từ bên ngoài, có thể **xóa node này** và dùng **Execute Workflow Trigger** thay thế.

##### **C. Cấu Hình Prompt (Nếu Cần Tùy Chỉnh)**
- Node **"Set Prompt"** cho phép **cập nhật lại yêu cầu nghiên cứu** (ví dụ: thay đổi từ "tổ chức sinh vật" sang "tổ chức môi trường").
- **Mở node này** → **Chỉnh sửa JSON** → Thay đổi `prompt` phù hợp.

##### **D. Kiểm Tra Node "If Hallucinations Present"**
- Nếu AI **đưa ra thông tin sai** (hallucination), workflow sẽ **tự động kiểm tra lại** và **sửa chữa**.
- **Không cần can thiệp**, nhưng các sếp nên **monitor log** để đảm bảo AI hoạt động chính xác.

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Gửi **một request mẫu** (ví dụ: `{"organization": "PETA"}`) vào **Webhook**.
  - Kiểm tra **output** xem có **báo cáo Markdown** không.
- **Active Workflow**:
  - Sau khi **test thành công**, chuyển **Active** sang **ON**.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
#### **1. Kết Nối Với Slack/Telegram**
- Thêm **node Slack/Telegram** sau **"Set Report"** để **gửi báo cáo tự động** khi hoàn thành.
- **Cách làm**:
  - Sau node **"Set Report"**, thêm **node Slack Webhook** (nếu dùng Slack).
  - Cấu hình **webhook URL** từ Slack (Settings → Custom Integrations → Incoming Webhooks).

#### **2. Lưu Log & Báo Cáo Định Kỳ**
- Thêm **node Google Sheets** sau **"Set Report"** để **lưu tất cả báo cáo** vào bảng Excel.
- **Cách làm**:
  - Sau node **"Set Report"**, thêm **node Google Sheets**.
  - Chọn **Sheet Name** và **Range** (ví dụ: `Sheet1!A1`).
  - **Lưu ý**: Cần **cấu hình OAuth 2.0** cho Google Sheets.

#### **3. Sử Dụng GPT-5 & Gemini Tối Ưu**
- **GPT-5** được sử dụng cho **những yêu cầu phức tạp** (ví dụ: phân tích sâu về tổ chức).
- **Gemini 2.5 Flash** được dùng cho **những yêu cầu nhanh chóng** (ví dụ: tra cứu nhanh thông tin).
- **Lưu ý**: Nếu **GPT-5 quá đắt**, có thể **thay thế bằng Gemini** trong **keyParameters**.

#### **4. Tối Ưu Hóa Cho OSINT**
- Nếu muốn **scraping thêm LinkedIn/Twitter**, có thể **thêm node ScrapingDog** mới.
- **Ví dụ**:
  - Sau khi **lấy tên tổ chức**, thêm **node LinkedIn Scraper** để **tìm CEO, thành viên**.
  - Sau đó **kết hợp với Jina AI** để **trích xuất thông tin**.

---

### 📌 **Kết Luận: Bắt Đầu Tự Động Hóa Nghiên Cứu AI Hôm Nay!**
Workflow này **không chỉ tiết kiệm thời gian**, mà còn **giảm thiểu sai sót** khi nghiên cứu tổ chức sinh vật và OSINT. Với **AI tiên tiến (GPT-5, Gemini) + 10+ nguồn dữ liệu công khai**, các sếp có thể:
✔ **Nghiên cứu nhanh chóng** mà **không cần code**.
✔ **Xác minh thông tin** một cách **chính xác**.
✔ **Sản sinh báo cáo tự động** để **chia sẻ với ban lãnh đạo**.

**Hành động ngay!**
1. **Import workflow** từ [n8n.io/workflows/12506](https://n8n.io/workflows/12506).
2. **Cấu hình API Keys** theo hướng dẫn trên.
3. **Test với tổ chức mẫu** (ví dụ: "PETA" hoặc "Humane Society").
4. **Active workflow** và **chờ kết quả tự động**!

**🚀 CÓ THỂ CẦN GỢI Ý HOẶC HỖ TRỢ KHÁC?** Hãy để lại **comment** bên dưới hoặc liên hệ **Open Paws** qua [GitHub](https://github.com/Open-Paws/documentation). Chúc các sếp thành công! 🐾