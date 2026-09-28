---
title: "🚀 Tự Động Hóa Lấy Dữ Liệu Giá Trị Lịch Sử Polymarket (Up/Down) Vào Supabase - Không Cần Code"
description: "Workflow này tự động thu thập dữ liệu giá lịch sử từ các thị trường Up/Down trên Polymarket (như Bitcoin, S&P 500) và lưu vào Supabase để phân tích SQL hoặc xây dựng pipeline dữ liệu tiên tiến. Giúp các sếp tiết kiệm thời gian và tối ưu hóa quy trình trading."
slug: "tu-dong-hoa-lay-du-lieu-gia-polymarket-vao-supabase"
tags: [n8n, automation, crypto-trading, supabase, no-code, data-collection]
keywords: [tự động hóa n8n, lấy dữ liệu Polymarket, Supabase, trading crypto, phân tích thị trường, SQL query, data pipeline]
---

# 🚀 **Tự Động Hóa Lấy Dữ Liệu Giá Lịch Sử Polymarket (Up/Down) Vào Supabase**

### **Giải Pháp Cho Các Sếp Trading & Analyst**
Bạn có bao giờ phải **tìm kiếm thủ công** dữ liệu giá lịch sử từ các thị trường Up/Down trên Polymarket (như Bitcoin Up/Down, S&P 500 Up/Down) để phân tích? Hoặc phải **lặp đi lặp lại** các bước lấy API, xử lý dữ liệu và lưu trữ? **Workflow này sẽ tự động hóa toàn bộ quy trình chỉ với một cú nhấp chuột!**

Dữ liệu được **lưu vào Supabase** (cơ sở dữ liệu cloud tiên tiến) để bạn có thể:
✅ **Trích xuất nhanh** thông qua SQL
✅ **Kết nối với Python/R** để xây dựng mô hình AI
✅ **Tự động hóa báo cáo** định kỳ
✅ **Tối ưu hóa chiến lược trading** dựa trên dữ liệu lịch sử

---

## 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[**Lợi Ích Cốt Lõi**]
- **Tiết kiệm thời gian**: Không cần thủ công lấy API hoặc xử lý dữ liệu.
- **Dữ liệu chính xác & toàn diện**: Lấy toàn bộ lịch sử giá từ Polymarket (không giới hạn).
- **Lưu trữ an toàn**: Dữ liệu được backup vào Supabase (không lo mất mát).
- **Hoạt động liên tục**: Workflow chạy 24/7 trên VPS (self-hosted).
- **Dễ dàng phân tích**: Dữ liệu sẵn sàng cho SQL, Python, hoặc Tableau.
:::

---

