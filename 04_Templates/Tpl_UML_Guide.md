---
type: Template
target: UML References
---
# Hướng Dẫn Vẽ Sơ Đồ Thiết Kế (UML Guide for Lark)

Bộ Guideline dành cho UML Engineer. Được tối ưu hoá để dùng mã lệnh PlantUML vẽ logic chạy cực chuẩn trên nền tảng Lark.

## Nguyên tắc hiển thị Lark trên Sơ đồ
| Thành phần Lark | Ký hiệu PlantUML | Giải thích |
|---|---|---|
| **Lark Base** | `database "Lark Base\n(Record Store)"` | Kho lưu trữ dữ liệu chính. |
| **Lark Approval** | `rectangle "Lark Approval\n(Workflow Gate)"` | Luồng xét duyệt/cổng logic. |
| **Lark Bot** | `queue "Lark Bot\n(Messenger)"` | Kênh phân phát thông báo rẽ nhánh. |
| **Lark AnyCross** | `hexagon "AnyCross\n(Integrator)"` | Hệ thống đẩy/chuyển dữ liệu qua nền tảng khác. |

---

## Mẫu 1: Context Diagram (Sơ đồ hệ thống tổng)
Dùng ở Phase 1 hoặc 3.
\`\`\`plantuml
@startuml
skinparam rectangle {
  BackgroundColor #F0F4FF
  BorderColor #3366CC
}
actor "Nhân viên Bán lẻ" as Staff
rectangle "Lark Suite\n(Collaboration Hub)" as Lark
rectangle "Hệ thống POS\n(External)" as POS

Staff --> Lark : 1. Submit Báo cáo chốt ca
POS --> Lark : 2. Đồng bộ tổng doanh thu (API)
@enduml
\`\`\`

---

## Mẫu 2: ERD Tự Động Xóa / Tự Động Build (Dành cho Auto-Build Bot)
Chuẩn xác Type để công cụ Lark MCP đọc hiểu.
> ⚠️ **Bắt buộc tuân thủ:** [[Tpl_LarkBase_Convention]] — Đối chiếu checklist trước khi chuyển ERD sang Phase 5.
\`\`\`plantuml
@startuml
entity "tbl_KhaoSats" as P_KhaoSat {
  * khaosat_id (AutoNumber)
  --
  loai_kh (SingleSelect)
  lien_he (Person)
  trang_thai (SingleSelect)
  dt_created (CreatedTime)
  dt_modified (ModifiedTime)
  nguoi_tao (Person)
}
entity "tbl_DanhGias" as P_DanhGia {
  * danhgia_id (AutoNumber)
  --
  fk_khaosat_id (DuplexLink)
  diem_rating (Number)
  trang_thai (SingleSelect)
  dt_created (CreatedTime)
  dt_modified (ModifiedTime)
}
P_KhaoSat "1" -- "N" P_DanhGia
@enduml
\`\`\`

---

## Mẫu 3: Sơ đồ Trình Tự (Sequence) Approval & Automation
\`\`\`plantuml
@startuml
autonumber
participant "Nhân sự" as HR
participant "Lark Approval" as Approver
participant "Lark Automations" as Auto
database "Lark Base" as Base

HR -> Approver : 1. Điền Form Nghỉ phép
alt Sếp duyệt
  Approver -> Auto : 2. Trạng thái Approved
  Auto -> Base : 3. Nạp data, trừ ngày phép
else Sếp từ chối
  Approver -> HR : Gửi Chat báo từ chối qua Bot
end
@enduml
\`\`\`
