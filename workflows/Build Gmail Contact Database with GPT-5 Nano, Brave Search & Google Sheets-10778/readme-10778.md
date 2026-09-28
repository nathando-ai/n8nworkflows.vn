---
title: "🚀 Tự Động Xây Dựng Cơ Sở Dữ Liệu Liên Lạc Gmail Siêu Tiện Ích Với GPT-5 Nano & Brave Search"
description: "Workflow tự động hóa 100% không code để xây dựng cơ sở dữ liệu liên lạc chuyên nghiệp từ Gmail, tích hợp AI GPT-5 Nano và Brave Search để trích xuất thông tin chi tiết (điện thoại, mạng xã hội, website) từ email và trang web. Kết quả: Cơ sở dữ liệu liên lạc được enrich đầy đủ, tiết kiệm 10+ giờ công mỗi tháng."
slug: "tay-dong-xay-dung-co-so-du-lieu-lien-lac-gmail-gpt-5-nano"
tags: [n8n, automation, lead-generation, ai-summarization, gmail, google-sheets, brave-search, gpt-5-nano]
keywords: [tự động hóa n8n, xây dựng cơ sở dữ liệu liên lạc, gpt-5 nano workflow, brave search api, enrich contact data, tự động trích xuất thông tin từ email]
---

# 🚀 **Tự Động Xây Dựng Cơ Sở Dữ Liệu Liên Lạc Gmail Siêu Tiện Ích Với GPT-5 Nano & Brave Search**

### **Giải Pháp Cho Nỗi Đau "Tìm Thấy Email Nhưng Không Có Thông Tin Chi Tiết"**
Các sếp đã từng gặp tình huống này chưa? Bạn có một danh sách liên lạc từ Gmail, nhưng chỉ có email và tên – **không có số điện thoại, trang web, LinkedIn, hay thông tin liên hệ khác** để xây dựng mối quan hệ chuyên nghiệp? Hoặc phải mất **10+ giờ** để thủ công tìm kiếm và enrich mỗi liên lạc?

Workflow này **tự động hóa toàn bộ quá trình** bằng cách kết hợp:
✅ **Gmail API** để lấy toàn bộ lịch sử email
✅ **GPT-5 Nano** (AI của OpenAI) để trích xuất thông tin chi tiết từ email
✅ **Brave Search API** để tìm trang web của liên lạc và trích xuất thông tin từ đó
✅ **Google Sheets** để lưu trữ cơ sở dữ liệu liên lạc được enrich

**Kết quả?** Một **cơ sở dữ liệu liên lạc chuyên nghiệp**, tự động cập nhật, với thông tin đầy đủ để các sếp **tích hợp vào CRM, CRM, hoặc sử dụng cho outreach marketing**.

---
## 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm 10+ giờ/tháng** so với cách thủ công.
- **Cơ sở dữ liệu liên lạc được enrich** với số điện thoại, trang web, LinkedIn, và thông tin khác từ email và trang web.
- **Tự động cập nhật** khi có email mới trong Gmail.
- **Không cần code** – chỉ cần cấu hình và chạy.
- **Dữ liệu chính xác cao** nhờ AI GPT-5 Nano và Brave Search.
- **Kết hợp với CRM** (HubSpot, Salesforce, Zoho) dễ dàng.
:::

---
## 🔧 **Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ**]
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản Gmail** (để lấy lịch sử email).
2. **API Key OpenAI** (để sử dụng GPT-5 Nano).
3. **API Key Brave Search** (để tìm trang web của liên lạc).
4. **Google Sheets** (để lưu trữ cơ sở dữ liệu).
5. **Danh sách email** (hoặc workflow sẽ lấy từ Gmail Sent Folder).
6. **Thời gian đầu tư**: ~30 phút để cấu hình lần đầu.
:::

