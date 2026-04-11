# 🚀 Lark Consult AI — Knowledge Base

Chào mừng bạn đến với Hệ thống tri thức (Knowledge Base) chính thức của **Lark Consult AI**. Đây là nơi lưu trữ toàn bộ phương pháp luận, quy trình tư vấn chuẩn (SOP), thư viện giải pháp và hồ sơ khách hàng của dự án.

Hệ thống được thiết kế để tối ưu hóa việc quản lý tri thức, giúp đội ngũ consultant triển khai các giải pháp Lark & AI một cách chuyên nghiệp và nhất quán.

---

## 📂 Tổng quan cấu trúc hệ thống (Repository Structure)

Dưới đây là sơ đồ tổ chức các thư mục chính trong dự án:

### 1. [00_MOC](./00_MOC) — Maps of Content
Điểm bắt đầu để điều hướng. Chứa các file liên kết giúp tra cứu nhanh các khu vực tri thức.
- `Home`: Trang chủ tổng quan hệ thống.
- `MOC Business`: Tri thức về mô hình kinh doanh & vận hành.
- `MOC Usecases`: Chỉ mục các giải pháp thực tế.

### 2. [01_Business_Model](./01_Business_Model) — Mô hình Kinh doanh
Lưu trữ các tài liệu định hướng chiến lược, tầm nhìn, sứ mệnh và các gói dịch vụ tư vấn của Lark Consult AI.

### 3. [02_Consulting_Process](./02_Consulting_Process) — Quy trình Tư vấn (SOP)
Bộ quy trình tiêu chuẩn qua 6 giai đoạn triển khai dự án:
- **Giai đoạn 1 — BA:** Khám phá nhu cầu & Phân tích hiện trạng.
- **Giai đoạn 2 — SA:** Xây dựng kiến trúc giải pháp kỹ thuật.
- **Giai đoạn 3 — UML:** Thiết kế sơ đồ quy trình & ERD Blueprint.
- **Giai đoạn 4 — Build:** Triển khai thực tế trên nền tảng Lark.
- **Giai đoạn 5 — Handoff:** Đào tạo & Bàn giao hệ thống.
- **Giai đoạn 6 — User Documentation:** Xây dựng tài liệu hướng dẫn End-user (theo chuẩn Swimlane & Form Table).

### 4. [03_Usecases_Lark_AI](./03_Usecases_Lark_AI) — Thư viện Giải pháp
Kho lưu trữ các bài toán thực tế đã được giải quyết (Fashion, Marketing, HR, Finance...), phục vụ việc tái sử dụng và demo cho khách hàng mới.

### 5. [04_Templates](./04_Templates) — Hệ thống Biểu mẫu Standard
Tổng hợp các template chuẩn cho mọi giai đoạn:
- Template Báo cáo BA/SA.
- Template thiết kế UML.
- **Tpl_User_Guide**: Mẫu tài liệu hướng dẫn sử dụng chuyên nghiệp cho khách hàng.

### 6. [05_Clients](./05_Clients) — Hồ sơ Khách hàng
Nơi lưu trữ dữ liệu triển khai thực tế của từng dự án dự án. Mỗi khách hàng được tổ chức trong một thư mục riêng biệt với đầy đủ hồ sơ từ lúc bắt đầu đến khi bàn giao.

### 7. [Diagram](./Diagram) & [Resources](./Resources)
- **Diagram**: Lưu trữ mã nguồn PlantUML và các sơ đồ kiến trúc.
- **Resources**: Công cụ hỗ trợ, tài liệu tham khảo và tài sản thương hiệu.

---

## 🛠️ Nguyên tắc vận hành

1. **Tính Nhất Quán (Standardization)**: Mọi dự án mới phải bắt đầu từ các Template chuẩn tại thư mục `04_Templates`.
2. **Trực quan hóa (Visualization)**: Mọi quy trình trong tài liệu hướng dẫn phải có sơ đồ Swimlane PlantUML để actor dễ dàng hình dung luồng công việc.
3. **Quản lý theo Role**: Tài liệu hướng dẫn End-user phải được viết theo từng vai trò cụ thể, chi tiết đến từng trường thông tin (Field-level documentation).

---
*© 2026 Lark Consult AI — Professionalizing Lark & AI Consultation.*
