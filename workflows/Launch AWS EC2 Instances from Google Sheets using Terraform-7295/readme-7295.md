---
title: "🚀 Tự động khởi chạy AWS EC2 Instances từ Google Sheets bằng Terraform và n8n"
description: "Hướng dẫn chi tiết cách tự động hóa quy trình deploy máy chủ AWS EC2 thông qua Google Sheets và Terraform, kết hợp gửi thông báo qua Gmail và cập nhật trạng thái thời gian thực."
slug: "tu-dong-khoi-chay-aws-ec2-tu-google-sheets-terraform-n8n"
tags: [n8n, automation, devops, aws, terraform, google-sheets]
keywords: [n8n workflow, tu dong hoa aws, terraform ec2 google sheets, quan ly ha tang n8n, devops automation]
---

# 🚀 Tự động khởi chạy AWS EC2 Instances từ Google Sheets với Terraform

Các sếp làm trong ngành DevOps hoặc quản lý hạ tầng chắc hẳn thường xuyên phải đối mặt với việc cấu hình thủ công từng con máy chủ AWS EC2 trên giao diện hoặc chạy lệnh Terraform dài dòng mỗi khi có yêu cầu mới. Việc này vừa mất thời gian, vừa dễ sai sót cấu hình.

Giải pháp là đây! Workflow n8n này sẽ tự động hóa toàn bộ quy trình: Đọc yêu cầu từ **Google Sheets**, thực thi mã **Terraform** thông qua kết nối **SSH**, cập nhật lại trạng thái thành công vào bảng tính và gửi email xác nhận chi tiết qua **Gmail**. Tất cả diễn ra hoàn toàn tự động mà không cần can thiệp thủ công!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%:** Loại bỏ hoàn toàn thao tác copy-paste lệnh Terraform thủ công.
- **Quản lý tập trung:** Chỉ cần điền thông số cấu hình (AMI, Instance Type, Key Name...) vào Google Sheet, hệ thống tự lo phần còn lại.
- **Minh bạch trạng thái:** Google Sheet tự động cập nhật kết quả deploy và Gmail gửi email chi tiết kèm Public IP ngay khi tạo xong.
- **Lịch trình linh hoạt:** Có thể chạy tự động định kỳ (ví dụ: 9 giờ sáng mỗi ngày) hoặc kích hoạt thủ công khi cần.
:::

### Yêu cầu cần thiết
:::info[CHUẨN BỊ TRƯỚC KHI "LÊN ĐỒ"]
- **n8n Instance:** Đã cài đặt n8n (Self-hosted hoặc Cloud).
- **Google Account:** File Google Sheets chứa danh sách yêu cầu khởi chạy EC2.
- **SSH Access:** Một máy chủ (hoặc Bastion Host) đã cài đặt Terraform, AWS CLI và có quyền gọi AWS API.
- **Gmail Account:** Đã cấu hình OAuth2 Credentials để gửi email thông báo.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy mã JSON của workflow từ nguồn hoặc tải file về, sau đó paste trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Workflow bao gồm 5 nodes chính, các sếp cần cấu hình kỹ các điểm sau:

- **Google Sheets Trigger (scheduleTrigger):** 
  - Mặc định trigger theo lịch (ví dụ: Daily lúc 9 AM). Các sếp có thể đổi sang chế độ chạy thủ công (Manual) tùy theo nhu cầu.
- **Extract Instance Details (googleSheets):**
  - Kết nối với tài khoản Google thông qua `googleApi`.
  - Chọn đúng File Google Sheet và Sheet Name chứa dữ liệu cấu hình EC2.
- **Launch EC2 Instance (ssh):**
  - Sử dụng kết nối `sshPrivateKey` để truy cập vào server chạy Terraform.
  - Tại đây, sếp cần chuẩn bị sẵn các file Terraform trên server như hướng dẫn bên dưới.
- **Update Google Sheet (googleSheets):**
  - Cấu hình operation là `append` để ghi log kết quả (IP, trạng thái, thời gian) ngược lại vào Google Sheet.
- **Send Confirmation Email (gmail):**
  - Cấu hình tài khoản `gmailOAuth2` để gửi email báo cáo chi tiết cho đội ngũ vận hành.

---

### 📂 Chuẩn bị mã nguồn Terraform trên Server (SSH Node)

Trên máy chủ Linux nơi SSH node kết nối tới, hãy tạo thư mục chứa các file cấu hình Terraform sau:

#### `main.tf`
```hcl
provider "aws" {
  region  = var.aws_region
  profile = var.aws_profile
}

resource "aws_instance" "example" {
  ami           = var.ami_id
  instance_type = var.instance_type
  key_name      = var.key_name

  tags = {
    Name = var.instance_name
  }
}

output "ec2_public_ip" {
  value = aws_instance.example.public_ip
}
```

#### `variables.tf`
```hcl
variable "aws_region" {
  description = "AWS region to deploy in"
  type        = string
}

variable "aws_profile" {
  description = "AWS CLI profile to use"
  type        = string
  default     = "default"
}

variable "ami_id" {
  description = "AMI ID for EC2 instance"
  type        = string
}

variable "instance_type" {
  description = "EC2 instance type"
  type        = string
  default     = "t2.micro"
}

variable "key_name" {
  description = "SSH key pair name"
  type        = string
}

variable "instance_name" {
  description = "EC2 instance Name tag"
  type        = string
}
```

#### `terraform.tfvars` (Ví dụ mẫu)
```hcl
aws_region     = "us-east-1"
ami_id         = "ami-0c55b159cbfafe1f0"
instance_type  = "t2.micro"
key_name       = "my-keypair"
instance_name  = "MyTerraformEC2"
```

---

#### 3. Kích hoạt ⚡️
- Nhấn **Test step** từng node để kiểm tra quyền truy cập Google Sheets, SSH và Gmail.
- Sau khi test thành công, bật công tắc **Active** góc trên cùng bên phải để workflow chính thức đi vào hoạt động tự động.

### ✍️ Mẹo & gợi ý nâng cao
- **Tích hợp ChatOps:** Thêm node **Slack** hoặc **Telegram** để bắn thông báo ngay lập tức vào nhóm chat kỹ thuật mỗi khi có server mới được khởi tạo thành công.
- **Xử lý lỗi (Error Handling):** Thêm Error Trigger để cảnh báo qua email/Slack nếu câu lệnh Terraform gặp lỗi (ví dụ: hếtquota AWS, sai AMI ID...).
- **Lưu trữ State:** Đảm bảo Terraform trên server sử dụng Remote State (S3 + DynamoDB) để tránh xung đột khi nhiều người cùng gọi workflow.

### 📌 Kết luận
Với workflow n8n kết hợp Terraform và Google Sheets này, việc quản lý và cấp phát tài nguyên AWS nay đã trở nên đơn giản, trực quan và không tốn chút sức lực thủ công nào. Hãy cài đặt ngay để tối ưu hóa quy trình DevOps cho đội ngũ của các sếp nhé!