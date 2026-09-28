---
title: "🚀 Tự động tạo nội dung quảng cáo và hình ảnh từ Website với Claude và AI"
description: "Hướng dẫn xây dựng workflow n8n tự động hóa hoàn toàn quy trình phân tích website, đánh giá hình ảnh sản phẩm bằng Claude và tạo creative quảng cáo chuyên nghiệp."
slug: "tu-dong-tao-quang-cao-tu-website-claude-ai"
tags: [n8n, automation, ai-content, claude, openrouter, google-drive]
keywords: [n8n workflow, tạo quảng cáo tự động, claude sonnet 4.5, openrouter, ai marketing, tự động hóa no-code]
---

# 🚀 Tự động tạo nội dung quảng cáo và hình ảnh từ Website với Claude và AI

Các sếp có bao giờ cảm thấy mệt mỏi khi phải tốn hàng giờ nghiên cứu website đối thủ, phân tích sản phẩm, viết copy quảng cáo và nghĩ ý tưởng hình ảnh mỗi khi lên chiến dịch mới? Việc làm thủ công này không chỉốn thời gian mà còn dễ gây cạn kiệt ý tưởng sáng tạo.

Workflow n8n này chính là giải pháp tự động hóa 100% không cần code (No-code) giúp các sếp giải quyết triệt để bài toán trên. Chỉ với một vài thông tin đầu vào đơn giản gồm **Website, Logo và Ảnh sản phẩm**, hệ thống sẽ tự động cào dữ liệu, phân tích thương hiệu bằng AI Claude, lên ý tưởng chiến dịch và xuất ra hình ảnh quảng cáo hoàn chỉnh cùng file lưu trữ trên Google Drive!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa hoàn toàn:** Chuyển đổi URL website và hình ảnh thô thành chiến dịch quảng cáo chỉ trong vài phút.
- **Phân tích sâu sắc:** Sử dụng AI Claude Sonnet 4.5 để thấu hiểu khách hàng, điểm đau, lợi ích sản phẩm và định vị thương hiệu từ nội dung website.
- **Sáng tạo nội dung đa chiều:** Tự động tạo tiêu đề (headline), phụ đề (subheadline), nút kêu gọi hành động (CTA) và hướng dẫn bố cục hình ảnh.
- **Đồng bộ lưu trữ:** Tự động hóa việc xuất file và lưu trữ hình ảnh quảng cáo trực tiếp lên Google Drive cá nhân hoặc doanh nghiệp.
:::

---

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
Để workflow hoạt động mượt mà, các sếp cần chuẩn bị sẵn các tài khoản và API keys sau:
- **Tài khoản Anthropic (Claude API):** Dùng cho các node LangChain Agent và Chat Model phân tích nội dung website và xây dựng chiến lược.
- **Tài khoản OpenRouter:** Dùng cho các node gọi mô hình đánh giá ảnh và tạo hình ảnh quảng cáo (`Call Claude - Photo Evaluation`, `Generate Ad Image`).
- **Tài khoản Google Drive (OAuth2):** Dùng để tự động upload kết quả file hình ảnh quảng cáo (`Upload file`).
:::

---

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
- Tải file JSON của workflow từ nguồn cung cấp hoặc sao chép toàn bộ mã JSON.
- Mở giao diện n8n Editor của các sếp, chọn **Import from File** hoặc dán trực tiếp vào vùng làm việc.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow này gồm 35 nodes được chia thành các cụm chức năng rõ ràng. Các sếp cần cấu hình chính xác các điểm sau:

- **Cụm Form Input (`Form Input`):** 
  - Đây là điểm bắt đầu của workflow dưới dạng biểu mẫu (Form). Khi chạy, hệ thống sẽ yêu cầu nhập `Website` (bắt buộc), tải lên `Logo` (bắt buộc) và `Product photo` (tùy chọn).
- **Cấu hình Credentials cho AI:**
  - Trong tất cả các node **Anthropic Chat Model** (`Anthropic Chat Model`, `Anthropic Chat Model1`, `Anthropic Chat Model2`, `Anthropic Chat Model3`), hãy chọn kết nối **Anthropic API credential** của các sếp.
  - Trong các node **Call Claude - Photo Evaluation** và **Generate Ad Image**, hãy chọn kết nối **OpenRouter API credential**.
- **Cấu hình Google Drive (`Upload file`):**
  - Kết nối tài khoản Google Drive OAuth2 để hệ thống có quyền tạo và tải file lên thư mục chỉ định. Nếu các sếp không muốn xuất file lên Drive, có thể tắt (disable) node này.

#### 3. Kích hoạt ⚡️
- Bấm **Execute Workflow** và điền thử nghiệm thông tin vào Form đầu vào để kiểm tra luồng chạy dữ liệu.
- Sau khi test thành công không báo lỗi, hãy bật công tắc **Active** ở góc trên bên phải để đưa workflow vào trạng thái hoạt động tự động 24/7.

---

### ✍️ Mẹo & gợi ý nâng cao
Để tối ưu hóa hiệu suất làm việc của hệ thống, các sếp có thể mở rộng workflow với các ý tưởng sau:
1. **Tích hợp thông báo:** Thêm node Telegram hoặc Slack ở cuối luồng để gửi trực tiếp hình ảnh và nội dung quảng cáo vừa tạo về group chat ngay khi hoàn tất.
2. **Lưu trữ dữ liệu mở rộng:** Thay vì chỉ lưu Google Drive, kết nối thêm Google Sheets để lưu lại lịch sử các chiến dịch quảng cáo đã tạo theo từng tên website.
3. **Đa dạng hóa kích thước ảnh:** Tùy chỉnh prompt trong node tạo ảnh để tạo ra nhiều định dạng kích thước khác nhau phục vụ cho Facebook, TikTok hoặc Instagram Story.

---

### 📌 Kết luận
Workflow **Generate AI ads from website and images with Claude and NanoBanana** là trợ thủ đắc lực giúp đội ngũ Marketing tiết kiệm 90% thời gian lên ý tưởng ban đầu. Hãy thiết lập ngay hôm nay để tối ưu hóa quy trình sáng tạo nội dung tự động cho doanh nghiệp của các sếp!