---
title: "🚀 Tự Động Hoàn Thành Nghiên Cứu Profile Creator Kuaishou Từ Từ Khóa (JustOneAPI) - Không Cần Code"
description: "Workflow này tự động tra cứu, phân tích và tổng hợp thông tin chi tiết của các creator Kuaishou từ bất kỳ từ khóa nào, giúp các sếp tiết kiệm thời gian nghiên cứu thị trường lên đến 80%. Kết quả được xuất dưới dạng danh sách profile đầy đủ, sẵn sàng sử dụng cho chiến dịch marketing hoặc phân tích đối thủ."
slug: "tieu-dong-hoan-thanh-nghien-cuu-profile-creator-kuaishou"
tags: [n8n, automation, market-research, justoneapi, no-code]
keywords: [n8n workflow nghiên cứu creator Kuaishou, tự động hóa tra cứu creator Kuaishou, JustOneAPI API integration, phân tích đối thủ thị trường Kuaishou, tự động hóa marketing]
---

# 🚀 Tự Động Hoàn Thành Nghiên Cứu Profile Creator Kuaishou Từ Từ Khóa (JustOneAPI)

## 📌 **Nỗi Đau Của Các Sếp Khi Nghiên Cứu Creator Kuaishou Thủ Công**
Hàng ngày, các sếp phải mất **giờ đồng hồ** để:
- Tra cứu danh sách creator Kuaishou từ từ khóa cụ thể (nhãn hàng, chủ đề, khu vực...).
- Lọc và kiểm tra từng profile để đảm bảo tính chính xác.
- Tổng hợp thông tin chi tiết (độ nổi tiếng, nội dung phổ biến, tương tác,...) để so sánh với đối thủ.
- Lưu trữ và cập nhật dữ liệu một cách thủ công, dễ bị lỗi hoặc thiếu sót.

**Workflow này giải quyết tất cả những vấn đề trên bằng cách tự động hóa toàn bộ quy trình từ tra cứu đến tổng hợp profile, chỉ trong vài giây!**

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết Quả Các Sếp Nhận Được**
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Thay vì mất 3-5 giờ/lần, chỉ cần **nhấp chuột kích hoạt workflow** (thời gian thực hiện < 1 phút).
- **Dữ liệu chính xác**: Tra cứu toàn bộ profile từ API JustOneAPI, không bị lỗi như tra cứu thủ công.
- **Danh sách profile đầy đủ**: Nhận thông tin chi tiết (tên, ID, số follower, nội dung phổ biến, tương tác,...) của **tất cả creator** phù hợp với từ khóa.
- **Cập nhật liên tục**: Có thể kích hoạt workflow định kỳ (hàng ngày/tuần) để theo dõi thay đổi của creator.
- **Sẵn sàng sử dụng**: Dữ liệu được xuất dưới dạng JSON hoặc có thể kết nối với Google Sheets/Excel để phân tích sâu hơn.
:::

---

