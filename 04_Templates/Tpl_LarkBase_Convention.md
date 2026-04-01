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
> **Triết lý:** Ưu tiên sự thân thiện với người dùng doanh nghiệp (Business Friendly). Tên bảng và trường phải rõ nghĩa, không chứa các tiền tố kỹ thuật gây khó hiểu.

---

## 1. Quy Ước Đặt Tên Bảng (Table)

| Quy tắc | Mô tả | Ví dụ đúng | Ví dụ sai |
|---|---|---|---|
| **Không tiền tố kỹ thuật** | Loại bỏ hoàn toàn `tbl_`, `ref_`, `junc_` | `Đơn hàng` | `tbl_Orders` |
| **Object-Based** | Tên bảng là tên đối tượng nghiệp vụ | `Khách hàng` | `Danh sách khách` |
| **Ngôn ngữ người dùng** | Sử dụng Tiếng Việt có dấu (hoặc Tiếng Anh nếu DN yêu cầu) | `Sản phẩm` | `San_pham` |
| **Danh từ số ít/nhiều** | Tên bảng nên là danh từ đại diện cho đối tượng | `Hợp đồng` | `Làm hợp đồng` |
| **Tối đa 50 ký tự** | Cho phép tên dài để rõ nghĩa nhưng không nên quá rườm rà | `Chi tiết phiếu nhập kho` | `CTPNK` |

### Bảng Liên Kết (Relationship Table)
- Không dùng `junc_`. Đặt tên theo mối quan hệ tự nhiên.
- Ví dụ: `Chi tiết đơn hàng` thay vì `tbl_junc_OrderProducts`.

---

## 2. Quy Ước Đặt Tên Trường (Field)

| Quy tắc | Mô tả | Ví dụ đúng | Ví dụ sai |
|---|---|---|---|
| **Rõ nghĩa & Tự nhiên** | Tên trường như cách người dùng gọi tên dữ liệu | `Ngày tạo đơn` | `dt_created` |
| **Không tiền tố kỹ thuật** | Loại bỏ `fk_`, `calc_`, `is_`, `dt_` | `Tổng tiền` | `calc_total_amount` |
| **Viết hoa chữ đầu** | Viết hoa chữ cái đầu tiên của mỗi từ | `Số điện thoại` | `so_dien_thoai` |
| **Tiếng Việt có dấu** | Đồng bộ với ngôn ngữ của bảng | `Trạng thái` | `trang_thai` |

### Quy tắc đặt tên cho các trường đặc biệt

| Vai trò | Cách đặt tên | Ví dụ |
|---|---|---|
| **Liên kết (Link)** | Tên của đối tượng được liên kết | `Khách hàng`, `Sản phẩm` |
| **Tính toán (Formula)** | Tên kết quả cuối cùng | `Thành tiền`, `Lợi nhuận` |
| **Lựa chọn (Select)** | Tên thuộc tính | `Phân loại`, `Nguồn khách` |
| **Ngày tháng** | Chứa từ "Ngày/Giờ/Năm" | `Ngày bắt đầu`, `Hạn thanh toán` |
| **Đúng/Sai (Checkbox)** | Câu hỏi hoặc Khẳng định | `Đã thanh toán`, `Kích hoạt?` |

---

## 3. Quy Ước Loại Trường (Field Type Mapping)

| Ký hiệu trong ERD | Lark Base Field Type | Lark MCP `type` value | Ghi chú |
|---|---|---|---|
| `(Text)` | Multiline Text | `1` | Văn bản nhiều dòng |
| `(Number)` | Number | `2` | Số lượng, điểm số |
| `(SingleSelect)` | Single Select | `3` | 1 lựa chọn |
| `(MultiSelect)` | Multiple Select | `4` | Nhiều lựa chọn |
| `(DateTime)` | DateTime | `5` | Ngày/Giờ |
| `(Checkbox)` | Checkbox | `7` | Đánh dấu |
| `(Person)` | Person | `11` | Chọn nhân sự |
| `(Phone)` | Phone Number | `13` | Số điện thoại |
| `(URL)` | Hyperlink | `15` | Đường dẫn |
| `(Attachment)` | Attachment | `17` | Đính kèm file |
| `(Link)` | One-way Link | `18` | Liên kết 1 chiều |
| `(Formula)` | Formula | `20` | Công thức |
| `(DuplexLink)` | Two-way Link | `21` | Liên kết 2 chiều |
| `(AutoNumber)` | Auto Number | `1005` | Mã tự động |
| `(CreatedTime)` | Created Time | `1001` | Ngày tạo hệ thống |
| `(ModifiedTime)` | Modified Time | `1002` | Ngày sửa hệ thống |

