---
title: "🚀 Tự Động Hái Leads Kinh Doanh Từ Google Maps Với AI OpenAI & Google Sheets (Không Cần Code)"
description: "Workflow tự động hóa thu thập thông tin khách hàng tiềm năng từ Google Maps, phân tích bằng AI OpenAI và lưu trữ vào Google Sheets - tiết kiệm 10+ giờ công mỗi tuần cho các sếp bán hàng."
slug: "tieu-dong-ha-leads-google-maps-ai-openai"
tags: [n8n, automation, sales, ai, google-maps, google-sheets, openai, no-code]
keywords: [tự động hóa n8n, thu thập leads google maps, ai openai, google sheets automation, tự động hóa bán hàng, workflow n8n sales]
---

# 🚀 **Tự Động Hái Leads Kinh Doanh Từ Google Maps Với AI OpenAI & Google Sheets**

### **Nỗi Đau Của Các Sếp Bán Hàng**
Hằng ngày, các sếp phải:
- **Tìm kiếm thủ công** trên Google Maps để tìm khách hàng tiềm năng (công ty, cửa hàng, dịch vụ).
- **Lọc thông tin** từ trang web, số điện thoại, email, và mô tả để đánh giá tiềm năng.
- **Ghi chép lại** vào Google Sheets hoặc CRM - công việc mệt mỏi và dễ sai sót.
- **Mất thời gian** lên đến **10+ giờ/tuần** cho việc này.

**Workflow này giải quyết tất cả!** Sử dụng **AI OpenAI** để phân tích thông tin từ Google Maps, **tự động lưu trữ** vào Google Sheets với định dạng chuyên nghiệp - giúp các sếp **tích cực hơn trong bán hàng** mà không cần viết một dòng code nào.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow hoạt động **24/7** và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS chuyên dụng:
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (ổn định, tốc độ cao)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm 10+ giờ/tuần** - Không cần tìm kiếm thủ công trên Google Maps.
✅ **Dữ liệu chính xác & tự động hóa** - AI OpenAI phân tích và tổng hợp thông tin chi tiết (địa chỉ, số điện thoại, mô tả, tiềm năng kinh doanh).
✅ **Lưu trữ sạch sẽ vào Google Sheets** - Dữ liệu được định dạng theo cột: Tên Công Ty, Địa chỉ, Số Điện Thoại, Mô Tả, Đánh Giá Tiềm Năng.
✅ **Hoạt động liên tục 24/7** - Workflow chạy tự động mỗi khi có cập nhật mới.
✅ **Cá nhân hóa & mở rộng** - Dễ dàng kết nối với Slack/Telegram để báo cáo kết quả.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
📌 **Tài khoản Google** (để truy cập Google Maps & Google Sheets).
📌 **API Key OpenAI** (đăng ký tại [OpenAI](https://platform.openai.com/)).
📌 **Google Sheets** (một bảng mới để lưu trữ leads).
📌 **N8n Self-hosted** (để workflow chạy ổn định).

---
### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể:
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/3443) và import vào **n8n Editor**.
- **Copy/Paste JSON** từ file vào **Create Workflow** trong n8n.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này sử dụng **các node chính sau** (các sếp phải cấu hình kỹ lưỡng):

##### **A. Node `n8n-nodes-base.httpRequest` (Lấy dữ liệu từ Google Maps)**
- **URL**: `https://www.google.com/maps/search/{keyword}` (ví dụ: `cửa hàng café Hà Nội`).
- **Headers**: Thêm `User-Agent` để tránh bị chặn (ví dụ: `Mozilla/5.0`).
- **Lưu ý**: Các sếp cần **xác định keyword** phù hợp với ngành nghề (ví dụ: "công ty xây dựng TP.HCM").

##### **B. Node `@n8n/n8n-nodes-langchain.toolSerpApi` (Trích xuất dữ liệu từ trang web)**
- **API Key**: Đăng ký tại [SerpAPI](https://serpapi.com/) (miễn phí cho thử nghiệm).
- **Query**: Cấu hình để trích xuất **tên công ty, địa chỉ, số điện thoại, mô tả**.

##### **C. Node `@n8n/n8n-nodes-langchain.lmChatOpenAi` (Phân tích AI)**
- **Model**: Chọn `gpt-3.5-turbo` (hoặc `gpt-4` nếu có budget).
- **Prompt**: Cấu hình để AI **đánh giá tiềm năng kinh doanh** (ví dụ: "Nếu tôi là doanh nhân, công ty này có tiềm năng không?").
- **API Key OpenAI**: Điền vào **Credentials** trong n8n.

##### **D. Node `n8n-nodes-base.googleSheets` (Lưu trữ vào Google Sheets)**
- **Credentials**: Kết nối Google Sheets với n8n (cách hướng dẫn [đây](https://docs.n8n.io/integrations/builtins/googleSheets/)).
- **Sheet Name**: Chọn bảng đã tạo trước đó.
- **Range**: Điền `Sheet1!A1` (hoặc tên cột phù hợp).

##### **E. Node `@n8n/n8n-nodes-langchain.memoryBufferWindow` (Lưu trữ lịch sử)**
- **Buffer Size**: 100 (để lưu trữ 100 lead gần nhất).
- **Lưu ý**: Node này giúp **tránh trùng lặp** và **tối ưu hóa AI**.

#### **3. Kích Hoạt ⚡️**
- **Test Run**: Chạy với **dữ liệu mẫu** (ví dụ: keyword "cửa hàng điện máy TP.HCM").
- **Active Workflow**: Sau khi kiểm tra thành công, **bật Active**.

---
### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết nối với Slack/Telegram** để nhận **báo cáo tự động** khi có lead mới.
   ```yaml
   - Node: `n8n-nodes-base.slack` (gửi thông báo khi có lead mới).
   ```
2. **Lưu log vào Google Drive** để theo dõi hoạt động của workflow.
3. **Tự động gửi email** (với node `n8n-nodes-base.email`) cho team khi có lead mới.
4. **Mở rộng keyword** bằng **Google Trends API** để tìm ra **ngành nghề hot nhất** trong khu vực.

---
### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp bán hàng, giúp họ **tích cực hơn trong bán hàng** mà không cần viết code. **Hãy tự động hóa ngay hôm nay!**

👉 **Bắt đầu với n8n Self-hosted** trên VPS để workflow **chạy 24/7** mà không bị gián đoạn.
👉 **Khám phá thêm workflow tự động hóa khác** tại [n8n.io](https://n8n.io/).

**Cảm ơn các sếp đã đọc đến đây!** 🚀 Chúc các sếp thành công với việc tự động hóa!