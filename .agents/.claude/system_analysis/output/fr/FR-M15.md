---
module: M15
ten_module: Analytics & Stats
ma_tai_lieu: FR-M15
phien_ban: 1.0
trang_thai: Đã chốt
ngay: 2026-10-24
tac_gia: Phạm Văn Đức
moc_nguon: DEC-269, QA-475, ISS-413, OPEN-012
steps_completed: [1, 2, 3, 4, 5, 6, 7]
---
# Tài liệu yêu cầu chức năng — M15 Analytics & Stats

| Mã tài liệu | FR-M15 |
|---|---|
| Dự án | iShare |
| Module | M15 — Analytics & Stats |
| Trạng thái | Đã chốt |
| Phiên bản | 1.0 |
| Ngày | 2026-10-24 |
| Tác giả | Phạm Văn Đức |

<!-- Quy ước chung cho mọi bảng dưới đây:
     - Thân tài liệu không ghi nguồn. Nguồn của mọi ID nằm ở Phụ lục A.
     - Ô không có nội dung ghi "—". Không xóa cột.
     - Mục chưa tới bước làm thì để dòng "(Chưa làm — bước N)". -->

## 1. Tổng quan

### 1.1 Mục đích

Module giúp Admin theo dõi tình hình của nền tảng qua ba trang thống kê: người dùng, nội dung và kiểm duyệt.
Mọi số liệu lấy từ dữ liệu nghiệp vụ sẵn có, tính tại lúc xem và lọc theo bốn khoảng thời gian chọn sẵn, phục vụ vận hành, demo và báo cáo.

### 1.2 Phạm vi

**Trong phạm vi:**

- Quyền xem: chỉ Admin mở được các trang thống kê.
- Thống kê người dùng: số tài khoản theo trạng thái (gồm hai nhóm chờ hoàn tất đăng ký và nhóm DELETED), xu hướng đăng ký mới, phân bố theo vai trò, theo Lớp/Khối, theo mức cảnh cáo.
- Thống kê nội dung: số bài theo trạng thái đăng và trạng thái kiểm duyệt, xu hướng bài mới, phân bố bài theo Topic, xu hướng bình luận mới, tỷ lệ Topic gợi ý được giữ lại (do M13 tính).
- Thống kê kiểm duyệt: báo cáo theo trạng thái và theo lý do (tách theo loại đối tượng), cảnh cáo theo mức theo thời gian, ban và gỡ ban theo thời gian, khiếu nại theo loại và kết quả.
- Bộ lọc thời gian dùng chung cho cả ba trang: Hôm nay, 7 ngày, 30 ngày, Toàn thời gian (lựa chọn sẵn khi mở trang); biểu đồ xu hướng theo giờ, ngày hoặc tháng.
- Số liệu tính tại lúc mở trang hoặc đổi khoảng thời gian.

**Ngoài phạm vi:**

- Chỉ số hoạt động người dùng kiểu DAU/WAU/MAU và hạ tầng ghi sự kiện chung — đã quyết không làm ở MS1 (hoãn có chủ đích).
- Xuất dữ liệu ra CSV — hoãn có chủ đích, không làm ở MS1.
- Chọn khoảng thời gian tùy ý — không làm.
- Mod xem thống kê, bảng xếp hạng Mod xử lý nhiều báo cáo nhất — đã cân nhắc và bỏ.
- Tỷ lệ bài trong nhóm so với bài độc lập, tỷ lệ bài ẩn danh — đã cân nhắc và bỏ.
- Số upvote theo ngày, Tag phổ biến (có trong draft) — đã bỏ.
- Cách tính tỷ lệ Topic gợi ý được giữ lại — M13. Chỉ số đánh giá AI kiểm duyệt; precision, recall, F1, accuracy của gợi ý Topic — không tính (M13).
- Thống kê cá nhân của từng người dùng (số bài, số sao, người theo dõi), bảng xếp hạng — M02, M12.
- Ghi nhận, lưu trữ dữ liệu được thống kê: tài khoản (M01), bài (M03), bình luận (M04), Topic và phản hồi gợi ý Topic (M05), báo cáo, cảnh cáo, ban (M08), khiếu nại (M09).
- Nhật ký kiểm duyệt, nhật ký thao tác Admin, cấu hình hệ thống — M08, M10.

## 2. Thuật ngữ và viết tắt

### 2.1 Thuật ngữ

| Thuật ngữ | Định nghĩa |
|---|---|
| Trang thống kê | Một trong ba trang chỉ Admin xem: thống kê người dùng, thống kê nội dung, thống kê kiểm duyệt. |
| Khoảng thời gian | Lựa chọn của bộ lọc dùng chung cho ba trang: Hôm nay, 7 ngày, 30 ngày, Toàn thời gian (BR-M15-03). |
| Giờ Việt Nam | Múi giờ Asia/Ho_Chi_Minh (UTC+7), cố định, không đổi giờ theo mùa. Mọi ranh giới ngày của module tính theo múi giờ này. |
| Hôm nay | Từ 00:00 của ngày đang xem, giờ Việt Nam, tới lúc xem. |
| 7 ngày, 30 ngày | Ngày lịch, gồm hôm nay: từ 00:00 của ngày thứ 7 (hoặc thứ 30) tính lùi cả hôm nay, giờ Việt Nam, tới lúc xem. |
| Toàn thời gian | Mọi dữ liệu đang có, không giới hạn thời gian; là lựa chọn sẵn khi mở trang. |
| Xu hướng | Chuỗi số đếm theo thời gian trong khoảng đã chọn, hiển thị dạng biểu đồ; mỗi cột một giờ, một ngày hoặc một tháng (BR-M15-19). |
| Đăng ký mới | Một tài khoản được tạo: xong bước 1 đăng ký email, hoặc lần đầu đăng nhập Google (M01). |
| Chờ xác minh email | Nhóm thống kê: tài khoản ACTIVE chưa xác minh email. |
| Chờ hoàn tất hồ sơ | Nhóm thống kê: tài khoản ACTIVE đã xác minh email (hoặc tài khoản Google) nhưng chưa xong bước 3 đăng ký. |
| Chưa khai | Nhóm thống kê Lớp/Khối: tài khoản không khai Lớp/Khối trên hồ sơ. |
| Trạng thái tài khoản | ACTIVE, DEACTIVATED, DELETED, BANNED (M01). |
| Vai trò | USER, MODERATOR, ADMIN (M10). |
| Lớp/Khối (trên hồ sơ) | Cấp học 10, 11 hoặc 12 người dùng tự khai, không bắt buộc (M02). |
| Mức cảnh cáo | Sạch (0 lần), LIGHT (1–2 lần), MEDIUM (3–4 lần), HEAVY (5–6 lần) (M08). |
| Trạng thái đăng của bài | Nháp, Chờ duyệt, Đã đăng, Tự ẩn, Bị từ chối, Đã xóa, Đã xóa hẳn (M03). |
| Trạng thái kiểm duyệt của bài | Bình thường, Bị gắn cờ, Bị Mod ẩn (M03). |
| Thời điểm tạo (bài) | Lúc bài được tạo (M03). |
| Thời điểm đăng (bài) | Lúc bài chuyển sang Đã đăng (M03). |
| Thời điểm đăng (bình luận) | Lúc hệ thống ghi nhận bình luận được gửi (M04). |
| Phản hồi gợi ý Topic | Bản ghi so sánh các Topic AI gợi ý với các Topic tác giả chọn cuối cùng (M05). |
| Tỷ lệ Topic gợi ý được giữ lại | Chỉ số chất lượng gợi ý Topic do M13 tính (BR-M15-09). |
| Báo cáo | Một lần người dùng tố cáo một đối tượng, hoặc một mục do AI tạo (M08). Trạng thái: Mở, Đã xử lý. |
| Vụ báo cáo | Tập các báo cáo đang mở về cùng một đối tượng; kết luận Có xử lý hoặc Bác bỏ (M08). |
| Lý do báo cáo | Lựa chọn trong danh sách riêng của loại đối tượng bị báo cáo (BR-M15-12). |
| Cảnh cáo | Một lần người dùng bị ghi nhận vi phạm, do AI hoặc Mod, Admin ra. Trạng thái: Đang tính, Đã bỏ, Bị lật (M08, M09). |
| Ban | Khóa tài khoản do Mod, Admin quyết định; loại tạm thời hoặc vĩnh viễn. Trạng thái: Đang hiệu lực, Hết hạn, Đã gỡ, Bị lật (M08, M09). |
| Gỡ ban | Thao tác Mod, Admin kết thúc một ban đang hiệu lực (M08). |
| Khiếu nại | Yêu cầu phản đối một xử lý kiểm duyệt. Loại: ban, cảnh cáo, bài viết. Trạng thái: Chờ xét, Đã kết luận (Chấp nhận hoặc Từ chối) (M09). |

### 2.2 Viết tắt

| Viết tắt | Đầy đủ |
|---|---|
| FR | Functional Requirement — yêu cầu chức năng |

## 3. Thông tin đầu vào

### 3.1 Tài liệu đầu vào

| Tài liệu | Phiên bản / mốc |
|---|---|
| Draft: docs/_temp/iShare_modules.md, iShare_specs_general.md | Theo ngày sửa tệp |
| Register: decisions, qa-log, issue-queue, open-issues, glossary, module-registry | DEC-269, QA-475, ISS-413, OPEN-012 (khớp `moc_nguon`) |

### 3.2 Tài liệu liên quan

| Module | Liên quan ở điểm nào |
|---|---|
| M01 Authentication & Account | Trạng thái tài khoản, mức xác minh và việc tạo tài khoản mới là nguồn của thống kê người dùng. |
| M02 User Profile | Lớp/Khối trên hồ sơ cho phân bố theo Lớp/Khối. |
| M03 Post & Content | Trạng thái đăng, trạng thái kiểm duyệt, thời điểm tạo và thời điểm đăng của bài là nguồn của thống kê nội dung. |
| M04 Comment | Thời điểm đăng của bình luận là nguồn của xu hướng bình luận mới; bình luận bị ẩn, bị xóa vẫn còn dữ liệu. |
| M05 Topic & Tag | Danh mục Topic, Topic của bài, bản ghi phản hồi gợi ý Topic. |
| M08 Moderation | Báo cáo, vụ việc, cảnh cáo, ban, gỡ ban là nguồn của thống kê kiểm duyệt; mức cảnh cáo của tài khoản. |
| M09 Appeal | Loại và kết quả khiếu nại. |
| M10 Admin Panel | Vai trò của tài khoản (chỉ Admin xem thống kê, phân bố theo vai trò); M15 không có cờ tính năng. |
| M13 AI Layer | Tính tỷ lệ Topic gợi ý được giữ lại theo khoảng thời gian. |

## 4. Tổng quan chức năng

### 4.1 Luật, tiêu chuẩn liên quan

Không có.

### 4.2 Vai trò

| Vai trò | Mô tả trong module này |
|---|---|
| Guest | Người chưa đăng nhập. Không xem được trang thống kê nào. |
| User | Người dùng đã đăng nhập. Không xem được trang thống kê nào. |
| Mod | Có quyền của User. Không xem được trang thống kê nào, kể cả thống kê kiểm duyệt. |
| Admin | Xem ba trang thống kê người dùng, nội dung, kiểm duyệt; chọn khoảng thời gian cho số liệu. |

### 4.3 Ma trận quyền

| Hành động | Guest | User | Mod | Admin | Yêu cầu |
|---|---|---|---|---|---|
| Xem thống kê người dùng | ✗ | ✗ | ✗ | ✓ | FR-M15-01.01, FR-M15-01.12 |
| Xem thống kê nội dung | ✗ | ✗ | ✗ | ✓ | FR-M15-02.01, FR-M15-02.16 |
| Xem thống kê kiểm duyệt | ✗ | ✗ | ✗ | ✓ | FR-M15-03.01, FR-M15-03.09, FR-M15-03.16 |

<!-- Ô nói thẳng: cột Admin (QA-241 "Chỉ ADMIN truy cập được cả 3 dashboard"; DEC-225 "Analytics (M15) is ADMIN-only");
     cột Mod (QA-241: đã cân nhắc mở Moderation Stats cho MOD và bỏ).
     Ô suy ra: cột Guest, User (QA-241 "Chỉ ADMIN" ⇒ vai trò khác bị từ chối). -->

### 4.4 Danh sách chức năng

| ID | Chức năng | Tác nhân chính | Kích hoạt |
|---|---|---|---|
| FR-M15-01 | Xem thống kê người dùng | Admin | Admin mở trang thống kê người dùng, hoặc đổi khoảng thời gian trên trang |
| FR-M15-02 | Xem thống kê nội dung | Admin | Admin mở trang thống kê nội dung, hoặc đổi khoảng thời gian trên trang |
| FR-M15-03 | Xem thống kê kiểm duyệt | Admin | Admin mở trang thống kê kiểm duyệt, hoặc đổi khoảng thời gian trên trang |

### 4.5 Mốc và ưu tiên

Toàn bộ yêu cầu của module thuộc MS1, ưu tiên **Could** (dòng M15 của bảng Module List và bảng MoSCoW Summary
của module-registry: Could gồm M14, M15). Không có yêu cầu ngoại lệ về ưu tiên.

## 5. Yêu cầu chức năng


### 5.1 FR-M15-01 Xem thống kê người dùng

**Yêu cầu cấp trên:** Hệ thống phải cho phép Admin xem số tài khoản theo trạng thái, vai trò, Lớp/Khối, mức cảnh cáo và xu hướng đăng ký mới, theo khoảng thời gian đã chọn.