---

## 4. Trường Bắt Buộc Cho Mọi Bảng (Mandatory Fields)

> Mọi bảng Lark Base tạo mới **PHẢI** có đủ các trường sau (ngôn ngữ thân thiện):

| # | Tên Trường | Loại | Vai trò |
|---|---|---|---|
| 1 | `Mã <Đối tượng>` | `(AutoNumber)` hoặc `(Text)` | **Primary Key** |
| 2 | `Trạng thái` | `(SingleSelect)` | Trình trạng vận hành |
| 3 | `Ngày tạo` | `(CreatedTime)` | Audit trail |
| 4 | `Người tạo` | `(Person)` hoặc `(CreatedUser)` | Audit trail |
| 5 | `Ngày cập nhật` | `(ModifiedTime)` | Audit trail |

---

## 5. Quy Ước Quan Hệ & Liên Kết

- **Mô tả:** Tên trường liên kết phải phản ánh đúng tên bảng đích hoặc vai trò của mối quan hệ.
- **Ví dụ:** Trong bảng `Đơn hàng`, trường liên kết đến `Khách hàng` sẽ tên là `Khách hàng`. Nếu có 2 liên kết đến cùng 1 bảng (ví dụ: Người phụ trách và Người duyệt), hãy đặt tên theo vai trò: `Người phụ trách`, `Người phê duyệt`.

---

## 6. Quy Ước Giá Trị Select (Option Naming)

- **Viết hoa:** `Chờ duyệt`, `Đã duyệt`.
- **Emoji:** Khuyến khích dùng để tăng trải nghiệm người dùng (UX).
- **Ví dụ:** `🟡 Đang xử lý`, `🟢 Hoàn thành`, `⚠ Quá hạn`.

---

## 7. Quy Ước View

Sử dụng tên mô tả hành động hoặc đối tượng lọc:
- `Tất cả đơn hàng` (Grid)
- `Đơn hàng theo Trạng thái` (Kanban)
- `Phiếu đăng ký mới` (Form)
- `Lịch xuất kho` (Calendar)

---

## 8. ERD PlantUML Thân Thiện (Mẫu chuẩn)

\`\`\`plantuml
@startuml
title **Lark Base ERD — Quản lý Bán hàng**
skinparam linetype ortho

entity "Khách hàng" as Accounts {
  * Mã khách hàng (AutoNumber)
  --
  Tên công ty (Text)
  Lĩnh vực (SingleSelect)
  Số điện thoại (Phone)
  Trạng thái (SingleSelect)
  Ngày tạo (CreatedTime)
  Người tạo (Person)
}

entity "Liên hệ" as Contacts {
  * Mã liên hệ (AutoNumber)
  --
  Khách hàng (DuplexLink)
  Họ và tên (Text)
  Email (Text)
  Chức vụ (Text)
  Là liên hệ chính? (Checkbox)
  Ngày tạo (CreatedTime)
}

entity "Đơn hàng" as Orders {
  * Mã đơn hàng (AutoNumber)
  --
  Khách hàng (DuplexLink)
  Người liên hệ (DuplexLink)
  Sản phẩm (SingleSelect)
  Thành tiền (Formula)
  Trạng thái (SingleSelect)
  Hạn thanh toán (DateTime)
  Ngày tạo (CreatedTime)
}

Accounts "1" -- "N" Contacts
Accounts "1" -- "N" Orders
Contacts "1" -- "N" Orders
@enduml
\`\`\`

---

## 9. Checklist Kiểm Tra Trước Build

- [ ] Tên bảng và trường không chứa `tbl_`, `fk_`, `calc_`, `dt_`, `is_`.
- [ ] Tên bảng/trường sử dụng ngôn ngữ nghiệp vụ rõ ràng (Ưu tiên Tiếng Việt có dấu).
- [ ] Mọi bảng có đủ 5 trường bắt buộc (Mã, Trạng thái, Ngày tạo, Người tạo, Ngày cập nhật).
- [ ] Tên trường Link phản ánh đúng đối tượng hoặc vai trò.
- [ ] ERD sử dụng đúng ký hiệu loại trường trong ngoặc `(Type)`.
