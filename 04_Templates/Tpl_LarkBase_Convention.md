---
type: Template
target: Lark Base Naming Convention
linked_by:
  - "[[Tpl_SA_Report]]"
  - "[[Tpl_UML_Guide]]"
  - "[[02_Chien_luoc_SA]]"
  - "[[03_Thiet_ke_UML]]"
---
# Quy Ước Đặt Tên & Cấu Trúc Lark Base (Naming Convention)

> **Phạm vi:** Tài liệu này là **BỘ QUY TẮC BẮT BUỘC** áp dụng cho mọi đầu ra liên quan đến Lark Base — từ Schema trong SA Report, ERD PlantUML của UML Engineer, đến lệnh Auto-Build qua Lark MCP API.
>
> **Liên kết:** [[Tpl_SA_Report]] · [[Tpl_UML_Guide]] · [[02_Chien_luoc_SA]] · [[03_Thiet_ke_UML]]

---

## 1. Quy Ước Đặt Tên Bảng (Table)

| Quy tắc | Mô tả | Ví dụ đúng | Ví dụ sai |
|---|---|---|---|
| **Tiền tố `tbl_`** | Mọi bảng bắt đầu bằng `tbl_` | `tbl_Orders` | `Orders`, `tb_Orders` |
| **PascalCase** | Tên bảng sau tiền tố viết PascalCase (chữ cái đầu mỗi từ viết hoa) | `tbl_DonHang` | `tbl_don_hang`, `tbl_donhang` |
| **Tiếng Anh ưu tiên** | Ưu tiên đặt tên tiếng Anh. Nếu nghiệp vụ đặc thù Việt Nam thì dùng tiếng Việt không dấu | `tbl_Leads`, `tbl_KhaoSat` | `tbl_Khảo_Sát` |
| **Số nhiều** | Tên bảng luôn ở dạng số nhiều (đại diện tập hợp bản ghi) | `tbl_Contacts` | `tbl_Contact` |
| **Không viết tắt** | Không viết tắt trừ từ phổ biến (HR, KPI, PO) | `tbl_Employees` | `tbl_Emps` |
| **Tối đa 30 ký tự** | Tên bảng (bao gồm `tbl_`) không quá 30 ký tự | `tbl_ServicePackages` | `tbl_ChiTietGoiDichVuTuVan` |

### Bảng Liên Kết N:N (Junction Table)
- Tiền tố: `tbl_junc_`
- Ghép tên 2 bảng cha: `tbl_junc_OrderProducts`
- Ví dụ: `tbl_Orders` ↔ `tbl_Products` → `tbl_junc_OrderProducts`

### Bảng Tra Cứu (Lookup / Master Data)
- Tiền tố: `tbl_ref_`
- Ví dụ: `tbl_ref_Departments`, `tbl_ref_ProductCategories`

---

## 2. Quy Ước Đặt Tên Trường (Field)

| Quy tắc | Mô tả | Ví dụ đúng | Ví dụ sai |
|---|---|---|---|
| **snake_case** | Tên trường viết snake_case (chữ thường, nối bằng `_`) | `order_date` | `OrderDate`, `orderdate` |
| **Tiền tố theo loại** | Các trường đặc biệt có tiền tố riêng (xem bảng bên dưới) | `fk_account_id` | `account` |
| **Đuôi `_id` cho khóa** | Trường khóa chính / khóa ngoại kết thúc bằng `_id` | `contact_id` | `contact_code` |
| **Không dùng dấu tiếng Việt** | Tên trường không dấu | `trang_thai` | `trạng_thái` |
| **Rõ nghĩa, tự giải thích** | Tên trường phải gợi ý rõ nội dung | `ngay_tao_don` | `date1` |

### Bảng Tiền Tố Trường Theo Vai Trò

