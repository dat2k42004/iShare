# Đầu vào của skill use-case-analysis

Mọi đường dẫn tính từ gốc repo iShare.

## Tệp bắt buộc

| Tệp | Vai trò | Bắt buộc |
|---|---|---|
| `docs/specs/fr/FR-Mxx.md` | Tài liệu Yêu cầu Chức năng của module cần phân tích | **Có** |

Thiếu tệp FR → dừng và báo người dùng. Không làm tiếp.

## Các mục cần đọc trong FR-Mxx.md

| Mục FR | Nội dung | Dùng ở Bước |
|---|---|---|
| Metadata (bảng đầu) | Tên module, phiên bản, ngày lập | 1 — điền metadata US |
| Mục 1 (Mục đích) | Phạm vi và mục tiêu của module | 1 — hiểu bối cảnh |
| Mục 4.2 (Vai trò) | Danh sách Actor và mô tả | 3 — xác định Actor |
| Mục 4.3 (Ma trận quyền) | Actor nào có quyền gì | 3 — liên kết Actor với UC |
| Mục 4.4 (Danh sách chức năng) | Mã và tên các chức năng con `FR-Mxx-nn` | 1 — bảng Mục 1 |
| Mục 5.x (Yêu cầu chi tiết) | Mô tả chi tiết từng chức năng và Business Rules | 2, 3, 4 |
| Mục 5.17 / BR (Business Rules) | Quy tắc nghiệp vụ | 4 — điều kiện UC con |

## Tệp tham khảo (không bắt buộc, giúp hiểu ngữ cảnh)

| Tệp | Dùng để |
|---|---|
| `docs/specs/us/US-M01.md` | Tài liệu mẫu đầu ra — đọc trước khi bắt đầu module đầu tiên |
| `docs/_temp/iShare_modules.md` | Bức tranh toàn cảnh các module, phụ thuộc |

## Cách xác định số module

- Từ tên file: `FR-M02.md` → module `M02`, số `02`.
- Tài liệu US đầu ra sẽ là: `docs/specs/us/US-M02.md`.
- Mã UC Chính: `UC-C01`, `UC-C02`, ... (đặt lại từ đầu cho mỗi module).
- Mã UC con: `UC-01.1`, `UC-01.2`, ... (số đầu là số thứ tự UC Chính).

