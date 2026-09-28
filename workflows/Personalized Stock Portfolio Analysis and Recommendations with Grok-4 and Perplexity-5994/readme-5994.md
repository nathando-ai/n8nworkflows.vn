---
title: "📈 **Tự Động Hóa Phân Tích Cổ Phiếu & Gợi Ý Đầu Tư Cá Nhân Hóa với Grok-4 & Perplexity (AI Agent)**
description: "Workflow tự động hóa hàng ngày phân tích danh mục đầu tư của bạn bằng Grok-4 (xAI) và Perplexity, kết hợp với Google Sheets để cung cấp gợi ý mua/bán/để yên dựa trên tin tức thị trường mới nhất. Giúp các nhà đầu tư tiết kiệm thời gian và đưa ra quyết định thông minh chỉ với 1 email hàng ngày."
slug: "tieu-dong-hoa-phan-tich-co-phieu-grok-4-perplexity"
tags: [n8n, automation, crypto-trading, ai-rag, grok-4, perplexity, google-sheets, gmail]
keywords: [n8n workflow đầu tư, tự động hóa phân tích cổ phiếu, Grok-4 AI, Perplexity AI, đầu tư thông minh, email báo cáo đầu tư hàng ngày]
---

# 🚀 **Tự Động Hóa Phân Tích Cổ Phiếu & Gợi Ý Đầu Tư Cá Nhân Hóa với Grok-4 & Perplexity**

