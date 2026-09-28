---
title: "🤖📧 **Tự Động Hóa Xử Lý Email: Phân Loại + Trả Lời Tự Động Với GPT-4o + GotoHuman (Review Nhân Sự)**"
description: "Workflow tự động hóa hoàn chỉnh phân loại email vào danh mục phù hợp, tự động viết trả lời bằng GPT-4o, sau đó gửi đến hệ thống **GotoHuman** để nhân viên kiểm duyệt và phê duyệt trước khi gửi. Giảm thiểu thời gian phản hồi 90% và đảm bảo chất lượng nội dung phù hợp với brand."
slug: "tieu-dong-hoa-xu-ly-email-voi-gpt-4o-gotohuman"
tags: [n8n, automation, no-code, gotoHuman, GPT-4o, email automation, AI email assistant, ticket management]
keywords: [tự động hóa email n8n, phân loại email AI, trả lời email tự động, GotoHuman review, GPT-4o tự động hóa, workflow email tự động]
---

# 🚀 **Tự Động Hóa Xử Lý Email: Phân Loại + Trả Lời Tự Động Với GPT-4o + GotoHuman**

## **💡 Giới Thiệu: Giải Pháp Tự Động Hóa Email "Từ Nhận Đến Gửi"**
Hàng ngày, các sếp và đội ngũ hỗ trợ khách hàng phải mất **giờ đồng hồ** để:
- Phân loại hàng trăm email vào các danh mục khác nhau (hỗ trợ kỹ thuật, phản ánh, đặt hàng,...).
- Viết trả lời chính xác, thân thiện và phù hợp với brand.
- Đảm bảo **không sai sót** trong thông tin (giá, thời gian, nội dung hợp đồng...).

**Workflow này giải quyết tất cả bằng cách:**
✅ **Phân loại tự động** email vào danh mục phù hợp (thông qua AI).
✅ **Viết trả lời tự động** bằng **GPT-4o** (cập nhật mới nhất của OpenAI).
✅ **Kiểm duyệt bởi nhân viên** trên **GotoHuman** (đảm bảo chất lượng trước khi gửi).
✅ **Gửi trả lời chính thức** chỉ khi được phê duyệt.