| Tiền tố | Vai trò | Ví dụ |
|---|---|---|
| *(không có)* | Trường dữ liệu thông thường | `ten_khach`, `so_luong` |
| `fk_` | Khóa ngoại (Link sang bảng khác) | `fk_account_id` |
| `calc_` | Trường tính toán (Formula) | `calc_tong_tien` |
| `is_` | Trường Boolean / Checkbox | `is_active`, `is_approved` |
| `dt_` | Trường ngày tháng (DateTime) | `dt_created`, `dt_deadline` |

---

## 3. Quy Ước Loại Trường (Field Type Mapping)

> Bảng dưới đây là **bắt buộc** khi viết Schema trong SA Report và chú thích trong ERD PlantUML.

| Ký hiệu trong ERD | Lark Base Field Type | Lark MCP `type` value | Ghi chú |
|---|---|---|---|
| `(Text)` | Multiline Text | `1` | Trường mặc định |
| `(Number)` | Number | `2` | Dùng cho số lượng, giá trị |
| `(SingleSelect)` | Single Select | `3` | Danh sách cố định 1 lựa chọn |
| `(MultiSelect)` | Multiple Select | `4` | Nhiều lựa chọn |
| `(DateTime)` | DateTime | `5` | Ngày giờ |
| `(Checkbox)` | Checkbox | `7` | True/False |
| `(Person)` | Person | `11` | User picker |
| `(Phone)` | Phone Number | `13` | Điện thoại |
| `(URL)` | Hyperlink | `15` | Đường link |
| `(Attachment)` | Attachment | `17` | File đính kèm |
| `(Link)` | One-way Link | `18` | Liên kết 1 chiều |
| `(Formula)` | Formula | `20` | Công thức tính toán |
| `(DuplexLink)` | Two-way Link | `21` | Liên kết 2 chiều |
| `(AutoNumber)` | Auto Number | `1005` | Mã tự tăng |
| `(CreatedTime)` | Created Time | `1001` | Thời gian tạo (hệ thống) |
| `(ModifiedTime)` | Modified Time | `1002` | Thời gian sửa (hệ thống) |
| `(Currency)` | Currency (Number) | `2` | Dùng `ui_type: Currency` |
| `(Progress)` | Progress (Number) | `2` | Dùng `ui_type: Progress` |

---

## 4. Trường Bắt Buộc Cho Mọi Bảng (Mandatory Fields)

> Mọi bảng Lark Base tạo mới **PHẢI** có đủ các trường sau:

| # | Tên Trường | Loại | Vai trò |
|---|---|---|---|
| 1 | `<entity>_id` | `(AutoNumber)` hoặc `(Text)` | **Primary Key** — Trường đầu tiên (Index Field) |
| 2 | `trang_thai` | `(SingleSelect)` | Trạng thái bản ghi (Active, Pending, Done...) |
| 3 | `dt_created` | `(CreatedTime)` | Thời gian tạo — Audit trail |
| 4 | `dt_modified` | `(ModifiedTime)` | Lần sửa cuối — Audit trail |
| 5 | `nguoi_tao` | `(Person)` hoặc `(CreatedUser)` | Người tạo bản ghi |

---

## 5. Quy Ước Quan Hệ (Relationship Convention)

| Quan hệ | Cách thể hiện trên Lark Base | Trong ERD PlantUML |
|---|---|---|
| **1:1** | DuplexLink (`multiple: false`) | `A "1" -- "1" B` |
| **1:N** | DuplexLink (`multiple: true` phía N) | `A "1" -- "N" B` |
| **N:N** | Tạo Junction Table `tbl_junc_AB` | `A "1" -- "N" J` + `B "1" -- "N" J` |

### Quy tắc đặt tên trường Link
- Trường Link đặt theo: `fk_<tên_bảng_đích>_id`
- Ví dụ: Bảng `tbl_Orders` link tới `tbl_Accounts` → trường link tên `fk_account_id`

---

## 6. Quy Ước Giá Trị Select (Option Naming)