### **Giải pháp cho những nhà đầu tư bận rộn muốn đầu tư thông minh mà không cần đọc hàng chục bài báo thị trường mỗi ngày**
Hàng ngày, các sếp phải mất nhiều thời gian để theo dõi tin tức thị trường, phân tích ảnh hưởng của các sự kiện đến danh mục đầu tư cá nhân. Với **Personalized Stock Portfolio Analysis**, các sếp sẽ nhận được **báo cáo cá nhân hóa hàng ngày** về tình hình thị trường liên quan đến danh mục đầu tư của mình, bao gồm:
- **Tóm tắt tin tức mới nhất** về các cổ phiếu trong danh mục (từ Perplexity).
- **Phân tích ảnh hưởng** của tin tức đó đến giá cổ phiếu (bằng Grok-4).
- **Gợi ý hành động** (mua, bán, giữ) dựa trên logic AI.
- **Email tự động** được gửi vào mỗi sáng, giúp các sếp quyết định đầu tư một cách nhanh chóng và chính xác.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động **24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên một VPS ổn định. N8n.io khuyến nghị sử dụng máy chủ riêng để đảm bảo tính riêng tư và hiệu suất tối ưu.
👉 **[Đăng ký VPS TinoHost - Giảm 39% với mã VPSN8N](https://tino.vn/vps-n8n?affid=388)**
👉 **[VPS Xeon 4GB chỉ 50k/tháng - Tối ưu cho AI](https://my.bnix.one/aff.php?aff=172)**
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không cần theo dõi tin tức thị trường thủ công hàng ngày.
- **Phân tích chuyên nghiệp**: AI Grok-4 kết hợp với Perplexity đưa ra đánh giá khách quan về ảnh hưởng của tin tức đến cổ phiếu.
- **Gợi ý cá nhân hóa**: Nhận **mỗi ngày 1 email** với danh sách gợi ý mua/bán/để yên cho từng cổ phiếu trong danh mục.
- **Hoạt động tự động**: Workflow chạy **mỗi sáng 10h** (có thể điều chỉnh) và gửi báo cáo ngay khi có tin tức mới.
- **Dễ dàng theo dõi**: Dữ liệu đầu vào và đầu ra được lưu trên **Google Sheets**, giúp các sếp theo dõi lịch sử phân tích.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google** (để kết nối **Google Sheets** và **Gmail**).
2. **API Key của Perplexity** (đăng ký tại [Perplexity API](https://www.perplexity.ai/api)).
3. **API Key của xAI (Grok-4)** (đăng ký tại [xAI Developer Portal](https://x.ai/developers)).
4. **Google Sheet mẫu** (sẽ được hướng dẫn cách cấu hình sau).
5. **Tài khoản Gmail** (để nhận email báo cáo hàng ngày).

---
:::note[CHUẨN BỊ GOOGLE SHEETS]
Các sếp cần tạo một **Google Sheet** với **2 tab**:
- **Tab 1: Portfolio** (danh sách cổ phiếu và số lượng sở hữu).
- **Tab 2: Logs** (lưu lịch sử phân tích của AI).
🔗 **Mẫu Google Sheet**: [Tải template](https://docs.google.com/spreadsheets/d/1074dZk-vhwz6LML5zoiwHdxg89Z8u_mgl7wwzqf3A98/edit?usp=sharing)
:::

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ **file JSON** hoặc **copy/paste JSON** vào **n8n Editor**:
- **Tải file JSON** từ [n8n.io/workflows/5994](https://n8n.io/workflows/5994).
- **Cách import**:
  1. Mở **n8n Editor** (trang chủ của workflow).
  2. Nhấn **Import** và chọn file JSON.
  3. Hoặc **copy toàn bộ JSON** và dán vào **Import Workflow** trong n8n.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Sau khi import, các sếp cần **cấu hình chi tiết** các node quan trọng:

##### **A. Schedule Trigger (Điều khiển lịch chạy)**
- **Thời gian mặc định**: 10:00 AM hàng ngày (UTC).
- **Cách chỉnh**:
  - Nhấn **double-click** vào node **Schedule Trigger**.
  - Chọn **Custom** và điều chỉnh thời gian phù hợp với múi giờ của các sếp.

##### **B. Google Sheets (Nguồn dữ liệu danh mục đầu tư)**
- **Credentials**: Chọn **googleSheetsOAuth2Api** (đã cấu hình trước khi import).
- **Sheet Name**: Điền tên **tab "Portfolio"** trong Google Sheet của các sếp.
- **Range**: Điền `Portfolio!A1:Z100` (hoặc điều chỉnh theo số lượng cổ phiếu).

##### **C. Perplexity (Tìm kiếm tin tức thị trường)**
- **Credentials**: Chọn **perplexityApi** (đã thêm API Key trước đó).
- **Query**: Workflow sẽ tự động lấy danh sách cổ phiếu từ Google Sheets và gửi yêu cầu tìm kiếm tin tức cho Perplexity.

##### **D. Grok-4 Stock Analyst Agent (Phân tích AI)**
- **Credentials**: Chọn **xAiApi** (API Key của Grok-4).
- **Model**: Đã mặc định là `grok-4-0709`.
- **Prompt**: Workflow sẽ tự động truyền dữ liệu từ Perplexity và Google Sheets vào Grok-4 để phân tích.

##### **E. Gmail (Gửi báo cáo hàng ngày)**
- **Credentials**: Chọn **gmailOAuth2** (đã cấu hình trước khi import).
- **Email To**: Điền địa chỉ email của các sếp.
- **Subject**: Đã mặc định là **"Daily Stock Portfolio Analysis"** (có thể chỉnh).
- **Body**: Workflow sẽ tự động tạo email với **tóm tắt tin tức + gợi ý đầu tư**.

##### **F. Summary Agent (Tóm tắt kết quả)**
- **Credentials**: Chọn **xAiApi** (API Key Grok-4).
- **Model**: `grok-4-0709`.
- **Prompt**: Workflow sẽ tự động tổng hợp kết quả phân tích thành một email dễ đọc.

---
#### **3. Kích hoạt ⚡️**
1. **Test Run** (để kiểm tra workflow):
   - Nhấn **Run Workflow** và chọn **Test Execution**.
   - Kiểm tra **Gmail** và **Google Sheets** để xác nhận dữ liệu.
2. **Bật Active**:
   - Sau khi test thành công, nhấn **Active** để workflow chạy tự động hàng ngày.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Thêm Slack/Telegram Notification**:
   - Sử dụng **node Slack** hoặc **Telegram Bot** để nhận báo cáo ngay khi có tin tức mới.
   - Cách thêm: Import **node Slack** và kết nối với **webhook** của Slack.

2. **Lưu Log Chi tiết**:
   - Workflow đã lưu dữ liệu vào **Google Sheets (tab "Logs")**, nhưng các sếp có thể thêm **node StickyNote** để lưu log chi tiết hơn.

3. **Tùy chỉnh Thời gian Chạy**:
   - Nếu các sếp muốn workflow chạy vào **giờ khác**, chỉnh **Schedule Trigger** thành **Custom** và chọn thời gian mong muốn.

4. **Kết hợp với Notion/ClickUp**:
   - Thay vì Gmail, các sếp có thể gửi báo cáo vào **Notion** hoặc **ClickUp** bằng **node Notion API** hoặc **ClickUp API**.

5. **Phân tích Cổ Phiếu Ngoài Google Sheets**:
   - Nếu các sếp muốn thêm **danh sách cổ phiếu mới**, chỉ cần **chỉnh sửa Google Sheet** và workflow sẽ tự động cập nhật.

---

### 📌 **Kết luận**
**Workflow này là giải pháp hoàn hảo cho các nhà đầu tư muốn:**
✅ **Tiết kiệm thời gian** (không cần đọc tin tức thủ công).
✅ **Nhận gợi ý đầu tư chính xác** (bằng AI Grok-4 + Perplexity).
✅ **Hoạt động tự động** (email báo cáo hàng ngày).

**Hành động ngay hôm nay!**
1. **Import workflow** và cấu hình theo hướng dẫn.
2. **Test Run** để đảm bảo hoạt động đúng.
3. **Bật Active** và bắt đầu nhận **báo cáo đầu tư thông minh** mỗi sáng!

🔗 **Xem tutorial chi tiết**: [Tutorial trên YouTube](https://youtu.be/OXzsh-Ba-8Y)
🔗 **Mẫu Google Sheet**: [Tải template](https://docs.google.com/spreadsheets/d/1074dZk-vhwz6LML5zoiwHdxg89Z8u_mgl7wwzqf3A98/edit?usp=sharing)

---
**Chúc các sếp thành công với chiến lược đầu tư thông minh!** 🚀💰