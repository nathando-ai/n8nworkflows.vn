---
title: "📊 Tự Động Tạo Báo Cáo Kết Quả Marketing qua Email với Google Sheets & Outlook (n8n)"
description: "Workflow tự động hóa hoàn toàn không cần code để tổng hợp dữ liệu marketing từ Google Sheets, tính toán chỉ số KPI quan trọng và gửi báo cáo định kỳ qua Outlook. Giúp các sếp tiết kiệm 10+ giờ/tháng và đưa ra quyết định dựa trên dữ liệu chính xác."
slug: "tieu-dong-tao-bao-cao-marketing-google-sheets-outlook"
tags: [n8n, automation, marketing, google-sheets, microsoft-outlook, no-code, ai-data-analysis]
keywords: [tự động hóa marketing, báo cáo kết quả quảng cáo, google sheets automation, n8n workflow marketing, tổng hợp dữ liệu marketing, gửi báo cáo email tự động]
---

# 🚀 **Tự Động Tạo Báo Cáo Kết Quả Marketing qua Email với Google Sheets & Outlook**

### **Giải pháp cho nỗi đau "Tôi phải tính toán và tổng hợp dữ liệu marketing thủ công hàng ngày"**
Các sếp marketing hay team quảng cáo thường phải mất **10-15 giờ/tuần** để:
- Lấy dữ liệu từ Google Sheets (hoặc Excel) về các chiến dịch quảng cáo.
- Tính toán **số lượng khách hàng duy nhất**, **tổng số click**, **tỷ lệ chuyển đổi**, và **chi phí tổng**.
- Viết báo cáo và gửi qua email cho team hoặc khách hàng.

**Workflow này tự động hóa toàn bộ quá trình** chỉ với một cú nhấp chuột! Sau khi cấu hình xong, hệ thống sẽ:
✅ **Tự động lấy dữ liệu** từ Google Sheets.
✅ **Tính toán tự động** tất cả chỉ số KPI quan trọng.
✅ **Tạo email báo cáo chuyên nghiệp** với thiết kế hiện đại (glassmorphic, responsive).
✅ **Gửi báo cáo định kỳ** (hàng ngày, hàng tuần) qua Outlook.

---
### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm 10+ giờ/tháng** cho việc tổng hợp và gửi báo cáo.
- **Dữ liệu chính xác 100%** (không sai sót như tính thủ công).
- **Báo cáo chuyên nghiệp** với thiết kế hiện đại, dễ đọc trên mọi thiết bị.
- **Hoạt động 24/7** mà không cần can thiệp của con người.
- **Cá nhân hóa** dễ dàng (thay đổi email nhận, chủ đề, hoặc nội dung).
:::

---
### 🔧 **Yêu cầu cần thiết**
:::info[CHUẨN BỊ]
Trước khi sử dụng workflow, các sếp cần chuẩn bị:
1. **Tài khoản Google Sheets** với dữ liệu mẫu đã cấu trúc (xem hướng dẫn dưới đây).
2. **Tài khoản Microsoft Outlook** (để gửi email báo cáo).
3. **API Key hoặc OAuth2 Credentials** cho:
   - **Google Sheets API** (để đọc dữ liệu).
   - **Microsoft Outlook API** (để gửi email).
4. **n8n Self-hosted** (không dùng phiên bản miễn phí trên cloud để đảm bảo hoạt động liên tục).
:::

