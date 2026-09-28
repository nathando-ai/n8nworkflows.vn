---
title: "🚀 **Công cụ Tự động SEO Content với Claude AI, Scrapeless & Phân Tích Thể Hệ - Tiết Kiệm 80% Thời Gian Viết Bài**"
description: "Workflow tự động hóa viết bài SEO cao cấp bằng Claude AI, phân tích xu hướng Google Trends, nghiên cứu nội dung đối thủ và lưu kết quả vào Google Sheets/Supabase - hoàn toàn không cần code. Giúp các sếp tiết kiệm thời gian, tăng hiệu quả SEO và cạnh tranh hiệu quả với đối thủ."
slug: "automated-seo-content-engine-claude-ai-scrapeless"
tags: [n8n, automation, seo, content-creation, ai, claude-ai, scrapeless, google-trends, supabase, google-sheets]
keywords: [n8n workflow seo, tự động hóa viết bài seo, claude ai viết bài, phân tích đối thủ seo, google trends api, supabase n8n, google sheets automation]
---

# 🚀 **Công cụ Tự động SEO Content với Claude AI, Scrapeless & Phân Tích Thể Hệ**

## **💡 Bạn đã từng gặp phải những vấn đề này?**
- **Viết bài SEO mất nhiều thời gian** mà vẫn không chắc chắn về xu hướng tìm kiếm?
- **Không biết đối thủ đang viết gì** và cách cải thiện nội dung của mình?
- **Cần nhiều nguồn dữ liệu** (Google Trends, crawl trang web đối thủ, phân tích từ khóa) nhưng phải làm thủ công?
- **Không có thời gian** để nghiên cứu và viết bài chất lượng cao?

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Phân tích xu hướng tìm kiếm** từ Google Trends
✅ **Crawl và phân tích nội dung** của đối thủ
✅ **Viết bài SEO hoàn chỉnh** bằng Claude AI (Claude Sonnet 4)
✅ **Lưu kết quả** vào Google Sheets hoặc Supabase
✅ **Lọc và ưu tiên** những chủ đề có tiềm năng cao

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để đảm bảo tính riêng tư và hiệu suất cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian** nghiên cứu và viết bài SEO.
- **Nội dung chất lượng cao** do Claude AI viết, phù hợp với xu hướng tìm kiếm.
- **Phân tích đối thủ chi tiết** để cải thiện chiến lược SEO.
- **Hoạt động liên tục** (24/7) mà không cần can thiệp thủ công.
- **Lưu trữ dữ liệu** vào Google Sheets hoặc Supabase để theo dõi và phân tích sau này.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
✔ **Tài khoản Scrapeless API** (để crawl và phân tích Google Trends)
✔ **API Key Anthropic** (để sử dụng Claude AI - Claude Sonnet 4)
✔ **Tài khoản Google Sheets** (để lưu kết quả)
✔ **Tài khoản Supabase** (tùy chọn, để lưu dữ liệu bài viết)

