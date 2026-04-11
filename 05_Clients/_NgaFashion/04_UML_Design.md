---
type: UML Design
client: Nga Fashion
project: Phân Ca Quản Lý Cửa Hàng
version: 1.1
---

# Báo Cáo Thiết Kế Hệ Thống (UML & ERD) — Nga Fashion

**Ngày tạo:** 2026-04-11 | **Tham chiếu:** 03_SA_Report | **Trạng thái:** Hoàn thành

Tài liệu này cung cấp các bản thiết kế kỹ thuật chi tiết, tuân thủ bộ quy tắc `Tpl_UML_Guide` và `Tpl_LarkBase_Convention`.

---

## 1. Sơ Đồ Ngữ Cảnh (Context Diagram)

Mô tả tổng quan sự tương tác giữa các bên liên quan và hệ sinh thái giải pháp Nga Fashion.

```plantuml
@startuml
skinparam rectangle {
  BackgroundColor #F0F4FF
  BorderColor #3366CC
}
actor "Quản lý (Chị Nga)" as Manager
actor "Nhân viên Sales (FT/PT)" as Staff

rectangle "Lark Suite Ecosystem" {
  database "Lark Base\n(Operational DB)" as Base
  rectangle "Lark Base Script\n(Solver Engine)" as Script
  queue "Lark Bot\n(Messenger)" as Bot
}

Manager --> Base : 1. Khai báo nhân sự & Ngày nghỉ
Script --> Base : 2. Đọc cấu hình & Tự động xếp ca
Base --> Bot : 3. Trigger thông báo lịch tuần
Bot --> Staff : 4. Nhận lịch & Phản hồi
@enduml
```

---

## 2. Sơ Đồ Hoạt Động (Swimlane Activity Diagram)

Mô tả quy trình nghiệp vụ và luồng xử lý chi tiết của **AppScript / Base Script Solver**.

```plantuml
@startuml
|Quản lý (Chị Nga)|
start
:Mở bảng "Nhân sự" trên Lark Base;
:Chọn ngày nghỉ (CN/T2) cho từng bạn;
:Nhấn nút [Auto-Schedule];

|#F0F4FF|AppScript / Base Script Solver|
:Phase A: Thu thập dữ liệu;
note right
  - Lấy danh sách Staff (FT/PT)
  - Lấy cấu hình ca & Target hours
end note
:Phase B: Phân tích Ràng buộc (Solver);
if (Check Hard Constraints) then (OK)
  :Ưu tiên gán FT vào ca Offline;
  :Gán PT vào ca Tối đêm;
  :Xử lý gán 2 ca/ngày nếu thiếu người;
else (Vi phạm)
  :Ghi log cảnh báo vào Base;
endif
:Phase C: Tối ưu hóa (Soft Constraints);
:Kiểm tra quy tắc WFH (< 2 ngày);
:Check "Trải đủ ca" cho FT;
:Phase D: Ghi kết quả;
:Batch Create records vào bảng "Lịch làm việc";

|Lark Base|
:Cập nhật Grid View & Calendar View;
:Formula chạy Validate (Xanh/Đỏ);

|Lark Bot|
:Trigger thông báo (Tối Thứ 7);
:Gửi Card lịch làm việc vào Group;

|Nhân viên Sales|
:Nhận thông báo trên Lark Messenger;
stop
@enduml
```

---

## 3. Sơ Đồ Thực Thể Liên Kết (ERD - Blueprint)

Bản vẽ thi công chuẩn hóa cho công cụ **Auto-Build**. Tuân thủ `Tpl_LarkBase_Convention`.

```plantuml
@startuml
title **ERD — Hệ thống Quản lý Phân ca Nga Fashion**
skinparam linetype ortho

entity "Nhân sự" as P_NhanSu {
  * Mã nhân sự (AutoNumber)
  --
  Tên nhân viên (Person)
  Loại hình (SingleSelect) : 🟡 FT, 🔵 PT
  Ngày nghỉ cố định (SingleSelect) : CN, Thứ 2
  Tổng giờ tuần này (Rollup)
  Số ngày làm tuần này (Rollup) : COUNT_DISTINCT
  Tình trạng (Formula) : 🟢 Chuẩn, 🔴 Cần chỉnh
  Trạng thái (SingleSelect)
  Ngày tạo (CreatedTime)
  Người tạo (Person)
  Ngày cập nhật (ModifiedTime)
}

entity "Danh mục ca" as P_DanhMucCa {
  * Mã ca (AutoNumber)
  --
  Tên ca (Text) : Sáng sớm, Sáng chiều...
  Bắt đầu (DateTime)
  Kết thúc (DateTime)
  Số giờ (Number)
  Hình thức (SingleSelect) : Online, Offline
  Trạng thái (SingleSelect)
  Ngày tạo (CreatedTime)
  Ngày cập nhật (ModifiedTime)
}

entity "Lịch làm việc" as P_LichLamViec {
  * Mã lịch trực (AutoNumber)
  --
  Nhân viên (DuplexLink) -> Nhân sự
  Ca làm việc (DuplexLink) -> Danh mục ca
  Ngày làm việc (DateTime)
  Tuần (Formula)
  Thứ (Formula)
  Ghi chú (Text)
  Trạng thái (SingleSelect)
  Ngày tạo (CreatedTime)
  Người tạo (Person)
  Ngày cập nhật (ModifiedTime)
}

P_NhanSu "1" -- "N" P_LichLamViec
P_DanhMucCa "1" -- "N" P_LichLamViec
@enduml
```

---

## 4. Sơ Đồ Trình Tự: Luồng Xử Lý Solver (Message Sequence)

Mô tả cách Script tương tác với API của Lark để ghi dữ liệu.

```plantuml
@startuml
autonumber
participant "Quản lý" as Manager
participant "Script Solver" as Solver
database "Lark Base API" as API

Manager -> Solver : Click [Auto-Schedule]
Solver -> API : GET (Dữ liệu Nhân sự & Quy tắc)
API --> Solver : Trả về JSON Data
Solver -> Solver : Chạy thuật toán Solver (Phân bổ ca)
note right of Solver
  **Thuật toán 5 bước (Priority Solver):**
  1. **Init:** Đọc Staff & Off-days đầu vào.
  2. **Offline Match:** Gán 3 FT vào các ca Offline 
     để đảm bảo shop luôn mở cửa (Ưu tiên Hard Rules).
  3. **Night Match:** Gán PT vào ca Tối đêm. Nếu thiếu 
     thì gán FT làm "2 ca/ngày" (Priority Rules).
  4. **Compliance Check:** Kiểm tra WFH (<2 ngày/tuần) 
     & Trải đều ca Sáng/Chiều cho FT (Soft Rules).
  5. **Balancing:** Kiểm soát tổng giờ PT = 1/2 FT.
end note
Solver -> API : POST (Batch Create Records - Lịch làm việc)
API --> Solver : 200 OK (Success)
Solver -> Manager : Hiển thị "Đã hoàn thành xếp ca"
@enduml
```

---
**Ghi chú cho Phase 5 (Auto-Build):**
- Sử dụng các Friendly Name trong ERD (Tiếng Việt) để tạo bảng.
- Đảm bảo thiết lập `multiple: true` cho trường `Nhân viên` trong bảng `Lịch làm việc` nếu cho phép nhiều nhân sự cùng 1 ca.
