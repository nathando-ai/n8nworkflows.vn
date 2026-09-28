---
title: "🚀 Đồng bộ người dùng Entra sang Zammad tự động 100% không cần code"
description: "Tự động đồng bộ người dùng và nhóm từ Microsoft Entra (Azure AD) sang Zammad, giảm công việc thủ công, luôn cập nhật chính xác."
slug: "dong-bo-nguoi-dung-entra-zo-zammad"
tags: [n8n, automation, no-code, azure, zammad, hr]
keywords: [n8n workflow, tự động hóa, Entra, Zammad, đồng bộ người dùng]
---

# 🚀 Đồng bộ người dùng Entra sang Zammad tự động 100% không cần code

Khi quản lý **HR, IT Ops** hoặc **Support**, việc duy trì đồng bộ danh sách người dùng giữa Microsoft Entra (Azure AD) và hệ thống ticket Zammad thường gặp những rắc rối:

* **Nhập liệu thủ công**: Xuất danh sách từ Entra, sau đó tạo hoặc cập nhật từng người dùng trong Zammad – tốn hàng giờ.
* **Dữ liệu lỗi thời**: Khi nhân viên rời công ty hoặc chuyển phòng ban, thông tin trên Zammad không được cập nhật kịp thời → ticket sai người phụ trách.
* **Rủi ro bảo mật**: Người dùng không còn hoạt động vẫn còn tài khoản trong Zammad, mở cửa cho các lỗ hổng tiềm ẩn.

Workflow **“Sync Entra User to Zammad User”** giải quyết toàn bộ vấn đề trên bằng cách **tự động đồng bộ 2‑chiều**:  
- Lấy nhóm và người dùng từ Entra.  
- So sánh với danh sách hiện có trong Zammad.  
- Tự động **tạo**, **cập nhật** hoặc **vô hiệu hoá** tài khoản Zammad tương ứng.  

> Không cần viết một dòng code nào – chỉ cần cấu hình các node và cung cấp credentials.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self‑hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Loại bỏ công việc xuất‑nhập thủ công, chỉ một lần thiết lập.
- **Độ chính xác 100%**: So sánh dữ liệu tự động, giảm lỗi nhập sai.
- **Cập nhật liên tục**: Khi người dùng thay đổi trong Entra, Zammad được đồng bộ ngay lập tức.
- **Bảo mật**: Người dùng không còn hoạt động sẽ tự động bị vô hiệu hoá trong Zammad.
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
1. **Tài khoản Microsoft Entra (Azure AD)** với quyền **Read groups & members**.  
2. **API credentials**:
   - `microsoftOAuth2Api` hoặc `microsoftGraphSecurityOAuth2Api` (client ID, client secret, tenant ID).  
3. **Zammad**:
   - Token API (`zammadTokenAuthApi`) có quyền **read, create, update** người dùng.  
