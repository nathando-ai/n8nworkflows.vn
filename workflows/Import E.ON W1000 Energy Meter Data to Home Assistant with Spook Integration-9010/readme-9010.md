---
title: "🚀 Tự động hóa nhập dữ liệu công tơ điện E.ON W1000 vào Home Assistant cực đỉnh"
description: "Hướng dẫn chi tiết workflow n8n tự động đọc file Excel từ email, xử lý dữ liệu điện năng E.ON W1000 và đẩy thống kê dài hạn vào Home Assistant qua Spook."
slug: "tu-dong-hoa-nhap-du-lieu-cong-to-dien-eon-w1000-vao-home-assistant"
tags: [n8n, automation, home-assistant, energy-meter, spook, eon, smart-home]
keywords: [n8n workflow, eon w1000, home assistant import statistics, spook integration, tu dong hoa nang luong, smart home automation]
---

# 🚀 Tự động hóa nhập dữ liệu công tơ điện E.ON W1000 vào Home Assistant

Các sếp đang sử dụng công tơ điện E.ON W1000 và đau đầu vì phải tải file Excel thủ công, tính toán lại các chỉ số tiêu thụ (AP, AM, 1.8.0, 2.8.0) rồi nhập vào Home Assistant? Việc làm thủ công này cực kỳ mất thời gian, dễ sai sót và làm gián đoạn theo dõi năng lượng gia đình.

Workflow n8n này sẽ giải quyết triệt để vấn đề đó: tự động bắt email từ E.ON, trích xuất file `.xlsx`, xử lý dữ liệu 15 phút thành tổng hàng giờ, và đẩy dữ liệu thống kê dài hạn trực tiếp vào Home Assistant thông qua Spook integration một cách mượt mà!

:::info[Gợi ý hạ tầng cho n8n]
Để workflow chạy ổn định 24/7, các sếp nên cài n8n trên VPS riêng (Self-hosted).
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

### 🎯 Kết quả các sếp nhận được
:::tip[LỢI ÍCH CỐT LÕI]
- **Tự động hóa 100%**: Không cần đụng tay vào file Excel từ lúc nhận email đến khi lên biểu đồ Home Assistant.
- **Xử lý dữ liệu chuẩn xác**: Tự động quy đổi thời gian Excel sang định dạng chuẩn, gom nhóm dữ liệu 15 phút thành tổng theo giờ.
- **Tích hợp sâu Home Assistant**: Đẩy dữ liệu vào bảng điều khiển năng lượng (Energy Dashboard) thông qua `recorder.import_statistics` và cập nhật các Helper `input_number`.
- **Hoạt động bền bỉ**: Hỗ trợ đa dạng trigger (Gmail, IMAP, hoặc chạy định kỳ theo lịch Schedule).
:::

### 🔧 Yêu cầu cần thiết
:::info[CHUẨN BỊ]
- **n8n Instance**: Đã cài đặt sẵn sàng.
- **Tài khoản Gmail hoặc IMAP**: Để nhận email chứa file báo cáo từ E.ON (với tiêu đề `[EON-W1000]`).
- **Home Assistant**: Đã cài đặt **Spook integration** (thông qua HACS) để hỗ trợ service `recorder.import_statistics`.
- **Home Assistant Long-Lived Access Token**: Để kết nối n8n với HA.
:::

### 🚀 Cách import & Lưu ý khi "lên đồ"

#### 1. Import Workflow 📥
Các sếp copy toàn bộ mã nguồn JSON của workflow (hoặc tải file JSON từ link gốc) và paste trực tiếp vào giao diện n8n Editor của mình.

#### 2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌
Sau khi import, các sếp cần cấu hình chính xác các thành phần sau:
- **Triggers (Gmail Trigger / Email Trigger / Schedule Trigger)**: Kết nối tài khoản Gmail của các sếp hoặc cấu hình IMAP. Đảm bảo bộ lọc tiêu đề khớp với `[EON-W1000]` và gửi từ địa chỉ của E.ON.
- **Extract from File**: Node này nhận file `.xlsx` đính kèm từ email để tiến hành đọc dữ liệu.
- **Các node Home Assistant**: 
  - Chọn Credentials loại `homeAssistantApi` sử dụng Long-Lived Access Token từ HA của các sếp.
  - Kiểm tra lại các entity ID (`sensor.grid_energy_import`, `sensor.grid_energy_export`, `input_number.grid_import_meter`, `input_number.grid_export_meter`) xem đã khớp với cấu hình thực tế trong HA chưa.

#### 3. Chuẩn bị Home Assistant trước khi chạy 🏠
Trước khi bật workflow, hãy chắc chắn các sếp đã thêm các Helper (`input_number`) và Template Sensors vào file `configuration.yaml` của Home Assistant:

```yaml
input_number:
  grid_import_meter:
    name: grid_import_meter
    mode: box
    initial: 0
    min: 0
    max: 9999999999
    step: 0.001
    unit_of_measurement: kWh
  grid_export_meter:
    name: grid_export_meter
    mode: box
    initial: 0
    min: 0
    max: 9999999999
    step: 0.001
    unit_of_measurement: kWh

template:
  - sensor:
      - name: "grid_energy_import"
        state: "{{ states('input_number.grid_import_meter') | float(0) }}"
        unit_of_measurement: "kWh"
        device_class: energy
        state_class: total_increasing
      - name: "grid_energy_export"
        state: "{{ states('input_number.grid_energy_export') | float(0) }}"
        unit_of_measurement: "kWh"
        device_class: energy
        state_class: total_increasing
```

#### 4. Kích hoạt ⚡️
- Chạy thử nghiệm (Test run) với một email mẫu để kiểm tra dữ liệu chảy qua các node tính toán (`Calculate hourly sum and`).
- Sau khi thấy dữ liệu trả về mượt mà, các sếp bật **Active workflow** để hệ thống tự động chạy ngầm.

### ✍️ Mẹo & gợi ý nâng cao
- **Thêm thông báo Telegram/Slack**: Gắn thêm node thông báo vào cuối workflow để nhận tin nhắn mỗi khi dữ liệu điện năng được cập nhật thành công vào Home Assistant.
- **Lưu trữ Log lỗi**: Sử dụng node `If` để bắt lỗi khi file Excel lỗi định dạng hoặc email không có file đính kèm, tránh làm gián đoạn workflow.
- **Chạy định kỳ**: Kết hợp `Schedule Trigger` để quét lại các email cũ trong trường hợp hệ thống gặp sự cố mất mạng tạm thời.

### 📌 Kết luận
Với workflow n8n này, việc quản lý và đồng bộ dữ liệu năng lượng từ công tơ E.ON W1000 vào Home Assistant đã trở nên hoàn toàn tự động, chính xác và chuyên nghiệp. Hãy triển khai ngay để tối ưu hóa hệ thống nhà thông minh của các sếp!