**Lý do:** Cho Admin nắm tình hình người dùng phục vụ vận hành, demo và báo cáo chỉ từ dữ liệu đã có; số tài khoản theo mốc thời gian đã đủ cho mục đích này, nên không xây thêm hạ tầng theo dõi hoạt động (DAU/WAU/MAU). Chỉ Admin xem để giữ module đơn giản.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M15-01.01 | Khi Admin mở trang thống kê người dùng, hệ thống phải hiện số tài khoản theo sáu nhóm trạng thái Chờ xác minh email, Chờ hoàn tất hồ sơ, ACTIVE, DEACTIVATED, BANNED, DELETED, mỗi tài khoản thuộc đúng một nhóm (BR-M15-07, BR-M15-20). |
| FR-M15-01.02 | Khi Admin mở trang thống kê người dùng, hệ thống phải hiện xu hướng đăng ký mới dạng biểu đồ, đếm mọi tài khoản được tạo trong khoảng, kể cả tài khoản về sau chưa hoàn tất đăng ký hoặc đã xóa (BR-M15-07, BR-M15-20). |
| FR-M15-01.03 | Khi Admin mở trang thống kê người dùng, hệ thống phải hiện số tài khoản theo từng vai trò USER, MODERATOR, ADMIN (BR-M15-07). |
| FR-M15-01.04 | Khi Admin mở trang thống kê người dùng, hệ thống phải hiện số tài khoản theo bốn nhóm Lớp/Khối trên hồ sơ 10, 11, 12, Chưa khai (BR-M15-07, BR-M15-20). |
| FR-M15-01.05 | Khi Admin mở trang thống kê người dùng, hệ thống phải hiện số tài khoản theo năm nhóm Sạch, LIGHT, MEDIUM, HEAVY, BANNED, mỗi tài khoản thuộc đúng một nhóm: tài khoản BANNED chỉ ở nhóm BANNED, tài khoản ADMIN ở nhóm Sạch (BR-M15-07, BR-M15-20). |
| FR-M15-01.06 | Hệ thống phải không có chỉ số người dùng hoạt động (DAU, WAU, MAU) và không ghi thêm dữ liệu hoạt động của người dùng để thống kê (BR-M15-06). |
| FR-M15-01.07 | Khi Admin chọn một khoảng thời gian khác, hệ thống phải tính lại mọi chỉ số của trang theo khoảng đó (BR-M15-03). |
| FR-M15-01.08 | Hệ thống phải chỉ cho chọn khoảng thời gian trong bốn lựa chọn Hôm nay, 7 ngày, 30 ngày, Toàn thời gian; không có chọn khoảng tùy ý (BR-M15-03). |
| FR-M15-01.09 | Hệ thống phải tính số liệu từ dữ liệu hiện có tại lúc Admin mở trang hoặc đổi khoảng thời gian, không dùng số liệu tính sẵn từ trước (BR-M15-05). |
| FR-M15-01.10 | Hệ thống phải xếp mỗi dữ liệu vào khoảng thời gian theo ngày giờ Việt Nam của thời điểm gắn với nó (BR-M15-04). |
| FR-M15-01.11 | Nếu trong khoảng đã chọn không có dữ liệu nào thuộc một nhóm, hệ thống phải hiện số 0 cho nhóm đó. |
| FR-M15-01.12 | Nếu người chưa đăng nhập hoặc tài khoản không có vai trò ADMIN mở trang, hệ thống phải từ chối (BR-M15-01). |
| FR-M15-01.13 | Hệ thống phải cho Admin mở trang mà không phụ thuộc cờ tính năng nào (BR-M15-02). |
| FR-M15-01.14 | Hệ thống phải không có thao tác xuất số liệu của trang ra tệp (BR-M15-15). |
| FR-M15-01.15 | Hệ thống phải chỉ đếm tài khoản đã xong bước 3 đăng ký và không ở trạng thái DELETED ở các phân bố theo vai trò, Lớp/Khối, mức cảnh cáo (BR-M15-20). |
| FR-M15-01.16 | Khi Admin mở trang, hệ thống phải chọn sẵn khoảng Toàn thời gian (BR-M15-03). |
| FR-M15-01.17 | Hệ thống phải đếm ở mọi chỉ số của trang các đối tượng được tạo, hoặc các sự kiện xảy ra, trong khoảng đã chọn, và xếp nhóm theo trạng thái của đối tượng tại lúc xem (BR-M15-18). |
| FR-M15-01.18 | Khi Admin chọn 7 ngày hoặc 30 ngày, hệ thống phải lấy khoảng từ 00:00 của ngày thứ 7 hoặc thứ 30 tính lùi cả hôm nay, giờ Việt Nam, tới lúc xem (BR-M15-04). |
| FR-M15-01.19 | Hệ thống phải chia biểu đồ xu hướng theo giờ khi chọn Hôm nay, theo ngày khi chọn 7 ngày hoặc 30 ngày, theo tháng khi chọn Toàn thời gian (BR-M15-19). |

### 5.2 FR-M15-02 Xem thống kê nội dung

**Yêu cầu cấp trên:** Hệ thống phải cho phép Admin xem số bài viết theo trạng thái đăng, trạng thái kiểm duyệt và Topic, xu hướng bài viết mới, xu hướng bình luận mới và tỷ lệ Topic gợi ý được giữ lại, theo khoảng thời gian đã chọn.

**Lý do:** Chỉ giữ các chỉ số phục vụ vận hành rõ ràng; tỷ lệ bài nhóm, bài ẩn danh bị bỏ vì thêm nhiễu. Tỷ lệ Topic gợi ý được giữ lại cho Admin theo dõi chất lượng gợi ý Topic của AI theo thời gian.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M15-02.01 | Khi Admin mở trang thống kê nội dung, hệ thống phải hiện số bài viết theo sáu trạng thái đăng Chờ duyệt, Đã đăng, Tự ẩn, Bị từ chối, Đã xóa, Đã xóa hẳn (BR-M15-08, BR-M15-21). |
| FR-M15-02.02 | Khi Admin mở trang thống kê nội dung, hệ thống phải hiện số bài viết theo từng trạng thái kiểm duyệt Bình thường, Bị gắn cờ, Bị Mod ẩn (BR-M15-08). |
| FR-M15-02.03 | Khi Admin mở trang thống kê nội dung, hệ thống phải hiện xu hướng bài viết mới dạng biểu đồ, xếp mỗi bài theo thời điểm đăng (BR-M15-08, BR-M15-21). |
| FR-M15-02.04 | Khi Admin mở trang thống kê nội dung, hệ thống phải hiện số bài viết theo từng Topic trong danh mục Topic hiện tại (BR-M15-08). |
| FR-M15-02.05 | Hệ thống phải đếm bài của một Topic đã được gộp vào Topic khác ở Topic đích (BR-M15-17). |
| FR-M15-02.06 | Khi Admin mở trang thống kê nội dung, hệ thống phải hiện xu hướng bình luận mới dạng biểu đồ, đếm mọi bình luận đăng trong khoảng theo thời điểm đăng, kể cả bình luận về sau bị ẩn hoặc bị xóa (BR-M15-08, BR-M15-21). |
| FR-M15-02.07 | Khi Admin mở trang thống kê nội dung, hệ thống phải hiện tỷ lệ Topic gợi ý được giữ lại của khoảng thời gian chọn, do M13 tính (BR-M15-09). |
| FR-M15-02.08 | Nếu khoảng thời gian chọn không có phản hồi gợi ý Topic nào, hệ thống phải báo không có dữ liệu ở chỉ số tỷ lệ Topic gợi ý được giữ lại thay vì một tỷ lệ (BR-M15-09). |
| FR-M15-02.09 | Trong khi công tắc AI tổng hoặc công tắc Topic suggestion tắt, hệ thống phải vẫn hiện tỷ lệ Topic gợi ý được giữ lại tính từ các phản hồi đã ghi trong khoảng thời gian chọn (BR-M15-09). |
| FR-M15-02.10 | Hệ thống phải không có chỉ số số upvote theo ngày, Tag phổ biến, tỷ lệ bài trong nhóm so với bài độc lập, tỷ lệ bài ẩn danh, chỉ số chất lượng của AI kiểm duyệt (BR-M15-16). |
| FR-M15-02.11 | Khi Admin chọn một khoảng thời gian khác, hệ thống phải tính lại mọi chỉ số của trang theo khoảng đó (BR-M15-03). |
| FR-M15-02.12 | Hệ thống phải chỉ cho chọn khoảng thời gian trong bốn lựa chọn Hôm nay, 7 ngày, 30 ngày, Toàn thời gian; không có chọn khoảng tùy ý (BR-M15-03). |
| FR-M15-02.13 | Hệ thống phải tính số liệu từ dữ liệu hiện có tại lúc Admin mở trang hoặc đổi khoảng thời gian, không dùng số liệu tính sẵn từ trước (BR-M15-05). |
| FR-M15-02.14 | Hệ thống phải xếp mỗi dữ liệu vào khoảng thời gian theo ngày giờ Việt Nam của thời điểm gắn với nó (BR-M15-04). |
| FR-M15-02.15 | Nếu trong khoảng đã chọn không có dữ liệu nào thuộc một nhóm, hệ thống phải hiện số 0 cho nhóm đó. |
| FR-M15-02.16 | Nếu người chưa đăng nhập hoặc tài khoản không có vai trò ADMIN mở trang, hệ thống phải từ chối (BR-M15-01). |
| FR-M15-02.17 | Hệ thống phải cho Admin mở trang mà không phụ thuộc cờ tính năng nào (BR-M15-02). |
| FR-M15-02.18 | Hệ thống phải không có thao tác xuất số liệu của trang ra tệp (BR-M15-15). |
| FR-M15-02.19 | Hệ thống phải không đếm bài đang ở trạng thái Nháp ở bất kỳ chỉ số nào của trang thống kê nội dung (BR-M15-21). |
| FR-M15-02.20 | Hệ thống phải đếm bài trong nhóm và bài ẩn danh như mọi bài viết khác (BR-M15-21). |
| FR-M15-02.21 | Hệ thống phải xếp bài vào khoảng thời gian theo thời điểm tạo bài ở các chỉ số theo trạng thái đăng, trạng thái kiểm duyệt và Topic (BR-M15-21). |
| FR-M15-02.22 | Hệ thống phải đếm một bài có nhiều Topic một lần ở mỗi Topic của bài (BR-M15-21). |
| FR-M15-02.23 | Khi Admin mở trang, hệ thống phải chọn sẵn khoảng Toàn thời gian (BR-M15-03). |
| FR-M15-02.24 | Hệ thống phải đếm ở mọi chỉ số của trang các đối tượng được tạo, hoặc các sự kiện xảy ra, trong khoảng đã chọn, và xếp nhóm theo trạng thái của đối tượng tại lúc xem (BR-M15-18). |
| FR-M15-02.25 | Khi Admin chọn 7 ngày hoặc 30 ngày, hệ thống phải lấy khoảng từ 00:00 của ngày thứ 7 hoặc thứ 30 tính lùi cả hôm nay, giờ Việt Nam, tới lúc xem (BR-M15-04). |
| FR-M15-02.26 | Hệ thống phải chia biểu đồ xu hướng theo giờ khi chọn Hôm nay, theo ngày khi chọn 7 ngày hoặc 30 ngày, theo tháng khi chọn Toàn thời gian (BR-M15-19). |
| FR-M15-02.27 | Hệ thống phải đếm bài theo trạng thái đăng, trạng thái kiểm duyệt và Topic của chính bài, kể cả bài bị ẩn vì tác giả ở trạng thái DEACTIVATED, DELETED hoặc vì nhóm của bài bị ẩn (BR-M15-21). |

### 5.3 FR-M15-03 Xem thống kê kiểm duyệt

**Yêu cầu cấp trên:** Hệ thống phải cho phép Admin xem số báo cáo theo trạng thái và lý do, số cảnh cáo theo mức, số lần ban và gỡ ban, số khiếu nại theo loại và kết quả, theo khoảng thời gian đã chọn.

**Lý do:** Chọn hiện nhiều chỉ số vì mọi chỉ số đều lấy sẵn từ dữ liệu báo cáo, cảnh cáo, ban, khiếu nại của M08, M09. Không mở cho Mod và không xếp hạng Mod vì việc lọc số liệu theo từng Mod làm tăng độ phức tạp so với giá trị của một module ưu tiên Could.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M15-03.01 | Khi Admin mở trang thống kê kiểm duyệt, hệ thống phải hiện số báo cáo, đếm theo từng báo cáo, theo ba nhóm Mở, Đã xử lý – Có xử lý, Đã xử lý – Bác bỏ (BR-M15-11, BR-M15-22). |
| FR-M15-03.02 | Hệ thống phải đếm mỗi mục do AI tạo (người báo cáo "Hệ thống (AI)"), kể cả yêu cầu ban do hệ thống tạo, là một báo cáo (BR-M15-11, BR-M15-22). |
| FR-M15-03.03 | Khi Admin mở trang thống kê kiểm duyệt, hệ thống phải hiện số báo cáo theo lý do, tách theo loại đối tượng bài viết, bình luận, người dùng, nhóm, không gộp các lý do cùng tên của hai loại đối tượng khác nhau (BR-M15-12, BR-M15-22). |
| FR-M15-03.04 | Khi Admin mở trang thống kê kiểm duyệt, hệ thống phải hiện số cảnh cáo đã ra theo thời gian, xếp mỗi cảnh cáo theo mức LIGHT, MEDIUM, HEAVY tài khoản đạt ngay sau cảnh cáo đó, gồm cảnh cáo do AI và do Mod, Admin ra, kể cả cảnh cáo về sau bị bỏ hoặc bị lật (BR-M15-13, BR-M15-22). |
| FR-M15-03.05 | Khi Admin mở trang thống kê kiểm duyệt, hệ thống phải hiện số lần ban theo thời gian, tách ban tạm thời và ban vĩnh viễn, kể cả ban về sau bị lật (BR-M15-14, BR-M15-22). |
| FR-M15-03.06 | Khi Admin mở trang thống kê kiểm duyệt, hệ thống phải hiện số lần gỡ ban theo thời gian, chỉ đếm thao tác gỡ ban của Mod, Admin; ban hết hạn và ban bị lật không được đếm là gỡ ban (BR-M15-14, BR-M15-22). |
| FR-M15-03.07 | Khi Admin mở trang thống kê kiểm duyệt, hệ thống phải hiện số khiếu nại theo loại ban, cảnh cáo, bài viết; khiếu nại bài bị gỡ và khiếu nại gộp thuộc loại bài viết (BR-M15-10). |
| FR-M15-03.08 | Khi Admin mở trang thống kê kiểm duyệt, hệ thống phải hiện số khiếu nại theo ba nhóm kết quả Chờ xét, Chấp nhận, Từ chối (BR-M15-10, BR-M15-22). |
| FR-M15-03.09 | Nếu một Mod mở trang thống kê kiểm duyệt, hệ thống phải từ chối, kể cả khi chỉ xem số liệu xử lý của chính Mod đó (BR-M15-01). |
| FR-M15-03.10 | Hệ thống phải không có bảng xếp hạng Mod theo số báo cáo đã xử lý (BR-M15-16). |
| FR-M15-03.11 | Khi Admin chọn một khoảng thời gian khác, hệ thống phải tính lại mọi chỉ số của trang theo khoảng đó (BR-M15-03). |
| FR-M15-03.12 | Hệ thống phải chỉ cho chọn khoảng thời gian trong bốn lựa chọn Hôm nay, 7 ngày, 30 ngày, Toàn thời gian; không có chọn khoảng tùy ý (BR-M15-03). |
| FR-M15-03.13 | Hệ thống phải tính số liệu từ dữ liệu hiện có tại lúc Admin mở trang hoặc đổi khoảng thời gian, không dùng số liệu tính sẵn từ trước (BR-M15-05). |
| FR-M15-03.14 | Hệ thống phải xếp mỗi dữ liệu vào khoảng thời gian theo ngày giờ Việt Nam của thời điểm gắn với nó (BR-M15-04). |
| FR-M15-03.15 | Nếu trong khoảng đã chọn không có dữ liệu nào thuộc một nhóm, hệ thống phải hiện số 0 cho nhóm đó. |
| FR-M15-03.16 | Nếu người chưa đăng nhập hoặc tài khoản không có vai trò ADMIN mở trang, hệ thống phải từ chối (BR-M15-01). |
| FR-M15-03.17 | Hệ thống phải cho Admin mở trang mà không phụ thuộc cờ tính năng nào (BR-M15-02). |
| FR-M15-03.18 | Hệ thống phải không có thao tác xuất số liệu của trang ra tệp (BR-M15-15). |
| FR-M15-03.19 | Khi Admin mở trang, hệ thống phải chọn sẵn khoảng Toàn thời gian (BR-M15-03). |
| FR-M15-03.20 | Hệ thống phải đếm ở mọi chỉ số của trang các đối tượng được tạo, hoặc các sự kiện xảy ra, trong khoảng đã chọn, và xếp nhóm theo trạng thái của đối tượng tại lúc xem (BR-M15-18). |
| FR-M15-03.21 | Khi Admin chọn 7 ngày hoặc 30 ngày, hệ thống phải lấy khoảng từ 00:00 của ngày thứ 7 hoặc thứ 30 tính lùi cả hôm nay, giờ Việt Nam, tới lúc xem (BR-M15-04). |
| FR-M15-03.22 | Hệ thống phải chia biểu đồ xu hướng theo giờ khi chọn Hôm nay, theo ngày khi chọn 7 ngày hoặc 30 ngày, theo tháng khi chọn Toàn thời gian (BR-M15-19). |

