---
title: "🚀 Tự Động Hoạt Động Apache Airflow Trên n8n: Lấy Giá Trị XCom Và Quản Lý DAG Như Chuyên Gia"
description: "Workflow này tự động kích hoạt DAG trên Apache Airflow, theo dõi trạng thái thực thi, và lấy giá trị XCom để tích hợp với các hệ thống khác - giải pháp hoàn hảo cho các sếp cần tự động hóa pipeline data 24/7."
slug: "tự-dộng-hoạt-dộng-apache-airflow-tren-n8n"
tags: [n8n, apache-airflow, automation, xcom-value, api-integration, data-pipeline]
keywords: [n8n workflow airflow, tự động hóa airflow, lấy giá trị xcom, quản lý dag airflow, tự động hóa data pipeline, api airflow]
---

# 🚀 **Tự Động Hoạt Động Apache Airflow Trên n8n: Lấy Giá Trị XCom Và Quản Lý DAG Như Chuyên Gia**

### **Giải pháp cho các sếp muốn tự động hóa pipeline data mà không cần viết code**
Bạn có bao giờ phải **thủ công kích hoạt DAG trên Apache Airflow**, **chờ đợi kết quả**, và **lấy giá trị XCom** để tích hợp với các hệ thống khác? Hoặc phải **kiểm tra trạng thái thực thi** nhiều lần để tránh lỗi? Với workflow này, **n8n sẽ tự động hóa toàn bộ quy trình** cho bạn:
- **Kích hoạt DAG** một cách tự động.
- **Theo dõi trạng thái** (queued, running, success, failed).
- **Lấy giá trị XCom** và truyền vào các workflow khác.
- **Ngăn chặn lỗi** khi DAG chạy quá lâu hoặc thất bại.

Không cần viết một dòng code, chỉ cần **cấu hình n8n** và **bật tự động hóa** - mọi thứ sẽ hoạt động **liên tục 24/7**.

---

