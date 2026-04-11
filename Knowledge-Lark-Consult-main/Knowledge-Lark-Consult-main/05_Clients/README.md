# 📁 05_Clients — Hồ sơ Khách Hàng

Thư mục này lưu trữ hồ sơ đầy đủ của các khách hàng đã và đang được tư vấn triển khai.

---

## 📐 Quy ước lưu trữ file (File Convention)

Mỗi khách hàng có **một thư mục riêng** theo chuẩn: `[MaKhachHang]_[TenCongTy]/`

> Ví dụ: `CL001_AnhDuong_Trading/`, `CL002_VietLogistics/`

Toàn bộ tài liệu phân tích đều được **tập trung (centralize)** trong thư mục này — không lưu rải rác ở Desktop hay Drive cá nhân.

### Cấu trúc chuẩn một thư mục khách hàng

```
[MaKH]_[TenCongTy]/
├── 00_Overview.md              ← Thông tin tổng quan + trạng thái tiến độ
├── 01_Problem_Statement.md     ← Đề bài: AS-IS / TO-BE / trích dẫn lời khách
├── 02_BA_Report.md             ← Kết quả phân tích BA (từ Tpl_BA_Report)
├── 03_SA_Report.md             ← Kết quả SA (từ Tpl_SA_Report)
├── 04_UML/                     ← Toàn bộ sơ đồ PlantUML (ERD, Sequence, Swimlane)
│   └── erd_blueprint.puml
├── 05_Communication_Log.md     ← Inbox trao đổi theo timeline (Zalo, Email, Gặp)
├── 06_User_Guide/              ← Tài liệu hướng dẫn end-user sau triển khai
│   └── [TenQuyTrinh]_Guide.md
└── 07_References/              ← Tài liệu đính kèm (PDF, Excel, ảnh, link)
    └── [tên file]
```

### Quy tắc đặt tên file

| Loại file | Quy ước đặt tên | Ví dụ |
|---|---|---|
| Tài liệu phân tích | `[Mã]_[TênTàiLiệu].md` | `02_BA_Report.md` |
| Sơ đồ PlantUML | `[loai]_[nguyen-the].puml` | `erd_don-hang.puml` |
| Hướng dẫn user | `[TenQuyTrinh]_Guide.md` | `Duyet_De_Xuat_Guide.md` |
| File đính kèm | Giữ nguyên tên gốc | `bao_cao_nam_2024.xlsx` |

---

## Cách tạo hồ sơ khách hàng mới

1. Tạo thư mục `[MaKH]_[TenCongTy]/` trong `05_Clients/`
2. Copy nội dung từ [[Tpl_Client_Project]] để điền `00_Overview.md`
3. Bắt đầu điền `01_Problem_Statement.md` ngay sau buổi gặp đầu tiên
4. Cập nhật `05_Communication_Log.md` sau mỗi cuộc trao đổi

---

## Danh sách Khách Hàng

| Mã KH | Tên Công Ty | Ngành | Trạng Thái | Gói DV | Link |
|---|---|---|---|---|---|
| _(Chưa có)_ | | | | | |