### 5.4 Quy tắc nghiệp vụ

| ID | Loại | Quy tắc | Ví dụ |
|---|---|---|---|
| BR-M15-01 | Ràng buộc | Chỉ tài khoản ADMIN xem được các trang thống kê. Guest, User, Mod bị từ chối, kể cả với thống kê kiểm duyệt. | Một Mod mở trang thống kê kiểm duyệt: bị từ chối. |
| BR-M15-02 | Sự kiện | Module không có cờ tính năng; Admin luôn mở được các trang thống kê. | — |
| BR-M15-03 | Ràng buộc | Bộ lọc thời gian chỉ có bốn lựa chọn Hôm nay, 7 ngày, 30 ngày, Toàn thời gian, dùng chung cho ba trang; không chọn được khoảng tùy ý. Khi mở trang, lựa chọn sẵn là Toàn thời gian (không giới hạn thời gian). | Admin muốn xem từ 01/10 đến 15/10: không chọn được, chỉ chọn một trong bốn lựa chọn. |
| BR-M15-04 | Ràng buộc | Một dữ liệu thuộc một ngày theo giờ Việt Nam của thời điểm gắn với nó. Hôm nay là từ 00:00 ngày đang xem, giờ Việt Nam, tới lúc xem. 7 ngày, 30 ngày là ngày lịch gồm hôm nay: từ 00:00 của ngày thứ 7, thứ 30 tính lùi cả hôm nay, tới lúc xem. | Xem lúc 15:00 ngày 10/10: 7 ngày là từ 00:00 ngày 04/10 (bài đăng 08:00 ngày 04/10 được tính, bài đăng 23:00 ngày 03/10 thì không); 30 ngày là từ 00:00 ngày 11/09. Bài đăng lúc 23:30 ngày 10/10 giờ Việt Nam (16:30 UTC ngày 10/10): thuộc Hôm nay khi xem trong ngày 10/10. Bài đăng 00:10 ngày 11/10 giờ Việt Nam (17:10 UTC ngày 10/10): không thuộc Hôm nay khi xem ngày 10/10. |
| BR-M15-05 | Sự kiện | Số liệu được tính trực tiếp từ dữ liệu hiện có mỗi lần Admin mở trang hoặc đổi khoảng thời gian; không lưu sẵn, không tính theo lô định kỳ. | Một bài được đăng lúc 10:00; Admin mở trang lúc 10:01: bài đã được đếm. |
| BR-M15-06 | Sự kiện | Mọi chỉ số lấy từ dữ liệu nghiệp vụ các module đã có. Module không ghi thêm dữ liệu hoạt động của người dùng và không có chỉ số người dùng hoạt động (DAU, WAU, MAU). | — |
| BR-M15-07 | Sự kiện | Trang thống kê người dùng gồm: số tài khoản theo trạng thái (Chờ xác minh email, Chờ hoàn tất hồ sơ, ACTIVE, DEACTIVATED, BANNED, DELETED); xu hướng đăng ký mới; số tài khoản theo vai trò (USER, MODERATOR, ADMIN); theo Lớp/Khối trên hồ sơ (10, 11, 12, Chưa khai); theo mức cảnh cáo (Sạch, LIGHT, MEDIUM, HEAVY, BANNED). | — |
| BR-M15-08 | Sự kiện | Trang thống kê nội dung gồm: số bài theo trạng thái đăng (Chờ duyệt, Đã đăng, Tự ẩn, Bị từ chối, Đã xóa, Đã xóa hẳn); số bài theo trạng thái kiểm duyệt (Bình thường, Bị gắn cờ, Bị Mod ẩn); xu hướng bài đăng mới; số bài theo Topic; xu hướng bình luận mới; tỷ lệ Topic gợi ý được giữ lại. | — |
| BR-M15-09 | Tính toán | Tỷ lệ Topic gợi ý được giữ lại = tổng số Topic AI gợi ý mà tác giả giữ lại ÷ tổng số Topic AI gợi ý, trên các phản hồi gợi ý Topic được ghi trong khoảng thời gian chọn, kể cả phản hồi của tài khoản đã xóa. Khoảng không có phản hồi nào thì không có tỷ lệ. Do M13 tính, M15 hiển thị. | Ba phản hồi trong khoảng: {Toán, Vật lý, Hóa} → {Toán, Hóa} (giữ 2/3); {Ngữ văn} → {Ngữ văn, Lịch sử} (giữ 1/1); {Tin học, Toán} → {Tin học, Toán} (giữ 2/2): tỷ lệ = 5/6 ≈ 83,3%. Khoảng Hôm nay chưa có phản hồi nào: không có dữ liệu. |
| BR-M15-10 | Sự kiện | Trang thống kê kiểm duyệt gồm: số báo cáo theo trạng thái; số báo cáo theo lý do; số cảnh cáo đã ra theo mức, theo thời gian; số lần ban và gỡ ban theo thời gian; số khiếu nại theo loại (ban, cảnh cáo, bài viết) và theo kết quả (Chờ xét, Chấp nhận, Từ chối). | — |
| BR-M15-11 | Sự kiện | Báo cáo ở trạng thái Mở hoặc Đã xử lý; vụ đã xử lý có kết luận Có xử lý hoặc Bác bỏ. Mục do AI tạo (người báo cáo "Hệ thống (AI)") là một báo cáo. | — |
| BR-M15-12 | Sự kiện | Lý do báo cáo theo loại đối tượng. Bài viết (8): Spam/Quảng cáo; Nội dung sai/hiểu nhầm; Đạo văn/Vi phạm bản quyền; Quấy rối/Bắt nạt; Ngôn từ thù ghét/Phân biệt; Nội dung người lớn/Không phù hợp; Bạo lực/Đe dọa; Khác. Bình luận (7): như bài viết, bỏ Đạo văn/Vi phạm bản quyền. Người dùng (2): Quấy rối/Bắt nạt có hệ thống; Khác. Nhóm (4): Nội dung người lớn/Không phù hợp; Group giả mạo; Quấy rối/Bắt nạt có hệ thống; Khác. | — |
| BR-M15-13 | Sự kiện | Cảnh cáo do AI hoặc Mod, Admin ra. Cảnh cáo bị bỏ hoặc bị lật vẫn còn bản ghi, có đánh dấu Đã bỏ hoặc Bị lật. | — |
| BR-M15-14 | Sự kiện | Ban có hai loại, tạm thời và vĩnh viễn. Một ban đang hiệu lực kết thúc khi hết hạn (ban tạm thời, tài khoản tự về ACTIVE), khi Mod, Admin gỡ ban, hoặc khi khiếu nại được chấp nhận (ban Bị lật). Không ra ban mới khi tài khoản đang có ban hiệu lực. | — |
| BR-M15-15 | Ràng buộc | Không xuất dữ liệu thống kê ra tệp ở MS1. | — |
| BR-M15-16 | Ràng buộc | Không có: số upvote theo ngày; Tag phổ biến; thống kê cho Mod; bảng xếp hạng Mod xử lý nhiều báo cáo; tỷ lệ bài trong nhóm so với bài độc lập; tỷ lệ bài ẩn danh; chỉ số chất lượng của AI kiểm duyệt. | — |
| BR-M15-17 | Suy diễn | Phân bố bài theo Topic theo danh mục Topic hiện tại. Khi Admin gộp Topic A vào Topic B, mọi bài của A thuộc B (bài có cả A và B giữ B một lần) và A không còn trong danh mục. | Trước gộp: Toán học 40 bài, Toán 5 bài, 2 bài có cả hai. Gộp "Toán" vào "Toán học": Toán học 43 bài, không còn dòng "Toán". |
| BR-M15-18 | Ràng buộc | Mọi chỉ số đếm các đối tượng được tạo, hoặc các sự kiện xảy ra, trong khoảng đã chọn, và xếp nhóm theo trạng thái của đối tượng tại lúc xem. Toàn thời gian cho số toàn hệ thống. | 1.000 tài khoản (950 ACTIVE, 30 DEACTIVATED, 20 BANNED); 50 tài khoản tạo trong 7 ngày, nay 48 ACTIVE, 2 BANNED. Toàn thời gian: 950 / 30 / 20. 7 ngày: 48 / 0 / 2. |
| BR-M15-19 | Ràng buộc | Biểu đồ xu hướng: Hôm nay mỗi cột một giờ; 7 ngày, 30 ngày mỗi cột một ngày; Toàn thời gian mỗi cột một tháng; ranh giới theo giờ Việt Nam. | Xem lúc 15:00 ngày 10/10: Hôm nay 16 cột 00h…15h; 7 ngày 7 cột 04/10…10/10; 30 ngày 30 cột 11/09…10/10; hệ thống chạy từ 01/03 thì Toàn thời gian 8 cột T3…T10. |
| BR-M15-20 | Ràng buộc | Thống kê người dùng: ô trạng thái có sáu nhóm, mỗi tài khoản đúng một nhóm — Chờ xác minh email (ACTIVE, chưa xác minh email), Chờ hoàn tất hồ sơ (ACTIVE, đã xác minh email hoặc tài khoản Google, chưa xong bước 3), ACTIVE (đã xong bước 3), DEACTIVATED, BANNED, DELETED. Đăng ký mới đếm mọi tài khoản được tạo. Phân bố vai trò, Lớp/Khối, mức cảnh cáo chỉ đếm tài khoản đã xong bước 3 và không DELETED; Lớp/Khối có nhóm Chưa khai; ở mức cảnh cáo, tài khoản BANNED chỉ ở nhóm BANNED, tài khoản ADMIN ở nhóm Sạch. | 60 tài khoản tạo trong 7 ngày: trạng thái 6 / 4 / 48 / 0 / 1 / 1 (Chờ xác minh email / Chờ hoàn tất hồ sơ / ACTIVE / DEACTIVATED / BANNED / DELETED); đăng ký mới 60; vai trò USER 49 (48 ACTIVE + 1 BANNED, không có Mod). |
| BR-M15-21 | Ràng buộc | Thống kê nội dung: bài Nháp không được đếm ở chỉ số nào; bài nhóm, bài ẩn danh đếm như bài khác; ô trạng thái đăng, trạng thái kiểm duyệt, Topic xếp bài theo thời điểm tạo; xu hướng bài viết mới xếp theo thời điểm đăng; bài nhiều Topic đếm một lần ở mỗi Topic; xu hướng bình luận mới đếm mọi bình luận đăng trong khoảng, kể cả về sau bị ẩn hoặc bị xóa; bài bị ẩn vì tác giả DEACTIVATED, DELETED hoặc vì nhóm bị ẩn vẫn được đếm theo trạng thái của chính bài. | 7 ngày: tạo 30 bài không phải Nháp, 25 đã đăng; thêm 2 bài tạo tuần trước, đăng tuần này → ô trạng thái đăng tổng 30, xu hướng bài viết mới tổng 27. Bài {Toán, Vật lý}: Toán +1, Vật lý +1. Ngày 05/10 có 62 bình luận, 3 về sau bị xóa hoặc ẩn → cột 05/10 vẫn 62. 500 bài Đã đăng, 15 của tài khoản đã vô hiệu hóa hoặc xóa, 5 trong nhóm bị ẩn → Đã đăng 500. |
| BR-M15-22 | Ràng buộc | Thống kê kiểm duyệt: đếm theo từng báo cáo, không theo vụ; mục do AI tạo, kể cả yêu cầu ban của hệ thống, là một báo cáo; lý do tách theo loại đối tượng; cảnh cáo xếp theo mức tài khoản đạt ngay sau cảnh cáo đó, kể cả cảnh cáo về sau bị bỏ hoặc bị lật; ban đếm mọi ban ra trong khoảng, tách tạm thời và vĩnh viễn, kể cả ban về sau bị lật; gỡ ban chỉ đếm thao tác gỡ của Mod, Admin; khiếu nại theo kết quả có ba nhóm Chờ xét, Chấp nhận, Từ chối. | Bài X bị 5 người báo cáo Spam (vụ Bác bỏ); bình luận Y bị 1 người và AI báo cáo Quấy rối/Bắt nạt (vụ Mở); người dùng Z bị báo cáo Khác (Có xử lý) → Mở 2, Bác bỏ 5, Có xử lý 1; lý do: Bài viết – Spam 5, Bình luận – Quấy rối/Bắt nạt 2, Người dùng – Khác 1. Cảnh cáo thứ 3 của một người: MEDIUM. 30 ngày: 10 ban (8 tạm thời, 2 vĩnh viễn, 1 về sau bị lật), Mod gỡ 2, 3 ban hết hạn → Ban 10, Gỡ ban 2. |

