---
title: "🔍 Tự Động Hoàn Thành Nghiên Cứu Khách Hàng Mới Với Perplexity AI + OpenAI & Lưu Trữ Trên Google Sheets"
description: "Workflow tự động hóa nghiên cứu khách hàng tiềm năng từ Perplexity AI, tổng hợp thông tin bằng OpenAI, và lưu kết quả vào Google Sheets - tiết kiệm thời gian lên đến 80% cho bộ phận kinh doanh. Đơn giản, chính xác và hoạt động 24/7."
slug: "tieu-dong-hoan-thanh-nghien-cuu-khach-hang-perplexity-openai-google-sheets"
tags: [n8n, automation, no-code, ai-summarization, google-sheets, openai, perplexity-ai]
keywords: [tự động hóa nghiên cứu khách hàng, n8n workflow, ai tổng hợp thông tin, google sheets tự động, perplexity api, openai chatbot, tự động hóa kinh doanh]
---

# 🚀 **Tự Động Hoàn Thành Nghiên Cứu Khách Hàng Mới Với AI (Perplexity + OpenAI) & Lưu Trữ Trên Google Sheets**

### **Giải pháp cho các sếp kinh doanh:**
Bạn đã bao giờ phải mất **giờ đồng hồ** để nghiên cứu thông tin khách hàng mới từ nhiều nguồn khác nhau, sau đó tổng hợp và lưu vào bảng tính? Hay phải lo lắng rằng thông tin thu thập không đầy đủ hoặc không chính xác? **Workflow này sẽ tự động hóa toàn bộ quy trình** cho bạn - từ tìm kiếm thông tin trên Perplexity AI, phân tích bằng OpenAI, đến lưu kết quả vào Google Sheets - **không cần viết một dòng code nào!**

:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động **ổn định 24/7** và không bị gián đoạn, các sếp nên cài đặt n8n trên **VPS riêng** (Self-hosted) thay vì dùng phiên bản cloud.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (Đảm bảo tốc độ cao, phù hợp với AI)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian lên đến 80%** - Không cần thủ công nhập liệu hoặc tìm kiếm thông tin.
✅ **Tính chính xác cao** - AI tự động phân tích và tổng hợp thông tin từ nhiều nguồn.
✅ **Cập nhật liên tục** - Workflow hoạt động **24/7**, không phụ thuộc vào giờ làm việc.
✅ **Dữ liệu sạch và cấu trúc** - Thông tin khách hàng được lưu vào Google Sheets với định dạng chuẩn.
✅ **Cá nhân hóa** - Dễ dàng mở rộng cho nhiều ngành nghề (dịch vụ, bán lẻ, công nghệ...).
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản Google** (để kết nối với Google Sheets).
2. **API Key của Perplexity AI** (để nghiên cứu thông tin).
3. **API Key của OpenAI** (để phân tích và tổng hợp dữ liệu).
4. **Bảng Google Sheets** (để lưu kết quả - có thể sử dụng mẫu từ [đây](https://docs.google.com/spreadsheets/d/1MnaU8hSi8PleDNVcNnyJ5CgmDYJSUTsr7X5HIwa-MLk/edit#gid=0)).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/8229](https://n8n.io/workflows/8229) và import vào n8n Editor.
- **Cách 2:** Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/8229) và dán vào **Import Workflow** trong n8n.

#### **2. Các bước cấu hình bắt buộc 📌**
Workflow này gồm **13 node** chính, nhưng các sếp chỉ cần chú ý đến **5 node quan trọng** sau:

##### **A. Cấu hình Credentials (Tài khoản API)**
1. **Google Sheets (OAuth2)**
   - Đi đến **Credentials → New → Google Sheets (OAuth2)**.
   - Đăng nhập tài khoản Google và **cho phép quyền truy cập**.
   - Trong **Google Sheets node**, chọn **Spreadsheet** và **Worksheet** muốn lưu kết quả (sử dụng mẫu từ [đây](https://docs.google.com/spreadsheets/d/1MnaU8hSi8PleDNVcNnyJ5CgmDYJSUTsr7X5HIwa-MLk/edit#gid=0)).

2. **Perplexity API**
   - Đăng ký API Key tại [Perplexity Docs](https://docs.perplexity.ai/guides/getting-started).
   - Đi đến **Credentials → New → Perplexity API** và dán API Key vào.

3. **OpenAI API**
   - Đăng ký API Key tại [OpenAI Platform](https://platform.openai.com/account/api-keys).
   - Đi đến **Credentials → New → OpenAI API** và dán API Key vào.
   - Trong **node "OpenAI Chat Model"**, chọn **model `gpt-4.1-mini`** (hoặc `gpt-4o-mini` nếu muốn sử dụng phiên bản mới nhất).

##### **B. Cấu hình các node chính**
1. **Node "Get Current Leads" (Lấy danh sách khách hàng hiện có)**
   - Chọn **Google Sheets** đã cấu hình và **Worksheet** chứa dữ liệu khách hàng.
   - **Lưu ý:** Cột đầu tiên phải là **ID hoặc tên khách hàng** để workflow phân biệt.

2. **Node "Research Leads" (Nghiên cứu thông tin khách hàng)**
   - Chọn **Perplexity API** đã cấu hình và **model `sonar`**.
   - **Prompt mặc định** đã được thiết lập, nhưng các sếp có thể **cập nhật** nếu cần thông tin cụ thể hơn (ví dụ: "Tìm thông tin về công ty [Tên Công Ty] trong ngành [Ngành Nghề]").

3. **Node "OpenAI Chat Model" (Tổng hợp thông tin)**
   - Chọn **OpenAI API** và **model `gpt-4.1-mini`**.
   - **Lưu ý:** Nếu muốn kết quả chi tiết hơn, có thể thay đổi **prompt** trong node này.

4. **Node "Send Leads to Google Sheets" (Lưu kết quả)**
   - Chọn **Google Sheets** cùng với **Worksheet** để lưu kết quả.
   - **Operation:** Chọn **appendOrUpdate** để thêm hoặc cập nhật dữ liệu.

#### **3. Kích hoạt ⚡️**
- **Test Run:** Chọn **Run Workflow** và kiểm tra kết quả trong Google Sheets.
- **Bật Active:** Sau khi kiểm tra thành công, **bật Active** để workflow chạy tự động khi có dữ liệu mới.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Tự động hóa định kỳ**
   - Sử dụng **node "Schedule"** để chạy workflow hàng ngày/tuần (ví dụ: nghiên cứu khách hàng mới vào mỗi sáng 8h).

2. **Gửi báo cáo qua Email/Slack**
   - Kết nối với **Gmail** hoặc **Slack** để nhận thông báo khi có dữ liệu mới được cập nhật.

3. **Lưu log hoạt động**
   - Sử dụng **node "Set"** để lưu thông tin debug vào Google Sheets hoặc **Google Drive** để theo dõi lỗi.

4. **Mở rộng cho nhiều ngành nghề**
   - Cập nhật **prompt** trong node Perplexity/OpenAI để phù hợp với ngành nghề cụ thể (ví dụ: nghiên cứu khách hàng trong ngành **bán lẻ**, **dịch vụ**, **công nghệ**).

5. **Sử dụng AI Vision (nếu cần)**
   - Nếu muốn phân tích **hình ảnh** (ví dụ: logo công ty), thay đổi model OpenAI thành **`gpt-4o`** (có khả năng xử lý vision).

---

### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp kinh doanh để tập trung vào **quyết định chiến lược** thay vì làm thủ công. Bằng cách kết hợp **Perplexity AI** (nghiên cứu thông tin), **OpenAI** (tổng hợp và phân tích), và **Google Sheets** (lưu trữ), bạn có một **hệ thống tự động hóa hoàn chỉnh** chỉ với **một lần cấu hình**.

**Hành động ngay!**
1. **Cài đặt n8n trên VPS** (để workflow hoạt động 24/7).
2. **Import workflow** và cấu hình credentials.
3. **Test Run** và bật **Active** để bắt đầu tự động hóa!

**Nếu có vấn đề**, các sếp có thể liên hệ với tác giả **Robert Breen** qua:
📧 [rbreen@ynteractive.com](mailto:rbreen@ynteractive.com)
🔗 [LinkedIn](https://www.linkedin.com/in/robert-breen-29429625/)
🌐 [ynteractive.com](https://ynteractive.com)

**Chúc các sếp thành công với quy trình tự động hóa mới!** 🚀