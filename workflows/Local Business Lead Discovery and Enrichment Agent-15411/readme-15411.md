---
title: "🚀 Xây dựng Local Business Lead Discovery & Enrichment Agent tự động với n8n và AI"
description: "Hướng dẫn chi tiết cách tự động tìm kiếm, làm giàu thông tin (enrichment) và chấm điểm khách hàng tiềm năng địa phương bằng n8n, OpenAI GPT-5.1 và Firecrawl."
slug: "local-business-lead-discovery-and-enrichment-agent"
tags: [n8n, automation, ai-agent, lead-generation, postgres, firecrawl]
keywords: [n8n workflow, lead generation, AI Agent, Firecrawl, OpenAI, tự động hóa tìm kiếm khách hàng]
---

# 🚀 Xây dựng Local Business Lead Discovery & Enrichment Agent tự động với n8n và AI

Chào các sếp! Việc tìm kiếm và sàng lọc khách hàng tiềm năng (local leads) thủ công như nha khoa, salon tóc, phòng gym, nhà hàng... thường ngốn rất nhiều thời gian của đội ngũ sales. Các sếp phải tự tay lướt bản đồ, check website từng bên xem có lỗi thời hay không, rồi mới đánh giá xem có nên tiếp cận hay không.

Quá khứ nay đã qua! Trong bài viết này, em sẽ hướng dẫn các sếp triển khai một **AI Agent tự động hoàn toàn** thực hiện toàn bộ quy trình: Tự động tìm kiếm, cào dữ liệu (scrape), đánh giá chất lượng website, chấm điểm cơ hội, lưu trữ vào Database và gửi báo cáo tổng hợp qua Gmail hàng tuần. Không cần code phức tạp, chỉ cần n8n kết hợp sức mạnh của OpenAI và Firecrawl!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7 mà không sợ gián đoạn, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động 100% định kỳ:** Chạy tự động mỗi Thứ Hai hàng tuần (hoặc theo lịch tùy chỉnh) để tìm ra top 10 leads chất lượng nhất.
- **AI thông minh đánh giá:** Tự động phát hiện các doanh nghiệp có website lỗi thời, không chuẩn mobile, hoặc chưa có website để tung chiến dịch tiếp cận chính xác.
- **Lưu trữ đồng bộ:** Tự động loại bỏ trùng lặp (dedup) và lưu trữ toàn bộ thông tin vào cơ sở dữ liệu PostgreSQL (hoặc Supabase).
- **Báo cáo trực quan:** Nhận ngay email tổng hợp danh sách leads mới qua Gmail vào đầu tuần để đội ngũ Sales chốt đơn ngay lập tức.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động trơn tru, các sếp cần chuẩn bị sẵn các tài nguyên sau:
- **n8n Instance:** (Self-hosted hoặc n8n Cloud).
- **OpenAI API Key:** Dành cho các model GPT-5.1 để AI phân tích và chạy Agent.
- **Firecrawl API Key:** Công cụ cực mạnh để search map và scrape website/directory.
- **PostgreSQL Database (hoặc Supabase):** Nơi lưu trữ thông tin leads.
- **Gmail Account / OAuth2:** Để gửi email báo cáo hàng tuần.
:::

---

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow này từ n8n template (link gốc [n8n.io/workflows/15411](https://n8n.io/workflows/15411)), sau đó dán trực tiếp vào n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 20 nodes phối hợp nhịp nhàng. Các sếp cần chú ý cấu hình kỹ các điểm sau:

- **Chuẩn bị Database (PostgreSQL):**
  Trước khi chạy, các sếp cần tạo bảng `marco_leads` trong Database của mình bằng đoạn lệnh SQL được cung cấp sẵn trên canvas:
  ```sql
  CREATE TABLE IF NOT EXISTS marco_leads (
    id BIGSERIAL PRIMARY KEY,
    fingerprint TEXT UNIQUE,
    business_name TEXT NOT NULL,
    category TEXT,
    address TEXT,
    phone TEXT,
    website TEXT,
    public_rating TEXT,
    review_count TEXT,
    website_issues TEXT,
    heuristic_assessment TEXT,
    services_listed TEXT,
    tech_signals TEXT,
    freshness_signal TEXT,
    operating_status TEXT,
    opportunity_score TEXT,
    why_lead TEXT,
    source_links TEXT,
    week_of DATE,
    discovered_at TIMESTAMPTZ
  );
  ```
- **Các node kết nối Credential:**
  - **GPT-5. / GPT-5.1 (`lmChatOpenAi`):** Kết nối API Key OpenAI của các sếp.
  - **Firecrawl Tools (`/search in Firecrawl`, `/scrape in Firecrawl`, v.v.):** Kết nối Firecrawl API Key.
  - **PostgreSQL nodes (`Fetch Seen Fingerprints`, `Postgres — Insert Lead`):** Điền thông tin kết nối database (Host, User, Password, Database Name).
  - **Gmail Node (`Gmail — Send Weekly Summary`):** Xác thực tài khoản Gmail qua OAuth2 và điền địa chỉ email nhận báo cáo.

- **Tinh chỉnh Schedule Trigger:**
  - Mặc định workflow chạy theo lịch hàng tuần (ví dụ: Thứ Hai lúc 9:00 sáng). Các sếp có thể đổi lại thời gian tùy theo nhu cầu thực tế của doanh nghiệp.

#### 3. Kích hoạt ⚡️
- Chạy thử (Test run) thủ công một lần để kiểm tra xem quá trình gọi API Firecrawl và OpenAI có trả về dữ liệu đúng chuẩn hay không.
- Kiểm tra lại dữ liệu đã được ghi vào bảng `marco_leads` chưa.
- Nếu mọi thứ xanh mướt, hãy gạt công tắc sang **Active** để hệ thống tự động chạy ngầm 24/7!

---

### ✍️ Mẹo & gợi ý nâng cao
Để hệ thống tối ưu hóa hơn nữa, các sếp có thể áp dụng các mô hình mở rộng sau:
- **Tích hợp Slack / Telegram:** Thay vì chỉ nhận email qua Gmail, hãy bắn thông báo ngay lập tức lên kênh Telegram hoặc Slack của team sales khi có lead điểm số (Opportunity Score) đạt mức "High".
- **Gửi Email tiếp cận tự động (Cold Outreach):** Nối tiếp workflow này bằng một nhánh tự động soạn thảo email cá nhân hóa dựa trên `website_issues` mà AI đã phân tích để gửi thẳng cho chủ doanh nghiệp.
- **Mở rộng khu vực & ngành hàng:** Dễ dàng thay đổi prompt trong AI Agent để quét các thành phố khác hoặc các ngành nghề kinh doanh khác ngoài nha khoa, salon và nhà hàng.

---

### 📌 Kết luận
Với sự kết hợp đỉnh cao giữa n8n, OpenAI và Firecrawl, việc tìm kiếm khách hàng tiềm năng địa phương nay không còn là gánh nặng thủ công. Hãy triển khai ngay hôm nay để đội ngũ sales của các sếp luôn có nguồn leads chất lượng đều đặn mỗi tuần! Chúc các sếp cài đặt thành công!