### 5.5 Dữ liệu nghiệp vụ

Module không có thực thể riêng; mọi thực thể dưới đây do module khác tạo và giữ, M15 chỉ đọc để đếm.

| Thực thể | Thuộc tính nguồn đã nêu | Quan hệ |
|---|---|---|
| Tài khoản (M01) | Trạng thái tài khoản; mức xác minh; vai trò (M10); Lớp/Khối trên hồ sơ (M02); mức cảnh cáo (M08); thời điểm tạo | Có nhiều Cảnh cáo, nhiều Ban |
| Bài viết (M03) | Trạng thái đăng; trạng thái kiểm duyệt; thời điểm tạo; thời điểm đăng; nhóm, ẩn danh; các Topic (M05) | Thuộc một Tài khoản; gắn 1–3 Topic |
| Bình luận (M04) | Thời điểm đăng; đã ẩn, đã xóa | Thuộc một Bài viết |
| Topic (M05) | Tên; danh mục hiện tại (Admin thêm, gộp, xóa) | Gắn với nhiều Bài viết |
| Phản hồi gợi ý Topic (M05) | Các Topic AI gợi ý; các Topic tác giả chọn cuối cùng; thời điểm ghi | Không còn gắn danh tính khi tài khoản tác giả đã xóa |
| Tỷ lệ Topic gợi ý được giữ lại (M13) | Giá trị theo khoảng thời gian | Tính từ Phản hồi gợi ý Topic |
| Báo cáo (M08) | Loại đối tượng; một lý do; trạng thái (Mở, Đã xử lý); người báo cáo (người dùng hoặc Hệ thống (AI)) | Thuộc một Vụ báo cáo |
| Vụ báo cáo (M08) | Trạng thái (Mở, Đã xử lý); kết luận (Có xử lý, Bác bỏ) | Gồm nhiều Báo cáo về cùng một đối tượng |
| Cảnh cáo (M08) | Người ra (AI, Mod hoặc Admin); thời điểm; mức tài khoản đạt sau cảnh cáo; trạng thái (Đang tính, Đã bỏ, Bị lật) | Thuộc một Tài khoản |
| Ban (M08) | Loại (tạm thời, vĩnh viễn); thời điểm bắt đầu; trạng thái (Đang hiệu lực, Hết hạn, Đã gỡ, Bị lật) | Thuộc một Tài khoản |
| Khiếu nại (M09) | Loại (ban, cảnh cáo, bài viết); thời điểm gửi; trạng thái (Chờ xét, Đã kết luận); kết luận (Chấp nhận, Từ chối) | Về một Cảnh cáo, Ban hoặc Bài viết |

**Ma trận CRUD:**

| Thực thể | Tạo | Đọc | Sửa | Xóa |
|---|---|---|---|---|
| Tài khoản | M01 | FR-M15-01.01, FR-M15-01.02, FR-M15-01.03, FR-M15-01.04, FR-M15-01.05 | M01, M02, M08, M10 | M01 |
| Bài viết | M03 | FR-M15-02.01, FR-M15-02.02, FR-M15-02.03, FR-M15-02.04 | M03, M08, M09 | M03 |
| Bình luận | M04 | FR-M15-02.06 | M04, M08 | M04 |
| Topic | M05 | FR-M15-02.04, FR-M15-02.05 | M05 | M05 |
| Phản hồi gợi ý Topic | M05 | M13 | Không có (M05) | Không có (M05: giữ cả khi tài khoản bị xóa) |
| Tỷ lệ Topic gợi ý được giữ lại | M13 | FR-M15-02.07, FR-M15-02.08 | Không có (BR-M15-05: tính lại mỗi lần xem) | Không có (BR-M15-05) |
| Báo cáo | M08 | FR-M15-03.01, FR-M15-03.02, FR-M15-03.03 | M08 | Không có (M08) |
| Vụ báo cáo | M08 | FR-M15-03.01 | M08 | Không có (M08) |
| Cảnh cáo | M08 | FR-M15-01.05, FR-M15-03.04 | M08, M09 | Không có (BR-M15-13) |
| Ban | M08 | FR-M15-03.05, FR-M15-03.06 | M08, M09 | Không có (M08, M09: bản ghi giữ) |
| Khiếu nại | M09 | FR-M15-03.07, FR-M15-03.08 | M09 | Không có (M09) |

<!-- M15 không tạo, sửa, xóa dữ liệu nào (BR-M15-05, BR-M15-06): mọi ô Tạo, Sửa, Xóa thuộc module khác hoặc "Không có"
     theo FR đã chốt của module đó. Ô Đọc của Phản hồi gợi ý Topic là M13, vì M13 tính tỷ lệ rồi M15 hiển thị. -->

### 5.6 Chuyển trạng thái

Không áp dụng: module không có thực thể có trạng thái riêng và không làm đổi trạng thái của thực thể nào. Trạng thái
được đếm (tài khoản, bài viết, báo cáo, cảnh cáo, ban, khiếu nại) do M01, M03, M08, M09 quản lý.

### 5.7 Giao tiếp với module khác

| Hướng | Module | Nội dung ở mức nghiệp vụ | Yêu cầu |
|---|---|---|---|
| Dùng | M01 | Trạng thái tài khoản; mức xác minh (đã xác minh email, đã xong bước 3); việc tạo tài khoản mới | FR-M15-01.01, FR-M15-01.02, FR-M15-01.15 |
| Dùng | M02 | Lớp/Khối trên hồ sơ | FR-M15-01.04 |
| Dùng | M10 | Vai trò của tài khoản (xác định Admin, đếm theo vai trò) | FR-M15-01.03, FR-M15-01.12, FR-M15-02.16, FR-M15-03.16 |
| Dùng | M03 | Trạng thái đăng, trạng thái kiểm duyệt của bài; bài viết mới | FR-M15-02.01, FR-M15-02.02, FR-M15-02.03 |
| Dùng | M04 | Bình luận và thời điểm đăng của bình luận | FR-M15-02.06 |
| Dùng | M05 | Danh mục Topic, liên kết bài viết–Topic, kết quả gộp Topic | FR-M15-02.04, FR-M15-02.05 |
| Dùng | M13 | Tỷ lệ Topic gợi ý được giữ lại theo khoảng thời gian | FR-M15-02.07, FR-M15-02.08, FR-M15-02.09 |
| Dùng | M08 | Mức cảnh cáo của tài khoản; báo cáo, vụ, kết luận, cảnh cáo, ban, gỡ ban | FR-M15-01.05, FR-M15-03.01, FR-M15-03.02, FR-M15-03.03, FR-M15-03.04, FR-M15-03.05, FR-M15-03.06 |
| Dùng | M09 | Khiếu nại theo loại và kết luận | FR-M15-03.07, FR-M15-03.08 |
| Cung cấp | — | Không có: module chỉ đọc dữ liệu, không cung cấp gì cho module khác | — |

### 5.8 AI hỗ trợ và hành vi khi tắt AI

Module không gọi AI. Chỉ số tỷ lệ Topic gợi ý được giữ lại do M13 tính từ phản hồi gợi ý Topic đã ghi; khi công tắc AI
tắt, chỉ số vẫn hiện từ phản hồi đã có (FR-M15-02.09), và báo không có dữ liệu khi khoảng chọn không có phản hồi nào
(FR-M15-02.08).

### 5.9 Yêu cầu HMI

Chưa có — chờ giai đoạn thiết kế.

### 5.10 Chuyển màn hình

Chưa có — chờ giai đoạn thiết kế.

## 6. Lịch sử sửa đổi

| Phiên bản | Ngày | Nội dung | Người sửa |
|---|---|---|---|
| 0.1 | 2026-10-24 | Tạo mới | Phạm Văn Đức |
| 1.0 | 2026-10-24 | Chốt sau 7 bước; bổ sung DEC-264–269 (danh sách chỉ số cuối, bộ lọc thời gian, tài khoản được đếm, cách đếm nội dung và kiểm duyệt, bài bị ẩn theo tài khoản hoặc nhóm). Đối chiếu chéo: cập nhật dòng giao tiếp ở FR-M01 (1.9), FR-M02 (1.5), FR-M03 (1.9), FR-M08 (1.6), FR-M10 (1.3), FR-M13 (1.2); tỷ lệ Topic gợi ý: M13 tính và không có giá trị khi khoảng không có phản hồi, M15 hiển thị "không có dữ liệu" | Phạm Văn Đức |

## Phụ lục A. Truy vết

