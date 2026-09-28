---
title: "🏠 **Tự Động Học Đánh Giá Đầu Tư Bất Động Sản với Claude AI, Google Sheets & Slack** – Không Cần Code!"
description: "Workflow tự động hóa đánh giá đầu tư bất động sản thông minh bằng AI Claude (Anthropic), tích hợp dữ liệu thị trường, dân số và dự đoán khả năng sinh lời. Giúp các sếp tiết kiệm 10+ giờ/ngày so sánh thủ công, lọc ra những cơ hội đầu tư ưu tiên với độ chính xác cao."
slug: "tieu-dong-hoa-danh-gia-dau-tu-bat-dong-san-voi-claude-ai"
tags: [n8n, automation, ai-claude, google-sheets, slack-integration, market-research, no-code]
keywords: [tự động hóa đầu tư bất động sản, Claude AI đánh giá nhà đất, n8n workflow bất động sản, tự động hóa phân tích thị trường bất động sản, AI đầu tư bất động sản không code]
---

# 🚀 **Tự Động Học Đánh Giá Đầu Tư Bất Động Sản – Từ Scrape Dữ Liệu Đến Top Picks AI**

### **Nỗi Đau Của Các Sếp Trong Thị Trường Bất Động Sản**
Mỗi ngày, các sếp phải:
- **Tốn 5-10 giờ** so sánh hàng trăm danh sách nhà đất thủ công trên Domain, Zillow, hoặc các trang web địa phương.
- **Không có tiêu chí khách quan** để lọc ra những cơ hội đầu tư "hàng đầu" giữa hàng ngàn lựa chọn.
- **Phải nhớ ghi chép** dữ liệu thị trường (giá trung bình, tỷ lệ thuê, dân số) vào Excel, dễ bị lỗi hoặc quên.
- **Không biết đâu là "điểm nóng"** – có thể là khu vực mới phát triển, nhưng thiếu dữ liệu về cơ sở hạ tầng hoặc nguy cơ môi trường.

**Workflow này giải quyết tất cả!** Nó tự động:
✅ **Scrape** tất cả danh sách nhà đất từ URL bạn chỉ định.
✅ **Tích hợp** dữ liệu thị trường (giá, thuê, dân số, cơ sở hạ tầng) từ API.
✅ **Sử dụng AI Claude** để đánh giá mỗi nhà đất từ 0-100 điểm dựa trên **5 tiêu chí chuyên nghiệp**:
   - Tỷ lệ thuê (rental yield)
   - Xu hướng tăng giá (capital growth)
   - Điểm số khu vực (transport, trường học, tiện ích)
   - Nguy cơ trống nhà (vacancy risk)
   - Lợi nhuận sau thuế (cash flow)