---
### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Cách 1:** Tải file JSON từ [n8n.io/workflows/7404](https://n8n.io/workflows/7404) và import vào n8n Editor.
- **Cách 2:** Copy toàn bộ JSON từ [đây](https://n8n.io/workflows/7404) và dán vào **Import Workflow** trong n8n.
- **Cách 3:** Sử dụng liên kết trực tiếp:
  ```bash
  https://n8n.io/workflows/7404
  ```

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
##### **📄 Cấu trúc dữ liệu Google Sheets**
Workflow **yêu cầu** Google Sheets có **tab "Data"** với các cột sau:
| **Customer ID** (ID khách hàng duy nhất) | **Campaign** (Tên chiến dịch) | **Clicks** (Số lần click) | **Conversions** (Số lần chuyển đổi) | **Spend ($)** (Chi phí chi tiêu) |
|------------------------------------------|-------------------------------|---------------------------|--------------------------------------|----------------------------------|
| `CUST001`                              | `Facebook Ads 2024`           | `1200`                    | `85`                                 | `5000`                           |

**Hướng dẫn thiết lập:**
1. Tải **mẫu dữ liệu** từ [đây](https://docs.google.com/spreadsheets/d/19aUQYZq02qHsCelO4eeV4sx_MTJJupC5qe0gDLQBtRA/edit?usp=sharing).
2. Nhấn **File → Make a copy** để sao chép.
3. Đổi tên thành **"My Marketing Performance"** và điền dữ liệu thực tế.

##### **🔐 Cấu hình Google Sheets API**
1. Truy cập [Google Cloud Console](https://console.cloud.google.com/).
2. Tạo **một dự án mới** hoặc chọn dự án hiện có.
3. Bật **Google Sheets API**:
   - Nhấn **Enable APIs and Services → Library**.
   - Tìm và bật **Google Sheets API**.
4. **Tạo OAuth2 Credentials**:
   - Nhấn **Credentials → Create Credentials → OAuth client ID**.
   - Chọn **Web application**.
   - Thêm `https://your-n8n-instance.com` vào **Authorized JavaScript origins**.
   - Nhấn **Save**.
5. **Chia sẻ Google Sheet với service account**:
   - Sao chép email của **service account** (kết thúc bằng `@appspot.gserviceaccount.com`).
   - Trong Google Sheets, nhấn **Share → Add people → Email của service account**.
   - Chọn quyền **Editor**.

##### **✉️ Cấu hình Microsoft Outlook**
1. Trong node **"Send Email Report"**, nhấn **Create New Credential**.
2. Chọn **Microsoft Outlook OAuth2**.
3. Đăng nhập tài khoản Outlook và cấp quyền.
4. **Cấu hình email**:
   - **To Recipients**: Thay `rbreen@ynteractive.com` thành email của bạn (hoặc team).
   - **Subject**: Thay `Daily Marketing Performance` thành chủ đề phù hợp (ví dụ: `Báo cáo KPI Chiến dịch [Tên Chiến dịch]`).
   - **Body Content**: Email đã được thiết kế sẵn với **thiết kế glassmorphic**, **responsive**, và **hover effects**.

##### **🔄 Cấu hình Node "Merge"**
- Node này **không cần thiết phải chỉnh sửa** vì đã được cấu hình sẵn để **ghép tất cả dữ liệu** từ các node tính toán (Customer, Campaign, Clicks, Conversions, Spend) thành một object duy nhất.

---
#### **3. Kích hoạt ⚡️**
1. **Test Run** với dữ liệu mẫu:
   - Nhấn **Execute Workflow** để kiểm tra email báo cáo có được gửi đúng không.
   - Kiểm tra **các chỉ số tính toán** (Unique Customers, Total Clicks, etc.) có chính xác không.
2. **Bật Active**:
   - Sau khi kiểm tra thành công, nhấn **Active** để workflow hoạt động tự động.

---
### ✍️ **Mẹo & gợi ý nâng cao**
:::info[NHỮNG Ý TƯỞNG MỞ RỘNG]
1. **Gửi báo cáo định kỳ tự động**:
   - Sử dụng **n8n Trigger Node (Schedule)** để chạy workflow hàng ngày/lần tuần thay vì dùng **Manual Trigger**.
   - Ví dụ: `0 9 * * *` (chạy lúc 9h sáng hàng ngày).

2. **Kết hợp với Slack/Telegram**:
   - Thêm node **Slack Webhook** hoặc **Telegram Bot** để thông báo khi báo cáo được gửi thành công.

3. **Lưu log hoạt động**:
   - Sử dụng node **Google Drive** hoặc **Airtable** để lưu lịch sử báo cáo.

4. **Tính toán thêm chỉ số AI**:
   - Thêm node **n8n-nodes-base.llm** (nếu có API OpenAI) để tự động **tóm tắt xu hướng** trong báo cáo.

5. **Cá nhân hóa email**:
   - Thay đổi **template email** bằng **n8n-nodes-base.template** để thêm logo, thông tin cá nhân, hoặc dữ liệu động.
:::

---
### 📌 **Kết luận**
Workflow này **giải phóng thời gian** cho các sếp marketing khỏi công việc thủ công, đồng thời **cung cấp báo cáo chuyên nghiệp** với dữ liệu chính xác. **Chỉ cần 30 phút để cấu hình**, sau đó hệ thống sẽ hoạt động tự động **một cách hiệu quả**.

**Hành động ngay hôm nay:**
1. **Cài đặt n8n Self-hosted** trên VPS (để đảm bảo hoạt động 24/7).
2. **Import workflow** và theo dõi hướng dẫn chi tiết trên bài viết này.
3. **Thử nghiệm với dữ liệu thật** và bắt đầu tự động hóa!

---
:::note[💡 LƯU Ý CUỐI CÙNG]
- **Không dùng phiên bản n8n cloud** vì nó ngừng hoạt động khi không hoạt động.
- **Nếu gặp lỗi**, liên hệ tác giả **Robert Breen** qua [email](mailto:robert@ynteractive.com) hoặc [LinkedIn](https://www.linkedin.com/in/robert-breen-29429625/).
- **Cập nhật dữ liệu thường xuyên** để báo cáo luôn mới nhất!
:::

---
:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::