| ID | Nguồn | Căn cứ | Ghi chú |
|---|---|---|---|
| FR-M15-01 | QA-242, QA-241, QA-245, QA-246, MR-A03, MR-M15, DM-9.5, DEC-225 | Nói thẳng | Trang User Stats theo QA-242; Total users, Active users của draft DM-9.5 được thay bởi QA-242 |
| FR-M15-02 | QA-243, DEC-203, DEC-264, QA-241, QA-245, QA-246, MR-A03, MR-M15, DM-9.5 | Nói thẳng | Trang Content Stats theo QA-243; DEC-203 thêm tỷ lệ Topic gợi ý được giữ lại; Stars per day, Popular tags của DM-9.5 bỏ (DEC-264) |
| FR-M15-03 | QA-244, QA-241, QA-245, QA-246, MR-A03, MR-M15, DM-9.5 | Nói thẳng | Trang Moderation Stats theo QA-244; Reports, Moderation statistics của DM-9.5 |
| FR-M15-01.01 | QA-242, DEC-266, DEC-018 | Nói thẳng | Hai nhóm chờ và nhóm DELETED là mở rộng phạm vi đã chấp nhận (CC-01) |
| FR-M15-01.02 | QA-242, DEC-266 | Nói thẳng | — |
| FR-M15-01.03 | QA-242 | Nói thẳng | — |
| FR-M15-01.04 | QA-242, DEC-266, DEC-014, DEC-140 | Nói thẳng | QA-242 ghi "grade_level"; Lớp/Khối của người dùng là Lớp/Khối trên hồ sơ (DEC-014) |
| FR-M15-01.05 | QA-242, DEC-266, QA-020, DEC-079 | Nói thẳng | — |
| FR-M15-01.06 | QA-242, QA-255 | Nói thẳng | Hoãn có chủ đích (TBD-M15-02) |
| FR-M15-01.07 | QA-245 | Nói thẳng | — |
| FR-M15-01.08 | QA-245 | Nói thẳng | — |
| FR-M15-01.09 | QA-246 | Nói thẳng | — |
| FR-M15-01.10 | DEC-127 | Nói thẳng | — |
| FR-M15-01.11 | QA-246 | Suy ra | Chỉ số là phép đếm (QA-246 "COUNT/GROUP BY") ⇒ nhóm không có dữ liệu có giá trị 0 |
| FR-M15-01.12 | QA-241, DEC-225 | Suy ra | QA-241 "Chỉ ADMIN truy cập được cả 3 dashboard" ⇒ Guest, User, Mod bị từ chối |
| FR-M15-01.13 | DEC-225 | Nói thẳng | — |
| FR-M15-01.14 | QA-247, OPEN-004 | Nói thẳng | Hoãn có chủ đích (TBD-M15-01) |
| FR-M15-01.15 | DEC-266 | Nói thẳng | — |
| FR-M15-01.16 | DEC-265 | Nói thẳng | — |
| FR-M15-01.17 | DEC-265 | Nói thẳng | — |
| FR-M15-01.18 | DEC-265, DEC-127 | Nói thẳng | — |
| FR-M15-01.19 | DEC-265 | Nói thẳng | — |
| FR-M15-02.01 | QA-243, DEC-268, DEC-031, DEC-184 | Nói thẳng | Tên trạng thái theo DEC-031, DEC-184 (FR-M03); không hiện Nháp (DEC-268) |
| FR-M15-02.02 | QA-243, DEC-032, DEC-161 | Nói thẳng | Danh sách trạng thái theo DEC-032, DEC-161 thay danh sách cũ ở QA-243 (C.2) |
| FR-M15-02.03 | QA-243, DEC-268, DM-9.5 | Nói thẳng | Draft "Posts per day" |
| FR-M15-02.04 | QA-243, DM-9.5, DEC-141 | Nói thẳng | Draft "Popular topics" |
| FR-M15-02.05 | DEC-141 | Suy ra | DEC-141: gộp chuyển mọi bài của Topic nguồn sang Topic đích và xóa Topic nguồn ⇒ bài được đếm ở Topic đích |
| FR-M15-02.06 | QA-243, DEC-268, DM-9.5 | Nói thẳng | Draft "Comments per day"; bình luận không bao giờ bị xóa hẳn (M04) |
| FR-M15-02.07 | DEC-203, QA-243 | Nói thẳng | — |
| FR-M15-02.08 | DEC-203 | Suy ra | Tỷ lệ chia cho tổng số Topic gợi ý; không có phản hồi thì mẫu số bằng 0 ⇒ không có tỷ lệ (như FR-M13-10.03) |
| FR-M15-02.09 | DEC-203, DEC-050 | Suy ra | Chỉ số tính trên phản hồi đã ghi (DEC-203); AI tắt thì không có gợi ý mới (DEC-050) nhưng phản hồi cũ còn |
| FR-M15-02.10 | QA-243, DEC-264, DEC-203 | Nói thẳng | Stars per day, Popular tags của DM-9.5 bỏ theo DEC-264 |
| FR-M15-02.11 | QA-245 | Nói thẳng | — |
| FR-M15-02.12 | QA-245 | Nói thẳng | — |
| FR-M15-02.13 | QA-246 | Nói thẳng | — |
| FR-M15-02.14 | DEC-127 | Nói thẳng | — |
| FR-M15-02.15 | QA-246 | Suy ra | Chỉ số là phép đếm (QA-246 "COUNT/GROUP BY") ⇒ nhóm không có dữ liệu có giá trị 0 |
| FR-M15-02.16 | QA-241, DEC-225 | Suy ra | QA-241 "Chỉ ADMIN truy cập được cả 3 dashboard" ⇒ Guest, User, Mod bị từ chối |
| FR-M15-02.17 | DEC-225 | Nói thẳng | — |
| FR-M15-02.18 | QA-247, OPEN-004 | Nói thẳng | Hoãn có chủ đích (TBD-M15-01) |
| FR-M15-02.19 | DEC-268 | Nói thẳng | — |
| FR-M15-02.20 | DEC-268 | Nói thẳng | — |
| FR-M15-02.21 | DEC-268 | Nói thẳng | — |
| FR-M15-02.22 | DEC-268 | Nói thẳng | — |
| FR-M15-02.23 | DEC-265 | Nói thẳng | — |
| FR-M15-02.24 | DEC-265 | Nói thẳng | — |
| FR-M15-02.25 | DEC-265, DEC-127 | Nói thẳng | — |
| FR-M15-02.26 | DEC-265 | Nói thẳng | — |
| FR-M15-02.27 | DEC-269, DEC-019, DEC-156, DEC-194 | Nói thẳng | Bài bị ẩn theo tài khoản tác giả (DEC-019, DEC-156) hoặc theo nhóm (DEC-194) |
| FR-M15-03.01 | QA-244, DEC-267, DEC-076 | Nói thẳng | "pending/resolved/dismissed" ở QA-244 ứng với trạng thái, kết luận của DEC-076 (C.2) |
| FR-M15-03.02 | DEC-190, DEC-267 | Nói thẳng | DEC-190 "the AI entry counts as one report" |
| FR-M15-03.03 | QA-244, DEC-267, DEC-072 | Nói thẳng | Danh sách lý do theo DEC-072 thay "5 category + Khác" ở QA-244 (C.2) |
| FR-M15-03.04 | QA-244, DEC-267, DEC-186 | Nói thẳng | — |
| FR-M15-03.05 | QA-244, DEC-267, DEC-080 | Nói thẳng | — |
| FR-M15-03.06 | QA-244, DEC-267, DEC-193 | Nói thẳng | QA-244 "Ban/Unban theo thời gian" |
| FR-M15-03.07 | QA-244, DEC-115, DEC-198, DEC-200 | Nói thẳng | — |
| FR-M15-03.08 | QA-244, DEC-267, DEC-089 | Nói thẳng | — |
| FR-M15-03.09 | QA-241 | Nói thẳng | QA-241: đã cân nhắc mở Moderation Stats cho MOD, lọc theo hoạt động của MOD đó, và bỏ |
| FR-M15-03.10 | QA-241 | Nói thẳng | — |
| FR-M15-03.11 | QA-245 | Nói thẳng | — |
| FR-M15-03.12 | QA-245 | Nói thẳng | — |
| FR-M15-03.13 | QA-246 | Nói thẳng | — |
| FR-M15-03.14 | DEC-127 | Nói thẳng | — |
| FR-M15-03.15 | QA-246 | Suy ra | Chỉ số là phép đếm (QA-246 "COUNT/GROUP BY") ⇒ nhóm không có dữ liệu có giá trị 0 |
| FR-M15-03.16 | QA-241, DEC-225 | Suy ra | QA-241 "Chỉ ADMIN truy cập được cả 3 dashboard" ⇒ Guest, User, Mod bị từ chối |
| FR-M15-03.17 | DEC-225 | Nói thẳng | — |
| FR-M15-03.18 | QA-247, OPEN-004 | Nói thẳng | Hoãn có chủ đích (TBD-M15-01) |
| FR-M15-03.19 | DEC-265 | Nói thẳng | — |
| FR-M15-03.20 | DEC-265 | Nói thẳng | — |
| FR-M15-03.21 | DEC-265, DEC-127 | Nói thẳng | — |
| FR-M15-03.22 | DEC-265 | Nói thẳng | — |
| BR-M15-01 | QA-241, DEC-225 | Nói thẳng | Guest, User bị từ chối suy từ "Chỉ ADMIN" |
| BR-M15-02 | DEC-225 | Nói thẳng | — |
| BR-M15-03 | QA-245, DEC-265 | Nói thẳng | — |
| BR-M15-04 | DEC-127, DEC-203, DEC-265 | Nói thẳng | "Hôm nay" từ 00:00 giờ Việt Nam: DEC-127 tính ranh giới ngày của preset M15 theo Asia/Ho_Chi_Minh |
| BR-M15-05 | QA-246 | Nói thẳng | — |
| BR-M15-06 | QA-242, QA-255, MR-A03 | Nói thẳng | — |
| BR-M15-07 | QA-242, DEC-266, DEC-018 | Nói thẳng | Tên trạng thái, vai trò, mức cảnh cáo theo FR-M01, FR-M08, FR-M10 |
| BR-M15-08 | QA-243, DEC-203, DEC-268, DEC-032, DEC-161 | Nói thẳng | Tên trạng thái kiểm duyệt theo DEC-032, DEC-161 thay danh sách cũ trong QA-243 (C.2) |
| BR-M15-09 | DEC-203, DEC-159, DEC-127 | Nói thẳng | Ví dụ lấy từ DEC-203; trùng BR-M13-29 |
| BR-M15-10 | QA-244, DEC-267, DEC-115, DEC-198, DEC-200, DEC-089 | Nói thẳng | Ba loại khiếu nại theo DEC-200 |
| BR-M15-11 | DEC-076, DEC-190 | Nói thẳng | — |
| BR-M15-12 | DEC-072 | Nói thẳng | Thay "5 category + Khác" của QA-244 (C.2) |
| BR-M15-13 | DEC-186, DEC-188 | Nói thẳng | — |
| BR-M15-14 | DEC-080, DEC-152, DEC-187, DEC-089 | Nói thẳng | — |
| BR-M15-15 | QA-247, OPEN-004 | Nói thẳng | — |
| BR-M15-16 | QA-241, QA-243, DEC-203, DEC-264 | Nói thẳng | — |
| BR-M15-17 | DEC-141 | Suy ra | DEC-141: gộp chuyển mọi bài của Topic nguồn sang Topic đích, bài có cả hai giữ đích một lần, Topic nguồn bị xóa ⇒ bài đếm ở Topic đích |
| BR-M15-18 | DEC-265 | Nói thẳng | Ví dụ lấy từ DEC-265 |
| BR-M15-19 | DEC-265 | Nói thẳng | — |
| BR-M15-20 | DEC-266 | Nói thẳng | Ví dụ lấy từ DEC-266 |
| BR-M15-21 | DEC-268, DEC-269 | Nói thẳng | Ví dụ lấy từ DEC-268, DEC-269 |
| BR-M15-22 | DEC-267 | Nói thẳng | Ví dụ lấy từ DEC-267 |

## Phụ lục B. Câu hỏi, giả định và TBD

### B.1 Câu hỏi đã hỏi

| Mã | Loại | Câu hỏi | Trả lời | Ghi vào register |
|---|---|---|---|---|
| Q-01 | Mâu thuẫn | Draft DM-9.5 có "Stars per day" và "Popular tags"; danh sách chỉ số chốt ở QA-242–244 không nhắc và cũng không nói bỏ. Hai chỉ số này còn hay bỏ? Đề xuất: bỏ cả hai. | Bỏ cả hai (A) | ISS-403, QA-465, DEC-264 |
| Q-02 | Mơ hồ | "7 ngày", "30 ngày" tính theo ngày lịch (hôm nay và 6, 29 ngày trước, từ 00:00 giờ Việt Nam) hay 7 × 24 giờ, 30 × 24 giờ lùi từ lúc xem? Đề xuất: theo ngày lịch. | Theo ngày lịch, gồm hôm nay, từ 00:00 giờ Việt Nam (A) | ISS-405, QA-467, DEC-265 |
| Q-03 | Mơ hồ | Bộ lọc thời gian áp cho các chỉ số đếm theo nhóm (trạng thái, vai trò, Lớp/Khối, mức cảnh cáo, trạng thái bài, Topic, báo cáo theo trạng thái, theo lý do) thế nào: đếm đối tượng tạo trong khoảng theo trạng thái hiện tại, hay đếm toàn bộ tại lúc xem? Đề xuất: đối tượng tạo trong khoảng. | Mọi chỉ số theo bộ lọc: đếm đối tượng tạo trong khoảng, xếp theo trạng thái lúc xem; Toàn thời gian là không lọc và là lựa chọn sẵn khi mở trang (A) | ISS-404, QA-466, DEC-265 |
| Q-04 | Thiếu chi tiết | Xu hướng (đăng ký mới, bài mới, bình luận mới, cảnh cáo, ban) chia theo đơn vị nào cho từng khoảng? Đề xuất: Hôm nay theo giờ; 7 ngày, 30 ngày theo ngày; Toàn thời gian theo tháng. | Hôm nay theo giờ; 7 ngày, 30 ngày theo ngày; Toàn thời gian theo tháng (A) | ISS-406, QA-468, DEC-265 |
| Q-05 | Thiếu chi tiết | Thống kê người dùng tính những tài khoản nào (DELETED; tài khoản chưa xong bước 3 đăng ký), và "đăng ký mới" tính theo lúc nào? | Ô trạng thái sáu nhóm, thêm Chờ xác minh email, Chờ hoàn tất hồ sơ, DELETED (mở rộng phạm vi, CC-01); đăng ký mới đếm mọi tài khoản được tạo; vai trò, Lớp/Khối, mức cảnh cáo chỉ đếm tài khoản đã xong bước 3, không DELETED | ISS-407, QA-469, DEC-266 |
| Q-06 | Mơ hồ | Thống kê báo cáo đếm theo từng báo cáo hay theo vụ; lý do báo cáo khác nhau giữa bài, bình luận, người dùng, nhóm thì gộp theo tên lý do hay tách theo loại đối tượng? | Đếm theo từng báo cáo; lý do tách theo loại đối tượng (A) | ISS-408, QA-470, DEC-267 |
| Q-07 | Mơ hồ | "Ban/Unban theo thời gian": ban gồm cả ban vĩnh viễn và ban về sau bị lật không; "gỡ ban" gồm gỡ thủ công, ban hết hạn, ban bị lật? | Ban: mọi ban, tách tạm thời, vĩnh viễn, kể cả về sau bị lật; gỡ ban: chỉ thao tác của Mod, Admin (A) | ISS-409, QA-471, DEC-267 |
| Q-08 | Thiếu chi tiết | Danh sách xác nhận FR-M15-01: (a) tài khoản không khai Lớp/Khối hiện thành nhóm "Chưa khai"; (b) ở phân bố mức cảnh cáo, tài khoản BANNED chỉ nằm ở nhóm BANNED, không đếm lại ở mức cảnh cáo của nó; tài khoản Admin (không bị cảnh cáo) ở nhóm Sạch. | Theo đề xuất | ISS-410, QA-472, DEC-266 |
| Q-09 | Thiếu chi tiết | Danh sách xác nhận FR-M15-02: (a) hiện đủ 7 trạng thái đăng, kể cả Nháp và Đã xóa hẳn; (b) bài trong nhóm, bài ẩn danh đếm như bài thường; (c) "bài viết mới" tính theo thời điểm đăng (lúc chuyển sang Đã đăng); (d) bài nhiều Topic được đếm ở mỗi Topic của nó; (e) xu hướng bình luận mới đếm mọi bình luận đăng trong khoảng, kể cả về sau bị ẩn hay bị xóa. | (a) không hiện Nháp, bài Nháp không đếm ở chỉ số nào; (b)–(e) theo đề xuất | ISS-411, QA-473, DEC-268 |
| Q-10 | Thiếu chi tiết | Danh sách xác nhận FR-M15-03: (a) "theo mức" là mức LIGHT, MEDIUM, HEAVY tài khoản đạt ngay sau cảnh cáo đó; (b) cảnh cáo về sau bị bỏ hoặc bị lật vẫn được đếm là đã ra; (c) khiếu nại chưa kết luận hiện ở nhóm "Chờ xét" bên cạnh Chấp nhận, Từ chối. | Theo đề xuất | ISS-412, QA-474, DEC-267 |
| Q-11 | Thiếu chi tiết | Phát sinh khi đối chiếu chéo M01, M11: bài Đã đăng nhưng bị ẩn vì tác giả vô hiệu hóa, xóa tài khoản (BR-M01-24) hoặc vì nhóm bị ẩn (BR-M11-27) đếm thế nào ở thống kê nội dung (DEC-268 chưa nói)? | Đếm theo trạng thái đăng của chính bài, không bỏ, không tách nhóm (A) | ISS-413, QA-475, DEC-269 |

### B.2 TBD

| ID | Nội dung | Ảnh hưởng | Lý do chưa chốt |
|---|---|---|---|
| TBD-M15-01 | Xuất dữ liệu ra CSV cho ba trang thống kê | Thấp | OPEN-004 hoãn có chủ đích |
| TBD-M15-02 | Chỉ số hoạt động người dùng (DAU/WAU/MAU) và hạ tầng ghi sự kiện | Thấp | OPEN-005 hoãn có chủ đích |

### B.3 Cần cân nhắc (ngoài dữ liệu hiện có)

| Mã | Điểm cần cân nhắc | Vì sao cần | Quyết định |
|---|---|---|---|
| CC-01 | Mở rộng phạm vi (người dùng đề xuất khi trả lời Q-05): thêm nhóm Chờ xác minh email, Chờ hoàn tất hồ sơ, DELETED vào ô trạng thái tài khoản | QA-242 chỉ liệt kê ACTIVE, DEACTIVATED, BANNED; dữ liệu mức xác minh, trạng thái DELETED đã có ở M01, không cần ghi nhận thêm | Chấp nhận (DEC-266) |