---
## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
Workflow được cung cấp dưới dạng **JSON**, các sếp có thể:
- **Tải file JSON** từ [n8n.io/workflows/10778](https://n8n.io/workflows/10778) và import vào n8n Editor.
- **Copy/Paste JSON** từ file vào **Import Workflow** trong n8n.

:::note[**Lưu ý quan trọng**]
- **Không chạy workflow ngay lập tức** sau khi import. Các sếp cần **cấu hình credentials và tham số** trước.
- **Không sử dụng GPT-5 Nano miễn phí** (nếu không có API Key OpenAI, workflow sẽ không hoạt động).
:::

---

### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**

#### **A. Cấu Hình Credentials**
Workflow sử dụng **4 loại credentials chính**:
1. **Gmail OAuth2** (để lấy email từ Gmail Sent Folder).
   - Cấu hình tại: **Settings > Credentials > Add Gmail OAuth2**.
   - Chọn quyền: `Read email` và `Read contacts`.
2. **OpenAI API** (để sử dụng GPT-5 Nano).
   - Cấu hình tại: **Settings > Credentials > Add OpenAI API**.
   - Điền `API Key` từ tài khoản OpenAI.
3. **Brave Search API** (để tìm trang web của liên lạc).
   - Cấu hình tại: **Settings > Credentials > Add Brave Search API**.
   - Đăng ký API tại [Brave Search Developer Portal](https://search.brave.com/api).
4. **Google Sheets OAuth2 API** (để ghi dữ liệu vào Google Sheets).
   - Cấu hình tại: **Settings > Credentials > Add Google Sheets OAuth2 API**.
   - Chọn quyền: `Edit spreadsheets`.

#### **B. Cấu Hình Node "WriteToDB" (Google Sheets)**
- **Sheet ID**: Các sếp cần **copy ID từ Google Sheets** (từ URL: `https://docs.google.com/spreadsheets/d/[ID]/edit`).
- **Tab Name**: Đặt tên tab là `Contacts` (hoặc chỉnh sửa trong node `SelectTabCC`).
- **Template**: Sử dụng **bảng mẫu** từ [đây](https://docs.google.com/spreadsheets/d/1ox0cP_v8UuonAFr3eXkOFRlBb_P86NRedEaK4fss5cA/edit?usp=sharing).

#### **C. Cấu Hình Node "ValidDomain?" (Lọc Domain Tính Hiệu Quả)**
- **Excluded Domains**: Các sếp có thể **chỉnh sửa danh sách domain không cần tìm kiếm** (ví dụ: `gmail.com`, `yahoo.com`, `outlook.com`).
- **Cách chỉnh**: Mở node `ValidDomain?` > `Set Condition` > Thêm điều kiện lọc.

#### **D. Cấu Hình Node "OpenAI Chat Model" (GPT-5 Nano)**
- **Model**: Đảm bảo chọn `gpt-5-nano` (nếu không có, workflow sẽ không hoạt động).
- **Prompt**: Workflow đã tự động cấu hình prompt để trích xuất thông tin từ email.

#### **E. Cấu Hình Node "SearchWebsite" (Brave Search)**
- **Query**: Workflow sẽ tự động xây dựng query từ domain của email (ví dụ: `example.com`).
- **Limit Results**: Đặt số lượng kết quả tối đa là **5** để tránh quá tải.

---
### **3. Kích Hoạt ⚡️**
1. **Test Run** với **1-2 email mẫu** để kiểm tra:
   - AI có trích xuất được thông tin không?
   - Brave Search có tìm được trang web không?
   - Dữ liệu có ghi vào Google Sheets không?
2. **Bật Active** workflow sau khi kiểm tra thành công.

---
## ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[**Tăng Cường Hiệu Quả**]
1. **Kết hợp với CRM**:
   - Sau khi có cơ sở dữ liệu liên lạc, các sếp có thể **export từ Google Sheets** và **import vào HubSpot, Salesforce, hoặc Zoho CRM**.
2. **Lưu Log & Monitoring**:
   - Thêm node **Slack/Telegram Notification** để nhận báo cáo khi workflow hoàn thành.
   - Sử dụng **Google Sheets Logs** để theo dõi lỗi.
3. **Tự Động Chạy Hàng Ngày**:
   - Sử dụng **n8n Cloud** hoặc **Self-hosted** để chạy workflow **tự động hàng ngày** (ví dụ: 12h đêm).
4. **Enrich Thêm Thông Tin**:
   - Sử dụng **PhantomBuster** hoặc **Apify** để trích xuất thêm thông tin từ trang web (nếu Brave Search không đủ).
5. **Tối Ưu AI Prompt**:
   - Nếu GPT-5 Nano không trích xuất được thông tin, các sếp có thể **cập nhật prompt** trong node `OpenAI Chat Model`.
:::

---
## 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp muốn **tự động hóa việc xây dựng cơ sở dữ liệu liên lạc** từ Gmail, **không cần code**, và **không tốn thời gian thủ công**.

**Bắt đầu ngay!**
1. **Import workflow** và cấu hình credentials.
2. **Chạy test** với 1-2 email.
3. **Bật tự động** và **nhận cơ sở dữ liệu liên lạc được enrich** trong vòng vài giờ!

:::success[**Kêu Gọi Hành Động**]
**👉 [Tải workflow ngay](https://n8n.io/workflows/10778) và bắt đầu tự động hóa!**
**👉 [Đăng ký VPS Self-hosted](https://tino.vn/vps-n8n?affid=388) để workflow chạy 24/7!**
:::

---
:::info[**Gợi ý hạ tầng cho n8n**]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**Chúc các sếp thành công với việc tự động hóa!** 🚀