---
:::info[CHUẨN BỊ]
- **Scrapeless API Key**: Đăng ký tại [Scrapeless](https://scrapeless.com/) và thêm vào n8n dưới **Credentials > Scrapeless API**.
- **Anthropic API Key**: Đăng ký tại [Anthropic](https://www.anthropic.com/) và thêm vào n8n dưới **Credentials > Anthropic API**.
- **Google Sheets OAuth2**: Cấu hình OAuth2 trong n8n để truy cập Google Sheets.
- **Supabase API** (nếu sử dụng): Thêm vào **Credentials > Supabase API**.
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/5985](https://n8n.io/workflows/5985) hoặc copy toàn bộ JSON từ trang này.
- Mở **n8n Editor** → Nhấn **Import Workflow** → Dán JSON và nhấn **Import**.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow được chia thành **3 Phase** chính. Dưới đây là hướng dẫn chi tiết cho từng phần:

##### **📌 Phase 1: Hot Topics (Phân tích xu hướng Google Trends)**
- **Node "Google Trends"**: Sử dụng Scrapeless API để lấy dữ liệu xu hướng từ khóa.
  - **Cấu hình**:
    - Chọn **Credentials**: `scrapelessApi`
    - Điền **Keywords** (ví dụ: "tự động hóa n8n", "seo content", "claude ai").
    - **Lưu ý**: Nếu muốn lấy dữ liệu từ file, sử dụng **Set seed keywords** để truyền danh sách từ khóa vào.

- **Node "Structured Output Parser"**: Chuyển đổi dữ liệu thành định dạng dễ đọc.
  - **Không cần chỉnh sửa**, chỉ cần chạy workflow.

##### **📌 Phase 2: Competitive Content Research (Phân tích đối thủ)**
- **Node "Crawl"**: Sử dụng Scrapeless API để crawl trang web đối thủ.
  - **Cấu hình**:
    - Chọn **Credentials**: `scrapelessApi`
    - Điền **URL** của trang web đối thủ (ví dụ: `https://example.com/blog`).
    - **Lưu ý**: Nếu muốn crawl nhiều trang, sử dụng **Filter TOP3 competitor links** để lọc ra 3 liên kết chính.

- **Node "Google Search"**: Tìm kiếm từ khóa liên quan từ Google.
  - **Cấu hình**:
    - Chọn **Credentials**: `scrapelessApi`
    - Điền **Query** (ví dụ: "tự động hóa seo content").

- **Node "AI Agent"**: Sử dụng Claude AI để phân tích và lọc nội dung.
  - **Không cần chỉnh sửa**, AI sẽ tự động xử lý.

- **Node "Filter out topics with priority above P2"**: Lọc ra những chủ đề có ưu tiên cao.
  - **Cấu hình**:
    - Đặt **Priority** (ví dụ: `P1`, `P2`, `P3`) để lọc chủ đề phù hợp.

##### **📌 Phase 3: Complete SEO Article Writing (Viết bài SEO)**
- **Node "Senior SEO content writer"**: Claude AI viết bài SEO hoàn chỉnh.
  - **Không cần chỉnh sửa**, AI sẽ tự động tạo nội dung dựa trên dữ liệu đầu vào.
  - **Lưu ý**: Nếu muốn thay đổi **Prompt**, chỉnh sửa trong **Anthropic Chat Model** (Claude Sonnet 4).

- **Node "Append or update row in sheet"**: Lưu kết quả vào Google Sheets.
  - **Cấu hình**:
    - Chọn **Credentials**: `googleSheetsOAuth2Api`
    - Chọn **Sheet Name** và **Range** (ví dụ: `Sheet1!A1`).
    - **Lưu ý**: Đảm bảo **Google Sheets OAuth2** đã được cấu hình đúng.

- **Node "Create a row" (Supabase)**: Lưu dữ liệu vào Supabase (nếu sử dụng).
  - **Cấu hình**:
    - Chọn **Credentials**: `supabaseApi`
    - Chọn **Table Name** và **Columns** cần lưu.

---

#### **3. Kích hoạt ⚡️**
- **Test Run**: Nhấn **Execute Workflow** để chạy thử với dữ liệu mẫu.
- **Bật Active**: Sau khi kiểm tra, nhấn **Active** để workflow chạy tự động khi kích hoạt.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tối ưu từ khóa**: Thêm **Set seed keywords** để tự động lấy danh sách từ khóa từ Google Sheets hoặc một nguồn khác.
2. **Lưu log hoạt động**: Sử dụng **Sticky Note** để ghi chú và theo dõi quá trình.
3. **Gửi báo cáo định kỳ**: Kết hợp với **Slack/Telegram** để thông báo kết quả.
4. **Cập nhật thường xuyên**: Để workflow luôn lấy dữ liệu mới nhất, **cập nhật API Key** và **tài khoản OAuth2** định kỳ.

---
### 📌 **Kết luận**
Workflow này là **công cụ tự động hóa SEO hoàn chỉnh**, giúp các sếp:
✔ **Tiết kiệm thời gian** viết bài và nghiên cứu.
✔ **Nội dung chất lượng cao** do AI viết.
✔ **Phân tích đối thủ** để cải thiện chiến lược.
✔ **Lưu trữ dữ liệu** để theo dõi và phân tích sau này.

**Hãy áp dụng ngay để cạnh tranh hiệu quả trên thị trường!** 🚀

---
:::note[Lưu ý cuối cùng]
- **Không cần kỹ năng code** để sử dụng workflow này.
- **Cập nhật thường xuyên** để tránh lỗi API.
- **Nếu gặp vấn đề**, tham khảo [hỗ trợ n8n](https://n8n.io/support) hoặc liên hệ Scrapeless.
:::

---
**Bắt đầu tự động hóa SEO của bạn ngay hôm nay!** 💻✨