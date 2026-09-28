---
title: "🔍 **Tự Động Hoàn Thành Nhiều Loại DNS Lookup Với Dịch Vụ DNS Công Của Google - Không Cần Code!**"
description: "Workflow này giúp các sếp tự động tra cứu tất cả các loại DNS (A, MX, TXT, NS,...) cho một domain chỉ trong vài giây, tiết kiệm thời gian so sánh thủ công lên đến 90%. Hoạt động liên tục 24/7 trên VPS, kết quả chính xác và dễ dàng tích hợp vào hệ thống quản lý domain."
slug: "tieu-dong-dns-lookup-voi-google-dns"
tags: [n8n, automation, devops, dns-lookup, google-dns]
keywords: [tự động hóa dns lookup, tra cứu dns tự động, n8n workflow dns, tra cứu mx txt ns domain, google public dns api]
---

# 🚀 **Tự Động Tra Cứu DNS Cho Domain - Giải Pháp Tiết Kiệm Thời Gian Cho Các Sếp IT & DevOps**

### **Nỗi Đau Thực Tế Của Các Sếp**
Trong công việc quản lý domain, kiểm tra cấu hình DNS (A, MX, TXT, NS,...) thường là một công việc **mệt mỏi và tốn thời gian**. Các sếp phải:
- **Tra cứu từng loại DNS một** trên các trang web khác nhau (Whois, DNS Checker,...) hoặc sử dụng CLI như `dig`/`nslookup`.
- **So sánh thủ công** kết quả giữa các loại DNS, dễ xảy ra lỗi nhầm lẫn.
- **Không có cách nào tự động hóa** để tra cứu **tất cả các loại DNS** một lúc, đặc biệt khi cần kiểm tra nhiều domain.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách:**
✅ **Tra cứu đồng thời tất cả các loại DNS** (A, MX, TXT, NS, CNAME,...) chỉ với một domain.
✅ **Sử dụng dịch vụ DNS công của Google** (không cần API key, miễn phí).
✅ **Hoạt động tự động 24/7** trên VPS, không cần can thiệp thủ công.
✅ **Kết quả được tổng hợp sạch sẽ**, dễ dàng tích hợp vào hệ thống quản lý domain.

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian lên đến 90%** so với tra cứu thủ công.
- **Chính xác 100%** nhờ sử dụng API DNS công của Google.
- **Dễ dàng tích hợp** với Slack, Email, hoặc hệ thống quản lý domain.
- **Hoạt động liên tục** mà không cần can thiệp.
- **Miễn phí** (không cần API key).
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Để workflow này hoạt động, các sếp cần:
1. **Tài khoản n8n Self-hosted** (cài trên VPS để hoạt động 24/7).
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)

2. **Không cần API key** (sử dụng dịch vụ DNS công của Google).

3. **Thời gian setup ~5 phút** (chỉ cần import workflow và cấu hình form input).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste JSON vào **n8n Editor**:
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/10200).
- **Nhấn "Import"** trong n8n Editor và chọn file JSON.
- **Hoặc copy toàn bộ JSON** và dán vào **Import Workflow** trong n8n.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này **không cần cấu hình API key** vì sử dụng dịch vụ DNS công của Google. Tuy nhiên, các sếp cần chú ý:

##### **A. Cấu Hình Form Input (Node: "Form input")**
- **Tên node:** `Form input` (loại `formTrigger`).
- **Cấu hình form:**
  - Thêm **1 trường text** với tên `domain` (để nhập domain cần tra cứu).
  - Thêm **1 trường dropdown** với tên `dnsTypes` (chọn loại DNS muốn tra cứu).
    - **Lựa chọn mặc định:** `"all"` (tra cứu tất cả các loại DNS).
    - **Các tùy chọn khác:** `A`, `MX`, `TXT`, `NS`, `CNAME`, `SOA`, `PTR`, `AAAA` (có thể thêm nhiều loại khác theo nhu cầu).

##### **B. Cấu Hịnh Node "Default to all DNS types" (loại `set`)**
- **Giá trị mặc định:** `"A,MX,TXT,NS,CNAME,SOA,PTR,AAAA"` (tất cả các loại DNS phổ biến).
- **Nếu muốn thêm loại DNS mới:**
  - Thêm vào danh sách trên và **cập nhật node "Form input"** để phản ánh các loại mới.

##### **C. Node "If no DNS type in input" (loại `if`)**
- **Điều kiện mặc định:** Nếu không chọn loại DNS nào, workflow sẽ **tra cứu tất cả** (do node `Default to all DNS types`).
- **Không cần chỉnh sửa** nếu muốn giữ logic mặc định.

##### **D. Node "For each DNS type" (loại `splitInBatches`)**
- **Không cần cấu hình thêm**, workflow sẽ tự động phân chia và tra cứu từng loại DNS.

##### **E. Node "DNS Lookup" (loại `httpRequest`)**
- **URL mặc định:** `https://dns.google/resolve?name={domain}&type={dnsType}`.
- **Không cần chỉnh sửa**, vì đã sử dụng API DNS công của Google.

#### **3. Kích Hoạt ⚡️**
- **Test run:**
  - Nhập một domain vào form (ví dụ: `google.com`).
  - Chọn loại DNS (hoặc chọn `all` để tra cứu tất cả).
  - Nhấn **Run Workflow** và kiểm tra kết quả.
- **Bật Active:**
  - Sau khi test thành công, **bật Active** để workflow hoạt động tự động.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::info[CÁCH SỬ DỤNG HIỆU QUẢ]
1. **Tích Hợp Với Slack/Telegram:**
   - Sau khi tra cứu xong, **gửi kết quả vào Slack/Telegram** bằng node `webhook` hoặc `slack`.
   - Ví dụ: Khi có domain mới được thêm vào hệ thống, workflow sẽ tự động tra cứu và báo cáo kết quả.

2. **Lưu Log Kết Quả:**
   - Sử dụng node `set` hoặc `code` để lưu kết quả vào **Google Sheets** hoặc **database** để theo dõi lịch sử.

3. **Gửi Báo Cáo Định Kỳ:**
   - Kết hợp với **n8n Scheduler** để tra cứu domain định kỳ (ví dụ: hàng ngày) và gửi báo cáo email.

4. **Thêm Loại DNS Mới:**
   - Theo [danh sách DNS của IANA](https://www.iana.org/assignments/dns-parameters/dns-parameters.xhtml), các sếp có thể thêm loại DNS mới vào node `Default to all DNS types` và cập nhật form input.

5. **Tự Động Tra Cứu Khi Domain Thay Đổi:**
   - Kết nối với **API của registrar** (như Cloudflare, GoDaddy) để khi domain được cập nhật, workflow tự động tra cứu lại.
:::

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp IT, DevOps và quản lý domain muốn **tự động hóa tra cứu DNS một cách nhanh chóng và chính xác**. Không cần code, không cần API key, và hoạt động **liên tục 24/7** trên VPS.

**Hãy áp dụng ngay để:**
✔ **Tiết kiệm thời gian** trong công việc tra cứu DNS.
✔ **Tránh lỗi nhầm lẫn** khi so sánh thủ công.
✔ **Tích hợp vào hệ thống quản lý domain** một cách dễ dàng.

**Bắt đầu ngay với n8n Self-hosted trên VPS và tự động hóa công việc của mình!** 🚀

---
**📩 Liên hệ với tác giả (Ossian Madisson) để hỗ trợ thêm:**
- Email: [ossian@smultronstudio.com](mailto:ossian@smultronstudio.com)
- Website: [Smultron Studio](https://smultronstudio.com)