## 🔧 **Yêu Cầu Cần Thiết**
:::info[**CHUẨN BỊ**]
Trước khi chạy workflow, các sếp cần chuẩn bị:
1. **Tài khoản Polymarket** (miễn phí, không cần API key).
2. **Tài khoản Supabase** (đăng ký tại [supabase.com](https://supabase.com/)).
3. **Bảng dữ liệu trong Supabase** (tạo theo schema sau):
   ```sql
   CREATE TABLE HYST_BTC_UP_DW_1H (
       EventId TEXT NOT NULL,
       price NUMERIC[] NOT NULL,
       time_of_price TIMESTAMPTZ[]
   );
   ```
4. **Bảng tạm trong n8n** (để lưu metadata sự kiện):
   - Tên: `Polymarket_Btc_1h_Event_List_1`
   - Cột cần thiết: `EventId`, `Status`, `EndTime`, `TokenIdUp`, `TokenIdDown`.
5. **VPS để self-host n8n** (để workflow chạy 24/7):
   👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
   👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)

---

## 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/12823](https://n8n.io/workflows/12823) hoặc copy/paste JSON vào **n8n Editor**.
- **Cách import**:
  1. Mở **n8n Workflow Editor**.
  2. Nhấn **Import** → Chọn file JSON hoặc dán JSON vào ô.
  3. Chọn **Create Workflow**.

### **2. Các Lưu Ý BẮT BUỘC Phải Chỉnh 📌**
Workflow gồm **2 phần chính**:
- **Phần 1**: Lấy danh sách sự kiện từ slug Polymarket.
- **Phần 2**: Lấy dữ liệu giá lịch sử và lưu vào Supabase.

#### **A. Cấu Hình Node Quan Trọng**
| **Node** | **Loại** | **Cần Chỉnh Gì?** |
|----------|----------|-------------------|
| **Form to include slug of the market** | `formTrigger` | Điền **slug** của thị trường (vd: `btc-1h-2024-05-20`). |
| **Find the Event ID from the Slug** | `httpRequest` | **URL**: `https://polymarket.com/api/v1/events/{slug}` (đổi `{slug}` thành slug bạn nhập). |
| **Find All the Events for that Series ID** | `httpRequest` | **URL**: `https://polymarket.com/api/v1/series/{seriesId}/events` (lấy `seriesId` từ node trước). |
| **Register Events in Table Polymarket_Btc_1h_Event_List_1** | `dataTable` | **Chọn bảng** `Polymarket_Btc_1h_Event_List_1` và **cập nhật cột** `EventId`, `Status`, `EndTime`. |
| **Fetch 100 unprocessed events** | `dataTable` | **Chọn bảng** `Polymarket_Btc_1h_Event_List_1` và **lọc** `Status = "unprocessed"`. |
| **Fetch UP/DOWN tokens and end time** | `httpRequest` | **URL**: `https://polymarket.com/api/v1/events/{eventId}` (lấy `eventId` từ bảng). |
| **Store UP/DOWN tokens and end time** | `dataTable` | **Cập nhật** `TokenIdUp`, `TokenIdDown`, `EndTime` trong bảng. |
| **Check if market has closed** | `if` | **Điều kiện**: `EndTime < current time` (để bỏ qua thị trường đang diễn ra). |
| **Convert end time to Unix timestamp** | `dateTime` | **Chọn format**: `Unix timestamp` (để tính toán thời gian bắt đầu). |
| **Convert end time to numeric and set start time** | `set` | **Cài đặt**:
   - `StartTimeUnix = EndTimeUnix - 3600` (giả sử thị trường 1h, điều chỉnh theo thời gian thị trường). |
| **Fetch price history** | `httpRequest` | **URL**: `https://polymarket.com/api/v1/tokens/{tokenId}/price_history` (lấy `tokenId` từ node trước). |
| **Store in Supabase** | `supabase` | **Chọn credentials**: `supabaseApi` (cấu hình sau). |
| **Mark as processed** | `dataTable` | **Cập nhật** `Status = "processed"` trong bảng. |

#### **B. Cấu Hình Supabase**
1. **Tạo credentials Supabase**:
   - Trong **n8n**, đi đến **Credentials** → **Add Credentials** → **Supabase**.
   - Điền:
     - **URL**: `https://[your-project-ref].supabase.co`
     - **Key**: `your-supabase-key` (tìm trong **Project Settings → API**).
2. **Chọn credentials** trong node `Store in Supabase`.

#### **C. Cấu Hình Bảng Tạm trong n8n**
- **Tên bảng**: `Polymarket_Btc_1h_Event_List_1`
- **Cột cần thiết**:
  - `EventId` (ID sự kiện)
  - `Status` (giá trị: `unprocessed` hoặc `processed`)
  - `EndTime` (thời gian kết thúc thị trường)
  - `TokenIdUp` (ID token Up)
  - `TokenIdDown` (ID token Down)

---

### **3. Kích Hoạt ⚡️**
1. **Chạy phần 1** (lấy danh sách sự kiện):
   - Nhập **slug** thị trường vào form (vd: `btc-1h-2024-05-20`).
   - Nhấn **Submit** → Workflow sẽ tự động lấy danh sách sự kiện và lưu vào bảng tạm.
2. **Chạy phần 2** (lấy dữ liệu giá):
   - Nhấn **Manual Trigger** (`Start Getting Prices Data`).
   - Workflow sẽ:
     - Lấy **100 sự kiện chưa xử lý**.
     - Lấy **dữ liệu giá lịch sử** từ Polymarket.
     - Lưu vào **Supabase**.
     - **Cập nhật trạng thái** thành `processed`.
3. **Kiểm tra kết quả**:
   - Mở **Supabase** → Bảng `HYST_BTC_UP_DW_1H` → Kiểm tra dữ liệu đã lưu.

---

## ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::note[**Tối Ưu Hóa Cho Các Sếp**]
1. **Lấy nhiều thị trường cùng lúc**:
   - Sử dụng **node `splitOut`** để chia nhỏ danh sách slug và chạy song song.
2. **Gửi báo cáo định kỳ**:
   - Kết nối với **Slack/Telegram** để thông báo khi hoàn thành.
   - Ví dụ: Sau khi lưu xong, gửi tin nhắn:
     ```json
     {
       "text": "📊 Dữ liệu Bitcoin Up/Down đã được cập nhật vào Supabase!"
     }
     ```
3. **Lưu log hoạt động**:
   - Sử dụng **node `stickyNote`** để ghi lại thời gian chạy và lỗi (nếu có).
4. **Tự động chạy hàng ngày**:
   - Sử dụng **n8n Cron Trigger** để chạy workflow vào mỗi sáng.
5. **Phân tích dữ liệu với Python**:
   - Kết nối Supabase với Python bằng `supabase-py` để xây dựng mô hình dự đoán.
   - Ví dụ:
     ```python
     import supabase
     supabase = supabase.create_client("URL", "KEY")
     data = supabase.table("HYST_BTC_UP_DW_1H").select("*").execute()
     ```
6. **Tạo dashboard**:
   - Kết nối Supabase với **Tableau/Power BI** để visual hóa dữ liệu.
:::

---

## 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi việc thủ công lấy dữ liệu Polymarket và **cung cấp cơ sở dữ liệu sạch** để phân tích. **Không cần code**, chỉ cần **import và chạy** là xong!

👉 **Bắt đầu ngay**:
1. **Cài đặt n8n trên VPS** (đăng ký mã giảm giá **VPSN8N**).
2. **Import workflow** và cấu hình Supabase.
3. **Nhập slug thị trường** và **chạy tự động hóa**!

**Hỏi đáp & hỗ trợ**:
- Có vấn đề gì? Đăng câu hỏi tại [n8n Community](https://community.n8n.io/) hoặc comment dưới bài viết này.
- Muốn **tùy chỉnh** workflow cho thị trường khác? Liên hệ với tôi!

---
**🚀 Chúc các sếp thành công với chiến lược trading dữ liệu!** 🚀