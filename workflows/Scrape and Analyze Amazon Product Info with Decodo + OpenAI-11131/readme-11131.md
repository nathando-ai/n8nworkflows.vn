---
title: "🔍 **Tự Động Hóa Scrape & Phân Tích Thông Tin Sản Phẩm Amazon Với AI (Decodo + OpenAI) - Không Cần Code!**"
description: "Workflow tự động hóa scrape dữ liệu sản phẩm Amazon, phân tích chi tiết bằng AI (GPT-4), và xuất báo cáo tự động vào Google Sheets. Giúp các sếp tiết kiệm thời gian nghiên cứu thị trường, so sánh cạnh tranh và tối ưu chiến lược marketing chỉ với 1 nhấp chuột."
slug: "tieu-dong-hoa-scrape-phan-tich-amazon-ai"
tags: [n8n, automation, market-research, ai-summarization, decodo, openai, google-sheets]
keywords: [tự động hóa scrape amazon, phân tích sản phẩm amazon bằng ai, n8n workflow market research, scrape dữ liệu sản phẩm amazon, tự động hóa nghiên cứu thị trường]
---

# 🚀 **Scrape & Phân Tích Sản Phẩm Amazon Với AI - Cách Tự Động Hóa Nghiên Cứu Thị Trường Mới**

### **Nỗi Đau Của Các Sếp Trong Nghiên Cứu Thị Trường Amazon**
Hàng ngày, các sếp phải:
- **Tốn thời gian** tra cứu thủ công hàng trăm sản phẩm trên Amazon để so sánh giá, đánh giá, và xu hướng.
- **Khó so sánh cạnh tranh** vì thiếu công cụ tự động hóa để tổng hợp và phân tích dữ liệu từ nhiều sản phẩm.
- **Bị mất thông tin quan trọng** trong quá trình ghi chép bằng tay, dẫn đến quyết định không chính xác.
- **Không có báo cáo tự động** để theo dõi xu hướng thị trường, khiến việc điều chỉnh chiến lược marketing trở nên khó khăn.

