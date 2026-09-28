---
title: "🚀 Tự Động Hóa Quảng Cáo Twitter với AI Claude Sonnet + Báo Cáo Google Sheets (Không Cần Code)"
description: "Workflow tự động tìm kiếm tweet liên quan từ Twitter, tạo phản hồi cá nhân hóa bằng AI Claude Sonnet của Anthropic, đăng lên Twitter và lưu báo cáo chi tiết vào Google Sheets. Giúp các sếp tiết kiệm 10+ giờ/tháng, tăng tương tác và theo dõi hiệu quả quảng cáo 24/7."
slug: "tu-dong-hoa-quang-cao-twitter-ai-claude-google-sheets"
tags: [n8n, automation, social-media, ai-claude, google-sheets, twitter-bot, no-code]
keywords: [tự động hóa twitter, ai claude sonnet, quảng cáo tự động, google sheets báo cáo, workflow n8n social media, chatbot twitter]
---

# 🚀 **Tự Động Hóa Quảng Cáo Twitter với AI Claude Sonnet + Báo Cáo Google Sheets**

## **🔥 Nỗi Đau Của Các Sếp?**
Bạn đã bao giờ phải:
- **Tìm kiếm thủ công** tweet liên quan đến keyword của brand trên Twitter?
- **Viết phản hồi** cá nhân hóa cho từng tweet, mất nhiều thời gian và không nhất quán?
- **Theo dõi hiệu quả** của chiến dịch quảng cáo bằng cách ghi chép vào Excel?
- **Bị quên** đăng phản hồi vì bận công việc khác?