## Phụ lục C. Sổ nguồn

**Owner keywords:** M15, Analytics, analytics, Analytics & Stats, Stats, thống kê, Thống kê, System Statistics, dashboard, Dashboard, User Stats, Content Stats, Moderation Stats, preset, Today/7d/30d, Hôm nay, Toàn thời gian, All-time, all-time, custom range, custom date range, real-time query, query-on-load, export, CSV, DAU, WAU, MAU, event-tracking, activity-log, tỷ lệ Topic gợi ý được giữ lại, share of suggested Topics kept, Top-N MOD, trend, biểu đồ, publish_state, mod_state, account_state, grade_level, warn level, warning level, mức warn, mức cảnh cáo, report categories, report category, unban, Unban, appeal outcome, is_stale, Topic-suggestion feedback, phản hồi gợi ý Topic, Feedback / Evaluation Loop, Evaluation loop, AI quality evaluation, merge topic, gộp Topic, Topic catalog, report status, lifting a ban, ban count, ban expiry, appeal type, Content Deletion Appeal
**Dependency keywords:** account_state, ACTIVE, DEACTIVATED, DELETED, BANNED, verify_level, vai trò, USER, MOD, ADMIN, grade_level, Lớp/Khối, warn, cảnh cáo, LIGHT, MEDIUM, HEAVY, Clean, publish_state, mod_state, under_review, removed, Topic, comment, bình luận, report, báo cáo, category, ban, unban, appeal, khiếu nại, timezone, Asia/Ho_Chi_Minh, feedback, gợi ý Topic, Topic suggestion, feature flag, cờ tính năng, Admin Panel, đăng ký, registration, Leaderboard
**Mục draft của module:** DM-9.5
**Loại khỏi bảng nguồn (khớp nhầm):** DEC-117, DEC-121, DEC-123, DEC-242, DEC-243, DEC-245, DEC-246, GL:Leaderboard, ISS-153, ISS-374, QA-038, QA-047, QA-202, QA-436, QA-441, MR-M12 ("all-time", "Toàn thời gian" của bảng xếp hạng, M12); DEC-118, QA-199, ISS-REWD-02, QA-204 (ẩn HEAVY, BANNED khỏi bảng xếp hạng, M12); ISS-342, QA-402 ("Hôm nay" của bộ lọc tìm kiếm, M06); DEC-095 (is_stale của embedding, M13); DEC-098, ISS-292, QA-352 (ngưỡng AI theo mức cảnh cáo, M13, M08); DEC-178, ISS-265 (hạn chế thao tác theo mức cảnh cáo, M03, M04); DEC-065, QA-124 (kênh thông báo ban/gỡ ban, M07); DEC-074 (thông báo kết quả báo cáo, M08); DEC-199 (thời hạn khiếu nại cảnh cáo, M09); DEC-033 (lock_level, M03); OPEN-001, OPEN-002, OPEN-003 (chỉ được nhắc cạnh OPEN-004 trong tổng kết)

### C.1 Bảng nguồn

