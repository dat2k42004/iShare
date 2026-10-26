# use-case-analysis — Hướng dẫn sử dụng

Skill này đọc tài liệu Yêu cầu Chức năng (FR) đã duyệt của một module iShare
và tạo ra tài liệu Đặc tả Use Case (US) tương ứng.

## Khi nào dùng

Dùng sau khi tài liệu `FR-Mxx.md` đã được phê duyệt và lưu vào `docs/specs/fr/`.

## Cách kích hoạt

Nói với agent:

> "Tạo tài liệu use case cho module M02"
> hoặc "Phân tích use case từ file docs/specs/fr/FR-M02.md"
> hoặc "Viết US-M03"

Agent sẽ tự tìm file FR tương ứng và bắt đầu quy trình 7 bước.

## Đầu vào bắt buộc

| Mục | Nơi chứa |
|---|---|
| Tài liệu FR của module | `docs/specs/fr/FR-Mxx.md` |

## Đầu ra

| Mục | Nơi chứa |
|---|---|
| Tài liệu US của module | `docs/specs/us/US-Mxx.md` |

## Quy trình (7 bước — có cổng xác nhận)

| Bước | Nội dung | Kết quả |
|---|---|---|
| 1 | Trích xuất chức năng con | Bảng tổng hợp (Mục 1) |
| 2 | Xác định Use Case Chính | Danh sách UC + Macro Diagram (Mục 2.1–2.2) |
| 3 | Ánh xạ Actor & Quy trình | Mô tả nghiệp vụ hoàn chỉnh (Mục 2.3) |
| 4 | Phân rã Use Case con | Per-UC Diagrams + Bảng quan hệ (Mục 3) |
| 5 | Xây dựng ma trận truy vết | 100% FR → UC (Mục 4.1) |
| 6 | Vẽ sơ đồ tổng hợp | Full module diagram (Mục 4.2) |
| 7 | Kiểm tra & hoàn thiện | Tài liệu US hoàn chỉnh |

Mỗi bước dừng chờ xác nhận trước khi sang bước tiếp theo.

## Tài liệu mẫu

- Xem `docs/specs/us/US-M01.md` để biết cấu trúc đầu ra chuẩn.
- Xem `output/us-template.md` để biết template có placeholder.