**Workflow này giải quyết tất cả đó!** Với sự kết hợp giữa **scrape dữ liệu Amazon bằng Decodo** và **phân tích AI bằng OpenAI (GPT-4)**, các sếp có thể:
✅ **Scrape dữ liệu sản phẩm** (giá, đánh giá, mô tả, quảng cáo) chỉ trong vài giây.
✅ **Tự động phân tích** thông tin chi tiết, tóm tắt mô tả sản phẩm, và so sánh cạnh tranh bằng AI.
✅ **Xuất báo cáo tự động** vào Google Sheets, giúp theo dõi và báo cáo định kỳ một cách dễ dàng.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**Lợi Ích Cốt Lõi**]
- **Tiết kiệm thời gian**: Thay vì mất 3-5 tiếng tra cứu thủ công, chỉ cần **1 nhấp chuột** để hoàn thành toàn bộ quá trình.
- **Dữ liệu chính xác và toàn diện**: Scrape **tất cả thông tin** (giá, đánh giá, quảng cáo, mô tả) từ Amazon, không bỏ sót chi tiết nào.
- **Phân tích sâu bằng AI**: AI tự động **tóm tắt mô tả sản phẩm**, **so sánh cạnh tranh**, và **phân tích xu hướng** từ dữ liệu scrape.
- **Báo cáo tự động**: Dữ liệu được xuất vào **Google Sheets** với định dạng sẵn, giúp theo dõi và báo cáo dễ dàng.
- **Hoạt động 24/7**: Workflow chạy tự động trên **n8n self-hosted**, không cần can thiệp thủ công.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[**Chuẩn Bị Trước Khi Bắt Đầu**]
Để workflow hoạt động, các sếp cần chuẩn bị:
1. **Tài khoản Decodo API** (dùng để scrape dữ liệu Amazon):
   - Đăng ký tại: [https://decodo.com/](https://decodo.com/)
   - Lấy **API Key** từ tài khoản Decodo.
2. **Tài khoản OpenAI API** (dùng để phân tích AI):
   - Đăng ký tại: [https://platform.openai.com/](https://platform.openai.com/)
   - Lấy **API Key** từ tài khoản OpenAI.
3. **Tài khoản Google Sheets** (để xuất báo cáo):
   - Một **Google Drive** và **Google Sheets** để lưu kết quả.
4. **n8n Self-Hosted** (không thể chạy trên n8n.cloud):
   - **👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   - **👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đủ mạnh để chạy workflow này).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải workflow JSON** từ [link gốc](https://n8n.io/workflows/11131) hoặc copy toàn bộ JSON từ trang này.
- **Mở n8n Editor** trên VPS đã cài đặt.
- Nhấn **Import Workflow** và dán JSON vào.
- **Kích hoạt workflow** bằng cách bật **Active** ở góc trên bên phải.

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này gồm **15 node**, nhưng có **3 node quan trọng** cần cấu hình kỹ lưỡng:

##### **A. Cấu Hình Credentials (API Keys)**
- **Decodo API**:
  - Đi đến **Credentials** → **Add Credential** → Chọn **"Decodo API"**.
  - Nhập **API Key** từ tài khoản Decodo.
  - **Lưu tên credential** là **"decodoApi"** (phải trùng với tên trong workflow).
- **OpenAI API**:
  - Đi đến **Credentials** → **Add Credential** → Chọn **"OpenAI"**.
  - Nhập **API Key** từ tài khoản OpenAI.
  - **Lưu tên credential** là **"openAiApi"** (phải trùng với tên trong workflow).
- **Google Sheets OAuth2**:
  - Đi đến **Credentials** → **Add Credential** → Chọn **"Google Sheets OAuth2"**.
  - Kết nối với tài khoản Google và chọn **Google Sheet** muốn xuất dữ liệu.
  - **Lưu tên credential** là **"googleSheetsOAuth2Api"** (phải trùng với tên trong workflow).

##### **B. Cấu Hình Node "Set the Input Fields"**
- Node này dùng để **định nghĩa sản phẩm cần scrape**.
- Mở node **"Set the Input Fields"** → Nhấn **Edit** → Điền **URL hoặc ASIN** của sản phẩm Amazon muốn scrape (ví dụ: `https://www.amazon.com/dp/B08XYZ1234`).
- **Lưu ý**: Nếu scrape nhiều sản phẩm, có thể **tạo một danh sách JSON** và truyền vào node này.

##### **C. Cấu Hình Node "OpenAI Chat Model"**
- Workflow sử dụng **GPT-4.1-mini** (mô hình miễn phí của OpenAI).
- **Không cần chỉnh sửa** nếu muốn sử dụng mặc định.
- **Nếu muốn thay đổi mô hình**, mở node **"OpenAI Chat Model"** → Chỉnh sửa tham số `model` thành:
  ```json
  {
    "__rl": true,
    "mode": "list",
    "value": "gpt-4"  // hoặc "gpt-3.5-turbo" nếu muốn tiết kiệm chi phí
  }
  ```

##### **D. Cấu Hình Node "Append or update row in sheet"**
- Node này **xuất dữ liệu vào Google Sheets**.
- Mở node → Chọn **Google Sheet** và **Sheet Name** (phải trùng với tên trong Google Sheets).
- **Lưu ý**:
  - **Cột đầu tiên** phải là **ID sản phẩm** (để tránh trùng lặp).
  - Nếu Sheet đã có dữ liệu, node sẽ **cập nhật** thay vì thêm mới.

#### **3. Kích Hoạt Workflow ⚡️**
- **Test Run**:
  - Nhấn **Execute Workflow** để chạy thử với dữ liệu mẫu.
  - Kiểm tra **Google Sheets** xem dữ liệu có xuất ra không.
- **Bật Active**:
  - Sau khi kiểm tra thành công, **bật Active** để workflow chạy tự động khi kích hoạt.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[**Cách Tối Ưu Hóa Workflow**]
1. **Scrape Nhiều Sản Phẩm Lần Lượt**:
   - Thay vì scrape 1 sản phẩm, có thể **tạo một danh sách JSON** chứa nhiều URL/ASIN và truyền vào node **"Set the Input Fields"** để scrape **tất cả cùng một lúc**.
   - **Ví dụ**:
     ```json
     [
       { "url": "https://www.amazon.com/dp/B08XYZ1234" },
       { "url": "https://www.amazon.com/dp/B09ABC5678" },
       { "url": "https://www.amazon.com/dp/B01DEF9012" }
     ]
     ```

2. **Gửi Báo Cáo Định Kỳ Vào Slack/Email**:
   - Sau khi dữ liệu xuất vào Google Sheets, có thể **kết nối với Slack/Email** để gửi báo cáo tự động.
   - **Cách làm**:
     - Thêm node **Slack Webhook** hoặc **Email Node** sau node **"Aggregate"**.
     - Cấu hình để gửi **báo cáo hàng tuần/tháng**.

3. **Lưu Log Dữ Liệu Cho Phân Tích Sau**:
   - Thêm node **Google Drive** hoặc **Database** (ví dụ: PostgreSQL) để lưu **lịch sử scrape** để phân tích xu hướng dài hạn.

4. **Tùy Chỉnh Prompt AI**:
   - Workflow sử dụng **prompt mặc định** của OpenAI.
   - **Nếu muốn thay đổi cách AI phân tích**, mở node **"Product Insights"** hoặc **"Competitive Analysis"** → Chỉnh sửa **prompt** trong tham số `input`.

5. **Kết Hợp Với Google Trends**:
   - Sau khi scrape dữ liệu, có thể **kết nối với Google Trends API** để so sánh **tendency search** của sản phẩm.

---

### 📌 **Kết Luận: Bắt Đầu Tự Động Hóa Nghiên Cứu Thị Trường Hôm Nay!**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn:
✔ **Tiết kiệm thời gian** trong nghiên cứu thị trường.
✔ **Nhận dữ liệu chính xác** từ Amazon mà không cần scrape thủ công.
✔ **Phân tích sâu bằng AI** để so sánh cạnh tranh và tối ưu chiến lược.
✔ **Xuất báo cáo tự động** vào Google Sheets để theo dõi và báo cáo dễ dàng.

**👉 Hành động ngay!**
1. **Cài đặt n8n trên VPS** (sử dụng mã giảm giá **VPSN8N** để tiết kiệm).
2. **Import workflow** và cấu hình **API Keys**.
3. **Chạy thử** và theo dõi kết quả trong Google Sheets.

**💡 Lời Khuyên Cuối Cùng**:
- **Không chạy trên n8n.cloud** vì sử dụng **node Decodo** (chỉ hỗ trợ self-hosted).
- **Monitor chi phí OpenAI** vì mỗi lần gọi API sẽ tính phí (từ ~0.001 USD/call).
- **Tùy chỉnh prompt AI** để phù hợp với nhu cầu phân tích cụ thể của doanh nghiệp.

**🚀 Chúc các sếp thành công với chiến lược marketing mới!** 🚀