---
type: UML Design
client: Nga Fashion
project: Phân Ca Quản Lý Cửa Hàng
version: 1.0
---

# Báo Cáo Thiết Kế Hệ Thống (UML & ERD) — Nga Fashion

**Ngày tạo:** 2026-04-11 | **Tham chiếu:** 03_SA_Report | **Trạng thái:** Hoàn thành

Tài liệu này cung cấp các bản thiết kế kỹ thuật chi tiết để phục vụ cho giai đoạn Build (Thiết lập Lark Base).

## 1. Sơ Đồ Ngữ Cảnh (Context Diagram)

Sơ đồ tổng quan về cách các bộ phận tương tác với hệ thống quản lý lịch trực.

```plantuml
@startuml
skinparam rectangle {
  BackgroundColor #F0F4FF
  BorderColor #3366CC
}
actor "Quản Lý Cửa Hàng" as Manager
actor "Nhân Viên (FT/PT)" as Staff

database "Lark Base\n(Quản lý Phân Ca)" as Base
queue "Lark Bot\n(Messenger)" as Bot

Manager --> Base : 1. Xếp ca hàng tuần & Kiểm tra Validate (Xanh/Đỏ)
Base --> Bot : 2. Tự động gửi thông báo lịch làm việc (20h T7)
Bot --> Staff : 3. Nhận lịch và xác nhận
@enduml
```

## 2. Sơ Đồ Thực Thể Liên Kết (ERD - Base Blueprint)

Sơ đồ ERD chuẩn bị cho việc khởi tạo bảng trên Lark Base. Đã định nghĩa rõ các field type tương thích với Lark.

```plantuml
@startuml
entity "Nhân Sự (tbl_NhanSu)" as P_NhanSu {
  * Mã Nhân Sự (AutoNumber)
  --
  Tên Nhân Sự (User)
  Loại Hình (SingleSelect) : FT / PT
  Tổng Giờ Tuần Này (Rollup) : SUM(Giờ)
  Số Ngày Làm Tuần Này (Rollup) : COUNT_DISTINCT(Ngày Làm)
  Validator_Trạng Thái (Formula) : Kiểm tra (Ngày=6? Giờ_PT=1/2_FT?)
}

entity "Danh Mục Ca (tbl_DanhMucCa)" as P_DanhMucCa {
  * Mã Ca (AutoNumber)
  --
  Tên Ca (Text) : Sáng sớm, Sáng chiều...
  Bắt Đầu (Time)
  Kết Thúc (Time)
  Số Giờ (Number)
}

entity "Lịch Làm Việc (tbl_LichLamViec)" as P_LichLamViec {
  * ID (AutoNumber)
  --
  Người Làm (DuplexLink) -> P_NhanSu
  Ca Làm (DuplexLink) -> P_DanhMucCa
  Ngày Làm (Date)
  Tuần (Formula) : YEARWEEK(Ngày Làm)
  Thứ (Formula) : WEEKDAY(Ngày Làm)
  Số Giờ Ca (Lookup) -> P_DanhMucCa.Số Giờ
  Là Ngày Nghỉ? (Checkbox) : Check nếu đăng ký nghỉ
}

P_NhanSu "1" -- "N" P_LichLamViec
P_DanhMucCa "1" -- "N" P_LichLamViec
@enduml
```

## 3. Sơ Đồ Trình Tự: Logic Cảnh Báo (Validation Logic)

Mô tả luồng Quản lý nhập liệu và hệ thống phản hồi kết quả tính toán giờ làm.

```plantuml
@startuml
autonumber
participant "Quản Lý" as Manager
database "Bảng Lịch Làm Việc\n(Lark Base)" as BaseLich
database "Bảng Nhân Sự\n(Lark Base)" as BaseNhanSu

Manager -> BaseLich : Thêm Record: Nguyễn Văn A, Ca Sáng, Ngày T3
BaseLich -> BaseNhanSu : Link record, Lookup Số Giờ
BaseNhanSu -> BaseNhanSu : Rollup tính tổng giờ + COUNT_DISTINCT(ngày làm)
BaseNhanSu -> BaseNhanSu : Chạy Formula Validate: \n1. Giờ PT = 1/2 FT? \n2. FT làm đủ 6 ngày độc nhất? \n3. Ngày nghỉ = T2/CN? \n4. Cảnh báo nếu ca trùng giờ?

alt Dữ liệu Hợp lệ
  BaseNhanSu --> Manager : Hiển thị 🟢 Chuẩn
else Dữ liệu Vi phạm (Lố giờ, thiếu ngày)
  BaseNhanSu --> Manager : Hiển thị 🔴 Cần xếp lại (Kèm lý do)
  Manager -> BaseLich : Điều chỉnh lại Ca / Ngày trực
end
@enduml
```

## 4. Sơ Đồ Trình Tự: Tự Động Gửi Lịch (Automation)

```plantuml
@startuml
autonumber
participant "Lark Automations" as Auto
database "Bảng Lịch Làm Việc" as BaseLich
queue "Lark Bot" as Bot
participant "Group Bán Hàng" as Group

Auto -> Auto : Trigger (Scheduled): 20h00, Thứ 7 hằng tuần
Auto -> BaseLich : Query: Lấy các Record lịch có Tuần = Tuần sau
BaseLich --> Auto : Trả về danh sách Lịch làm việc
Auto -> Bot : Generate tin nhắn tổng hợp kèm link Grid View
Bot -> Group : Gửi tin nhắn: "Lịch làm việc tuần tới..."
@enduml
```

---
**Cần chuẩn bị cho Phase 4 (Build):**
- Tạo 3 bảng `tbl_NhanSu`, `tbl_DanhMucCa`, `tbl_LichLamViec`.
- Code chính xác các Formula kiểm duyệt:
  - `IF(AND(Loại Hình='FT', Số Ngày!=6), '🔴 Sai ngày', '🟢 K.Tra Giờ')`
  - Đảm bảo logic tính chéo giờ PT = 1/2 FT (Có thể lấy Target = 20h nếu lập lịch chuẩn 40h).