**Workflow này giải quyết tất cả!** Với AI Claude Sonnet của Anthropic, n8n sẽ:
✅ **Tự động tìm kiếm** tweet mới liên quan đến keyword của bạn.
✅ **Tạo phản hồi** chuyên nghiệp, cá nhân hóa, và hấp dẫn.
✅ **Đăng phản hồi** lên Twitter tự động.
✅ **Lưu báo cáo** chi tiết vào Google Sheets, bao gồm URL tweet, phản hồi của bạn, và ngày tháng.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tháng**: Không cần phải tìm kiếm, viết và đăng tweet thủ công.
- **Tương tác cao hơn**: Phản hồi cá nhân hóa giúp tăng engagement và brand awareness.
- **Báo cáo minh bạch**: Dữ liệu được tự động lưu vào Google Sheets, dễ theo dõi và phân tích.
- **Hoạt động 24/7**: Workflow chạy tự động theo lịch trình (mỗi 4 giờ), không bỏ lỡ bất kỳ tweet nào.
- **Tăng hiệu quả quảng cáo**: AI Claude Sonnet giúp tạo nội dung hấp dẫn hơn so với con người.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Google** (để kết nối với Google Sheets).
2. **Tài khoản Twitter** (để đăng phản hồi).
3. **Tài khoản Anthropic** (để sử dụng AI Claude Sonnet).
4. **Tài khoản twitterapi.io** (để tìm kiếm tweet).
5. **Google Sheet** (để lưu báo cáo).
6. **Keyword** (từ khóa để tìm tweet liên quan).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/7131](https://n8n.io/workflows/7131) hoặc copy/paste JSON vào **n8n Editor**.
- **Cách import**:
  1. Mở **n8n Workflow Editor**.
  2. Nhấn **Import** và chọn file JSON.
  3. Hoặc nhấn **Create Workflow** → **Import** → Dán JSON.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflows này có **20 node**, nhưng các bước quan trọng nhất cần chú ý:

##### **A. Kết Nối Các Dịch Vụ**
1. **Google Sheets**:
   - Theo [tutorial này](https://www.youtube.com/watch?v=pWGXlZBGu4k) để kết nối tài khoản Google.
   - **Chọn Google Sheet** trong các node `googleSheets` (ví dụ: `Add info to the Report Table`).
   - **Tạo Sheet mới** nếu chưa có (node `Create new sheet`).

2. **Twitter**:
   - Kết nối tài khoản Twitter trong node `Post on Twitter` theo [tutorial này](https://www.youtube.com/watch?v=jxKKwYZQF7Q).
   - **Chú ý**: Node `Twitter Search by Keyword` cần kết nối với **twitterapi.io** (tutorial [đây](https://www.youtube.com/watch?v=lEo7IAgj0UY)).

3. **Anthropic (Claude AI)**:
   - Kết nối tài khoản trong node `Anthropic Chat Model` theo [tutorial này](https://www.youtube.com/watch?v=1jl_vBoVvq0).
   - **Model mặc định**: `claude-sonnet-4-20250514` (có thể thay đổi nếu cần).

4. **TwitterAPI.io**:
   - Đăng ký tài khoản và lấy **API Key** để node `Twitter Search by Keyword` hoạt động.

##### **B. Cấu Hình Cụ Thể**
| **Node** | **Lưu Ý** | **Tham Số Cần Điền** |
|----------|-----------|----------------------|
| **SET KEYWORD** | Đặt từ khóa tìm kiếm tweet (ví dụ: `#marketing`, `#startup`) | `keyword = "#marketing"` |
| **Compose Comment (Agent)** | Thay thế `[PLACEHOLDERS]` bằng thông tin brand của bạn | `brand_name`, `product_name`, `website_link` |
| **Google Sheets (Create new sheet)** | Tạo Sheet mới nếu chưa có | `Sheet Name = "Twitter Promotions - [Month]"` |
| **Define sheet headers** | Xác định cột trong Sheet | `URL`, `Response`, `Date`, `Engagement` |
| **Schedule Trigger** | Chạy mỗi 4 giờ (có thể điều chỉnh) | `cron: 0 */4 * * *` |

##### **C. Test Run & Bật Workflow**
1. **Nhấn "Test Workflow"** để kiểm tra:
   - AI có tạo phản hồi không?
   - Twitter có đăng tweet không?
   - Google Sheets có lưu báo cáo không?
2. **Bật Active** sau khi kiểm tra thành công.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[CÁCH LÀM NGOÀI THƯỜNG]
1. **Tích Hợp Slack/Telegram**:
   - Thêm node `slack` hoặc `telegram` để thông báo khi workflow hoàn thành.
   - Ví dụ: Gửi tin nhắn "Đã đăng phản hồi cho tweet này: [URL]".

2. **Lưu Log Chi Tiết**:
   - Sử dụng node `set` hoặc `stickyNote` để lưu log lỗi/thành công vào Google Sheets.

3. **Báo Cáo Định Kỳ**:
   - Tạo một **Google Sheet tổng hợp** để theo dõi hiệu quả của nhiều keyword.
   - Sử dụng node `googleSheets` với `operation: append` để thêm dữ liệu mới.

4. **Tối Ưu Hóa AI**:
   - Thay đổi **prompt** trong node `Compose Comment` để AI tạo phản hồi phù hợp với giọng điệu brand.
   - Ví dụ: Nếu brand là **hài hước**, thêm: `"Viết phản hồi với giọng điệu hài hước và thân thiện"`.

5. **Lọc Tweet Trùng Lặp**:
   - Sử dụng node `code` để loại bỏ tweet đã phản hồi trước đó (tránh trùng lặp).
   ```javascript
   // Ví dụ mã trong node Code (Split tweets)
   return $input.all().filter(item => !item.alreadyResponded);
   ```
:::

---

### 📌 **Kết Luận**
Workflow này **giúp các sếp tự động hóa toàn bộ quy trình quảng cáo Twitter**, từ tìm kiếm tweet đến đăng phản hồi và báo cáo, **không cần viết một dòng code nào**. Với AI Claude Sonnet, phản hồi của bạn sẽ **cá nhân hóa, chuyên nghiệp và hấp dẫn**, tăng tương tác và hiệu quả cho brand.

**Hành động ngay!**
1. **Import workflow** và kết nối các dịch vụ.
2. **Đặt keyword** và bật **Schedule Trigger**.
3. **Theo dõi kết quả** trên Google Sheets và Twitter.

**🎁 Đăng ký VPS TinoHost để chạy n8n 24/7 (Self-hosted)**
👉 [Đăng ký VPS](https://tino.vn/vps-n8n?affid=388) với mã giảm giá **VPSN8N** (giảm tới 39%).
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).

---
**Chia sẻ workflow này với đồng nghiệp nếu bạn thấy hữu ích!** 🚀