| Quy tắc | Mô tả | Ví dụ |
|---|---|---|
| **Viết hoa chữ đầu** | Capitalize mỗi option | `Đang xử lý`, `Hoàn thành` |
| **Emoji prefix (tuỳ chọn)** | Dùng emoji trước để dễ nhìn trên Kanban | `🟡 Chờ duyệt`, `🟢 Đã duyệt`, `🔴 Từ chối` |
| **Tiếng Việt nếu user-facing** | Option mà end-user nhìn thấy → dùng tiếng Việt | `Đang xử lý` thay vì `Processing` |
| **Tiếng Anh nếu system** | Option cho logic nội bộ / Automation → dùng tiếng Anh | `Approved`, `Rejected` |

---

## 7. Quy Ước View

| Loại View | Đặt tên | Ví dụ |
|---|---|---|
| **Grid (Mặc định)** | `vw_All_<TenBang>` | `vw_All_Orders` |
| **Kanban** | `vw_Kanban_<TieuChi>` | `vw_Kanban_TrangThai` |
| **Form** | `vw_Form_<MucDich>` | `vw_Form_TaoDon` |
| **Calendar** | `vw_Calendar_<TenBang>` | `vw_Calendar_Tasks` |
| **Gantt** | `vw_Gantt_<TenBang>` | `vw_Gantt_Projects` |
| **Gallery** | `vw_Gallery_<TenBang>` | `vw_Gallery_Products` |

---

## 8. ERD PlantUML Chuẩn Mẫu (Theo Quy Ước)

> Dưới đây là ví dụ ERD tuân thủ đầy đủ quy ước. UML Engineer và SA phải đối chiếu mọi ERD output với file này.

\`\`\`plantuml
@startuml
title **Lark Base ERD — [Tên Dự Án]**
skinparam linetype ortho

entity "tbl_Accounts" as Accounts {
  * account_id (AutoNumber)
  --
  ten_cong_ty (Text)
  linh_vuc (SingleSelect)
  so_dien_thoai (Phone)
  trang_thai (SingleSelect)
  dt_created (CreatedTime)
  dt_modified (ModifiedTime)
  nguoi_tao (Person)
}

entity "tbl_Contacts" as Contacts {
  * contact_id (AutoNumber)
  --
  fk_account_id (DuplexLink)
  ho_ten (Text)
  email (Text)
  chuc_vu (Text)
  is_primary (Checkbox)
  dt_created (CreatedTime)
  dt_modified (ModifiedTime)
}

entity "tbl_Orders" as Orders {
  * order_id (AutoNumber)
  --
  fk_account_id (DuplexLink)
  fk_contact_id (DuplexLink)
  san_pham (SingleSelect)
  calc_tong_tien (Formula)
  trang_thai (SingleSelect)
  dt_deadline (DateTime)
  dt_created (CreatedTime)
  dt_modified (ModifiedTime)
}

Accounts "1" -- "N" Contacts
Accounts "1" -- "N" Orders
Contacts "1" -- "N" Orders
@enduml
\`\`\`

---

## 9. Checklist Kiểm Tra Trước Build

> SA và UML Engineer **BẮT BUỘC** đối chiếu checklist này trước khi chuyển ERD sang Phase 5 Auto-Build.

- [ ] Mọi bảng có tiền tố `tbl_` (hoặc `tbl_junc_`, `tbl_ref_`)
- [ ] Mọi bảng có đủ 5 Mandatory Fields (ID, trạng thái, audit)
- [ ] Tên trường đúng snake_case, không dấu tiếng Việt
- [ ] Mỗi trường có chú thích Type trong ngoặc: `(Text)`, `(SingleSelect)`...
- [ ] Quan hệ ghi rõ cardinality: `1:1`, `1:N`, `N:N`
- [ ] Trường Link đặt theo `fk_<bảng>_id`
- [ ] Trường Formula đặt theo `calc_<tên>`
- [ ] Trường Boolean đặt theo `is_<tên>`
- [ ] Trường DateTime đặt theo `dt_<tên>`
- [ ] Không bảng nào vượt quá 15 field ở Phase 1
- [ ] ERD có `title` ghi rõ tên dự án
