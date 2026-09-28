```yaml
---
title: "🎥 Tự động đăng video lên Facebook Pages/Groups bằng n8n"
description: "Hướng dẫn chi tiết cách tự động hóa việc đăng video lên Facebook Pages/Groups bằng n8n, tiết kiệm thời gian và nâng cao hiệu quả quản lý nội dung"
slug: "tu-dong-dang-video-facebook-pages-groups-n8n"
tags: [n8n, automation, social media, facebook, no-code]
keywords: [n8n workflow, tự động hóa facebook, đăng video tự động, facebook graph api]
---

# 🎥 Tự động đăng video lên Facebook Pages/Groups bằng n8n

[Các sếp] có biết không? Việc đăng video lên Facebook Pages/Groups thủ công đang tốn thời gian quý giá của đội ngũ marketing. Với workflow này, các sếp có thể tự động hóa toàn bộ quy trình từ việc chuẩn bị nội dung đến đăng tải lên các trang và nhóm Facebook của mình.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động hóa toàn bộ quy trình đăng video lên Facebook
- **Chính xác 100%**: Không còn lỗi do tay người trong quá trình đăng tải
- **Quản lý tập trung**: Theo dõi và điều chỉnh nội dung từ một nơi duy nhất
- **Tăng tương tác**: Đăng video đúng thời điểm với nội dung phù hợp
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- Tài khoản Facebook Developer với quyền `publish_video`
- Page Access Token có quyền `publish_video`
- ID của Facebook Page/Group cần đăng video
- File video cần đăng tải (có thể từ Google Drive, Dropbox, hoặc local)
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
1. Truy cập [n8n.io/workflows/13366](https://n8n.io/workflows/13366)
2. Click vào nút "Import" để tải workflow về máy
3. Trong n8n Editor, chọn "Import from File" và chọn file JSON đã tải về

Hoặc có thể copy/paste JSON sau vào n8n Editor:

```json
{
  "nodes": [
    {
      "name": "Trigger: Video Upload Form",
      "type": "formTrigger",
      "parameters": {
        "path": "e07a66ec-3718-4e19-91c5-5df1e81335f3"
      }
    },
    {
      "name": "Prepare Video Metadata",
      "type": "set"
    },
    {
      "name": "Initiate Video Upload",
      "type": "httpRequest"
    },
    {
      "name": "Merge Upload Paths",
      "type": "merge"
    },
    {
      "name": "Upload Video Chunk",
      "type": "httpRequest"
    },
    {
      "name": "Complete Video Upload",
      "type": "httpRequest"
    },
    {
      "name": "Triggered by Another Workflow",
      "type": "executeWorkflowTrigger"
    }
  ]
}
```

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌

1. **Node "Trigger: Video Upload Form"**:
   - Điền thông tin Page Access Token vào trường `access_token`
   - Điền ID của Facebook Page/Group vào trường `target_id`

2. **Node "Prepare Video Metadata"**:
   - Cấu hình các trường metadata cần thiết cho video (title, description, privacy settings...)

3. **Node "Initiate Video Upload"**:
   - Đảm bảo URL endpoint của Facebook Graph API là chính xác
   - Kiểm tra các headers và body parameters

4. **Node "Upload Video Chunk"**:
   - Điều chỉnh chunk size nếu cần (mặc định là 10MB)
   - Kiểm tra timeout và retry settings

5. **Node "Complete Video Upload"**:
   - Xác nhận các trường bắt buộc trong body request
   - Kiểm tra trường `upload_phase` được đặt thành "finish"

#### 3. Kích hoạt ⚡️
1. Sau khi cấu hình xong, click vào nút "Activate" để kích hoạt workflow
2. Test với một video mẫu nhỏ trước khi sử dụng với video lớn
3. Kiểm tra kết quả trên Facebook Page/Group của bạn

### ✍️ Mẹo & gợi ý nâng cao
1. **Kết hợp với Slack/Telegram**: Thêm node gửi thông báo khi video được đăng thành công
2. **Lưu log hoạt động**: Thêm node lưu log các video đã đăng vào Google Sheets
3. **Lập lịch đăng**: Kết hợp với node "Schedule Trigger" để đăng video theo lịch
4. **Xử lý lỗi tự động**: Thêm node xử lý lỗi và gửi báo cáo khi có vấn đề xảy ra

### 📌 Kết luận
Workflow này giúp các sếp tự động hóa hoàn toàn quy trình đăng video lên Facebook Pages/Groups, tiết kiệm thời gian quý giá và nâng cao hiệu quả quản lý nội dung. Hãy thử ngay và trải nghiệm sự tiện lợi mà n8n mang lại cho quá trình marketing của bạn!