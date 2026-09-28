---
title: "🚀 **Quét Thẻ Business Card Tự Động Sang Google Sheets & Điện Thoại iPhone Vía Telegram** – Không Cần Code!"
description: "Tự động hóa việc quét, trích xuất thông tin từ thẻ business card (thậm chí cả chồng thẻ) thành dữ liệu Google Sheets và file vCard để thêm trực tiếp vào điện thoại iPhone thông qua Telegram. Giúp tiết kiệm thời gian và tránh mất mát thông tin sau các buổi hội nghị."
slug: "quet-the-business-card-tu-dong-sang-google-sheets-va-dien-thoai"
tags: [n8n, automation, document-extraction, ai-summarization, telegram-bot, google-sheets, easybits, no-code]
keywords: [n8n workflow quét thẻ business, tự động hóa trích xuất thông tin, Google Sheets tự động, Telegram bot thêm contact, easybits AI, không cần code]
---

# 🚀 **Quét Thẻ Business Card Tự Động Sang Google Sheets & Điện Thoại iPhone – Không Cần Code!**

### **Giải pháp cho ai?**
Các sếp, nhân viên marketing, hoặc bất kỳ ai phải quản lý hàng loạt thẻ business card sau các buổi hội nghị, hội thảo, hoặc gặp gỡ khách hàng. Thay vì phải nhập thủ công từng thông tin, **chỉ cần chụp ảnh chồng thẻ và gửi qua Telegram**, workflow này sẽ tự động:
✅ **Trích xuất** tên, chức vụ, công ty, email, số điện thoại, website, địa chỉ từ ảnh.
✅ **Lọc bỏ trùng lặp** với dữ liệu đã có trong Google Sheets.
✅ **Tạo file vCard** cho mỗi contact mới.
✅ **Gửi file vCard** qua Telegram để **nhấp một lần là thêm vào điện thoại iPhone** (hoặc Android).

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không phải nhập thủ công từng thẻ (giúp tiết kiệm **30+ phút/lần** cho 30 thẻ).
- **Chính xác 100%**: AI easybits trích xuất thông tin với độ chính xác cao, thậm chí với ảnh chồng thẻ.
- **Không trùng lặp**: Dữ liệu mới chỉ được lưu và gửi nếu chưa tồn tại trong Google Sheets.
- **Tích hợp hoàn hảo**: File vCard được gửi qua Telegram, **nhấp một lần là thêm vào điện thoại** (không cần copy-paste).
- **Hoạt động 24/7**: Cài đặt 1 lần, tự động hóa mọi lần sau đó.
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản n8n**:
   - **Self-hosted** (khuyến nghị) để lưu trữ dữ liệu riêng tư.
   - 👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%).
   - 👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172).

