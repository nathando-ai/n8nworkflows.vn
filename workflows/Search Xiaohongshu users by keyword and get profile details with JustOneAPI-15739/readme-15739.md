---
title: "🔍 Tự Động Tìm Kiếm & Lấy Thông Tin Chi Tiết Người Dùng Xiaohongshu (小红书) Với JustOneAPI - Không Cần Code!"
description: "Workflow tự động hóa tìm kiếm người dùng Xiaohongshu theo từ khóa và lấy thông tin chi tiết (tên, ảnh đại diện, bài viết, tương tác...) chỉ trong vài giây. Giúp các sếp nghiên cứu thị trường, phân tích đối thủ và xây dựng chiến lược marketing hiệu quả."
slug: "tu-dong-hoa-tim-kiem-xiaohongshu-justoneapi"
tags: [n8n, automation, market-research, social-media-analytics, justoneapi]
keywords: [tự động hóa n8n, tìm kiếm người dùng Xiaohongshu, JustOneAPI, nghiên cứu thị trường, phân tích đối thủ, marketing digital]
---

# 🚀 **Tự Động Tìm Kiếm & Lấy Thông Tin Người Dùng Xiaohongshu (小红书) Với JustOneAPI**

### **Giải pháp cho các sếp muốn nghiên cứu thị trường, phân tích đối thủ và tối ưu chiến lược marketing trên Xiaohongshu**

Xiaohongshu (小红书) là nền tảng mạng xã hội nổi tiếng tại Trung Quốc với hơn **300 triệu người dùng** hàng tháng. Tuy nhiên, việc tìm kiếm và phân tích thông tin người dùng thủ công là **rất tốn thời gian và không hiệu quả**. Bằng cách sử dụng **n8n + JustOneAPI**, các sếp có thể **tự động hóa toàn bộ quy trình** chỉ trong vài giây, giúp:
✅ **Tìm kiếm người dùng** theo từ khóa, tên hoặc lĩnh vực
✅ **Lấy thông tin chi tiết** (tên, ảnh đại diện, bài viết, số người theo dõi, tương tác...)
✅ **Xuất dữ liệu** dưới dạng JSON hoặc CSV để phân tích sâu
✅ **Tiết kiệm thời gian** so với cách làm thủ công (từ **30 phút/lần** xuống còn **vài giây**)

---
## 🎯 **Kết quả các sếp nhận được**
:::tip[**LỢI ÍCH CỐT LÕI**]
- **Tiết kiệm thời gian**: Không cần thủ công nhập từ khóa và tra cứu trên Xiaohongshu.
- **Dữ liệu chính xác**: Lấy thông tin từ API chính thức (JustOneAPI) thay vì scrape thủ công (rủi ro bị chặn).
- **Phân tích đối thủ**: So sánh nội dung, tương tác và chiến lược của các nhà cạnh tranh.
- **Chiến lược marketing**: Hiểu rõ xu hướng, sở thích của người dùng mục tiêu.
- **Dữ liệu sẵn sàng**: Xuất ra Excel/CSV để phân tích sâu với Power BI, Excel, hoặc Google Sheets.
:::