4. **n8n** (phiên bản mới nhất) đã cài đặt và có quyền truy cập internet để gọi API Microsoft & Zammad.  
5. (Tùy chọn) **Webhook URL** nếu muốn kích hoạt workflow tự động theo lịch hoặc webhook từ Entra.  
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Mở n8n → **Workflows** → **Import**.  
2. Chọn **Upload JSON** và tải file `Sync Entra User to Zammad User.json` (tải từ link gốc: https://n8n.io/workflows/2587).  
3. Hoặc **Copy/Paste** nội dung JSON vào ô **Import from Clipboard** và nhấn **Import**.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Dưới đây là các node quan trọng và cách cấu hình chúng:

| Node | Mô tả | Cấu hình cần thay đổi |
|------|------|----------------------|
| **When clicking ‘Test workflow’** (Manual Trigger) | Dùng để test nhanh workflow. | Không cần thay đổi. |
| **Get Groups from Entra** (HTTP Request) | Gọi API Microsoft Graph để lấy danh sách nhóm. | - Chọn **Credentials**: `microsoftOAuth2Api` hoặc `microsoftGraphSecurityOAuth2Api`. <br> - URL: `https://graph.microsoft.com/v1.0/groups?$filter=mailEnabled eq false and securityEnabled eq true` (hoặc tùy chỉnh). |
| **Remove outer Array** (SplitOut) | Tách mảng nhóm ra từng item. | Không cần cấu hình. |
| **Select Entra Zammad default Group** (If) | Lọc ra nhóm **Zammad default** (tên nhóm được định nghĩa trong workflow). | - Trong **Condition**, nhập tên nhóm Entra mà bạn muốn đồng bộ (ví dụ: `Zammad Users`). |
| **Remove outer Array from Entra User** (SplitOut) | Tách danh sách thành từng người dùng. | Không cần cấu hình. |
| **Zammad Universal User Object** (Set) | Tạo mẫu đối tượng người dùng Zammad chuẩn. | - Map các trường: `login`, `firstname`, `lastname`, `email`, `organization_id`… <br> - Đảm bảo các trường khớp với dữ liệu từ Entra (sử dụng **Expression** như `{{$json["mail"]}}`). |
| **Get Zammad Users** (Zammad – Get All) | Lấy toàn bộ người dùng hiện có trong Zammad. | - Chọn **Credentials**: `zammadTokenAuthApi`. |
| **Merge** (Merge) | Gộp danh sách người dùng Entra và Zammad để so sánh. | - **Mode**: `Pass Through` hoặc `Append`. |
| **Get Members of the default group** (HTTP Request) | Lấy danh sách thành viên của nhóm Entra đã chọn. | - Credentials: Microsoft OAuth. <br> - URL: `https://graph.microsoft.com/v1.0/groups/{groupId}/members`. |
| **Find new Zammad Users** (Compare Datasets) | Xác định người dùng mới chưa tồn tại trong Zammad. | - **Key**: `email` hoặc `login`. |
| **Update Zammad User** (Zammad – Update) | Cập nhật thông tin người dùng đã tồn tại. | - Chọn **Credentials**: `zammadTokenAuthApi`. <br> - Đặt **User ID** từ kết quả `Find new Zammad Users`. |
| **Create Zammad User** (Zammad – Create) | Tạo người dùng mới trong Zammad. | - Credentials: `zammadTokenAuthApi`. <br> - Dùng dữ liệu từ **Zammad Universal User Object**. |
| **Deactivate Zammad User** (Zammad – Update) | Vô hiệu hoá người dùng đã rời Entra. | - Credentials: `zammadTokenAuthApi`. <br> - Đặt `active: false`. |
| **Find removed Users** (Compare Datasets) | So sánh để tìm người dùng đã bị xóa khỏi Entra. | - **Key**: `email`. |
| **If** (If) | Kiểm tra có người dùng cần vô hiệu hoá không. | - Condition: `{{ $json["exists"] === false }}`. |
| **Select only active Users and entra_obect_type="user"** (If) | Lọc chỉ người dùng thực sự (không phải group). | - Condition: `{{ $json["objectType"] === "user" && $json["active"] === true }}`. |

> **Lưu ý:** Đảm bảo **Scope** trong Azure AD app bao gồm `Group.Read.All` và `User.Read.All`. Nếu API trả về lỗi 403, kiểm tra lại quyền và consent.

#### 3. Kích hoạt ⚡️
1. **Test** workflow bằng nút **Execute Workflow** → kiểm tra log từng node.  
2. Khi mọi thứ ổn, bật **Active** (toggle ở góc trên bên phải).  
3. (Tùy chọn) Đặt **Cron** hoặc **Webhook** để tự động chạy hàng ngày/giờ.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm Slack/Telegram**: Sau khi đồng bộ, dùng node **Slack** hoặc **Telegram** gửi thông báo cho admin về số lượng người dùng mới, cập nhật, hoặc bị vô hiệu hoá.  
- **Lưu log vào Google Sheet**: Dùng node **Google Sheets** để ghi lại lịch sử đồng bộ, giúp audit và phân tích xu hướng.  
- **Xử lý đa nhóm**: Sao chép phần **Get Groups** + **If** để đồng bộ nhiều nhóm Entra vào các tổ chức (organizations) khác nhau trong Zammad.  
- **Retry & Alert**: Dùng node **Error Trigger** + **Email** để gửi cảnh báo khi có lỗi API (quota, token hết hạn).  

### 📌 Kết luận
Với workflow **Sync Entra User to Zammad User**, các sếp có thể **tự động đồng bộ người dùng** giữa Entra và Zammad chỉ trong vài phút thiết lập, giảm thiểu lỗi thủ công, tăng tốc độ phản hồi support và nâng cao bảo mật. Hãy triển khai ngay hôm nay, để đội ngũ IT & HR của bạn tập trung vào công việc chiến lược hơn là quản lý tài khoản! 🚀