2. **Tài khoản Telegram**:
   - Tạo **bot Telegram** miễn phí tại [@BotFather](https://t.me/BotFather) và lấy **API Token**.
   - Thêm bot vào chat cá nhân để nhận ảnh thẻ.

3. **Google Sheets**:
   - Tạo một bảng mới với **các cột sau** (đảm bảo tên chính xác):
     ```
     timestamp, name, title, company, email, phone, website, address, notes
     ```
   - Cấp quyền cho bot n8n truy cập vào bảng (Settings → Share → "Anyone with link" hoặc "Specific people").

4. **Tài khoản easybits**:
   - Đăng ký tại [easybits.tech](https://easybits.tech) và tạo **Pipeline** mới.
   - Lấy **Pipeline ID** và **API Key** từ trang chi tiết Pipeline.

5. **N8n Community Node**:
   - Nếu tự host, cài đặt node easybits:
     ```
     @easybits/n8n-nodes-extractor
     ```
     (Trên n8n Cloud, node này đã sẵn sàng sử dụng).
:::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [link gốc](https://n8n.io/workflows/15530) hoặc copy toàn bộ JSON từ trang này.
- Mở **n8n Editor** → **Import Workflow** → Dán JSON và nhấn **Import**.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
#### **🔹 Node "New Photo from Telegram"**
- **Cấu hình Telegram Credential**:
  - Trong **Settings → Credentials**, thêm credential mới với loại **Telegram**.
  - Điền **API Token** từ BotFather và chọn **Updates** = `message`.
  - Đánh dấu **`download: true`** để n8n tự động tải ảnh từ Telegram.

#### **🔹 Node "easybits: Extract Contacts"**
- **Điền Pipeline ID và API Key**:
  - Từ trang chi tiết Pipeline của easybits, copy **Pipeline ID** và **API Key**.
  - Đặt **Input Type** = `Binary Files` (n8n sẽ tự động lấy ảnh từ Telegram).
- **Lưu ý**: Node này **trích xuất từng thẻ riêng biệt** trong ảnh, dù ảnh có chồng nhiều thẻ.

#### **🔹 Node "Read Existing Contacts" (Google Sheets)**
- **Chọn Credential Google**:
  - Trong **Settings → Credentials**, thêm credential Google với quyền truy cập vào Sheet.
- **Chọn Sheet và Range**:
  - Đảm bảo Sheet có **các cột bắt buộc** (`timestamp`, `name`, `email`, ...).
  - **Operation** = `getRows`.

#### **🔹 Node "Add Match Key (New) & Add Match Key (Existing)"**
- **Logic trùng lặp**:
  - Nếu contact có **email**, sử dụng email làm `match_key`.
  - Nếu không có email, kết hợp `name|company` (ví dụ: `Sarah|Acme Corp`).
  - **Lowercase và trim** để tránh trùng lặp do ký tự hoa/thường (ví dụ: `Sarah@Acme.com` vs `sarah@acme.com`).

#### **🔹 Node "Filter Out Duplicates"**
- **Cấu hình**:
  - **Combine by Matching Fields**: Chọn `match_key`.
  - **Output**: Chọn **Keep Non-Matches from Input 1** (lọc bỏ contact đã tồn tại).

#### **🔹 Node "Save to Google Sheets"**
- **Chọn Sheet và Range**:
  - Đảm bảo Sheet có **các cột bắt buộc** (nếu thiếu, node sẽ báo lỗi).
  - **Operation** = `append` (thêm mới chứ không ghi đè).
- **Định dạng Phone**:
  - Nếu phone là mảng (ví dụ: `[+84123456789, +84987654321]`), node sẽ nối thành chuỗi `+84123456789,+84987654321`.

#### **🔹 Node "Build vCard File"**
- **Kiểm tra định dạng**:
  - File vCard sẽ được tạo với định dạng **vCard 3.0** (hoàn toàn tương thích với iPhone, Android, Outlook).
  - **Không có lỗi ký tự đặc biệt** (ví dụ: dấu phẩy trong địa chỉ).

#### **🔹 Node "Send vCard to Telegram"**
- **Chọn Credential Telegram**:
  - Sử dụng credential Telegram đã cấu hình ở bước 1.
- **Định dạng Caption**:
  - Caption mặc định: `📇 [Name] – [Title] @ [Company]`.
  - Ví dụ: `📇 Sarah Jones – Head of Sales @ Acme Corp`.

---
### **3. Kích hoạt ⚡️**
1. **Test Run**:
   - Gửi một ảnh thẻ business card qua Telegram bot.
   - Kiểm tra **Google Sheets** có thêm dữ liệu mới không.
   - Kiểm tra **Telegram** có nhận được file vCard không.

2. **Bật Active**:
   - Nhấn **Active** trên workflow để nó hoạt động liên tục.

---
## ✍️ **Mẹo & gợi ý nâng cao**
:::info[NHỮNG Ý TƯỞNG TIẾP THEO]
1. **Tích hợp Slack/Email**:
   - Sau khi lưu vào Google Sheets, gửi thông báo qua **Slack** hoặc **Email** để team biết đã thêm contact mới.
   - Sử dụng node **Slack** hoặc **Email** để gửi tin nhắn tự động.

2. **Lưu log hoạt động**:
   - Thêm node **Sticky Note** hoặc **Google Sheets** để ghi lại lịch sử hoạt động (ngày giờ, contact mới, contact bị bỏ qua).

3. **Báo cáo định kỳ**:
   - Sử dụng **Google Apps Script** hoặc **n8n Schedule Node** để gửi báo cáo tổng hợp contact mới hàng tuần qua Email.

4. **Tối ưu cho nhiều thẻ**:
   - Nếu thường quét **trên 100 thẻ**, hãy chia ảnh thành nhiều phần (ví dụ: 50 thẻ/ảnh) để tránh quá tải easybits.

5. **Sử dụng AI nâng cao**:
   - Nếu easybits không trích xuất được thông tin chính xác, thử **cải tiến prompt** hoặc sử dụng node **LLM** (ví dụ: Mistral AI) để kiểm tra lại.
:::

---
## 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi công việc nhập liệu thủ công, đồng thời **tăng cường tính chính xác** và **tích hợp hoàn hảo** với điện thoại thông qua Telegram. **Chỉ cần chụp ảnh và gửi qua bot**, dữ liệu sẽ tự động được xử lý và sẵn sàng sử dụng trên mọi thiết bị.

🚀 **Hành động ngay**:
1. **Cài đặt n8n** trên VPS (nếu chưa có).
2. **Import workflow** và cấu hình theo hướng dẫn.
3. **Test với 1-2 thẻ** và bắt đầu tự động hóa!

**Cần hỗ trợ?** Đăng ký tại [TinoHost](https://tino.vn/vps-n8n?affid=388) để có VPS ổn định cho n8n và nhận **mã giảm giá VPSN8N** (giảm tới 39%). 🎁