---
## 🔧 **Yêu cầu cần thiết**
:::info[**CHUẨN BỊ**]
Để workflow hoạt động, các sếp cần:
✔ **Tài khoản JustOneAPI** (mua gói API từ [JustOneAPI](https://www.justoneapi.com/))
✔ **API Key** của JustOneAPI (đăng ký tại [đây](https://www.justoneapi.com/))
✔ **Tài khoản n8n** (self-hosted hoặc dùng phiên bản miễn phí trên [n8n.io](https://n8n.io/))
✔ **Từ khóa tìm kiếm** (ví dụ: "sản phẩm skincare", "du lịch Trung Quốc", "mốt thời trang")
:::

---
## 🚀 **Cách import & Lưu ý khi "lên đồ"**

### **1. Import Workflow 📥**
Các sếp có thể **import workflow** từ file JSON hoặc **copy/paste JSON** vào n8n Editor:
- **Tải file JSON** từ [đây](https://n8n.io/workflows/15739) (nếu có quyền truy cập).
- **Hoặc copy toàn bộ JSON** từ [link gốc](https://n8n.io/workflows/15739) và dán vào **n8n Editor** → **Import Workflow**.

### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflow này gồm **9 node**, các sếp cần **cấu hình chính xác** các phần sau:

#### **🔹 Node 1: "Set API and Search Parameters" (n8n-nodes-base.set)**
- **Điền vào `baseUrl`**: `https://api.justoneapi.com`
- **Điền vào `apiKey`**: API Key của JustOneAPI (mua tại [JustOneAPI](https://www.justoneapi.com/))
- **Điền vào `keyword`**: Từ khóa tìm kiếm (ví dụ: `"skincare"`)
- **Điền vào `limit`**: Số lượng người dùng muốn lấy (mặc định là 10)

#### **🔹 Node 2: "Search Xiaohongshu Users by Keyword" (n8n-nodes-base.httpRequest)**
- **Method**: `GET`
- **URL**: `https://api.justoneapi.com/xiaohongshu/search/users?keyword={{ $node["Set API and Search Parameters"].json["keyword"] }}&limit={{ $node["Set API and Search Parameters"].json["limit"] }}`
- **Headers**:
  ```
  {
    "Authorization": "Bearer {{ $node["Set API and Search Parameters"].json["apiKey"] }}"
  }
  ```

#### **🔹 Node 3: "Extract User IDs from Search Results" (n8n-nodes-base.code)**
- **Mã JavaScript mặc định** (không cần chỉnh sửa nếu API trả về đúng format):
  ```javascript
  return {
    userIds: $input.all().map(item => item.data.users.map(user => user.id))
  };
  ```

#### **🔹 Node 4: "Get Xiaohongshu User Profiles" (n8n-nodes-base.httpRequest)**
- **Method**: `GET`
- **URL**: `https://api.justoneapi.com/xiaohongshu/users?ids={{ $node["Output Extracted User IDs List"].json["userIds"].join(",") }}`
- **Headers**:
  ```
  {
    "Authorization": "Bearer {{ $node["Set API and Search Parameters"].json["apiKey"] }}"
  }
  ```

#### **🔹 Node 5: "Build Combined User Profiles" (n8n-nodes-base.code)**
- **Mã JavaScript mặc định** (không cần chỉnh sửa):
  ```javascript
  return {
    profiles: $input.all().map(item => item.data.users)
  };
  ```

#### **🔹 Node 6: "Output Final User Profile Data" (n8n-nodes-base.set)**
- **Dữ liệu cuối cùng** sẽ được lưu trong `{{ $node["Build Combined User Profiles"].json["profiles"] }}`.

---
### **3. Kích hoạt ⚡️**
- **Test run** với từ khóa mẫu (ví dụ: `"skincare"`).
- **Bật Active workflow** và chạy thủ công khi cần.

---
## ✍️ **Mẹo & gợi ý nâng cao**
:::info[**CÁCH LÀM NÂNG CAO**]
- **Gửi kết quả ra Slack/Telegram**: Sử dụng node **Slack** hoặc **Telegram Bot** để thông báo khi workflow hoàn thành.
- **Lưu log vào Google Sheets**: Dùng node **Google Sheets** để ghi lại lịch sử tìm kiếm.
- **Tự động chạy hàng ngày**: Sử dụng **n8n Cron Trigger** để chạy workflow định kỳ (ví dụ: mỗi sáng 8h).
- **Phân tích dữ liệu với Python**: Xuất dữ liệu JSON ra và xử lý với **Pandas** để tìm xu hướng.
- **Kết hợp với LLM (ChatGPT)**: Sử dụng node **LLM** để tổng kết nội dung bài viết của người dùng.
:::

---
## 📌 **Kết luận**
Workflow này giúp các sếp **tự động hóa việc tìm kiếm và phân tích người dùng Xiaohongshu** một cách **nhanh chóng, chính xác và không cần code**. **Không cần phải thủ công tra cứu trên trang web**, mà chỉ cần **nhấn một nút**, dữ liệu sẽ sẵn sàng để phân tích.

👉 **Hãy áp dụng ngay** và tối ưu chiến lược marketing của mình trên Xiaohongshu!

---
:::info[**Gợi ý hạ tầng cho n8n**]
Để workflow chạy **ổn định 24/7**, các sếp nên cài **n8n trên VPS riêng (Self-hosted)**.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới **39%**)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---
**Bạn có câu hỏi về workflow này?** Hãy để lại comment bên dưới! 🚀