| Nguồn | Nhãn | Trạng thái | Dùng ở | Ghi chú |
|---|---|---|---|---|
| DM-9.5 | Sở hữu | Sửa một phần bởi DEC-264 | FR-M15-01, FR-M15-02, FR-M15-03 | Nhóm A. Draft: danh sách thống kê hệ thống Admin xem; Active users bỏ theo QA-242; Stars per day, Popular tags bỏ theo DEC-264 |
| ISS-178 | Sở hữu | Trùng với QA-241 | — | Nhóm A. Ai truy cập |
| ISS-179 | Sở hữu | Trùng với QA-242 | — | Nhóm A. Chỉ số User Stats |
| ISS-180 | Sở hữu | Trùng với QA-243 | — | Nhóm A. Chỉ số Content Stats |
| ISS-181 | Sở hữu | Trùng với QA-244 | — | Nhóm A. Chỉ số Moderation Stats |
| ISS-182 | Sở hữu | Trùng với QA-245 | — | Nhóm A. Bộ lọc thời gian |
| ISS-183 | Sở hữu | Trùng với QA-246 | — | Nhóm A. Cách tính |
| ISS-184 | Sở hữu | Trùng với QA-247 | — | Nhóm A. Xuất dữ liệu |
| QA-241 | Sở hữu | Hiện hành | FR-M15-01, FR-M15-02, FR-M15-03, BR-M15-01, BR-M15-16 | Nhóm A. Chỉ ADMIN; bỏ quyền MOD và Top-N MOD |
| QA-242 | Sở hữu | Sửa một phần bởi DEC-266 | FR-M15-01, BR-M15-06, BR-M15-07 | Nhóm A. User Stats: trạng thái, đăng ký mới, vai trò, Lớp/Khối, mức cảnh cáo; bỏ DAU/WAU/MAU |
| QA-243 | Sở hữu | Sửa một phần bởi DEC-203, DEC-032, DEC-161, DEC-264, DEC-268 | FR-M15-02, BR-M15-08, BR-M15-16 | Nhóm A. Content Stats: publish_state, mod_state, bài mới, Topic, bình luận mới; bỏ tỷ lệ bài nhóm, ẩn danh; danh sách mod_state là tên cũ của DEC-012 (C.2) |
| QA-244 | Sở hữu | Sửa một phần bởi DEC-072, DEC-076, DEC-267 | FR-M15-03, BR-M15-10 | Nhóm A. Moderation Stats: báo cáo theo trạng thái, loại; cảnh cáo; ban/gỡ ban; khiếu nại; "5 category + Khác" lấy từ QA-042 đã bị thay; tên trạng thái báo cáo theo DEC-076 (C.2) |
| QA-245 | Sở hữu | Sửa một phần bởi DEC-265 | FR-M15-01, FR-M15-02, FR-M15-03, BR-M15-03 | Nhóm A. Preset Hôm nay/7 ngày/30 ngày/Toàn thời gian, không chọn khoảng tùy ý |
| QA-246 | Sở hữu | Hiện hành | FR-M15-01, FR-M15-02, FR-M15-03, BR-M15-05 | Nhóm A. Tính trực tiếp mỗi lần mở, không cache/batch |
| QA-247 | Sở hữu | Hiện hành | BR-M15-15, TBD-M15-01 | Nhóm A. Không xuất CSV ở MS1 (OPEN-004) |
| MR-A03 | Sở hữu | Sửa một phần bởi DEC-203 | FR-M15-01, FR-M15-02, FR-M15-03, BR-M15-06 | Nhóm A. Tổng kết deep dive M15: 3 dashboard, bỏ DAU/WAU/MAU, bỏ quyền MOD, preset, real-time, OPEN-004; DEC-203 thêm một chỉ số vào Content Stats (không có dấu sửa) |
| MR-M15 | Sở hữu | Sửa một phần bởi DEC-203, DEC-264, DEC-265, DEC-266, DEC-267, DEC-268 | FR-M15-01, FR-M15-02, FR-M15-03 | Nhóm A. Dòng module: ADMIN-only, 3 dashboard, real-time, preset, không export; DEC-203 thêm chỉ số |
| DEC-011 | Phụ thuộc | Sửa một phần bởi DEC-162, DEC-184 | Không áp dụng: phần còn hiệu lực nằm ở DEC-184 (trạng thái Đã xóa hẳn) | Nhóm B. M03: xóa mềm bài, 7 ngày khôi phục |
| DEC-012 | Phụ thuộc | Bị thay bởi DEC-031, DEC-032 | — | Nhóm B. M03: mô hình 3 trường trạng thái, bản đầu; không có dấu sửa, cùng chủ đề trạng thái bài |
| DEC-013 | Phụ thuộc | Sửa một phần bởi DEC-161 | Không áp dụng: chính sách quét của M03; trạng thái kiểm duyệt lấy theo DEC-032, DEC-161 | Nhóm B. M03: quét trước bài mới, mod_state khi quét; DEC-195 (bài của Admin không quét) không chạm phần M15 |
| DEC-014 | Phụ thuộc | Hiện hành | FR-M15-01.04 | Nhóm B. M01: Lớp/Khối là tùy chọn ở bước 3 đăng ký |
| DEC-018 | Phụ thuộc | Hiện hành | BR-M15-07 | Nhóm B. M01: account_state 4 giá trị (có DELETED) |
| DEC-031 | Phụ thuộc | Sửa một phần bởi DEC-184 | FR-M15-02.01 | Nhóm B. M03: publish_state 6 giá trị; thêm trạng thái cuối Đã xóa hẳn (không có dấu sửa) |
| DEC-032 | Phụ thuộc | Sửa một phần bởi DEC-161, DEC-190 | BR-M15-08 | Nhóm B. M03: mod_state NORMAL/FLAGGED/HIDDEN |
| DEC-050 | Phụ thuộc | Sửa một phần bởi DEC-142, DEC-144 | FR-M15-02.09 | Nhóm B. M05: phản hồi gợi ý chỉ ghi khi không is_stale |
| DEC-076 | Phụ thuộc | Hiện hành | BR-M15-11 | Nhóm B. M08: vụ việc, trạng thái báo cáo OPEN → RESOLVED (action_taken | dismissed) |
| DEC-079 | Phụ thuộc | Sửa một phần bởi DEC-188 | FR-M15-01.05 | Nhóm B. M08: mức cảnh cáo, thời gian thử thách; DEC-118, DEC-122, DEC-163, DEC-211 không chạm phần M15 |
| DEC-080 | Phụ thuộc | Sửa một phần bởi DEC-152, DEC-187 | BR-M15-14 | Nhóm B. M08: ban tạm thời leo thang, ban vĩnh viễn |
| DEC-083 | Phụ thuộc | Hiện hành | Không áp dụng: M15 không đếm bình luận theo trạng thái kiểm duyệt | Nhóm B. M04/M08: bình luận có mod_state NORMAL/HIDDEN |
| DEC-089 | Phụ thuộc | Hiện hành | BR-M15-10, BR-M15-14 | Nhóm B. M09: kết quả khiếu nại chấp nhận, ban bị lật; DEC-199, DEC-201 sửa hệ quả khi lật, không đổi loại kết quả |
| DEC-115 | Phụ thuộc | Sửa một phần bởi DEC-198, DEC-200 | BR-M15-10 | Nhóm B. M09: loại khiếu nại thứ ba, xóa nội dung (chỉ bài); DEC-202 không chạm phần M15 |
| DEC-127 | Phụ thuộc | Hiện hành | BR-M15-04, BR-M15-09 | Nhóm B. Dùng chung: múi giờ Asia/Ho_Chi_Minh, nêu thẳng preset M15 |
| DEC-133 | Nhắc tới | Hiện hành | Không áp dụng: chỉ nhắc tới M15, không quy định hành vi mới | Nhóm B. Dùng chung: nhật ký AI, khớp do nhắc khiếu nại xóa nội dung; DEC-207 làm rõ, không chạm M15 |
| DEC-140 | Phụ thuộc | Hiện hành | FR-M15-01.04 | Nhóm B. M05: grade_level là trường độc lập của bài |
| DEC-141 | Phụ thuộc | Hiện hành | FR-M15-02.04, FR-M15-02.05, BR-M15-17 | Nhóm B. M05: thêm, gộp, xóa Topic (ảnh hưởng phân bố theo Topic) |
| DEC-152 | Phụ thuộc | Hiện hành | BR-M15-14 | Nhóm B. M01: ban tạm hết hạn tự về ACTIVE |
| DEC-156 | Phụ thuộc | Sửa một phần bởi DEC-159 | Không áp dụng: phần M15 dùng nằm ở DEC-159 | Nhóm B. M01: dữ liệu bị xóa khi DELETED (có Lớp/Khối) |
| DEC-159 | Phụ thuộc | Hiện hành | BR-M15-09 | Nhóm B. M01/M05: phản hồi gợi ý Topic của tài khoản đã xóa được giữ; DEC-215 chỉ bỏ theo dõi bài viết, không chạm phản hồi gợi ý |
| DEC-186 | Phụ thuộc | Hiện hành | BR-M15-13 | Nhóm B. M08: AI tự cảnh cáo; DEC-195, DEC-204 không chạm phần M15 |
| DEC-187 | Phụ thuộc | Hiện hành | BR-M15-14 | Nhóm B. M08: chỉ có cảnh cáo và ban; cách đếm số lần ban; không ban chồng |
| DEC-190 | Phụ thuộc | Hiện hành | BR-M15-11 | Nhóm B. M08: vụ việc do AI tạo, yêu cầu ban thành vụ việc |
| DEC-193 | Phụ thuộc | Hiện hành | FR-M15-03.06 | Nhóm B. M08: gỡ ban được ghi nhật ký |
| DEC-203 | Sở hữu | Hiện hành | FR-M15-02, BR-M15-04, BR-M15-08, BR-M15-09, BR-M15-16 | Nhóm B. M13: chỉ số tỷ lệ Topic gợi ý được giữ lại hiện ở Content Stats, theo preset M15 |
| DEC-225 | Sở hữu | Hiện hành | FR-M15-01, BR-M15-01, BR-M15-02 | Nhóm B. M10: M15 không có cờ tính năng vì chỉ ADMIN dùng; DEC-236, DEC-245, DEC-256 chỉ làm rõ cờ của M11, M12, M16, không chạm phần M15 |
| DG-6 | Phụ thuộc | Sửa một phần bởi DEC-203 | Không áp dụng: phần còn hiệu lực nằm ở DEC-203 | Nhóm B. Draft: vòng phản hồi là năng lực AI bắt buộc; mục 5 vòng phản hồi |
| DM-10.1 | Phụ thuộc | Sửa một phần bởi DEC-072, DEC-076 | Không áp dụng: phần còn hiệu lực nằm ở DEC-072, DEC-076 | Nhóm B. Draft M08: đối tượng, lý do báo cáo |
| DM-11.5 | Phụ thuộc | Sửa một phần bởi DEC-203 | Không áp dụng: phần còn hiệu lực nằm ở DEC-203 | Nhóm B. Draft M13: vòng phản hồi, đánh giá AI |
| DM-x02 | Nhắc tới | Hiện hành | Không áp dụng: chỉ nhắc tới M15, không quy định hành vi mới | Nhóm B. Draft: Statistics trong phạm vi dự án |
| GL:Admin (ADMIN) | Nhắc tới | Hiện hành | Không áp dụng: chỉ nhắc tới M15, không quy định hành vi mới | Nhóm B. Thuật ngữ: Admin xem thống kê hệ thống |
| GL:Feedback / Evaluation Loop | Phụ thuộc | Sửa một phần bởi DEC-203 | Không áp dụng: phần còn hiệu lực nằm ở DEC-203 | Nhóm B. Thuật ngữ: vòng đánh giá AI (precision, recall) |
| ISS-046 | Nhắc tới | Trùng với QA-033 | — | Nhóm B. Câu hỏi phân loại, đã có QA-033 |
| ISS-050 | Nhắc tới | Trùng với QA-042 | — | Nhóm B. Câu hỏi loại báo cáo, đã có QA-042 |
| ISS-064 | Nhắc tới | Trùng với DEC-031 | — | Nhóm B. Câu hỏi trạng thái bài, đã có DEC-031, DEC-032 |
| ISS-081 | Nhắc tới | Trùng với DEC-050 | — | Nhóm B. Câu hỏi gợi ý Topic, đã có DEC-050 |
| ISS-117 | Nhắc tới | Trùng với DEC-089 | — | Nhóm B. Câu hỏi kết quả khiếu nại, đã có DEC-089 |
| ISS-144 | Nhắc tới | Trùng với DEC-115 | — | Nhóm B. Câu hỏi mở rộng khiếu nại, đã có DEC-115 |
| ISS-189 | Nhắc tới | Trùng với DEC-127 | — | Nhóm B. Câu hỏi múi giờ, đã có DEC-127 |
| ISS-195 | Nhắc tới | Trùng với DEC-133 | — | Nhóm B. Câu hỏi nhật ký AI, đã có DEC-133 |
| ISS-196 | Nhắc tới | Trùng với QA-255 | — | Nhóm B. Câu hỏi event-tracking, đã có QA-255 |
| ISS-220 | Nhắc tới | Trùng với DEC-141 | — | Nhóm B. Câu hỏi gộp Topic, đã có DEC-141 |
| ISS-260 | Nhắc tới | Trùng với DEC-159 | — | Nhóm B. Câu hỏi, đã có DEC-159 |
| ISS-332 | Nhắc tới | Trùng với DEC-203 | — | Nhóm B. M13: danh sách xác nhận, đã có DEC-203 |
| OPEN-004 | Sở hữu | Hiện hành | TBD-M15-01, BR-M15-15 | Nhóm B. Hoãn xuất CSV cho 3 dashboard |
| OPEN-005 | Phụ thuộc | Hiện hành | TBD-M15-02 | Nhóm B. Dùng chung: hoãn event-tracking |
| QA-003 | Nhắc tới | Hiện hành | Không áp dụng: chỉ nhắc tới M15, không quy định hành vi mới | Nhóm B. Phase 1: thước đo MS1 định tính, dữ liệu demo seed |
| QA-017 | Phụ thuộc | Sửa một phần bởi DEC-203 | Không áp dụng: phần còn hiệu lực nằm ở DEC-203 | Nhóm B. Phase 2: lựa chọn cuối của tác giả là phản hồi cho gợi ý Topic |
| QA-018 | Phụ thuộc | Hiện hành | Không áp dụng: máy trạng thái tài khoản thuộc M01; tập trạng thái lấy theo DEC-018 | Nhóm B. M01: máy trạng thái tài khoản, BANNED → gỡ ban → ACTIVE; DEC-149, DEC-246 sửa thời hạn vô hiệu hóa, hiển thị; máy trạng thái giữ nguyên |
| QA-019 | Phụ thuộc | Sửa một phần bởi DEC-187 | Không áp dụng: phần M15 dùng nằm ở DEC-080, DEC-187 | Nhóm B. M08: ban/gỡ ban do MOD, ADMIN; DEC-189 (quyền cảnh cáo, ban Mod) không chạm phần M15 |
| QA-020 | Phụ thuộc | Sửa một phần bởi DEC-186, DEC-188 | FR-M15-01.05 | Nhóm B. M08: 3 mức cảnh cáo LIGHT/MEDIUM/HEAVY, Clean; tập mức và số lần giữ nguyên |
| QA-028 | Phụ thuộc | Bị thay bởi DEC-031, DEC-032 | — | Nhóm B. M03: mô hình trạng thái bài, bản đầu |
| QA-029 | Phụ thuộc | Bị thay bởi DEC-032 | — | Nhóm B. M03: mod_state pending/active/under_review/removed, bản đầu |
| QA-030 | Phụ thuộc | Trùng với DEC-013 | — | Nhóm B. M03: chính sách quét |
| QA-033 | Phụ thuộc | Sửa một phần bởi DEC-140 | Không áp dụng: phần còn hiệu lực nằm ở DEC-140 | Nhóm B. M05/M03: grade_level là trường độc lập; ý grade_level là trường độc lập còn hiệu lực |
| QA-034 | Phụ thuộc | Hiện hành | Không áp dụng: Lớp/Khối không tự tăng là quy tắc của M02 | Nhóm B. M02: Lớp/Khối trên hồ sơ không tự tăng; DEC-176 chỉ bỏ nhắc cập nhật Lớp/Khối |
| QA-042 | Phụ thuộc | Bị thay bởi DEC-072 | — | Nhóm B. M08: 5 loại báo cáo + Khác; không có dấu sửa, cùng chủ đề lý do báo cáo |
| QA-062 | Phụ thuộc | Trùng với DEC-018 | — | Nhóm B. M01: các trạng thái tài khoản |
| QA-082 | Phụ thuộc | Trùng với DEC-031 | — | Nhóm B. M03: publish_state 6 giá trị |
| QA-083 | Phụ thuộc | Trùng với DEC-032 | — | Nhóm B. M03: mod_state 3 giá trị |
| QA-104 | Phụ thuộc | Trùng với DEC-050 | — | Nhóm B. M05: phản hồi chỉ ghi khi không is_stale |
| QA-147 | Nhắc tới | Trùng với DEC-080 | — | Nhóm B. M08: thời hạn ban, đã có DEC-080 |
| QA-193 | Phụ thuộc | Trùng với DEC-115 | — | Nhóm B. M09: khiếu nại xóa nội dung |
| QA-248 | Phụ thuộc | Trùng với DEC-127 | — | Nhóm B. Dùng chung: múi giờ, nêu preset M15 |
| QA-254 | Nhắc tới | Trùng với DEC-133 | — | Nhóm B. Nhật ký AI, đã có DEC-133 |
| QA-255 | Phụ thuộc | Hiện hành | BR-M15-06 | Nhóm B. Dùng chung: không xây event-tracking, gốc từ QA-242 |
| QA-270 | Nhắc tới | Trùng với DEC-141 | — | Nhóm B. M05: thêm Topic, đã có DEC-141 |
| QA-272 | Nhắc tới | Trùng với DEC-141 | — | Nhóm B. M05: không đổi tên Topic, đã có DEC-141 |
| QA-320 | Phụ thuộc | Trùng với DEC-159 | — | Nhóm B. M01: giữ phản hồi gợi ý Topic của tài khoản đã xóa |
| QA-385 | Sở hữu | Trùng với DEC-203 | — | Nhóm B. M13: Admin xem chỉ số đánh giá AI ở trang thống kê M15 |
| QA-392 | Sở hữu | Trùng với DEC-203 | — | Nhóm B. M13: mục 6, chỉ số bản tối thiểu ở M15 |
| F-POST-06 | Phụ thuộc | Sửa một phần bởi DEC-184 | Không áp dụng: phần còn hiệu lực nằm ở DEC-184 | Nhóm B. M03: xóa mềm bài |
| F-POST-07 | Phụ thuộc | Hiện hành | Không áp dụng: mô hình trạng thái thuộc M03; tên trạng thái lấy theo DEC-031, DEC-032 | Nhóm B. M03: mô hình 3 trường trạng thái |
| F-POST-09 | Phụ thuộc | Hiện hành | Không áp dụng: đây là Lớp/Khối trên bài viết; M15 đếm Lớp/Khối trên hồ sơ | Nhóm B. M03: grade_level 10/11/12, tùy chọn |
| MR-A04 | Nhắc tới | Hiện hành | Không áp dụng: chỉ nhắc tới M15, không quy định hành vi mới | Nhóm B. Tổng kết Phase 6, nhắc M15 |
| MR-M01 | Phụ thuộc | Trùng với DEC-018 | — | Nhóm B. M01: account_state, verify_level; các sửa đổi DEC-147–153, DEC-214 không chạm tập trạng thái tài khoản |
| MR-M03 | Phụ thuộc | Sửa một phần bởi DEC-184 | Không áp dụng: tên trạng thái lấy theo DEC-031, DEC-032, DEC-184 | Nhóm B. M03: publish_state(6), mod_state(3) |
| MR-M05 | Nhắc tới | Sửa một phần bởi DEC-140, DEC-141 | Không áp dụng: chỉ nhắc tới M15, không quy định hành vi mới | Nhóm B. M05: dòng module |
| DEC-128 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M15 |
| DEC-129 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M15 |
| DEC-130 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M15 |
| DEC-131 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M15 |
| DEC-132 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M15 |
| DEC-134 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M15 |
| DEC-135 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M15 |
| DEC-136 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M15 |
| DEC-137 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M15 |
| DEC-138 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M15 |
| ISS-190 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M15 |
| ISS-191 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M15 |
| ISS-192 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M15 |
| ISS-193 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M15 |
| ISS-194 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M15 |
| ISS-197 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M15 |
| ISS-198 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M15 |
| ISS-199 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M15 |
| ISS-200 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M15 |
| ISS-201 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M15 |
| ISS-202 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M15 |
| ISS-203 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M15 |
| ISS-204 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M15 |
| QA-249 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M15 |
| QA-250 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M15 |
| QA-251 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M15 |
| QA-252 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M15 |
| QA-253 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M15 |
| QA-256 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M15 |
| QA-257 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M15 |
| QA-258 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M15 |
| QA-259 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M15 |
| QA-260 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M15 |
| QA-261 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M15 |
| QA-262 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M15 |
| QA-263 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M15 |
| QA-264 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M15 |
| MR-A05 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M15 |
| DEC-072 | Phụ thuộc | Hiện hành | BR-M15-12 | Nhóm B (bước 2). M08: lý do báo cáo theo loại đối tượng (Bài 8, Bình luận 7, Người dùng 2, Nhóm 4); DEC-191, DEC-194 không chạm phần M15 |
| QA-134 | Phụ thuộc | Trùng với DEC-072 | — | Nhóm B (bước 2). M08: lý do báo cáo riêng theo loại đối tượng |
| DEC-161 | Phụ thuộc | Hiện hành | BR-M15-08 | Nhóm B (bước 2). M03: bài mới NORMAL; "gỡ" là HIDDEN, không có trạng thái removed; DEC-185 không chạm phần M15 |
| DEC-162 | Phụ thuộc | Sửa một phần bởi DEC-184 | Không áp dụng: khôi phục bài là việc của M03 | Nhóm B (bước 2). M03: xóa ở mọi trạng thái, khôi phục về trạng thái trước, hạn 7 × 24 giờ |
| DEC-184 | Phụ thuộc | Hiện hành | FR-M15-02.01 | Nhóm B (bước 2). M03: hết hạn khôi phục gắn cờ Đã xóa hẳn, không xóa dữ liệu |
| DEC-188 | Phụ thuộc | Hiện hành | BR-M15-13 | Nhóm B (bước 2). M08: hạ mức cảnh cáo; cảnh cáo bị bỏ hoặc bị lật vẫn giữ bản ghi, có đánh dấu |
| DEC-142 | Phụ thuộc | Hiện hành | Không áp dụng: cách ghi phản hồi gợi ý thuộc M05; M15 chỉ hiện tỷ lệ do M13 tính | Nhóm B (bước 2). M05: gợi ý Topic cả khi sửa bài đã gửi, cùng quy tắc ghi phản hồi |
| DEC-144 | Phụ thuộc | Hiện hành | Không áp dụng: cách ghi phản hồi gợi ý thuộc M05; M15 chỉ hiện tỷ lệ do M13 tính | Nhóm B (bước 2). M05: Topic AI trả về ngoài danh mục bị bỏ |
| DEC-198 | Phụ thuộc | Hiện hành | BR-M15-10 | Nhóm B (bước 2). M09: khiếu nại bài bị AI từ chối, gộp với cảnh cáo AI, thuộc loại "bài" |
| DEC-200 | Phụ thuộc | Hiện hành | BR-M15-10 | Nhóm B (bước 2). M09: một danh sách khiếu nại, ba loại ban, cảnh cáo, bài |
| DEC-264 | Sở hữu | Hiện hành | FR-M15-02, FR-M15-02.10, BR-M15-16 | Nhóm A (bước 6). Danh sách chỉ số cuối; bỏ Stars per day, Popular tags |
| DEC-265 | Sở hữu | Hiện hành | FR-M15-01.16–01.19, FR-M15-02.23–02.26, FR-M15-03.19–03.22, BR-M15-03, BR-M15-04, BR-M15-18, BR-M15-19 | Nhóm A (bước 6). Bộ lọc áp cho mọi chỉ số, mặc định Toàn thời gian, ngày lịch, đơn vị biểu đồ |
| DEC-266 | Sở hữu | Hiện hành | FR-M15-01.01, FR-M15-01.02, FR-M15-01.04, FR-M15-01.05, FR-M15-01.15, BR-M15-07, BR-M15-20 | Nhóm A (bước 6). Tài khoản được đếm ở thống kê người dùng; mở rộng phạm vi CC-01 |
| DEC-267 | Sở hữu | Hiện hành | FR-M15-03.01, FR-M15-03.02, FR-M15-03.03, FR-M15-03.04, FR-M15-03.05, FR-M15-03.06, FR-M15-03.08, BR-M15-10, BR-M15-22 | Nhóm A (bước 6). Cách đếm ở thống kê kiểm duyệt |
| DEC-268 | Sở hữu | Sửa một phần bởi DEC-269 | FR-M15-02.01, FR-M15-02.03, FR-M15-02.06, FR-M15-02.19, FR-M15-02.20, FR-M15-02.21, FR-M15-02.22, BR-M15-08, BR-M15-21 | Nhóm A (bước 6). Cách đếm ở thống kê nội dung |
| QA-465 | Sở hữu | Trùng với DEC-264 | — | Nhóm A (bước 6). Bỏ Stars per day, Popular tags |
| QA-466 | Sở hữu | Trùng với DEC-265 | — | Nhóm A (bước 6). Bộ lọc áp cho mọi chỉ số; mặc định Toàn thời gian |
| QA-467 | Sở hữu | Trùng với DEC-265 | — | Nhóm A (bước 6). 7 ngày, 30 ngày theo ngày lịch |
| QA-468 | Sở hữu | Trùng với DEC-265 | — | Nhóm A (bước 6). Đơn vị biểu đồ xu hướng |
| QA-469 | Sở hữu | Trùng với DEC-266 | — | Nhóm A (bước 6). Sáu nhóm trạng thái tài khoản; tài khoản được đếm |
| QA-470 | Sở hữu | Trùng với DEC-267 | — | Nhóm A (bước 6). Đếm theo báo cáo; lý do theo loại đối tượng |
| QA-471 | Sở hữu | Trùng với DEC-267 | — | Nhóm A (bước 6). Ban, gỡ ban |
| QA-472 | Sở hữu | Trùng với DEC-266 | — | Nhóm A (bước 6). Danh sách xác nhận Q-08 |
| QA-473 | Sở hữu | Trùng với DEC-268 | — | Nhóm A (bước 6). Danh sách xác nhận Q-09 |
| QA-474 | Sở hữu | Trùng với DEC-267 | — | Nhóm A (bước 6). Danh sách xác nhận Q-10 |
| ISS-403 | Sở hữu | Trùng với DEC-264 | — | Nhóm A (bước 6). Câu hỏi bước 6, đã có DEC-264 |
| ISS-404 | Sở hữu | Trùng với DEC-265 | — | Nhóm A (bước 6). Câu hỏi bước 6, đã có DEC-265 |
| ISS-405 | Sở hữu | Trùng với DEC-265 | — | Nhóm A (bước 6). Câu hỏi bước 6, đã có DEC-265 |
| ISS-406 | Sở hữu | Trùng với DEC-265 | — | Nhóm A (bước 6). Câu hỏi bước 6, đã có DEC-265 |
| ISS-407 | Sở hữu | Trùng với DEC-266 | — | Nhóm A (bước 6). Câu hỏi bước 6, đã có DEC-266 |
| ISS-408 | Sở hữu | Trùng với DEC-267 | — | Nhóm A (bước 6). Câu hỏi bước 6, đã có DEC-267 |
| ISS-409 | Sở hữu | Trùng với DEC-267 | — | Nhóm A (bước 6). Câu hỏi bước 6, đã có DEC-267 |
| ISS-410 | Sở hữu | Trùng với DEC-266 | — | Nhóm A (bước 6). Câu hỏi bước 6, đã có DEC-266 |
| ISS-411 | Sở hữu | Trùng với DEC-268 | — | Nhóm A (bước 6). Câu hỏi bước 6, đã có DEC-268 |
| ISS-412 | Sở hữu | Trùng với DEC-267 | — | Nhóm A (bước 6). Câu hỏi bước 6, đã có DEC-267 |
| DEC-269 | Sở hữu | Hiện hành | FR-M15-02.27, BR-M15-21 | Nhóm A (bước 7). Bài bị ẩn theo tài khoản tác giả hoặc theo nhóm vẫn đếm theo trạng thái đăng |
| QA-475 | Sở hữu | Trùng với DEC-269 | — | Nhóm A (bước 7). Câu trả lời khi đối chiếu chéo module |
| ISS-413 | Sở hữu | Trùng với DEC-269 | — | Nhóm A (bước 7). Câu hỏi bước 7, đã có DEC-269 |
| DEC-019 | Phụ thuộc | Sửa một phần bởi DEC-156 | FR-M15-02.27 | Nhóm C (bước 7). M01: bài của tài khoản vô hiệu hóa bị ẩn; DEC-148, DEC-149 chỉ sửa thời hạn, username, email |
| DEC-194 | Phụ thuộc | Hiện hành | FR-M15-02.27 | Nhóm C (bước 7). M08: nhóm bị ẩn, mọi nội dung không hiện, dữ liệu giữ; DEC-235 chỉ làm rõ nhóm Bị khóa |

