# Service Boundary của nhóm

## 1. Thông tin nhóm

- Tên nhóm: 7
- Lớp: CNTT 17-09
- Thành viên: Đỗ Quốc Khánh
- Service nhóm phụ trách: Dịch vụ tiếp nhận và xử lý luồng camera
- Sản phẩm tổng thể của lớp: Hệ thống giám sát camera thông minh

---

## 2. Actor

Ai tương tác với hệ thống/service?

- Người quản trị hệ thống
- Camera IP
- Người dùng theo dõi camera
- Service AI nhận diện hình ảnh

---

## 3. System Boundary

Nhóm em xây phần nào?

### Phần nhóm kiểm soát

- Nhận luồng video từ camera
- Xử lý frame hình ảnh
- Chuyển tiếp dữ liệu cho service AI
- Lưu metadata camera
- Cung cấp API truy cập trạng thái camera

### Phần nhóm chỉ tích hợp

- Database
- Service AI nhận diện
- Dashboard giao diện người dùng
- Hệ thống xác thực tài khoản

---

## 4. Service Boundary

Service của nhóm có trách nhiệm gì?

- Kết nối camera IP
- Nhận và xử lý luồng video
- Kiểm tra trạng thái camera
- Gửi frame đến AI service
- Trả kết quả xử lý cho hệ thống khác

Service KHÔNG làm gì?

- Không xử lý giao diện người dùng
- Không lưu video dài hạn
- Không quản lý tài khoản
- Không huấn luyện AI model

---

## 5. Input / Output

### Input

- Luồng video từ camera
- Yêu cầu kiểm tra trạng thái
- Yêu cầu lấy frame

### Output

- Frame hình ảnh đã xử lý
- Trạng thái camera
- Metadata camera
- Kết quả nhận diện từ AI

---

## 6. API dự kiến

| Method | Endpoint | Mục đích |
|---|---|---|
| GET | /health | Kiểm tra service |
| GET | /camera/status | Kiểm tra trạng thái camera |
| POST | /camera/connect | Kết nối camera |
| GET | /camera/frame | Lấy frame hiện tại |
| POST | /camera/process | Xử lý frame camera |

---

## 7. Phụ thuộc service khác

Service này gọi đến service nào?

- AI Detection Service
- Database Service
- Authentication Service

Service nào gọi đến service này?

- Frontend Dashboard
- Monitoring Service
- Gateway API

---

## 8. Sơ đồ minh họa

```mermaid
flowchart LR
    Camera[IP Camera] --> Service[Camera Processing Service]
    Service --> AI[AI Detection Service]
    Service --> DB[(Database)]
    User[Admin/User] --> Dashboard[Frontend Dashboard]
    Dashboard --> Service