:::info[Gợi ý hạ tầng cho n8n]
Để workflow này chạy ổn định và không bị gián đoạn, các sếp nên **self-host n8n** trên VPS để đảm bảo tính liên tục cao.
👉 [Đăng ký VPS TinoHost](https://tino.vn/vps-n8n?affid=388) (🎁 Mã giảm giá: **VPSN8N** - giảm tới 39%)
👉 [Đăng ký VPS Xeon 4GB chỉ 50k/tháng](https://my.bnix.one/aff.php?aff=172)
:::

---

### 🎯 **Kết quả các sếp nhận được**
:::tip[LỢI ÍCH CỐT LÕI]
✅ **Tiết kiệm thời gian**: Không cần thủ công kích hoạt DAG hoặc kiểm tra trạng thái.
✅ **Tự động hóa hoàn toàn**: Workflow chạy liên tục, không phụ thuộc vào người dùng.
✅ **Lấy giá trị XCom**: Giúp tích hợp dữ liệu từ Airflow vào các hệ thống khác (Slack, Email, Database...).
✅ **Ngăn chặn lỗi**: Dừng tự động nếu DAG chạy quá lâu hoặc thất bại.
✅ **Chuẩn mực chuyên nghiệp**: Quản lý DAG như một chuyên gia DevOps.
:::

---

### 🔧 **Yêu cầu cần thiết**
Trước khi import workflow, các sếp cần chuẩn bị:
1. **Tài khoản Airflow** với quyền truy cập API.
2. **Credentials HTTP Basic Auth** cho API Airflow (tạo trong n8n dưới `Credentials` → `Add` → `HTTP Basic Auth`).
   - **Username & Password**: Điền thông tin từ Airflow (thường là `airflow`/`airflow` hoặc từ `AIRFLOW__WEB_SERVER__USER`).
   - **URL API**: Thường là `http://<your-airflow-server>/api/v1/` (hoặc `http://localhost:8080/api/v1/` nếu local).
3. **Thời gian chờ tối đa (wait_time)**: Thời gian (giây) để chờ DAG hoàn thành trước khi dừng (ví dụ: `3600` = 1 giờ).
4. **DAG ID**: ID của DAG bạn muốn kích hoạt (ví dụ: `my_dag_id`).

---

### 🚀 **Cách import & Lưu ý khi "lên đồ"**

#### **1. Import Workflow 📥**
- **Tải file JSON** từ [n8n.io/workflows/3026](https://n8n.io/workflows/3026) hoặc copy toàn bộ JSON từ link trên.
- **Mở n8n Editor** → Nhấn `Import` → Dán JSON và nhấn `Import`.

#### **2. Các lưu ý (BẮT BUỘC) phải chỉnh 📌**
Workflows này có **7 node quan trọng** cần cấu hình cẩn thận:

##### **A. Cấu hình Credentials cho API Airflow**
- **Node `Airflow: dag_run`**, `Airflow: dag_run - state` và `Airflow: dag_run - get result`:
  - Chọn **credentials** là `httpBasicAuth` (đã tạo trước).
  - **Method**: `POST` (cho `dag_run`) và `GET` (cho `state` và `get result`).
  - **URL**:
    - `dag_run`: `{{ $json["url"] }}/dags/{{ $json["dag_id"] }}/dagRuns` (ví dụ: `http://airflow-server/api/v1/dags/my_dag/dagRuns`).
    - `state`: `{{ $json["url"] }}/dags/{{ $json["dag_id"] }}/dagRuns/{{ $json["dag_run_id"] }}`.
    - `get result`: `{{ $json["url"] }}/dags/{{ $json["dag_id"] }}/dagRuns/{{ $json["dag_run_id"] }}`.

##### **B. Điền tham số DAG**
- Trong **node `Airflow: dag_run`**:
  - **Headers**:
    ```json
    {
      "Content-Type": "application/json"
    }
    ```
  - **Body (JSON)**:
    ```json
    {
      "conf": {},
      "execution_date": "{{ $json["execution_date"] }}",
      "run_id": "{{ $json["run_id"] }}",
      "wait_for_completion": false
    }
    ```
  - **Tham số cần truyền vào**:
    - `dag_id`: ID của DAG (ví dụ: `my_dag`).
    - `execution_date`: Ngày giờ kích hoạt (ví dụ: `{{ $now("YYYY-MM-DDTHH:mm:ss") }}`).
    - `run_id`: ID duy nhất cho lần chạy (ví dụ: `manual__{{ $now("YYYYMMDDTHHmmss") }}`).

##### **C. Cấu hình thời gian chờ và kiểm tra trạng thái**
- **Node `Wait`**:
  - Đặt **thời gian chờ** (ví dụ: `10` giây).
- **Node `If count > wait_time`**:
  - `wait_time` = số lần chờ tối đa (ví dụ: `36` = 36 * 10s = 6 phút).
- **Node `Switch: state`**:
  - Kiểm tra `$.state` và chuyển hướng:
    - `success` → `in data` (truyền giá trị XCom).
    - `failed` → `dag run fail` (dừng với lỗi).
    - `running` → tiếp tục chờ.

##### **D. Lấy giá trị XCom**
- **Node `Airflow: dag_run - get result`**:
  - Sau khi DAG hoàn thành (`state = success`), node này sẽ lấy **tất cả giá trị XCom** từ DAG.
  - **Headers**:
    ```json
    {
      "Content-Type": "application/json"
    }
    ```
  - **Body**: Rỗng.
  - **Output**: Giá trị XCom sẽ ở `$.xcom` (dạng JSON).

##### **E. Truyền giá trị XCom vào workflow khác**
- **Node `in data`**:
  - Đây là **trigger** để kích hoạt workflow khác (nếu cần).
  - **Data truyền vào**: `$.xcom` (giá trị từ Airflow).

---

#### **3. Kích hoạt ⚡️**
1. **Test run với dữ liệu mẫu**:
   - Điền `dag_id`, `execution_date`, `run_id` vào **node `Airflow: dag_run`**.
   - Chạy **Manual Run** để kiểm tra:
     - DAG có được kích hoạt không?
     - Trạng thái có được theo dõi đúng không?
     - Giá trị XCom có được lấy được không?
2. **Bật Active workflow**:
   - Sau khi test thành công, **bật `Active`** và **lưu workflow**.

---

### ✍️ **Mẹo & gợi ý nâng cao**
1. **Gửi thông báo Slack/Email khi DAG hoàn thành**:
   - Sau `in data`, thêm **node `slack`** hoặc **`email`** để thông báo kết quả.
   - Ví dụ: `DAG {{ $json["dag_id"] }} hoàn thành với XCom: {{ $json["xcom"] }}`.

2. **Lưu log vào Google Sheets/Database**:
   - Thêm **node `googleSheets`** hoặc **`database`** để ghi lại lịch sử chạy DAG.

3. **Kết hợp với LLM (AI) để phân tích XCom**:
   - Sử dụng **node `LLM`** (n8n-nodes-ai) để phân tích giá trị XCom và tự động tạo báo cáo.

4. **Tự động kích hoạt DAG theo lịch**:
   - Sử dụng **node `executeWorkflowTrigger`** kết hợp với **cron** để chạy DAG định kỳ.

5. **Xử lý lỗi tự động**:
   - Thêm **node `email`** để gửi cảnh báo khi DAG thất bại.

---

### 📌 **Kết luận**
Workflow này **giải phóng bạn khỏi việc quản lý DAG thủ công** trên Apache Airflow, đồng thời **tích hợp giá trị XCom** vào các hệ thống khác một cách tự động. **Không cần viết code**, chỉ cần **cấu hình n8n** và **bật tự động hóa** - mọi thứ sẽ chạy **liên tục, chính xác và hiệu quả**.

**Hành động ngay hôm nay**:
1. **Import workflow** vào n8n.
2. **Cấu hình credentials Airflow** và tham số DAG.
3. **Test và bật Active**.
4. **Tích hợp với Slack/Email/Database** để tối ưu hóa hơn.

👉 **Bắt đầu tự động hóa pipeline data của bạn ngay bây giờ!** 🚀

---