### C.2 Chuỗi quyết định

| Chuỗi | Nội dung hiện hành |
|---|---|
| DM-9.5 → QA-242, QA-243, QA-244 (MR-A03) → DEC-203 → DEC-264 | Ba trang thống kê có đúng các chỉ số của QA-242–244 cùng tỷ lệ Topic gợi ý được giữ lại (DEC-203). Active users (QA-242), Stars per day và Popular tags (DEC-264) của draft bị bỏ. |
| QA-245, QA-246 → DEC-265 | Bộ lọc thời gian áp cho mọi chỉ số của ba trang: đếm đối tượng được tạo (hoặc sự kiện xảy ra) trong khoảng, xếp nhóm theo trạng thái lúc xem; Toàn thời gian là không giới hạn và là lựa chọn sẵn khi mở trang. Hôm nay từ 00:00; 7 ngày, 30 ngày là ngày lịch gồm hôm nay; giờ Việt Nam. Biểu đồ: Hôm nay theo giờ, 7 ngày và 30 ngày theo ngày, Toàn thời gian theo tháng. Số liệu tính lúc mở trang hoặc đổi khoảng (QA-246). |
| QA-242 → DEC-266 | Ô trạng thái tài khoản có sáu nhóm: Chờ xác minh email, Chờ hoàn tất hồ sơ, ACTIVE, DEACTIVATED, BANNED, DELETED. Đăng ký mới đếm mọi tài khoản được tạo. Vai trò, Lớp/Khối (có nhóm Chưa khai), mức cảnh cáo (BANNED chỉ ở nhóm BANNED, Admin ở Sạch) chỉ đếm tài khoản đã xong bước 3, không DELETED. Không có DAU/WAU/MAU (QA-242, QA-255). |
| QA-243 → DEC-268 → DEC-269 | Bài Nháp không được đếm; ô trạng thái đăng có sáu nhóm Chờ duyệt, Đã đăng, Tự ẩn, Bị từ chối, Đã xóa, Đã xóa hẳn. Bài nhóm, bài ẩn danh đếm như bài khác. Ô trạng thái đăng, trạng thái kiểm duyệt, Topic xếp bài theo thời điểm tạo; xu hướng bài viết mới theo thời điểm đăng. Bài nhiều Topic đếm ở mỗi Topic. Xu hướng bình luận mới đếm mọi bình luận đăng trong khoảng, kể cả về sau bị ẩn hoặc xóa. Bài bị ẩn vì tác giả DEACTIVATED, DELETED hoặc vì nhóm bị ẩn vẫn đếm theo trạng thái của chính bài (DEC-269). |
| QA-244 → DEC-267 | Đếm theo từng báo cáo; ba nhóm Mở, Đã xử lý – Có xử lý, Đã xử lý – Bác bỏ; mục do AI tạo (kể cả yêu cầu ban) là một báo cáo; lý do tách theo loại đối tượng. Cảnh cáo xếp theo mức đạt ngay sau cảnh cáo, kể cả cảnh cáo về sau bị bỏ, bị lật. Ban: mọi ban, tách tạm thời, vĩnh viễn, kể cả về sau bị lật; gỡ ban chỉ là thao tác của Mod, Admin. Khiếu nại theo kết quả: Chờ xét, Chấp nhận, Từ chối. |
| DEC-012, QA-028, QA-029 → DEC-031, DEC-032 → DEC-161, DEC-184, DEC-190 → DEC-268 | Trạng thái đăng: Nháp, Chờ duyệt, Đã đăng, Tự ẩn, Bị từ chối, Đã xóa (DEC-031), thêm trạng thái cuối Đã xóa hẳn (DEC-184); thống kê không đếm Nháp (DEC-268). Trạng thái kiểm duyệt: Bình thường, Bị gắn cờ, Bị Mod ẩn (DEC-032); bài mới là Bình thường, "gỡ" là Bị Mod ẩn (DEC-161); chỉ AI quét lại làm bài Bị gắn cờ (DEC-190). Danh sách "pending/active/under_review/removed" ở QA-243 là tên của DEC-012 đã bị thay; QA-243 chỉ còn hiệu lực ở ý "phân bố bài theo trạng thái kiểm duyệt". |
| DEC-011 → DEC-162 → DEC-184 | Bài bị xóa giữ 7 × 24 giờ để khôi phục; hết hạn thì gắn cờ Đã xóa hẳn, dữ liệu giữ nguyên. |
| QA-042 → DEC-072 (QA-134) → DEC-191, DEC-194 → DEC-267 | Lý do báo cáo riêng theo loại đối tượng: Bài 8, Bình luận 7, Người dùng 2, Nhóm 4; thống kê tách theo loại đối tượng (DEC-267). "5 category + Khác" ở QA-244 lấy từ QA-042 đã bị thay. DEC-191 (không báo cáo chính mình, không báo cáo trùng), DEC-194 (ẩn, khóa nhóm bị báo cáo) không chạm phần M15. |
| DM-10.1 → DEC-076 (DEC-190) → DEC-267 | Báo cáo Mở → Đã xử lý; vụ kết luận Có xử lý hoặc Bác bỏ; IN_REVIEW, REJECTED của draft không dùng. Thống kê đếm theo từng báo cáo, ba nhóm Mở / Đã xử lý – Có xử lý / Đã xử lý – Bác bỏ (DEC-267). Mục do AI tạo, kể cả yêu cầu ban, là một báo cáo (DEC-190, DEC-267). |
| QA-020 → DEC-079 → DEC-186, DEC-188 | Mức cảnh cáo: Sạch, LIGHT (1–2 lần), MEDIUM (3–4), HEAVY (5–6). AI cũng cảnh cáo (DEC-186). Hết thử thách thì hạ một mức; cảnh cáo bị bỏ hoặc bị lật vẫn giữ bản ghi, có đánh dấu (DEC-188). |
| QA-019 → DEC-080 → DEC-152, DEC-187 (DEC-193) → DEC-267 | Ban tạm thời 30 ngày → 90 ngày → vĩnh viễn, và ban vĩnh viễn thủ công. Ban tạm hết hạn thì tự về ACTIVE (DEC-152). Chỉ có cảnh cáo và ban, không ban chồng (DEC-187). Mod, Admin gỡ ban, có ghi nhật ký (DEC-193). Thống kê đếm mọi ban kể cả về sau bị lật; gỡ ban chỉ đếm thao tác của Mod, Admin (DEC-267). |
| DEC-115 → DEC-198, DEC-200 | Ba loại khiếu nại: ban, cảnh cáo, bài (bị gỡ hoặc bị AI từ chối, DEC-198). Kết quả Chấp nhận hoặc Từ chối (DEC-089). |
| QA-017, DM-11.5, DG-6, GL:Feedback / Evaluation Loop → DEC-203 | Chỉ đánh giá gợi ý Topic, một chỉ số: số Topic gợi ý được giữ ÷ số Topic gợi ý, trên các bản ghi phản hồi trong khoảng đã chọn, theo giờ Asia/Ho_Chi_Minh. Không tính precision, recall, F1, accuracy; không đánh giá AI kiểm duyệt; không có Mod đánh dấu đúng/sai. |
| DEC-050 → DEC-142, DEC-144 | Phản hồi gợi ý chỉ ghi khi gợi ý không cũ (is_stale), kể cả khi tác giả gợi ý lúc sửa bài đã gửi (DEC-142); Topic ngoài danh mục bị bỏ khỏi gợi ý (DEC-144). |
| DEC-156 → DEC-159 | Tài khoản DELETED: phản hồi gợi ý Topic được giữ, không còn gắn danh tính. |
| DEC-225 → DEC-236, DEC-245, DEC-256 | M15 không có cờ tính năng vì chỉ Admin dùng; các làm rõ sau chỉ nói về cờ của M11, M12, M16, không chạm phần M15. |
| DEC-089 → DEC-199, DEC-201 | Kết quả khiếu nại vẫn là Chấp nhận hoặc Từ chối; DEC-199 (vẫn lật khi xử lý đã kết thúc), DEC-201 (lật ban của Mod không trả vai trò, bắt buộc lý do kết luận) chỉ đổi hệ quả, không đổi cách đếm của M15. |
| DEC-115 → DEC-202 | DEC-202 quy định một xử lý chỉ bị lật một lần; không đổi loại khiếu nại M15 đếm. |
| DEC-159 → DEC-215 | DEC-215 chỉ bỏ theo dõi bài viết; phản hồi gợi ý Topic của tài khoản đã xóa vẫn được giữ. |
| DEC-186 → DEC-195, DEC-204 (DEC-097) | AI vẫn tự ra cảnh cáo; DEC-195 (nội dung Admin không bị quét), DEC-204 (thứ tự nhóm khi bằng điểm, theo DEC-097) không chạm phần M15. |
| DEC-079 → DEC-118, DEC-122, DEC-163, DEC-211 | Tập mức cảnh cáo giữ nguyên; các sửa đổi chỉ nói về bảng xếp hạng (ẩn HEAVY, BANNED), tạo bài khi bị hạn chế và giảm hạng trong tìm kiếm, không chạm phần M15. |
| DEC-132 → DEC-141 | Danh mục Topic: 11 Topic ban đầu; chỉ Admin thêm, gộp, xóa; gộp chuyển mọi bài của Topic nguồn sang Topic đích rồi xóa Topic nguồn. Phần DEC-141 sửa ở DEC-132 (đối chiếu gợi ý với danh mục hiện tại) không chạm phần M15. |
| DEC-019 → DEC-148, DEC-149, DEC-156 | Bài của tài khoản DEACTIVATED, DELETED bị ẩn; DEC-148, DEC-149 (thời hạn 14 × 24 giờ, username, email), DEC-156 (danh mục dữ liệu bị xóa) không đổi việc ẩn bài. |
| DEC-194 → DEC-235 | Nhóm bị ẩn: nhóm và mọi nội dung không hiện với ai, dữ liệu giữ; DEC-235 chỉ làm rõ nhóm Bị khóa. |
| QA-033 → DEC-140 | Topic phẳng; Lớp/Khối là trường độc lập, tùy chọn. |
