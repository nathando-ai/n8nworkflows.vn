---
title: "🚀 Tự động tải lên nhiều file lên Google Drive cùng quản lý thư mục"
description: "Workflow n8n giúp tự động kiểm tra thư mục, tạo mới nếu chưa tồn tại và tải lên tất cả file từ form mà không cần code."
slug: "tang-lai-nhi-hon-file-lon-gdrive-quan-ly-thu-muc"
tags: [n8n, automation, no-code, google-drive, upload-file, folder-management]
keywords: [n8n workflow, tự động hóa, tải lên Google Drive, quản lý thư mục, upload file]
---

# 🚀 Tự động tải lên nhiều file lên Google Drive cùng quản lý thư mục

Bạn đang phải mất hàng giờ để upload từng file thủ công vào Google Drive, đồng thời phải tự tay tạo thư mục mới khi cần?  
Workflow **Bulk File Upload to Google Drive with Folder Management** sẽ giải quyết mọi nỗi đau này:  
- Nhận dữ liệu từ form (có thể upload nhiều file cùng lúc).  
- Kiểm tra thư mục mục tiêu đã tồn tại chưa.  
- Tạo thư mục mới nếu chưa có.  
- Tải lên tất cả file vào thư mục đúng vị trí, giữ nguyên tên và cấu trúc.

Với workflow này, bạn có thể **tự động hóa 100%** quy trình upload file, giảm thiểu sai sót và tiết kiệm thời gian đáng kể.

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).  
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)  
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)  
:::

## 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tiết kiệm thời gian**: Tự động upload hàng trăm file chỉ trong vài giây.  
- **Độ chính xác cao**: Không còn sai sót khi nhập tên thư mục hay đường dẫn.  
- **Tổ chức thư mục hợp lý**: Mỗi lần upload sẽ được lưu vào thư mục đúng tên, tránh trùng lặp.  
- **Hoạt động liên tục**: Workflow chạy 24/7, không phụ thuộc vào người dùng.  
:::

## 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **Tài khoản Google Drive**: Đã cấp quyền OAuth2 cho n8n.  
- **Google Drive OAuth2 API**: Tạo credential trong n8n (`Credentials > Google Drive OAuth2 API`).  
- **Form**: Cần có form (ví dụ Google Forms, Typeform, hoặc custom form) hỗ trợ upload file và nhập tên thư mục.  
- **Parent Folder ID**: ID thư mục cha (nếu muốn lưu trong thư mục cụ thể).  
:::

## 🚀 Cách import & Lưu ý khi "lên đồ"

### 1. Import Workflow 📥
1. Tải file JSON của workflow từ [link gốc](https://n8n.io/workflows/2979).  
2. Trong n8n Editor, chọn **Import** → **Import from File** → chọn file JSON.  
3. Hoặc copy toàn bộ JSON và dán vào **Import from Clipboard**.

### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
| Node | Mô tả | Cấu hình cần chỉnh |
|------|-------|---------------------|
| **On form submission** | Trigger khi form được submit | Đặt URL webhook (nếu dùng custom form) hoặc cấu hình trigger của form provider. |
| **Get Folder Name** | Lấy tên thư mục từ form | `folderName` = `{{$json["folderName"]}}` (đảm bảo trường có trong form). |
| **Search specific folder** | Tìm thư mục đã tồn tại | `Query` = `mimeType='application/vnd.google-apps.folder' and name = '{{ $json.folderName }}' and '<folderId>' in parents` (thay `<folderId>` bằng ID thư mục cha). |
| **Folder found ?** | Kiểm tra kết quả tìm kiếm | `Has results` → `true` → existing path, `false` → new path. |
| **Create Folder** | Tạo thư mục mới | `Name` = `{{$json.folderName}}`, `Parent ID` = `<folderId>` (hoặc `root`). |
| **Prepare Files for Upload** | Tách file cho upload vào thư mục hiện có | Code node: `return items.map(item => ({ json: item.json, binary: { file: item.binary.file } }));` |
| **Upload Files** | Upload vào thư mục đã tồn tại | `Folder ID` = `{{$node["Search specific folder"].json[0].id}}` (đảm bảo trường tồn tại). |
| **Prepare Files for New Folder** | Tách file cho upload vào thư mục mới | Tương tự như node trên. |
| **Upload to New Folder** | Upload vào thư mục vừa tạo | `Folder ID`