✅ **Lọc ra top 5-10 nhà đất** ưu tiên và gửi **báo cáo định kỳ** lên Slack/Google Sheets.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/ngày** so sánh thủ công → **tăng hiệu suất 300%**.
- **Đánh giá khách quan** dựa trên AI + dữ liệu thị trường thực tế (không dựa vào cảm nhận cá nhân).
- **Top picks tự động** – không phải mất công lọc hàng trăm danh sách.
- **Lịch sử đầu tư** được lưu trữ trên Google Sheets, dễ theo dõi và phân tích dài hạn.
- **Báo cáo Slack hàng ngày** – không bỏ lỡ cơ hội mới.
- **Cập nhật liên tục** – workflow chạy tự động hàng ngày (hoặc theo lịch bạn thiết lập).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản Anthropic API** (để sử dụng Claude AI):
   - Đăng ký tại [Anthropic Developer Portal](https://www.anthropic.com/api) và lấy **API Key**.
   - **Mã giảm giá**: Sử dụng mã `N8NAI` để giảm 20% phí đầu tiên (nếu có).
   :::

2. **Tài khoản Google Sheets**:
   - Tạo một **Google Sheet mới** để lưu trữ lịch sử đánh giá (cấu trúc sẽ được tự động tạo khi chạy workflow đầu tiên).
   - **Chia sẻ với n8n** bằng cách cấp quyền "Editor" cho email liên kết với n8n của bạn.

3. **Tài khoản Slack** (nếu muốn nhận báo cáo hàng ngày):
   - Tạo một **app Slack** và lấy **OAuth Token** từ [Slack API](https://api.slack.com/apps).
   - Chọn **channel** hoặc **DM** để nhận báo cáo.

4. **API Key cho dữ liệu thị trường** (lựa chọn một trong các dịch vụ sau):
   - **RapidAPI** (ví dụ: [Zillow API](https://rapidapi.com/apidojo/api/zillow/), [Domain API](https://rapidapi.com/apidojo/api/domain/))
   - **Zillow API** (nếu làm việc ở Mỹ/Australia)
   - **Domain API** (nếu làm việc ở Việt Nam/Australia)
   - **Ghi chú**: Nếu không muốn mua API, workflow vẫn chạy được với dữ liệu scrape từ trang web công khai (nhưng hiệu quả thấp hơn).

5. **URL danh sách nhà đất** (ví dụ):
   - `https://www.domain.com.au/sale/sydney/?bedrooms=2-4&price=500000-900000`
   - Các sếp có thể scrape từ **Domain, Sotheby’s, Century 21**, hoặc các trang web địa phương.

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Cách 1**: Tải file JSON từ [n8n.io/workflows/13686](https://n8n.io/workflows/13686) và import vào n8n Editor.
- **Cách 2**: Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/13686/export) và paste vào **Import Workflow** trong n8n.
- **Cách 3**: Sử dụng **n8n CLI** (nếu tự host):
   ```bash
   n8n import workflow.json --name "PropertyInvestmentScorer"
   ```

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow có **17 node**, nhưng chỉ có **5 node quan trọng** cần cấu hình kỹ lưỡng:

##### **A. Node "Claude AI Model" (lmChatAnthropic)**
- **Tham số cần thiết**:
  - **Credentials**: Chọn `anthropicApi` (đã tạo ở bước chuẩn bị).
  - **Model**: Đặt `claude-sonnet-4-20250514` (mặc định).
  - **Prompt**: Workflow đã tự động cấu hình, **không cần chỉnh sửa** (nếu muốn tối ưu, có thể thêm tiêu chí cá nhân vào node "Score Investment with Claude AI").

##### **B. Node "Save All Scored Listings to Sheets" (googleSheets)**
- **Tham số cần thiết**:
  - **Credentials**: Chọn `googleApi` (đã tạo ở bước chuẩn bị).
  - **Sheet ID**: Lấy từ URL của Google Sheet bạn tạo (ví dụ: `1AbCdEfGhIjKlMnOpQrStUvWxYz`).
  - **Sheet Name**: Đặt tên mặc định là **"PropertyInvestmentScores"** (nếu muốn khác, chỉnh ở node này).
  - **Operation**: Đặt `append` (thêm dữ liệu mới vào cuối sheet).

##### **C. Node "Send Top Picks Digest to Slack" (httpRequest)**
- **Tham số cần thiết**:
  - **Credentials**: Chọn `slackApi` (đã tạo ở bước chuẩn bị).
  - **URL**: Workflow tự động cấu hình, **không cần chỉnh**.
  - **Payload**: Nội dung báo cáo sẽ tự động format, **không cần chỉnh** (nếu muốn thay đổi format, chỉnh ở node "Format Investment Report").

##### **D. Node "Configure Scrape Targets" (set)**
- **Tham số cần thiết**:
  - **searchUrl**: Điền URL danh sách nhà đất bạn muốn scrape (ví dụ: `https://www.domain.com.au/sale/sydney/`).
  - **suburb**: Nếu scrape khu vực cụ thể, điền tên (ví dụ: `Parramatta`).
  - **maxListings**: Số lượng danh sách scrape (mặc định 20, có thể tăng lên 50-100 nếu cần).

##### **E. Node "Filter Top Picks by Score" (filter)**
- **Tham số cần thiết**:
  - **Score Threshold**: Đặt điểm tối thiểu để lọc top picks (mặc định 65, có thể tăng lên 70-80 nếu muốn chọn lọc chặt).

#### **3. Kích Hoạt ⚡️**
- **Test Run**:
  - Chạy **Manual Execution** với dữ liệu mẫu (ví dụ: gõ vào node "Return Final Report" và gửi payload mẫu từ [đây](https://github.com/OneclickAI-Squad/n8n-workflows/blob/main/property-investment-scorer/README.md#sample-webhook-payload)).
  - Kiểm tra:
    - Dữ liệu scrape có đúng không?
    - AI Claude có đánh giá điểm không?
    - Top picks có xuất hiện trên Slack/Google Sheets không?
- **Bật Active**:
  - Sau khi test thành công, **bật Active** workflow và chọn **Daily Schedule Trigger** (hoặc chỉnh lịch theo nhu cầu).

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[TIẾP CẬN HƠN]
1. **Thêm Email Notification**:
   - Sử dụng node **n8n-nodes-base.email** để gửi báo cáo hàng ngày qua email thay vì Slack.
   - Cấu hình tại node "Send Top Picks Digest to Slack" bằng **SMTP** (ví dụ: Gmail, SendGrid).

2. **Lưu Log Dữ Liệu**:
   - Thêm node **n8n-nodes-base.log** sau node "Save All Scored Listings to Sheets" để theo dõi lỗi và debug.

3. **Tích Hợp với Notion**:
   - Thay vì Google Sheets, sử dụng **Notion API** để lưu trữ dữ liệu với giao diện đẹp hơn.
   - Cài node **n8n-nodes-base.notion** và cấu hình tương tự như Google Sheets.

4. **Tối Ưu AI Claude**:
   - Nếu muốn Claude AI **phân tích sâu hơn**, chỉnh sửa node "Score Investment with Claude AI" bằng **LangChain Prompt**:
     ```json
     {
       "prompt": "Analyze this property listing {{$json.data}} and provide a detailed SWOT analysis with risk factors. Use the following criteria: rental yield, capital growth, location score, vacancy risk, and cash flow. Rate from 0-100."
     }
     ```

5. **Scrape Nhiều URL**:
   - Sử dụng node **n8n-nodes-base.loop** để scrape từ **nhiều URL khác nhau** (ví dụ: Sydney, Melbourne, Brisbane).

6. **Báo Cáo Hàng Tháng**:
   - Thêm node **n8n-nodes-base.scheduleTrigger** với lịch **monthly** để gửi báo cáo tổng hợp.
---

### 📌 **Kết Luận**
Workflow này **không chỉ là một công cụ tự động hóa**, mà là **công cụ phân tích đầu tư bất động sản thông minh** giúp các sếp:
✔ **Tiết kiệm thời gian** và tập trung vào chiến lược đầu tư.
✔ **Nhận quyết định dựa trên dữ liệu** thay vì cảm nhận.
✔ **Không bỏ lỡ cơ hội** nhờ báo cáo Slack/email hàng ngày.

**Hành động ngay!**
1. **Chuẩn bị tài khoản** (Anthropic, Google Sheets, Slack).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Bật Active** và bắt đầu nhận **top picks đầu tư tự động**!

---
:::note[LƯU Ý CUỐI CUNG]
- **N8n Self-Hosted**: Để workflow chạy **24/7** mà không bị giới hạn, các sếp nên **tự host n8n** trên VPS.
  👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
  👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).
- **Cập Nhật Dữ Liệu**: Nếu API scrape bị thay đổi, các sếp cần **cập nhật node "Scrape Property Listings"** bằng cách kiểm tra HTML của trang web.
- **Mở rộng**: Workflow này có thể **tích hợp với nhiều API khác** (ví dụ: **CoreLogic, REA Group**) để lấy dữ liệu chi tiết hơn.
:::

---
**Chúc các sếp thành công với đầu tư bất động sản thông minh!** 🚀🏠