### 🔧 **Yêu Cầu Cần Thiết**
Trước khi bắt đầu, các sếp cần chuẩn bị:
1. **Tài khoản JustOneAPI**:
   - [Đăng ký tài khoản JustOneAPI](https://justoneapi.com/) (miễn phí hoặc trả phí tùy nhu cầu).
   - **API Key**: Tạo và sao chép `API Key` từ dashboard JustOneAPI.
   - **Base URL**: Địa chỉ API của JustOneAPI (thường là `https://api.justoneapi.com`).
2. **Từ khóa nghiên cứu**:
   - Danh sách từ khóa creator Kuaishou muốn tra cứu (ví dụ: "đồ uống năng lượng", "thời trang nam", "du lịch Việt Nam").
3. **N8n Editor**:
   - Tài khoản n8n (cài đặt self-hosted hoặc dùng phiên bản cloud miễn phí).

---

### 🚀 **Cách Import & Lưu Ý Khi "Lên Đồ"**

#### **1. Import Workflow 📥**
Các sếp có thể import workflow từ file JSON hoặc copy/paste mã JSON vào **n8n Editor**:
- **Tải file JSON**: Tải workflow từ [đây](https://n8n.io/workflows/16012) (hoặc sao chép mã JSON từ trang này).
- **Import vào n8n**:
  1. Mở **n8n Editor** (trang chủ của workflow).
  2. Nhấp vào **Import** (icon "↑" ở góc trên bên phải).
  3. Chọn file JSON hoặc dán mã JSON vào ô **Paste JSON**.
  4. Nhấp **Import**.

#### **2. Các Lưu Ý (BẮT BUỘC) Phải Chỉnh 📌**
Workflow này có **10 node** chính, các sếp cần chú ý cấu hình các node sau:

##### **Node 1: Manual Execution Trigger**
- **Chức năng**: Kích hoạt workflow thủ công.
- **Lưu ý**: Không cần chỉnh sửa gì, chỉ cần nhấp vào nút **Run Workflow** khi cần.

##### **Node 2: Set API and Research Parameters**
- **Chức năng**: Điền thông tin API và từ khóa tra cứu.
- **Cấu hình cần thiết**:
  - **API Key**: Dán `API Key` từ JustOneAPI vào trường `JustOneAPIKey`.
  - **Base URL**: Điền `https://api.justoneapi.com`.
  - **Keyword**: Nhập từ khóa muốn tra cứu (ví dụ: `"sữa chua"`).
  - **Limit**: Số lượng kết quả trả về (mặc định là 100, có thể điều chỉnh).

##### **Node 3: Fetch Kuaishou Users by Keyword**
- **Chức năng**: Gửi yêu cầu API tra cứu creator Kuaishou.
- **Lưu ý**:
  - **Endpoint**: Địa chỉ API của JustOneAPI để tra cứu creator (thường là `https://api.justoneapi.com/kuaishou/search`).
  - **Headers**: Thêm `Authorization: Bearer {JustOneAPIKey}` vào headers.
  - **Body**: Sử dụng cấu trúc JSON như sau:
    ```json
    {
      "keyword": "{{ $node["Set API and Research Parameters"].json["keyword"] }}",
      "limit": "{{ $node["Set API and Research Parameters"].json["limit"] }}"
    }
    ```

##### **Node 4-5: Parse User IDs from Results & Output Parsed User IDs**
- **Chức năng**: Lọc và trích xuất ID của các creator từ kết quả tra cứu.
- **Lưu ý**:
  - Node **Code** này sử dụng JavaScript để lọc ID. Các sếp **không cần chỉnh sửa** mã code, trừ khi muốn thay đổi logic lọc.
  - Kết quả sẽ là danh sách ID creator dưới dạng JSON.

##### **Node 6: Check User ID Exists**
- **Chức năng**: Kiểm tra xem ID creator có tồn tại hay không.
- **Lưu ý**:
  - Node **If** này sẽ lọc bỏ ID không hợp lệ.
  - **Condition**: Sử dụng `{{ $node["Parse User IDs from Results"].json["userIds"] }}` để kiểm tra.

##### **Node 7: Fetch Kuaishou User Details**
- **Chức năng**: Tra cứu chi tiết profile của từng creator.
- **Lưu ý**:
  - **Endpoint**: Địa chỉ API tra cứu chi tiết creator (ví dụ: `https://api.justoneapi.com/kuaishou/user/{userId}`).
  - **Headers**: Thêm `Authorization: Bearer {JustOneAPIKey}`.
  - **Dynamic User ID**: Sử dụng `{{ $node["Check User ID Exists"].json["userId"] }}` để truyền ID creator vào API.

##### **Node 8-9: Build User Profile Data List & Output User Profile Data**
- **Chức năng**: Tổng hợp và xuất danh sách profile đầy đủ.
- **Lưu ý**:
  - Node **Code** này kết hợp dữ liệu từ các node trước để tạo danh sách profile.
  - **Output**: Kết quả sẽ là danh sách JSON chứa thông tin chi tiết của tất cả creator (tên, ID, số follower, nội dung phổ biến,...).

#### **3. Kích Hoạt ⚡️**
1. **Test Run**:
   - Nhấp vào nút **Run Workflow** để chạy thử với dữ liệu mẫu.
   - Kiểm tra kết quả ở node **Output User Profile Data** để đảm bảo dữ liệu chính xác.
2. **Active Workflow**:
   - Sau khi kiểm tra, nhấp vào **Active** để bật workflow.

---

### ✍️ **Mẹo & Gợi Ý Nâng Cao**
1. **Kết Nối Với Google Sheets/Excel**:
   - Sử dụng node **Google Sheets** để lưu kết quả vào bảng tính tự động.
   - Cách làm: Thêm node **Google Sheets** vào cuối workflow và cấu hình:
     - **Sheet Name**: Tên bảng muốn lưu.
     - **Range**: `A1` (để ghi dữ liệu từ ô A1).
     - **Data**: Chọn `{{ $node["Output User Profile Data"].json }}`.

2. **Gửi Báo Cáo Định Kỳ**:
   - Kết hợp với **n8n Scheduler** để kích hoạt workflow hàng ngày/tuần.
   - Cách làm:
     1. Thêm node **n8n-nodes-base.schedule**.
     2. Cấu hình lịch chạy (ví dụ: hàng ngày lúc 8h sáng).
     3. Kết nối với node **Manual Execution Trigger**.

3. **Lưu Log Dữ Liệu**:
   - Thêm node **n8n-nodes-base.fileSystem** để lưu log của workflow.
   - Cách làm:
     - Chọn thư mục lưu (ví dụ: `/data/logs/kuaishou`).
     - Ghi dữ liệu từ node **Output User Profile Data** vào file JSON.

4. **Tích Hợp Slack/Telegram**:
   - Gửi thông báo kết quả tra cứu qua Slack/Telegram.
   - Cách làm:
     - Thêm node **Slack** hoặc **Telegram Bot**.
     - Cấu hình message template:
       ```json
       {
         "text": "📊 Kết quả tra cứu creator Kuaishou từ từ khóa '{{ $node["Set API and Research Parameters"].json["keyword"] }}':\n\n- Tổng số creator: {{ $node["Output User Profile Data"].json["length"] }}\n- Danh sách: {{ $node["Output User Profile Data"].json }}"
       }
       ```

---

### 📌 **Kết Luận**
Workflow này là **giải pháp hoàn hảo** cho các sếp cần nghiên cứu thị trường Kuaishou một cách nhanh chóng và chính xác. Bằng cách tự động hóa toàn bộ quy trình từ tra cứu đến tổng hợp profile, các sếp sẽ:
- **Tiết kiệm thời gian** lên đến 80% so với phương pháp thủ công.
- **Nhận dữ liệu đầy đủ và chính xác** từ API JustOneAPI.
- **Cập nhật liên tục** thông tin creator để theo dõi xu hướng thị trường.

**Hành động ngay hôm nay!**
1. **Chuẩn bị tài khoản JustOneAPI** và API Key.
2. **Import workflow** vào n8n Editor.
3. **Chỉnh sửa các node quan trọng** như hướng dẫn trên.
4. **Kích hoạt và chạy thử** để xem kết quả!

Nếu có bất kỳ câu hỏi hoặc gặp khó khăn, hãy để lại comment bên dưới. Chúc các sếp thành công với chiến dịch nghiên cứu của mình! 🚀

---