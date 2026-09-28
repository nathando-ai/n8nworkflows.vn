---
title: "🛡️ Tự Động Phân Tích URL Phishing & Threat Intelligence với NixGuard AI (N8n)"
description: "Workflow tự động hóa phân tích URL phishing và nhận diện mối đe dọa thực thời bằng NixGuard AI + Wazuh, giúp các sếp SOC/IR nhanh chóng nhận diện và phản ứng trước các mối nguy hiểm mạng. Kết quả: Tiết kiệm 80% thời gian phân tích thủ công, giảm thiểu lỗ hổng an ninh."
slug: "tự-dộng-phân-tích-url-phishing-threat-intelligence-nixguard"
tags: [n8n, automation, secops, ai-summarization, cybersecurity, threat-intelligence, wazuh, soar]
keywords: [n8n workflow phân tích URL phishing, tự động hóa SOC, NixGuard AI, Wazuh integration, threat intelligence automation, tự động hóa an ninh mạng]
---

# 🚀 **Tự Động Phân Tích URL Phishing & Threat Intelligence với NixGuard AI**

### **Nỗi Đau Của Các Sếp SOC/IR**
Hàng ngày, các đội ngũ an ninh mạng phải thủ công:
✅ **Tra cứu URL phishing** trên nhiều nguồn dữ liệu khác nhau
✅ **Phân tích log từ Wazuh** để xác định mối đe dọa thực thời
✅ **Tạo báo cáo và cảnh báo** cho đội ngũ phản ứng khẩn cấp
✅ **Tích hợp với SOAR/IR** để tự động hóa phản ứng

**Kết quả?** Thời gian phản ứng chậm, rủi ro bị tấn công tăng cao, và công việc trở nên mệt mỏi.

**Giải pháp?** **Workflow này tự động hóa toàn bộ quy trình phân tích URL phishing và threat intelligence bằng NixGuard AI + Wazuh**, giúp các sếp:
✔ **Nhận cảnh báo tức thời** khi phát hiện URL phishing hoặc mối đe dọa mạng
✔ **Tích hợp với Slack/Telegram** để cảnh báo ngay lập tức
✔ **Lưu log phân tích** vào Google Sheets hoặc cơ sở dữ liệu
✔ **Tự động tạo ticket Jira** cho các sự kiện nguy hiểm

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này hoạt động 24/7 với hiệu suất tối ưu, các sếp nên **self-host n8n trên VPS** để tránh giới hạn của phiên bản cloud.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (Đảm bảo tốc độ cao cho AI)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 80% thời gian phân tích thủ công** bằng tự động hóa
- **Nhận cảnh báo tức thời** trên Slack/Telegram khi phát hiện URL phishing
- **Tích hợp với SOAR/IR** để phản ứng nhanh chóng
- **Lưu log phân tích** để auditing và báo cáo định kỳ
- **Reusable Logic**: Sử dụng cùng một logic phân tích cho nhiều nguồn dữ liệu (webhook, API, lịch trình...)
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
✅ **Tài khoản NixGuard** (miễn phí tại [thenex.world/security/subscribe](https://thenex.world/security/subscribe))
✅ **API Key của NixGuard** (để kết nối với API)
✅ **Workflow chính "Get Real-Time Security Insights"** (cần import từ [đây](https://n8n.io/workflows/4693))
✅ **Credentials Slack/Telegram** (nếu muốn cảnh báo tức thời)
✅ **Google Sheets hoặc cơ sở dữ liệu** (nếu muốn lưu log)

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/5937](https://n8n.io/workflows/5937)
- **Mở n8n Editor** và nhấn **Import** → Chọn file JSON vừa tải
- **Hoặc copy/paste** JSON từ file vào Editor

#### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow này là một **"Dispatcher"** (máy phân phối) để gọi workflow chính. Các bước cấu hình quan trọng:

##### **A. Cấu Hình Node "Set API Key & Initial Prompt"**
- **Mở node này** và điền:
  - `apiKey`: **API Key của NixGuard** (từ tài khoản của bạn)
  - `initialPrompt`: **Không cần thay đổi** (sẵn sàng cho workflow chính xử lý)

##### **B. Kết Nối Workflow Chính**
- **Mở node "Execute NixGuard & Wazuh Workflow"**
- Trong trường `Workflow`, chọn **workflow chính "Get Real-Time Security Insights"** (đã import từ [đây](https://n8n.io/workflows/4693))
- **Lưu workflow** sau khi cấu hình xong

##### **C. (Tùy Chọn) Cấu Hình Cảnh Báo Slack**
- **Mở node "(Optional) Send Slack Alert for High-Risk Events"**
- **Thêm credentials Slack**:
  - Nhấn **Add** → Chọn **Slack**
  - Đăng nhập tài khoản Slack và cấp quyền
- **Chỉnh sửa message template** (nếu muốn thay đổi nội dung cảnh báo)

#### **3. Kích Hoạt ⚡️**
- **Test Run** với dữ liệu mẫu:
  - Gửi một **webhook request** đến `e74aeb1a-0659-4a89-8ede-17bb9fdbe317` (từ node Webhook)
  - Kiểm tra kết quả phân tích từ NixGuard và Wazuh
- **Bật Active workflow** khi đã kiểm tra xong

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Tích Hợp với Jira**
   - Thêm **node Jira** để tự động tạo ticket khi phát hiện sự kiện nguy hiểm
   - Cấu hình trường `Issue Type` là "Security Incident"

2. **Lưu Log vào Google Sheets**
   - Thêm **node Google Sheets** sau node `Format NixGuard AI Summary`
   - Cấu hình để ghi dữ liệu phân tích vào sheet mới

3. **Cảnh Báo trên Telegram**
   - Thay thế node Slack bằng **node Telegram Bot**
   - Cấu hình bot Telegram và gửi cảnh báo tức thời

4. **Lịch Trình Hoạt Động (Cron Job)**
   - Thêm **node Schedule** để chạy workflow định kỳ (ví dụ: mỗi giờ)
   - Dùng để phân tích URL mới từ nguồn dữ liệu

5. **Tích Hợp với SIEM (Wazuh)**
   - Nếu đang sử dụng **Wazuh**, kết nối node này với **Wazuh API** để lấy log thực thời

---

### 📌 **Kết Luận**
Workflow này là **một giải pháp tự động hóa hoàn chỉnh** cho việc phân tích URL phishing và threat intelligence, giúp các sếp:
✅ **Tiết kiệm thời gian** bằng tự động hóa
✅ **Nhận cảnh báo tức thời** trên Slack/Telegram
✅ **Tích hợp với SOAR/IR** để phản ứng nhanh chóng
✅ **Lưu log phân tích** để auditing và báo cáo

**Hành động ngay!**
- **Import workflow** và cấu hình theo hướng dẫn
- **Kết nối với Slack/Telegram** để nhận cảnh báo tức thời
- **Tích hợp với Jira/Google Sheets** để quản lý incident

**🔗 Tài liệu tham khảo:**
- [NixGuard Official](https://thenex.world)
- [Workflow Chính (Get Real-Time Security Insights)](https://n8n.io/workflows/4693)
- [TinoHost VPS (Self-Host n8n)](https://tino.vn/vps-n8n?affid=388)