**Kết quả?** **Tiết kiệm 90% thời gian phản hồi**, giảm sai sót, và duy trì **tính chuyên nghiệp** trong tất cả các tương tác với khách hàng.

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy **ổn định 24/7**, các sếp nên cài **n8n trên VPS riêng (Self-hosted)** để tránh giới hạn của phiên bản cloud.
👉 **[Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388)** (🎁 **Mã giảm giá: VPSN8N** - giảm tới **39%**)
👉 **[Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)** (đủ sức mạnh cho workflow này)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 90% thời gian** phản hồi email (tự động hóa từ phân loại đến gửi).
- **Chất lượng cao nhất** với hệ thống **kiểm duyệt nhân sự** trước khi gửi.
- **Phù hợp với brand** (nhân viên có thể chỉnh sửa trước khi gửi).
- **Hoạt động 24/7** (không cần người quản lý trực tiếp).
- **Giảm sai sót** (AI + kiểm tra nhân sự).
- **Dễ mở rộng** (thêm các danh mục email mới chỉ cần cập nhật prompt).
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
✔ **Tài khoản Gmail** (để lấy email mới và gửi trả lời).
✔ **Tài khoản OpenAI** (để sử dụng **GPT-4o-mini**).
✔ **Tài khoản GotoHuman** (để kiểm duyệt và phê duyệt trả lời).
✔ **API Key** của:
   - OpenAI (tạo tại [OpenAI API](https://platform.openai.com/account/api-keys)).
   - GotoHuman (tạo tại [GotoHuman Dashboard](https://app.gotohuman.com/)).

---
:::note[LƯU Ý QUAN TRỌNG]
- **Không cần code** – workflow hoàn toàn **no-code**.
- **Không giới hạn số lượng email** – chạy 24/7 trên VPS.
- **Dễ dàng cập nhật** (chỉ cần chỉnh sửa prompt trong node **Set Prompt**).
:::

---

## 🚀 **Cách Import & Cấu Hình Workflow**

### **1. Import Workflow 📥**
#### **Phương pháp 1: Import từ file JSON**
1. **Tải workflow** từ [n8n.io/workflows/7301](https://n8n.io/workflows/7301) (chọn **Export as JSON**).
2. **Mở n8n Editor** (trên VPS hoặc phiên bản cloud).
3. **Nhấp vào "Import"** và chọn file JSON vừa tải.
4. **Chọn "Import"** – workflow sẽ xuất hiện trên canvas.

#### **Phương pháp 2: Copy/Paste JSON**
1. **Tải file JSON** từ link trên.
2. **Mở n8n Editor** → **Nhấp vào "Import"** → **Chọn "Paste JSON"** → Dán nội dung file vào.
3. **Nhấp "Import"** để hoàn tất.

---
### **2. Các bước cấu hình BẮT BUỘC phải chỉnh 📌**

#### **🔹 Bước 1: Cài đặt Node GotoHuman (Nếu chưa có)**
- **Trước khi import**, các sếp phải **cài đặt node GotoHuman** vào n8n:
  1. Mở **n8n Editor** → **Nhấp vào "Add Node"** → **Search "gotoHuman"** → **Chọn và thêm vào canvas**.
  2. **Không cần cấu hình gì** tại bước này, chỉ cần node này tồn tại là đủ.

#### **🔹 Bước 2: Cấu hình Credentials cho các Node**
Sau khi import, các sếp cần **cấu hình credentials** cho các node quan trọng:

| **Node**               | **Tham số cần điền**               | **Hướng dẫn**                                                                 |
|------------------------|-------------------------------------|-------------------------------------------------------------------------------|
| **New Email (gmailTrigger)** | Chọn tài khoản Gmail | Nhấp vào node → **Credentials** → Chọn tài khoản Gmail muốn lấy email. |
| **OpenAI Chat Model**  | API Key OpenAI                   | Tạo API Key tại [OpenAI](https://platform.openai.com/account/api-keys) → Điền vào **Credentials** của node. |
| **gotoHuman**          | API Key GotoHuman + Template ID     | - API Key: Tạo tại [GotoHuman](https://app.gotohuman.com/) → Điền vào **Credentials**. <br> - **Template ID**: `v81wzxwYoFYvWpmuIBgX` (đã cung cấp). <br> - **Template Name**: Chọn "Email Smart Reply" (sau khi import template). |

#### **🔹 Bước 3: Cập nhật Prompt (Nếu cần)**
Workflow sử dụng **2 prompt chính**:
1. **Prompt phân loại email** (node **AI Classifier**).
2. **Prompt viết trả lời** (node **AI Email Writer**).

**Cách chỉnh sửa:**
1. Nhấp vào node **Set Prompt** → **Chọn "Edit"** → **Chỉnh sửa nội dung prompt** theo yêu cầu.
   - Ví dụ: Thêm các **danh mục email mới** (ví dụ: "Hỗ trợ tài khoản VIP", "Phản ánh sản phẩm").
   - Cập nhật **tôn chỉ brand** (ví dụ: "Tôn trọng khách hàng", "Trả lời trong 24h").
2. Nhấp vào node **Set (edited) prompt** → **Làm tương tự** nếu cần chỉnh sửa prompt viết trả lời.

#### **🔹 Bước 4: Kiểm tra và Bật Workflow**
1. **Test Run** với email mẫu:
   - Gửi một email mẫu vào Gmail (đã kết nối).
   - Nhấp vào **Play Button (▶)** trên node **New Email** để chạy workflow.
   - Kiểm tra kết quả:
     - Email có được phân loại đúng không?
     - Trả lời AI có hợp lý không?
     - Nếu cần sửa đổi, **nhân viên sẽ review trên GotoHuman**.
2. **Bật Active**:
   - Sau khi test thành công, **nhấp vào "Active"** trên workflow.

---

### ✍️ **Mẹo & Gợi ý Nâng Cao**

#### **🔹 1. Tối ưu hóa Prompt cho Dịch Vụ Hỗ Trợ Khách Hàng**
- **Thêm các trường hợp đặc biệt** vào prompt phân loại:
  ```json
  "Danh mục": [
    "Hỗ trợ kỹ thuật",
    "Phản ánh sản phẩm",
    "Đặt hàng mới",
    "Hỏi giá",
    "Yêu cầu hoàn tiền",
    "Khiếu nại",
    "Thông tin chung"
  ]
  ```
- **Định nghĩa rõ ràng** các trường hợp cần **phê duyệt nhân sự**:
  ```json
  "Nếu email chứa từ khóa: 'hoàn tiền', 'khiếu nại', 'sai sót', 'hủy đơn' → Yêu cầu phê duyệt."
  ```

#### **🔹 2. Lưu Log Email & Trả Lời (Dùng Node StickyNote)**
- Thêm **node StickyNote** sau **Reply to thread** để lưu:
  - Nội dung email gốc.
  - Trả lời AI.
  - Trả lời cuối cùng (sau khi phê duyệt).
- **Cách làm**:
  1. Thêm node **StickyNote** vào workflow.
  2. Kết nối với node **Reply to thread**.
  3. Chọn **Save to Execution Data** → **Lưu vào biến `email_log`**.

#### **🔹 3. Gửi Báo Cáo Định Kỳ (Dùng Node Email hoặc Slack)**
- **Cài đặt node Email/Slack** để gửi báo cáo hàng ngày:
  - **Dữ liệu báo cáo**:
    - Số email đã xử lý.
    - Số email cần phê duyệt.
    - Thời gian phản hồi trung bình.
  - **Cách làm**:
    1. Thêm node **Email** hoặc **Slack**.
    2. Kết nối với **StickyNote** (để lấy dữ liệu).
    3. Sử dụng **node Set** để tính toán thống kê.
    4. **Chạy hàng ngày** bằng **node Schedule** (n8n Pro).

#### **🔹 4. Kết hợp với CRM (Salesforce, HubSpot)**
- Nếu doanh nghiệp sử dụng **CRM**, có thể:
  - **Tự động tạo ticket** trong CRM khi email cần phê duyệt.
  - **Cập nhật trạng thái** của email trong CRM sau khi gửi trả lời.
- **Cách làm**:
  1. Thêm node **Salesforce/HubSpot**.
  2. Kết nối với node **gotoHuman** (trước khi gửi trả lời).

#### **🔹 5. Sử dụng GPT-4o-mini thay vì GPT-4 (Giảm chi phí)**
- Workflow đã mặc định sử dụng **GPT-4o-mini** (rẻ hơn GPT-4).
- **Nếu muốn nâng cấp**:
  - Đổi model trong node **OpenAI Chat Model** → Chọn **gpt-4o** (tốn nhiều hơn).

---

## 📌 **Kết Luận: Áp Dụng Ngay Để Tiết Kiệm Thời Gian & Tăng Trải Nghiệm Khách Hàng**

Workflow này **giải phóng đội ngũ hỗ trợ** khỏi công việc lặp lại, đồng thời **đảm bảo chất lượng cao nhất** với hệ thống **kiểm duyệt nhân sự**. Các sếp có thể:
✅ **Tự động hóa 90% email** (phân loại + viết trả lời).
✅ **Giảm sai sót** nhờ AI + kiểm tra nhân sự.
✅ **Tiết kiệm thời gian** để tập trung vào công việc chiến lược.
✅ **Mở rộng** cho nhiều dịch vụ khác (chăm sóc khách hàng, bán hàng,...).

**Bắt đầu ngay!**
1. **Cài đặt VPS** (nếu chưa có).
2. **Import workflow** và **cấu hình credentials**.
3. **Test với email mẫu**.
4. **Bật Active** và **đón chờ tự động hóa!**

---
**🚀 Cần hỗ trợ thêm?** Đăng ký **hỗ trợ kỹ thuật n8n** tại:
👉 [TinoHost - Hỗ trợ n8n](https://tino.vn/hotline)
👉 [XeonHost - Hỗ trợ tự động hóa](https://my.bnix.one/support)