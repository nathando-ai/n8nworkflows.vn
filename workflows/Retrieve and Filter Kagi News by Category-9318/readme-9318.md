---
title: "📰 Tự Động Lấy & Lọc Tin Tức Kagi News Theo Danh Mục - Không Cần Code!"
description: "Workflow này tự động lấy danh sách tin tức từ Kagi News theo danh mục mong muốn, lọc và trả về tiêu đề tin tức duy nhất - tiết kiệm thời gian cho các sếp khi cần cập nhật tin tức chuyên ngành."
slug: "tu-dong-lay-loc-tin-tuc-kagi-news-theo-danh-muc"
tags: [n8n, automation, no-code, api-integration, tin-tuc-tự-dộng]
keywords: [n8n workflow tin tức, tự động hóa lấy tin Kagi News, lọc tin theo danh mục, API Kagi News, tự động hóa không code]
---

# 🚀 **Tự Động Lấy & Lọc Tin Tức Kagi News Theo Danh Mục - Không Cần Code!**

### **Nỗi Đau Của Các Sếp?**
Hàng ngày, các sếp phải tốn thời gian **quét qua hàng trăm bài tin** trên Kagi News để tìm kiếm tin tức liên quan đến ngành nghề, dự án hoặc lĩnh vực mình quan tâm. Thao tác này không chỉ **tốn thời gian** mà còn dễ **bỏ lỡ tin quan trọng** do sự phân tán hoặc thiếu tập trung. **Workflow này giải quyết vấn đề này bằng cách tự động:**
✅ **Lấy danh sách danh mục tin tức** từ Kagi News.
✅ **Lọc tin theo danh mục cụ thể** (ví dụ: Tech, Finance, Health).
✅ **Trích xuất tiêu đề tin tức** (hoặc thông tin khác) để các sếp **nhận được thông tin chính xác, nhanh chóng và tập trung**.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài n8n trên **VPS riêng (Self-hosted)** để tránh giới hạn của phiên bản cloud.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đủ sức mạnh cho workflow n8n)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Không phải quét thủ công hàng trăm bài tin.
- **Tính chính xác cao**: Lọc tin theo danh mục **một cách tự động và không sai sót**.
- **Cá nhân hóa**: Chỉ lấy tin tức **liên quan đến ngành nghề** của mình.
- **Hoạt động liên tục**: Workflow **chạy 24/7** và cập nhật tin tức mới nhất.
- **Dễ dàng mở rộng**: Có thể **thêm thông tin khác** (tóm tắt, điểm nổi bật) vào tiêu đề.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
:::info[CHUẨN BỊ]
Workflow này **không yêu cầu API Key** hoặc tài khoản đặc biệt, nhưng các sếp cần:
- **Trình duyệt hoặc API Kagi News** (n8n sẽ tự động gọi API từ bên trong workflow).
- **n8n Self-hosted** (để tránh giới hạn của phiên bản cloud).
- **Thiết lập `category`** khi kích hoạt workflow (xem phần **Cách kích hoạt**).
:::

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể **import workflow** từ file JSON hoặc **copy/paste JSON** vào **n8n Editor**:
1. **Tải file JSON** từ [đây](https://n8n.io/workflows/9318) (hoặc sao chép từ link trên).
2. Mở **n8n Editor** → Nhấn **Import** → Dán JSON vào.
3. **Kích hoạt workflow** bằng cách **set `category`** (xem phần sau).

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này **không cần cấu hình API Key**, nhưng các sếp cần **điền tham số `category`** khi kích hoạt:

| **Node** | **Lưu Ý Cần Chỉnh** | **Hướng Dẫn** |
|----------|----------------------|----------------|
| **Start (Execute Workflow Trigger)** | Thiết lập `category` | Nhập **danh mục tin tức** bạn muốn (ví dụ: `"tech"`, `"finance"`, `"health"`). Nếu không biết danh mục, các sếp có thể **lấy danh sách từ node "Get Latest Categories"** (xem phần sau). |
| **Get Latest Categories (HTTP Request)** | **Không cần chỉnh** | Node này tự động lấy danh sách danh mục từ API Kagi News. |
| **Filter by wanted category (Filter)** | **Không cần chỉnh** | Node này **lọc danh mục** theo `category` bạn đã set ở **Start**. |
| **Get Stories in Category (HTTP Request)** | **Không cần chỉnh** | Node này lấy **tin tức trong danh mục** đã chọn. |
| **Split out stories (Split Out)** | **Không cần chỉnh** | Chia tin tức thành **mảng riêng biệt** để xử lý. |
| **Pick only title (Set)** | **Không cần chỉnh** | **Trích xuất chỉ tiêu đề** tin tức (có thể thay đổi thành `summary` hoặc `talking points` nếu muốn). |
| **Limit to 1 category (Limit)** | **Không cần chỉnh** | **Giới hạn số lượng tin tức** (mặc định là 100, có thể điều chỉnh). |

#### **3. Kích Hoạt ⚡️**
1. **Test Run** (để kiểm tra):
   - Nhấn **Run Workflow** và **điền `category`** (ví dụ: `"tech"`).
   - Kiểm tra **output** để đảm bảo workflow lấy được tin tức đúng danh mục.
2. **Bật Active**:
   - Sau khi test thành công, **bật Active** để workflow **chạy tự động** khi kích hoạt.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
:::tip[CÁCH MỞ RỘNG WORKFLOW]
1. **Gửi tin tức lên Slack/Telegram**:
   - Thêm **node Slack/Telegram Webhook** sau **Pick only title** để **báo cáo tin tức mới** ngay khi có.
   - Cài đặt **alert tự động** cho các sếp khi có tin tức mới trong danh mục quan tâm.

2. **Lưu log vào Google Sheets/Notion**:
   - Thêm **node Google Sheets** hoặc **Notion** sau **Pick only title** để **lưu tin tức vào bảng tính/note** cho theo dõi lâu dài.

3. **Tự động gửi email báo cáo**:
   - Kết hợp với **node Email (SMTP)** để **gửi tin tức mới** vào email cá nhân hàng ngày.

4. **Thêm thông tin khác (summary, talking points)**:
   - Thay đổi **node "Pick only title"** thành **trích xuất `summary` hoặc `talking points`** từ tin tức.

5. **Lọc tin theo từ khóa**:
   - Thêm **node Filter** sau **Split out stories** để **lọc tin tức chứa từ khóa cụ thể** (ví dụ: `"AI"`, `"Blockchain"`).
:::

---

### 📌 **Kết Luận**
Workflow này **giải phóng thời gian** cho các sếp khỏi việc **quét tin tức thủ công**, đồng thời **tăng cường hiệu quả** trong việc cập nhật thông tin ngành nghề. **Chỉ cần import, set `category` và bật Active**, workflow sẽ **tự động lấy và lọc tin tức** theo yêu cầu!

👉 **Hãy áp dụng ngay** và **tận hưởng sự tự động hóa hoàn toàn** cho công việc của mình! Nếu có thắc mắc, các sếp có thể **đăng ký hỗ trợ** tại [n8n Community](https://community.n8n.io/) hoặc liên hệ với **TinoHost** để cài đặt VPS n8n ổn định.

---
**#TựĐộngHóa #N8N #TinTứcTựĐộng #NoCode #APIIntegration**