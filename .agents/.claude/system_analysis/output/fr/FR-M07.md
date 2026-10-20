---
module: M07
ten_module: Notification
ma_tai_lieu: FR-M07
phien_ban: 1.0
trang_thai: Đã chốt
ngay: 2026-10-21
tac_gia: Phạm Văn Đức
moc_nguon: DEC-220, QA-411, ISS-351, OPEN-012
steps_completed: [1, 2, 3, 4, 5, 6, 7]
---
# Tài liệu yêu cầu chức năng — M07 Notification

| Mã tài liệu | FR-M07 |
|---|---|
| Dự án | iShare |
| Module | M07 — Notification |
| Trạng thái | Đã chốt |
| Phiên bản | 1.0 |
| Ngày | 2026-10-21 |
| Tác giả | Phạm Văn Đức |

<!-- Quy ước chung cho mọi bảng dưới đây:
     - Thân tài liệu không ghi nguồn. Nguồn của mọi ID nằm ở Phụ lục A.
     - Ô không có nội dung ghi "—". Không xóa cột.
     - Mục chưa tới bước làm thì để dòng "(Chưa làm — bước N)". -->

## 1. Tổng quan

### 1.1 Mục đích

Module Notification cho người dùng biết những việc xảy ra liên quan tới mình: tương tác trên bài viết và bình luận, nhắc tên, người theo dõi mới, kết quả kiểm duyệt và khiếu nại, hoạt động trong nhóm, phần thưởng, tin nhắn và các sự kiện bảo mật tài khoản. Thông báo hiện trong ứng dụng qua chuông thông báo; riêng nhóm sự kiện bảo mật và ban được gửi thêm qua email. Module cũng cho người dùng theo dõi người dùng và Topic để nhận cập nhật, và báo khi người mình theo dõi có bài mới.

### 1.2 Phạm vi

**Trong phạm vi:**

- Sinh thông báo trong ứng dụng cho các sự kiện của các module khác theo danh sách sự kiện và kênh đã chốt.
- Gộp nhiều upvote trong một khoảng thời gian ngắn thành một thông báo.
- Gửi email cho nhóm sự kiện bảo mật và ban, không chặn thao tác gây ra sự kiện.
- Chuông thông báo: danh sách thông báo gần nhất, trang xem toàn bộ thông báo, trạng thái đã đọc/chưa đọc, đánh dấu đã đọc khi mở, đánh dấu tất cả đã đọc.
- Đẩy thông báo mới tới người dùng đang mở ứng dụng; thông báo đã lưu là nguồn chính, người dùng luôn thấy đủ khi mở lại.
- Báo tin nhắn mới bằng popup nhỏ và biểu tượng Tin nhắn riêng trên thanh điều hướng (số cuộc trò chuyện có tin chưa đọc), dẫn tới hộp thư Chat; tin nhắn không hiện ở chuông.
- Tắt thông báo theo từng bài viết; tắt thông báo theo từng cuộc trò chuyện và cho toàn bộ Chat.
- Theo dõi (Follow) và bỏ theo dõi người dùng, Topic; thông báo người theo dõi mới; thông báo bài mới của người dùng đang theo dõi.
- Giữ thông báo vô thời hạn.

**Ngoài phạm vi:**

- Điều kiện và nội dung nghiệp vụ của từng sự kiện (khi nào sự kiện xảy ra, ai liên quan): module phát sinh sự kiện sở hữu — M01, M03, M04, M08, M09, M10, M11, M12, M16. Ví dụ: thời điểm gửi thông báo nhắc tên và email cảnh báo trước khi tự xóa (M01); thông báo gộp bài bị AI từ chối và cảnh cáo AI (M09); mở nội dung đã bị xử lý ở chế độ chỉ đọc từ thông báo (M03, M04).
- Hộp thư Chat và trạng thái đã xem của tin nhắn — M16 Chat & Messaging.
- Hiện số và danh sách người theo dõi, đang theo dõi trên hồ sơ — M02 User Profile.
- Tab Following và banner "có bài mới" của feed — M14 Feed & Discovery; bộ lọc chỉ nội dung đang theo dõi — M06 Search.
- Chuyển, bỏ lượt theo dõi Topic khi gộp, xóa Topic — M05 Topic & Tag; xóa quan hệ theo dõi khi tài khoản DELETED — M01.
- Theo dõi Group, Tag, bài viết (đã quyết không làm); thông báo bài mới trong Topic đang theo dõi (đã quyết không làm, Topic đang theo dõi chỉ dùng cho tab Following và bộ lọc tìm kiếm).
- Email tổng hợp (digest) và trang cài đặt thông báo theo loại (đã quyết không làm).
- Thông báo Accepted Answer (MS1 không có Accepted Answer) và thông báo nhắc cập nhật Lớp/Khối đầu năm học (không làm ở MS1).
- Thông báo cho tác giả khi Mod/Admin đổi Topic, Tag trên bài (đã quyết không thông báo).
- Tự xóa thông báo cũ (đã quyết không có chính sách xóa).

## 2. Thuật ngữ và viết tắt

### 2.1 Thuật ngữ

| Thuật ngữ | Định nghĩa |
|---|---|
| Sự kiện | Một việc xảy ra ở một module (ví dụ có bình luận mới, một ban được tạo) mà danh sách sự kiện thông báo (BR-M07-01) quy định là phải báo cho người nhận. Module phát sinh sự kiện quyết định khi nào sự kiện xảy ra và ai là người nhận. |
| Thông báo | Bản ghi báo cho một người nhận về một sự kiện, hiện trong ứng dụng ở chuông và trang Thông báo. Mỗi người nhận có thông báo riêng. |
| Người nhận | Người dùng mà một sự kiện hướng tới. |
| Người gây sự kiện | Người dùng làm ra sự kiện (người bình luận, người upvote, người theo dõi, tác giả bài mới…). Không có thông báo cho người gây sự kiện khi người đó cũng là người nhận. |
| Chuông thông báo | Biểu tượng trên thanh điều hướng; bấm vào mở danh sách thông báo gần nhất. |
| Trang Thông báo | Trang riêng (/notifications) hiện toàn bộ thông báo của người dùng. |
| Đã đọc, chưa đọc | Trạng thái của một thông báo. Thông báo mới tạo là chưa đọc; người dùng bấm vào nó hoặc bấm "Đánh dấu tất cả đã đọc" thì nó thành đã đọc. |
| Biểu tượng Tin nhắn | Biểu tượng riêng trên thanh điều hướng cho tin nhắn 1-1 và nhóm chat. Số trên biểu tượng là số cuộc trò chuyện có tin chưa đọc theo mốc đã đọc của M16, gồm cả cuộc đã tắt thông báo. Bấm vào thì tới hộp thư Chat (M16). Tin nhắn không hiện ở chuông. |
| Popup tin nhắn | Ô thông báo nhỏ hiện trên màn hình khi có tin nhắn mới, với thành viên đang mở ứng dụng mà không xem đúng cuộc trò chuyện đó. |
| Gộp upvote | Lượt upvote đầu của một bài hay một bình luận được báo ngay; các lượt sau trong cửa sổ 5 phút cập nhật chính thông báo đó thành "A và N người khác đã upvote…", với A là người upvote mới nhất, N là số người khác nhau còn lại trong cửa sổ. |
| Cửa sổ 5 phút | Khoảng 5 × 60 giây tính từ lượt upvote mở thông báo, riêng cho từng bài viết và từng bình luận; không kéo dài theo lượt upvote sau. Lượt upvote đầu tiên sau khi cửa sổ hết mở thông báo và cửa sổ mới. |
| Nhóm sự kiện có email | Các sự kiện được gửi thêm qua email: mật khẩu đã đổi, đã liên kết Google, cảnh báo trước khi tự xóa, ban, gỡ ban, kết luận khiếu nại ban (BR-M07-03). |
| Hàng đợi email | Danh sách email đang chờ gửi. Sự kiện thuộc nhóm có email ghi một email vào hàng đợi; hàng đợi được quét mỗi 1 phút (60 giây) và các email trong đó được gửi đi. |
| Đẩy thông báo | Gửi ngay thông báo vừa tạo tới các thiết bị đang mở ứng dụng của người nhận, theo kiểu cố gắng: đẩy không tới thì không thử lại. |
| Hiển thị công khai | Lúc nội dung (bài, bình luận) hiện được với người khác, tức sau khi qua bước quét trước khi đăng. Thông báo nhắc tên gửi ở mốc này. |
| Bài mới | Bài của một người dùng lần đầu hiển thị công khai. Sửa bài hoặc khôi phục bài đã xóa không phải bài mới. |
| Theo dõi | Quan hệ giữa một người dùng (người theo dõi) và một đối tượng theo dõi. |
| Đối tượng theo dõi | Người dùng hoặc Topic. Tag, Group và bài viết không phải đối tượng theo dõi. |
| Thời điểm bắt đầu theo dõi | Lúc người dùng bắt đầu theo dõi một đối tượng; M02 dùng để xếp danh sách theo dõi. |
| Tắt thông báo cho bài | Cài đặt của một người dùng trên một bài: không nhận thông báo bình luận mới, trả lời, upvote bài và upvote các bình luận của mình trong bài đó; vẫn nhận thông báo nhắc tên. |
| Tắt thông báo cuộc trò chuyện | Cài đặt của một thành viên trên một cuộc trò chuyện 1-1 hoặc nhóm chat: tin nhắn mới của cuộc đó không hiện popup; số trên biểu tượng Tin nhắn vẫn tính cuộc đó. |
| Tắt thông báo toàn bộ Chat | Cài đặt của một người dùng: tin nhắn mới của mọi cuộc trò chuyện 1-1 và nhóm chat không hiện popup, không có ngoại lệ; số trên biểu tượng Tin nhắn vẫn tính đủ. |
| 24 giờ | 24 × 60 phút, tính theo thời điểm thật, giờ Asia/Ho_Chi_Minh khi hiển thị. |

### 2.2 Viết tắt

| Viết tắt | Đầy đủ |
|---|---|
| FR | Functional Requirement — yêu cầu chức năng |
| BR | Business Rule — quy tắc nghiệp vụ |
| AI | Trí tuệ nhân tạo; trong tài liệu này là việc AI ẩn bình luận, từ chối bài, ra cảnh cáo (M08, M13) sinh ra sự kiện thông báo |
| UTC | Giờ quốc tế, dùng để lưu thời điểm; hiển thị theo giờ Asia/Ho_Chi_Minh (UTC+7) |
| MS1 | Milestone 1 — mốc demo của đồ án |
| TBD | To Be Determined — điểm chưa chốt |

## 3. Thông tin đầu vào

### 3.1 Tài liệu đầu vào

| Tài liệu | Phiên bản / mốc |
|---|---|
| Draft: docs/_temp/iShare_modules.md, iShare_specs_general.md | Theo ngày sửa tệp |
| Register: decisions, qa-log, issue-queue, open-issues, glossary, module-registry | DEC-220, QA-411, ISS-351, OPEN-012 (khớp `moc_nguon`) |

### 3.2 Tài liệu liên quan

| Module | Liên quan ở điểm nào |
|---|---|
| M01 Authentication & Account | Sự kiện bảo mật tài khoản (đổi, đặt lại mật khẩu; liên kết Google; cảnh báo trước khi tự xóa); nhắc tên; nhiều thiết bị; xóa quan hệ theo dõi khi DELETED. |
| M02 User Profile | Hiện số và danh sách người theo dõi, đang theo dõi từ quan hệ theo dõi. |
| M03 Post & Content | Sự kiện bài được đăng, bị từ chối, bị ẩn, poll kết thúc; nơi bật tắt thông báo theo bài. |
| M04 Comment | Sự kiện bình luận mới, trả lời, nhắc tên, upvote bình luận, bình luận bị ẩn. |
| M05 Topic & Tag | Danh mục Topic để theo dõi; chuyển, bỏ lượt theo dõi khi gộp, xóa Topic. |
| M06 Search | Dùng quan hệ theo dõi cho bộ lọc chỉ nội dung đang theo dõi. |
| M08 Moderation | Sự kiện kết quả báo cáo, cảnh cáo, ban, gỡ ban. |
| M09 Appeal | Sự kiện kết luận khiếu nại; đường dẫn khiếu nại trong thông báo. |
| M10 Admin Panel | Sự kiện đề xuất làm Mod. |
| M11 Group | Sự kiện mời, gia nhập, duyệt, thăng cấp, kick trong nhóm; quyền xem nhóm Private. |
| M12 Gamification | Sự kiện upvote, badge, mốc điểm, danh hiệu tuần. |
| M14 Feed & Discovery | Dùng quan hệ theo dõi cho tab Following. |
| M16 Chat & Messaging | Sự kiện tin nhắn mới, mốc đã đọc tin nhắn, cuộc trò chuyện đang xem; popup tin nhắn, tắt thông báo theo cuộc trò chuyện và toàn bộ Chat. |

## 4. Tổng quan chức năng

### 4.1 Luật, tiêu chuẩn liên quan

Không có.

### 4.2 Vai trò

| Vai trò | Mô tả trong module này |
|---|---|
| Guest | Người chưa đăng nhập. Không nhận thông báo, không có chuông và biểu tượng Tin nhắn, không theo dõi được (theo dõi cần đăng nhập). |
| User | Người dùng đã đăng nhập. Nhận thông báo về sự kiện liên quan tới mình, xem và đánh dấu đã đọc thông báo của mình, theo dõi và bỏ theo dõi người dùng, Topic, tắt thông báo theo bài và theo Chat. |
| Mod | Như User. Nguồn không cho Mod quyền thêm trong module này. |
| Admin | Như User. Nguồn không cho Admin quyền thêm trong module này. |
| Người nhận | Vai trò theo ngữ cảnh: người dùng mà một sự kiện hướng tới (ví dụ tác giả bài được bình luận, người được nhắc tên, người bị cảnh cáo). Mỗi người chỉ thấy thông báo của chính mình. |
| Thành viên cuộc trò chuyện | Vai trò theo ngữ cảnh (M16): người dùng thuộc một cuộc trò chuyện 1-1 hoặc nhóm chat; nhận thông báo tin nhắn của cuộc trò chuyện đó và tắt được thông báo của nó. |
| Hệ thống | Tạo thông báo khi nhận sự kiện, đẩy thông báo tới người đang mở ứng dụng, gửi email qua hàng đợi. |

### 4.3 Ma trận quyền

| Hành động | Guest | User | Mod | Admin | Yêu cầu |
|---|---|---|---|---|---|
| Theo dõi người dùng, Topic | ✗ | ✓ | ✓ | ✓ | FR-M07-01.01, FR-M07-01.03, FR-M07-01.11, FR-M07-01.12 |
| Bỏ theo dõi người dùng, Topic | ✗ | ✓ (của mình) | ✓ (của mình) | ✓ (của mình) | FR-M07-01.03, FR-M07-01.08 |
| Xem thông báo (chuông, trang Thông báo) | ✗ | ✓ (của mình) | ✓ (của mình) | ✓ (của mình) | FR-M07-05.01, FR-M07-05.02, FR-M07-05.05, FR-M07-05.06 |
| Đánh dấu một thông báo, tất cả thông báo đã đọc | ✗ | ✓ (của mình) | ✓ (của mình) | ✓ (của mình) | FR-M07-06.01, FR-M07-06.03, FR-M07-06.06 |
| Xem số tin nhắn chưa đọc trên biểu tượng Tin nhắn | ✗ | ✓ (của mình) | ✓ (của mình) | ✓ (của mình) | FR-M07-07.02, FR-M07-07.04 |
| Tắt, bật thông báo cho một bài viết | ✗ | ✓ (cho mình) | ✓ (cho mình) | ✓ (cho mình) | FR-M07-08.02, FR-M07-08.04, FR-M07-08.05 |
| Tắt, bật thông báo cho một cuộc trò chuyện | ✗ | ✓ (thành viên) | ✓ (thành viên) | ✓ (thành viên) | FR-M07-09.01, FR-M07-09.05, FR-M07-09.06 |
| Tắt, bật thông báo cho toàn bộ Chat | ✗ | ✓ (cho mình) | ✓ (cho mình) | ✓ (cho mình) | FR-M07-09.03, FR-M07-09.06 |

<!-- Ô suy ra: cột Guest (theo dõi cần đăng nhập — DEC-126, QA-227; Guest không có tương tác, nhắn tin — QA-011, nên không có thông báo);
     "(của mình)" ở các hàng xem, đánh dấu (thông báo gửi cho từng người nhận; nguồn không có ai xem thông báo của người khác);
     "(cho mình)" ở hàng tắt thông báo bài, toàn bộ Chat (DEC-070: công tắc trên mỗi bài và một cài đặt Chat, chỉ đổi thông báo của người bật);
     cột Mod, Admin (nguồn không cho Mod, Admin quyền khác User trong module này). -->

### 4.4 Danh sách chức năng

| ID | Chức năng | Tác nhân chính | Kích hoạt |
|---|---|---|---|
| FR-M07-01 | Theo dõi và bỏ theo dõi người dùng, Topic | User, Mod, Admin | Người dùng bấm theo dõi hoặc bỏ theo dõi trên trang hồ sơ hoặc Topic |
| FR-M07-02 | Tạo thông báo khi có sự kiện | Hệ thống | Một module báo một sự kiện thuộc danh sách sự kiện thông báo |
| FR-M07-03 | Đẩy thông báo mới tới người dùng đang mở ứng dụng | Hệ thống | Một thông báo vừa được tạo cho người dùng đang mở ứng dụng trên một hay nhiều thiết bị |
| FR-M07-04 | Gửi email thông báo | Hệ thống | Một sự kiện thuộc nhóm có email xảy ra; hàng đợi email được quét mỗi phút |
| FR-M07-05 | Xem thông báo | User, Mod, Admin | Người dùng bấm chuông thông báo hoặc mở trang Thông báo |
| FR-M07-06 | Đánh dấu thông báo đã đọc | User, Mod, Admin | Người dùng bấm vào một thông báo, hoặc bấm "Đánh dấu tất cả đã đọc" |
| FR-M07-07 | Báo tin nhắn mới qua popup và biểu tượng Tin nhắn | User, Mod, Admin | Có tin nhắn mới trong cuộc trò chuyện của người dùng; người dùng bấm biểu tượng Tin nhắn |
| FR-M07-08 | Tắt thông báo cho một bài viết | User, Mod, Admin | Người dùng bật hoặc tắt "Tắt thông báo cho bài này" trên một bài |
| FR-M07-09 | Tắt thông báo Chat | User, Mod, Admin | Người dùng tắt hoặc bật thông báo của một cuộc trò chuyện, hoặc cài đặt "Tắt thông báo cho toàn bộ Chat" |

### 4.5 Mốc và ưu tiên

Toàn bộ yêu cầu của module thuộc MS1, ưu tiên **Must** (bảng MoSCoW Summary của module-registry: Must gồm M01–M10, M13;
dòng M07 của bảng Module List bị lệch cột, không có giá trị MoSCoW nên không dùng). Không có yêu cầu ngoại lệ về ưu tiên.
Các sự kiện phát sinh từ module Should (M11 Group, M12 Gamification, M16 Chat & Messaging) chỉ có khi module đó có mặt.

## 5. Yêu cầu chức năng

### 5.1 FR-M07-01 Theo dõi và bỏ theo dõi người dùng, Topic

**Yêu cầu cấp trên:** Hệ thống phải cho người dùng đã đăng nhập theo dõi và bỏ theo dõi người dùng, Topic, và giữ quan hệ theo dõi cho các module khác dùng.

**Lý do:** Người dùng theo dõi để "nhận cập nhật về nội dung hoặc chủ đề" (DM-4.5). Không theo dõi Group vì tham gia, rời nhóm đã đủ nghĩa đó (QA-043).

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M07-01.01 | Khi người dùng đã đăng nhập bấm theo dõi một người dùng hoặc một Topic, hệ thống phải tạo quan hệ theo dõi giữa người dùng đó và đối tượng, kèm thời điểm bắt đầu theo dõi. |
| FR-M07-01.02 | Hệ thống phải không cho theo dõi Tag, Group và bài viết (BR-M07-15). |
| FR-M07-01.03 | Nếu người chưa đăng nhập bấm theo dõi hoặc bỏ theo dõi, hệ thống phải từ chối và yêu cầu đăng nhập. |
| FR-M07-01.04 | Khi người dùng theo dõi một người dùng khác lần đầu, hệ thống phải tạo sự kiện "có người theo dõi mới" cho người được theo dõi (BR-M07-25). |
| FR-M07-01.05 | (Đã bỏ ở phiên bản 0.2 — hành vi thuộc M05, xem FR-M05-07.06.) |
| FR-M07-01.06 | (Đã bỏ ở phiên bản 0.2 — hành vi thuộc M05, xem FR-M05-08.06.) |
| FR-M07-01.07 | (Đã bỏ ở phiên bản 0.2 — hành vi thuộc M01, xem FR-M01-12.08.) |
| FR-M07-01.08 | Khi người dùng bấm bỏ theo dõi một người dùng hoặc một Topic đang theo dõi, hệ thống phải xóa quan hệ theo dõi đó, để số người theo dõi của đối tượng giảm 1 (BR-M07-25). |
| FR-M07-01.09 | Khi người dùng bỏ theo dõi, hệ thống phải không tạo thông báo cho ai. |
| FR-M07-01.10 | Nếu người dùng theo dõi lại một người dùng đã nhận thông báo "có người theo dõi mới" từ chính người đó, hệ thống phải không tạo lại sự kiện này. |
| FR-M07-01.11 | Nếu người dùng bấm theo dõi chính mình, hệ thống phải từ chối. |
| FR-M07-01.12 | Nếu người dùng bấm theo dõi một tài khoản đang BANNED, hệ thống phải từ chối. |
| FR-M07-01.13 | Khi một tài khoản đang được theo dõi chuyển BANNED hoặc DEACTIVATED, hệ thống phải giữ các quan hệ theo dõi đã có với tài khoản đó. |


### 5.2 FR-M07-02 Tạo thông báo khi có sự kiện

**Yêu cầu cấp trên:** Khi một module báo một sự kiện thuộc danh sách sự kiện thông báo, hệ thống phải tạo thông báo trong ứng dụng cho người nhận của sự kiện, theo các quy tắc gộp, tắt thông báo và quyền xem.

**Lý do:** Upvote được gộp để tránh làm phiền người nhận ("batched within 5-min window to avoid spam", QA-126). Nhắc tên vẫn được báo khi bài đã bị tắt thông báo vì đó là lời gọi có chủ đích tới người dùng (DEC-070).

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M07-02.01 | Khi một module báo một sự kiện thuộc BR-M07-01, hệ thống phải tạo một thông báo ở trạng thái chưa đọc cho mỗi người nhận của sự kiện. |
| FR-M07-02.02 | Hệ thống phải dùng người nhận, nội dung liên quan và thời điểm xảy ra sự kiện do module phát sinh sự kiện cung cấp. |
| FR-M07-02.03 | Khi bài viết hoặc bình luận của người dùng nhận một upvote mà nó không có cửa sổ 5 phút đang mở, hệ thống phải tạo ngay thông báo upvote hiện tên người upvote và mở cửa sổ 5 phút cho bài viết hoặc bình luận đó (BR-M07-05). |
| FR-M07-02.04 | Khi bài viết hoặc bình luận nhận thêm upvote trong cửa sổ 5 phút đang mở của nó, hệ thống phải cập nhật chính thông báo upvote đó thành "A và N người khác đã upvote…", chuyển nó về chưa đọc và đưa nó lên đầu danh sách. |
| FR-M07-02.05 | (Đã bỏ ở phiên bản 0.2 — hành vi thuộc M01, xem FR-M01-14.10.) |
| FR-M07-02.06 | (Đã bỏ ở phiên bản 0.2 — hành vi thuộc M01, xem FR-M01-14.10.) |
| FR-M07-02.07 | Nếu người được nhắc tên đã tắt thông báo cho bài chứa lượt nhắc, hệ thống phải vẫn tạo thông báo nhắc tên. |
| FR-M07-02.08 | Nếu người nhận đã tắt thông báo cho một bài, hệ thống phải không tạo cho người đó thông báo bình luận mới, trả lời, upvote bài và upvote các bình luận của người đó trong bài (BR-M07-07). |
| FR-M07-02.09 | Nếu người nhận đã tắt thông báo cho một bài, hệ thống phải vẫn tạo cho người đó các thông báo khác về bài, ngoài bình luận mới, trả lời, upvote. |
| FR-M07-02.10 | Hệ thống phải không đưa tin nhắn 1-1 và nhóm chat vào chuông thông báo; tin nhắn được báo ở biểu tượng Tin nhắn (FR-M07-07). |
| FR-M07-02.11 | Nếu sự kiện liên quan tới nội dung trong nhóm Private, hệ thống phải chỉ tạo thông báo cho người nhận có quyền xem nội dung đó (BR-M07-18). |
| FR-M07-02.12 | (Đã bỏ ở phiên bản 0.2 — hành vi thuộc M09, xem FR-M09-01.19.) |
| FR-M07-02.13 | Khi sự kiện là một xử lý khiếu nại được (cảnh cáo, ban, bài bị Mod/Admin gỡ, bài bị AI từ chối), hệ thống phải đưa đường dẫn khiếu nại vào thông báo. |
| FR-M07-02.14 | Khi Admin gửi đề xuất làm Mod cho một người dùng (M10), hệ thống phải tạo cho người đó thông báo có hai lựa chọn Chấp nhận và Từ chối (BR-M07-20). |
| FR-M07-02.15 | Khi người được đề xuất bấm Chấp nhận trên thông báo, hệ thống phải chuyển lựa chọn cho M10 để đặt vai trò MOD ngay. |
| FR-M07-02.16 | Khi người được đề xuất bấm Từ chối trên thông báo, hệ thống phải giữ nguyên vai trò của người đó. |
| FR-M07-02.17 | Hệ thống phải không tạo thông báo cho các trường hợp ở BR-M07-21. |
| FR-M07-02.18 | Hệ thống phải gộp upvote riêng cho từng bài viết và từng bình luận. |
| FR-M07-02.19 | Khi một người dùng bỏ upvote, hệ thống phải giữ nguyên thông báo upvote đã tạo. |
| FR-M07-02.20 | Nếu một người đã được đếm upvote lại trong cùng cửa sổ, hệ thống phải không đếm người đó thêm lần nữa. |
| FR-M07-02.21 | Khi bài của một người dùng hiển thị công khai lần đầu, hệ thống phải tạo thông báo "người bạn theo dõi có bài mới" cho mỗi người đang theo dõi người dùng đó (BR-M07-23). |
| FR-M07-02.22 | Nếu bài được đăng ẩn danh, hệ thống phải không tạo thông báo bài mới cho người theo dõi tác giả. |
| FR-M07-02.23 | Nếu bài bị từ chối, được sửa hoặc được khôi phục, hệ thống phải không tạo thông báo bài mới. |
| FR-M07-02.24 | Hệ thống phải không tạo thông báo khi một Topic có bài mới, kể cả cho người đang theo dõi Topic đó. |
| FR-M07-02.25 | Nếu người gây sự kiện cũng là người nhận, hệ thống phải không tạo thông báo cho người đó (BR-M07-24). |
| FR-M07-02.26 | Nếu người nhận đang BANNED hoặc DEACTIVATED, hệ thống phải vẫn tạo thông báo cho người đó. |
| FR-M07-02.27 | Nếu người nhận đã DELETED, hệ thống phải không tạo thông báo cho người đó. |
| FR-M07-02.28 | Khi người được đề xuất đã chọn Chấp nhận hoặc Từ chối, hệ thống phải hiện lựa chọn đó trên thông báo và không cho chọn lại (BR-M07-20). |
| FR-M07-02.29 | Hệ thống phải không đặt hạn cho thông báo đề xuất làm Mod chưa được trả lời. |
| FR-M07-02.30 | Khi Admin đề xuất lại cho cùng người dùng, hệ thống phải tạo một thông báo đề xuất mới. |


### 5.3 FR-M07-03 Đẩy thông báo mới tới người dùng đang mở ứng dụng

**Yêu cầu cấp trên:** Hệ thống phải đẩy mỗi thông báo vừa được lưu tới mọi thiết bị đang mở ứng dụng của người nhận, theo kiểu cố gắng.

**Lý do:** Thông báo đã lưu là nguồn chính nên không cần thử đẩy lại: người dùng luôn tải thông báo chưa đọc khi mở trang hoặc bấm chuông ("client fetch-on-load covers gaps", QA-131; DEC-069).

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M07-03.01 | Khi một thông báo được tạo, hệ thống phải lưu thông báo đó trước khi đẩy (BR-M07-09). |
| FR-M07-03.02 | Khi một thông báo đã được lưu, hệ thống phải đẩy thông báo đó tới mọi thiết bị đang mở ứng dụng của người nhận (BR-M07-10). |
| FR-M07-03.03 | Nếu đẩy thông báo tới một thiết bị không thành công, hệ thống phải không thử đẩy lại. |
| FR-M07-03.04 | Khi người dùng mở trang hoặc bấm chuông, hệ thống phải tải thông báo chưa đọc từ thông báo đã lưu, dù việc đẩy trước đó thành công hay không. |

### 5.4 FR-M07-04 Gửi email thông báo

**Yêu cầu cấp trên:** Hệ thống phải gửi email cho các sự kiện thuộc nhóm có email, bất đồng bộ qua hàng đợi email được quét mỗi 1 phút.

**Lý do:** Email chạy bất đồng bộ để không chặn thao tác gây ra sự kiện (DEC-068, QA-130). Cảnh báo trước khi tự xóa chỉ gửi email vì tài khoản DEACTIVATED không đăng nhập được (DEC-065).

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M07-04.01 | Khi một sự kiện thuộc nhóm có email xảy ra, hệ thống phải ghi một email cho người nhận vào hàng đợi email (BR-M07-03, BR-M07-11). |
| FR-M07-04.02 | Hệ thống phải quét hàng đợi email mỗi 1 phút và gửi các email chưa gửi trong đó. |
| FR-M07-04.03 | Hệ thống phải hoàn tất thao tác gây ra sự kiện mà không chờ email được gửi. |
| FR-M07-04.04 | Nếu sự kiện không thuộc nhóm có email, hệ thống phải không gửi email cho sự kiện đó. |
| FR-M07-04.05 | (Đã bỏ ở phiên bản 0.2 — hành vi thuộc M01, xem FR-M01-12.05, BR-M01-32.) |
| FR-M07-04.06 | Hệ thống phải không tạo thông báo trong ứng dụng cho cảnh báo trước khi tự xóa. |
| FR-M07-04.07 | (Đã bỏ ở phiên bản 0.2 — hành vi thuộc M01, xem FR-M01-12.05, BR-M01-32.) |
| FR-M07-04.08 | Khi gửi email về ban, hệ thống phải đưa vào email đường dẫn tới trang khiếu nại. |
| FR-M07-04.09 | Nếu gửi một email không thành công, hệ thống phải giữ email đó trong hàng đợi để gửi lại ở lần quét kế tiếp, tối đa 3 lần gửi lại (BR-M07-26). |
| FR-M07-04.10 | Nếu email vẫn không gửi được sau 3 lần gửi lại, hệ thống phải dừng gửi email đó. |


### 5.5 FR-M07-05 Xem thông báo

**Yêu cầu cấp trên:** Hệ thống phải cho người dùng đã đăng nhập xem thông báo của mình: danh sách gần nhất khi bấm chuông và toàn bộ ở trang Thông báo.

**Lý do:** Thông báo được giữ vô thời hạn, theo cách làm của Facebook, Twitter, Discord, GitHub (DEC-071).

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M07-05.01 | Khi người dùng bấm chuông thông báo, hệ thống phải hiện 10 thông báo gần nhất của người dùng, mới nhất trước theo lần cập nhật cuối (BR-M07-12). |
| FR-M07-05.02 | Khi người dùng mở trang Thông báo, hệ thống phải hiện thông báo của người dùng mới nhất trước, tải thêm 20 thông báo mỗi lần cuộn, tới thông báo cũ nhất. |
| FR-M07-05.03 | Hệ thống phải hiện mỗi thông báo kèm trạng thái đã đọc hoặc chưa đọc. |
| FR-M07-05.04 | Hệ thống phải hiện thời điểm của thông báo theo giờ Asia/Ho_Chi_Minh (BR-M07-22). |
| FR-M07-05.05 | Hệ thống phải chỉ hiện cho mỗi người dùng các thông báo của chính người đó. |
| FR-M07-05.06 | Nếu người chưa đăng nhập mở trang Thông báo, hệ thống phải từ chối và yêu cầu đăng nhập. |
| FR-M07-05.07 | Hệ thống phải giữ mọi thông báo vô thời hạn, không tự xóa (BR-M07-13). |
| FR-M07-05.08 | (Đã bỏ ở phiên bản 0.2 — hành vi thuộc M03, M04, xem FR-M04-06.01.) |
| FR-M07-05.09 | Trong khi tài khoản đang BANNED, hệ thống phải không cho xem chuông và trang Thông báo. |
| FR-M07-05.10 | Hệ thống phải hiện trên chuông số thông báo chưa đọc của người dùng, không tính tin nhắn. |
| FR-M07-05.11 | Khi người dùng mở chuông, hệ thống phải giữ nguyên trạng thái đã đọc, chưa đọc của các thông báo. |
| FR-M07-05.12 | Hệ thống phải hiện tên người gây sự kiện là "Tài khoản tạm thời vô hiệu hoá" khi tài khoản đó DEACTIVATED và "[Người dùng đã xóa]" khi tài khoản đó DELETED (BR-M07-24). |
| FR-M07-05.13 | Nếu nội dung liên quan của thông báo đã bị xóa, bị ẩn hoặc người dùng không còn quyền xem, khi người dùng bấm thông báo, hệ thống phải hiện "Nội dung không tồn tại", trừ khi chủ nội dung xem nội dung của mình đã bị xử lý theo M03, M04 (BR-M07-27). |


### 5.6 FR-M07-06 Đánh dấu thông báo đã đọc

**Yêu cầu cấp trên:** Hệ thống phải cho người dùng đánh dấu thông báo của mình là đã đọc: từng thông báo khi bấm vào, hoặc tất cả cùng lúc.

**Lý do:** Nguồn chưa nêu lý do.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M07-06.01 | Khi người dùng bấm vào một thông báo chưa đọc, hệ thống phải chuyển thông báo đó sang đã đọc (BR-M07-14). |
| FR-M07-06.02 | Khi người dùng bấm vào một thông báo, hệ thống phải chuyển người dùng tới nội dung liên quan của thông báo. |
| FR-M07-06.03 | Khi người dùng bấm "Đánh dấu tất cả đã đọc", hệ thống phải chuyển mọi thông báo chưa đọc của người dùng sang đã đọc. |
| FR-M07-06.04 | Nếu người dùng bấm vào một thông báo đã đọc, hệ thống phải giữ thông báo đó ở trạng thái đã đọc. |
| FR-M07-06.05 | Khi người dùng bấm "Đánh dấu tất cả đã đọc", hệ thống phải giữ nguyên trạng thái đã đọc của tin nhắn. |
| FR-M07-06.06 | Nếu người chưa đăng nhập đánh dấu thông báo đã đọc, hệ thống phải từ chối. |

### 5.7 FR-M07-07 Báo tin nhắn mới qua popup và biểu tượng Tin nhắn

**Yêu cầu cấp trên:** Hệ thống phải báo tin nhắn mới 1-1 và nhóm chat bằng popup nhỏ và bằng biểu tượng Tin nhắn riêng hiện số cuộc trò chuyện có tin chưa đọc, dẫn tới hộp thư Chat.

**Lý do:** Nguồn chưa nêu lý do.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M07-07.01 | Hệ thống phải hiện biểu tượng Tin nhắn trên thanh điều hướng, tách khỏi chuông thông báo. |
| FR-M07-07.02 | Hệ thống phải hiện trên biểu tượng Tin nhắn số cuộc trò chuyện có tin chưa đọc của người dùng theo mốc đã đọc của M16, gồm cả cuộc đã tắt thông báo (BR-M07-02). |
| FR-M07-07.03 | Khi người dùng bấm biểu tượng Tin nhắn, hệ thống phải chuyển người dùng tới hộp thư Chat (M16). |
| FR-M07-07.04 | Hệ thống phải chỉ hiện biểu tượng Tin nhắn cho người đã đăng nhập. |
| FR-M07-07.05 | Khi có tin nhắn mới trong một cuộc trò chuyện mà người dùng là thành viên và người dùng đang mở ứng dụng, hệ thống phải hiện một popup nhỏ báo tin nhắn đó (BR-M07-28). |
| FR-M07-07.06 | Nếu người dùng đang xem đúng cuộc trò chuyện có tin nhắn mới, hệ thống phải không hiện popup cho tin nhắn đó. |
| FR-M07-07.07 | Nếu cuộc trò chuyện đã bị người dùng tắt thông báo, hoặc người dùng đang bật "Tắt thông báo cho toàn bộ Chat", hệ thống phải không hiện popup cho tin nhắn của cuộc đó (BR-M07-08). |


### 5.8 FR-M07-08 Tắt thông báo cho một bài viết

**Yêu cầu cấp trên:** Hệ thống phải cho người dùng đã đăng nhập tắt và bật lại, chỉ cho chính mình, thông báo bình luận mới, trả lời, upvote phát sinh từ một bài viết.

**Lý do:** Thay cho trang cài đặt thông báo theo loại, không làm ở bản đầu ("No granular global preference settings page for v1", DEC-070; QA-132). Nhắc tên vẫn được báo vì đó là lời gọi có chủ đích tới người dùng (DEC-070).

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M07-08.01 | Hệ thống phải hiện công tắc "Tắt thông báo cho bài này" trên mỗi bài viết cho người đã đăng nhập. |
| FR-M07-08.02 | Khi người dùng bật "Tắt thông báo cho bài này", hệ thống phải ghi bài đó là đã tắt thông báo cho người dùng. |
| FR-M07-08.03 | Khi người dùng tắt "Tắt thông báo cho bài này", hệ thống phải bỏ ghi nhận đã tắt để người dùng nhận lại thông báo của bài từ lúc đó. |
| FR-M07-08.04 | Hệ thống phải chỉ áp việc tắt thông báo bài cho người đã bật nó; người khác vẫn nhận thông báo của bài. |
| FR-M07-08.05 | Nếu người chưa đăng nhập dùng công tắc tắt thông báo bài, hệ thống phải từ chối và yêu cầu đăng nhập. |


### 5.9 FR-M07-09 Tắt thông báo Chat

**Yêu cầu cấp trên:** Hệ thống phải cho người dùng tắt và bật lại thông báo tin nhắn của từng cuộc trò chuyện mình là thành viên, và của toàn bộ Chat.

**Lý do:** Thay cho trang cài đặt thông báo theo loại; cài đặt toàn bộ Chat dùng cùng cài đặt từng cuộc để chỉnh chi tiết hơn ("coexists with per-conversation mute for finer override", DEC-070).

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M07-09.01 | Khi thành viên tắt thông báo một cuộc trò chuyện, hệ thống phải ghi cuộc trò chuyện đó là đã tắt thông báo cho thành viên (BR-M07-08). |
| FR-M07-09.02 | Khi thành viên bật lại thông báo một cuộc trò chuyện, hệ thống phải bỏ ghi nhận đã tắt để tin nhắn của cuộc đó hiện popup lại từ lúc đó. |
| FR-M07-09.03 | Khi người dùng bật "Tắt thông báo cho toàn bộ Chat", hệ thống phải ngừng hiện popup cho tin nhắn của mọi cuộc trò chuyện 1-1 và nhóm chat của người dùng, không có ngoại lệ. |
| FR-M07-09.04 | Khi người dùng tắt "Tắt thông báo cho toàn bộ Chat", hệ thống phải hiện popup theo cài đặt tắt của từng cuộc trò chuyện, giữ các cuộc đã tắt riêng ở trạng thái tắt. |
| FR-M07-09.05 | Nếu người dùng không là thành viên của một cuộc trò chuyện, hệ thống phải từ chối tắt thông báo cuộc trò chuyện đó. |
| FR-M07-09.06 | Nếu người chưa đăng nhập dùng cài đặt tắt thông báo Chat, hệ thống phải từ chối và yêu cầu đăng nhập. |
| FR-M07-09.07 | Hệ thống phải giữ số trên biểu tượng Tin nhắn như nhau dù cuộc trò chuyện có bị tắt thông báo hay không. |


### 5.10 Quy tắc nghiệp vụ

| ID | Loại | Quy tắc | Ví dụ |
|---|---|---|---|
| BR-M07-01 | Sự kiện | Sự kiện sinh thông báo trong ứng dụng: mật khẩu đã đổi (đổi trong Cài đặt hoặc đặt lại); đã liên kết Google; có người theo dõi mới; người bạn theo dõi có bài mới; bài được đăng, bị từ chối, bị ẩn, poll kết thúc; upvote bài viết, upvote bình luận (gộp theo BR-M07-05); bình luận mới, trả lời, nhắc tên; "Bình luận của bạn đã bị ẩn" khi AI ẩn bình luận; kết quả báo cáo, nhận cảnh cáo; ban, gỡ ban; kết luận khiếu nại về ban, về bài viết, về cảnh cáo; nhóm: mời, gia nhập, duyệt, thăng cấp, kick; badge, mốc điểm, danh hiệu tuần; đề xuất làm Mod. | — |
| BR-M07-02 | Sự kiện | Tin nhắn mới trong cuộc trò chuyện 1-1 hoặc nhóm chat được báo bằng popup nhỏ (BR-M07-28) và bằng số trên biểu tượng Tin nhắn; không hiện ở chuông thông báo, không gửi email. Số trên biểu tượng Tin nhắn là số cuộc trò chuyện có tin chưa đọc, gồm cả cuộc đã tắt thông báo. | Bình gửi An 5 tin, Chi gửi An 2 tin, An chưa đọc → biểu tượng Tin nhắn hiện 2; chuông của An không đổi; An không nhận email. An đọc cuộc với Bình → còn 1. |
| BR-M07-03 | Ràng buộc | Chỉ các sự kiện sau được gửi thêm qua email: mật khẩu đã đổi, đã liên kết Google, cảnh báo trước khi tự xóa, ban, gỡ ban, kết luận khiếu nại về ban. Mọi sự kiện khác chỉ báo trong ứng dụng. Không có email tổng hợp. | An bị ban: thông báo trong ứng dụng và email. An nhận cảnh cáo: chỉ trong ứng dụng. Khiếu nại ban của An được kết luận: trong ứng dụng và email; khiếu nại cảnh cáo được kết luận: chỉ trong ứng dụng. |
| BR-M07-04 | Kích hoạt | Cảnh báo trước khi tự xóa chỉ gửi qua email, không có thông báo trong ứng dụng; gửi đúng một email, lúc còn 24 giờ trước khi tài khoản DEACTIVATED tự chuyển DELETED. | Vô hiệu hóa 01/10 21:00 → DELETED lúc 15/10 21:00 → email cảnh báo lúc 14/10 21:00. Kích hoạt lại lúc 14/10 20:00 → không gửi email. |
| BR-M07-05 | Tính toán | Upvote được gộp riêng cho từng bài viết và từng bình luận. Upvote mà bài/bình luận không có cửa sổ đang mở thì được báo ngay bằng thông báo mới hiện tên người upvote và mở cửa sổ 5 phút tính từ lượt đó. Upvote sau trong cửa sổ cập nhật chính thông báo đó thành "A và N người khác đã upvote…" (A: người upvote mới nhất; N: số người khác nhau còn lại trong cửa sổ), chuyển về chưa đọc, đưa lên đầu. Cửa sổ không kéo dài theo lượt sau. Bỏ upvote không đổi thông báo; một người upvote lại trong cùng cửa sổ không được đếm thêm. | 10:00 Bình upvote bài X → mới "Bình đã upvote bài X", cửa sổ X đến trước 10:05:00. 10:02 Chi upvote X → cùng thông báo "Chi và 1 người khác đã upvote bài X", chưa đọc, lên đầu. 10:03 Bình bỏ rồi upvote lại X → không đổi. 10:04 Dũng upvote bình luận Y → thông báo mới riêng cho Y. 10:05:00 Em upvote X → cửa sổ đã hết → thông báo mới "Em đã upvote bài X". |
| BR-M07-06 | Suy diễn | Nhắc tên luôn sinh thông báo cho người được nhắc, dù lượt nhắc nằm trong bài viết hay bình luận, kể cả khi người đó đã tắt thông báo cho bài. Thông báo gửi khi nội dung chứa lượt nhắc hiển thị công khai; khi sửa nội dung, chỉ người mới được nhắc thêm nhận thông báo. | Bài nhắc @An gửi 10:00, qua quét và đăng 10:01 → An nhận lúc 10:01. Bài bị giữ chờ Mod tới 11:00 rồi được duyệt → An nhận lúc 11:00. Tác giả sửa bài, giữ @An, thêm @Bình → chỉ Bình nhận. An đã tắt thông báo cho bài, có bình luận nhắc @An → An vẫn nhận. |
| BR-M07-07 | Suy diễn | Khi một người dùng tắt thông báo cho một bài, người đó không nhận thông báo bình luận mới, trả lời, upvote bài và upvote các bình luận của mình trong bài đó; các thông báo khác về bài đó (nhắc tên, bài bị ẩn, kết quả báo cáo…) vẫn gửi. Công tắc có trên mọi bài cho người đã đăng nhập. Bật lại thì từ đó nhận như thường. | An tắt thông báo bài X: Bình bình luận vào X → An không nhận; Chi upvote bình luận của An trong X → An không nhận; Mod ẩn X → An vẫn nhận "bài bị ẩn". |
| BR-M07-08 | Suy diễn | Tắt thông báo (một cuộc trò chuyện hoặc toàn bộ Chat) chỉ làm tin nhắn mới không hiện popup; số trên biểu tượng Tin nhắn vẫn tính đủ. "Tắt thông báo cho toàn bộ Chat" áp cho mọi cuộc, không bật riêng được cuộc nào. Bỏ tắt toàn bộ thì các cuộc đã tắt riêng vẫn tắt. | An tắt cuộc với Bình. Bình gửi 3 tin, Chi gửi 1 tin → chỉ tin của Chi hiện popup; biểu tượng hiện 2. An bật tắt toàn bộ → không tin nào hiện popup. An bỏ tắt toàn bộ → tin của Chi hiện popup lại; cuộc với Bình vẫn không. |
| BR-M07-09 | Sự kiện | Mỗi thông báo được lưu trước, rồi mới đẩy tới các thiết bị đang mở ứng dụng của người nhận. Thông báo đã lưu là nguồn chính: đẩy không tới thì không thử lại; người dùng thấy đủ thông báo khi mở trang hoặc bấm chuông. | An mất mạng lúc 10:00 khi có bình luận mới; thông báo không đẩy tới được. 10:05 An mở lại ứng dụng → thấy thông báo đó, chưa đọc. |
| BR-M07-10 | Sự kiện | Người dùng đăng nhập trên nhiều thiết bị cùng lúc thì mỗi thiết bị đang mở ứng dụng đều được đẩy thông báo. | An mở ứng dụng trên điện thoại và máy tính; có người theo dõi An → cả hai thiết bị nhận thông báo. |
| BR-M07-11 | Ràng buộc | Email được gửi bất đồng bộ: sự kiện thuộc nhóm có email ghi một email vào hàng đợi email; hàng đợi được quét mỗi 1 phút và các email trong đó được gửi. Thao tác gây ra sự kiện không chờ việc gửi email. | Đổi mật khẩu lúc 10:00:20, lần quét kế tiếp lúc 10:01:00 → email được gửi trong lần quét 10:01:00; việc đổi mật khẩu hoàn tất ngay lúc 10:00:20. |
| BR-M07-12 | Ràng buộc | Chuông thông báo hiện 10 thông báo gần nhất, mới nhất trước theo lần cập nhật cuối, kèm số thông báo chưa đọc (không tính tin nhắn); mở chuông không đổi trạng thái đã đọc. Trang Thông báo hiện mọi thông báo mới nhất trước, tải thêm 20 mỗi lần cuộn, tới thông báo cũ nhất. | An có 25 thông báo, 3 chưa đọc: chuông hiện số 3 và 10 thông báo mới nhất; mở chuông xong vẫn 3. Trang Thông báo hiện 20, cuộn tải nốt 5. Thông báo upvote 10:00 đã đọc, 10:02 có upvote gộp thêm → lên đầu chuông, số chưa đọc thành 4. |
| BR-M07-13 | Ràng buộc | Thông báo được giữ vô thời hạn: không tự xóa, không có việc dọn định kỳ. | Thông báo tạo năm 2026 vẫn còn trên trang Thông báo năm 2030. |
| BR-M07-14 | Kích hoạt | Bấm vào một thông báo thì thông báo đó thành đã đọc và người dùng được chuyển tới nội dung liên quan. Bấm "Đánh dấu tất cả đã đọc" thì mọi thông báo chưa đọc của người dùng thành đã đọc. | An có 3 thông báo chưa đọc; bấm một cái → còn 2 chưa đọc và An sang bài liên quan. Bấm "Đánh dấu tất cả đã đọc" → 0 chưa đọc. |
| BR-M07-15 | Sự kiện | Đối tượng theo dõi là người dùng và Topic. Tag, Group, bài viết không theo dõi được. Theo dõi cần đăng nhập. Không theo dõi được chính mình và không bắt đầu theo dõi được tài khoản BANNED; lượt theo dõi đã có với tài khoản BANNED, DEACTIVATED được giữ. Theo dõi Topic không sinh thông báo. | An theo dõi được Bình và Topic Toán học; không theo dõi được Tag #tíchphân, một Group, một bài hay chính An. Chi đang BANNED → An không theo dõi mới được Chi. An theo dõi Dũng, sau đó Dũng bị ban → An vẫn theo dõi Dũng. |
| BR-M07-16 | — | (Đã bỏ ở phiên bản 0.2 — quy tắc thuộc M05, xem FR-M05-07.06, FR-M05-08.06.) | — |
| BR-M07-17 | — | (Đã bỏ ở phiên bản 0.2 — quy tắc thuộc M01, xem BR-M01-47.) | — |
| BR-M07-18 | Ràng buộc | Thông báo về nội dung trong Group dùng cùng cơ chế như ngoài Group; với nhóm Private, thông báo chỉ gửi cho người có quyền xem nội dung đó. | Bài trong nhóm Private G nhắc @An, An không là thành viên G → An không nhận thông báo (Suy ra). |
| BR-M07-19 | — | (Đã bỏ ở phiên bản 0.2 — quy tắc thuộc M09, xem FR-M09-01.19.) | — |
| BR-M07-20 | Sự kiện | Thông báo "Đề xuất làm Mod" có hai lựa chọn Chấp nhận và Từ chối, chọn được một lần; sau đó thông báo hiện lựa chọn đã chọn. Đề xuất không có hạn. Chấp nhận thì vai trò thành MOD ngay; Từ chối thì không có gì thay đổi; Admin đề xuất lại thì là một thông báo mới. | Admin đề xuất An; An bấm Từ chối → thông báo hiện "Đã từ chối", An vẫn là USER. Tuần sau Admin đề xuất lại → An nhận thông báo đề xuất mới và bấm Chấp nhận → An là MOD ngay. |
| BR-M07-21 | Sự kiện | Không có thông báo cho: tác giả khi Mod/Admin đổi Topic, Tag trên bài của họ; việc một khiếu nại chỉ ADMIN thấy được; nhắc cập nhật Lớp/Khối đầu năm học. | — |
| BR-M07-22 | Ràng buộc | Thời điểm của thông báo được lưu theo UTC và hiển thị theo giờ Asia/Ho_Chi_Minh (UTC+7). | Thông báo tạo lúc 02:30 UTC hiển thị 09:30. |
| BR-M07-23 | Kích hoạt | Khi bài của một người dùng hiển thị công khai lần đầu, mỗi người đang theo dõi người đó nhận thông báo "người bạn theo dõi có bài mới" (chỉ trong ứng dụng). Không gửi khi bài ẩn danh, khi người theo dõi không xem được bài (nhóm Private, BR-M07-18), khi bài bị từ chối, khi bài được sửa hoặc khôi phục. | Bình đăng bài lúc 10:00, qua quét và công khai 10:01 → An (theo dõi Bình) nhận lúc 10:01. Bình đăng ẩn danh → An không nhận. Bình sửa bài lúc 11:00 → An không nhận lại. |
| BR-M07-24 | Ràng buộc | Không có thông báo cho người gây sự kiện khi người đó cũng là người nhận. Thông báo vẫn được tạo cho người nhận BANNED, DEACTIVATED (thấy khi tài khoản ACTIVE lại), không tạo cho người nhận DELETED. Tên người gây sự kiện hiện "Tài khoản tạm thời vô hiệu hoá" khi tài khoản đó DEACTIVATED, "[Người dùng đã xóa]" khi DELETED. | An bình luận vào bài của An → An không nhận. Có người trả lời bình luận cũ của Bình đang BANNED → thông báo vẫn được tạo cho Bình. Chi upvote bài của An rồi Chi bị xóa tài khoản → thông báo của An hiện "[Người dùng đã xóa] đã upvote…". |
| BR-M07-25 | Ràng buộc | Người dùng bỏ theo dõi được người dùng, Topic đang theo dõi; quan hệ bị xóa, số người theo dõi giảm 1, không ai nhận thông báo. Thông báo "có người theo dõi mới" chỉ gửi một lần cho mỗi cặp người theo dõi – người được theo dõi. | An theo dõi Bình (Bình nhận "An đã theo dõi bạn"), bỏ theo dõi, rồi theo dõi lại 10 lần → Bình chỉ có một thông báo đó; số người theo dõi của Bình sau cùng tăng 1 so với ban đầu. |
| BR-M07-26 | Ràng buộc | Email gửi không thành công ở lại hàng đợi và được gửi lại ở lần quét kế tiếp, tối đa 3 lần gửi lại; sau đó dừng. | Email ban lỗi lúc quét 10:01 → gửi lại 10:02, 10:03, 10:04; nếu cả ba lần đều lỗi thì dừng, không gửi lúc 10:05. |
| BR-M07-27 | Suy diễn | Bấm một thông báo mà nội dung liên quan đã bị xóa, bị ẩn hoặc người dùng không còn quyền xem thì thông báo thành đã đọc và hiện "Nội dung không tồn tại"; thông báo vẫn được giữ. Chủ nội dung xem nội dung của mình đã bị xử lý theo M03, M04. | An nhận thông báo bình luận trong nhóm Private G, sau đó An rời G; An bấm thông báo → thông báo thành đã đọc, hiện "Nội dung không tồn tại". |
| BR-M07-28 | Kích hoạt | Mỗi tin nhắn mới hiện một popup nhỏ cho thành viên của cuộc trò chuyện đang mở ứng dụng, trừ khi thành viên đang xem đúng cuộc trò chuyện đó hoặc đã tắt thông báo theo BR-M07-08. | An đang ở trang chủ, Bình nhắn → popup hiện. An đang mở cuộc với Bình, Bình nhắn → không popup, tin hiện ngay trong cuộc. |


### 5.11 Dữ liệu nghiệp vụ

| Thực thể | Thuộc tính nguồn đã nêu | Quan hệ |
|---|---|---|
| Thông báo | Người nhận; loại sự kiện; nội dung liên quan để chuyển tới khi bấm; trạng thái đã đọc/chưa đọc; thời điểm tạo; thời điểm cập nhật cuối; người gây sự kiện (tên người upvote, "A và N người khác" khi gộp, những người khác nhau đã upvote và thời điểm mở cửa sổ 5 phút với thông báo upvote); đường dẫn khiếu nại khi sự kiện là xử lý khiếu nại được; lựa chọn Chấp nhận/Từ chối và lựa chọn đã chọn với đề xuất làm Mod | Thuộc một Người dùng (M01); trỏ tới bài viết (M03), bình luận (M04), nhóm (M11), báo cáo, cảnh cáo, ban (M08), khiếu nại (M09), đề xuất làm Mod (M10), badge, danh hiệu (M12) |
| Email thông báo (trong hàng đợi) | Người nhận (địa chỉ email của tài khoản); loại sự kiện; thời điểm vào hàng đợi; đã gửi hay chưa (Suy ra từ "quét rồi gửi"); số lần đã gửi lại | Thuộc một Người dùng (M01); sinh từ một sự kiện thuộc nhóm có email |
| Quan hệ theo dõi | Người theo dõi; đối tượng theo dõi (người dùng hoặc Topic); thời điểm bắt đầu theo dõi | Người theo dõi là Người dùng (M01); đối tượng là Người dùng (M01) hoặc Topic (M05) |
| Tắt thông báo cho bài | Người dùng; bài viết | Người dùng (M01), Bài viết (M03) |
| Tắt thông báo cuộc trò chuyện | Thành viên; cuộc trò chuyện | Người dùng (M01), Cuộc trò chuyện (M16) |
| Tắt thông báo toàn bộ Chat | Người dùng; bật hoặc tắt | Người dùng (M01) |

Thực thể của module khác mà M07 chỉ đọc: Người dùng, địa chỉ email, trạng thái tài khoản (M01); Bài viết (M03); Bình luận (M04);
Topic (M05); nhóm và thành viên nhóm, quyền xem nhóm Private (M11); cuộc trò chuyện, tin nhắn, mốc đã đọc tin nhắn, cuộc trò chuyện người dùng đang xem (M16).

**Ma trận CRUD:**

| Thực thể | Tạo | Đọc | Sửa | Xóa |
|---|---|---|---|---|
| Thông báo | FR-M07-02.01 | FR-M07-05.01, FR-M07-05.02, FR-M07-03.02 | FR-M07-06.01, FR-M07-06.03 (đã đọc); FR-M07-02.04 (gộp upvote); FR-M07-02.28 (lựa chọn đề xuất) | Không có (BR-M07-13, FR-M07-05.07) |
| Email thông báo (trong hàng đợi) | FR-M07-04.01 | FR-M07-04.02 | FR-M07-04.02 (đã gửi), FR-M07-04.09 (gửi lại) | Không có (nguồn không có việc xóa; DEC-129 chỉ xóa hẳn khi thật sự an toàn) |
| Quan hệ theo dõi | FR-M07-01.01 | M02 (số, danh sách theo dõi), M06 (bộ lọc), M14 (tab Following), M01 (thứ tự gợi ý nhắc tên) | M05 (gộp Topic, FR-M05-07.06) | M05 (xóa Topic, FR-M05-08.06), M01 (DELETED, FR-M01-12.08), FR-M07-01.08 (bỏ theo dõi) |
| Tắt thông báo cho bài | FR-M07-08.02 | FR-M07-02.08, FR-M07-08.01 | Không có (chỉ bật hoặc tắt) | FR-M07-08.03 (bật lại thông báo) |
| Tắt thông báo cuộc trò chuyện | FR-M07-09.01 | FR-M07-09.04, FR-M07-07.07 | Không có (chỉ bật hoặc tắt) | FR-M07-09.02 (bật lại thông báo) |
| Tắt thông báo toàn bộ Chat | FR-M07-09.03 | FR-M07-07.07 | FR-M07-09.03, FR-M07-09.04 | Không có (là một cài đặt bật/tắt) |

### 5.12 Chuyển trạng thái

#### Thông báo

| Từ | Sự kiện | Điều kiện | Sang | Yêu cầu |
|---|---|---|---|---|
| (bắt đầu) | Hệ thống tạo thông báo cho một sự kiện | Người nhận không tắt loại thông báo đó (BR-M07-07, BR-M07-08) | Chưa đọc | FR-M07-02.01, FR-M07-02.08 |
| Chưa đọc | Người nhận bấm vào thông báo | — | Đã đọc | FR-M07-06.01 |
| Chưa đọc | Người nhận bấm "Đánh dấu tất cả đã đọc" | — | Đã đọc | FR-M07-06.03 |
| Đã đọc | Thông báo upvote được gộp thêm một upvote | Trong cửa sổ 5 phút của nó (BR-M07-05) | Chưa đọc | FR-M07-02.04 |

Người dùng không tự chuyển thông báo về Chưa đọc; chỉ thông báo upvote được gộp thêm mới quay về Chưa đọc. Không có trạng thái kết thúc (BR-M07-13).

#### Thông báo của một bài với một người dùng

| Từ | Sự kiện | Điều kiện | Sang | Yêu cầu |
|---|---|---|---|---|
| (bắt đầu) | Người dùng xem một bài lần đầu | — | Đang nhận | FR-M07-08.01 |
| Đang nhận | Người dùng bật "Tắt thông báo cho bài này" | Đã đăng nhập | Đã tắt | FR-M07-08.02, FR-M07-08.05 |
| Đã tắt | Người dùng tắt "Tắt thông báo cho bài này" | — | Đang nhận | FR-M07-08.03 |

#### Thông báo của một cuộc trò chuyện với một thành viên

| Từ | Sự kiện | Điều kiện | Sang | Yêu cầu |
|---|---|---|---|---|
| (bắt đầu) | Người dùng trở thành thành viên cuộc trò chuyện (M16) | — | Đang nhận | FR-M07-09.02 |
| Đang nhận | Thành viên tắt thông báo cuộc trò chuyện | Là thành viên | Đã tắt | FR-M07-09.01, FR-M07-09.05 |
| Đã tắt | Thành viên bật lại thông báo cuộc trò chuyện | — | Đang nhận | FR-M07-09.02 |

"Đã tắt" chỉ làm tin nhắn không hiện popup (BR-M07-08). Cài đặt "Tắt thông báo cho toàn bộ Chat" cũng có hai trạng thái
Đang nhận / Đã tắt; khi nó Đã tắt thì mọi cuộc trò chuyện coi như Đã tắt, và khi nó trở lại Đang nhận thì mỗi cuộc theo
trạng thái riêng (FR-M07-09.03, FR-M07-09.04). Quan hệ theo dõi không có trạng thái (chỉ có hoặc không có).

### 5.13 Giao tiếp với module khác

| Hướng | Module | Nội dung ở mức nghiệp vụ | Yêu cầu |
|---|---|---|---|
| Dùng | M01 | Sự kiện mật khẩu đã đổi (đổi, đặt lại), đã liên kết Google, nhắc tên khi nội dung công khai, cảnh báo trước khi tự xóa; địa chỉ email và trạng thái tài khoản (BANNED, DEACTIVATED, DELETED); các thiết bị đang mở ứng dụng | FR-M07-02.01, FR-M07-02.07, FR-M07-04.01, FR-M07-04.06, FR-M07-05.09, FR-M07-03.02 |
| Dùng | M03 | Sự kiện bài được đăng, bị từ chối, bị ẩn, poll kết thúc; bài hiển thị công khai lần đầu, bài ẩn danh, tác giả bài (cho thông báo bài mới); bài viết để tắt thông báo; mở bài đã xử lý ở chế độ chỉ đọc; trang "Nội dung không tồn tại" | FR-M07-02.01, FR-M07-02.21, FR-M07-02.22, FR-M07-08.01, FR-M07-05.13 |
| Dùng | M04 | Sự kiện bình luận mới, trả lời, "Bình luận của bạn đã bị ẩn"; mở bình luận đã xử lý ở chế độ chỉ đọc | FR-M07-02.01, FR-M07-02.08 |
| Dùng | M05 | Topic để theo dõi; việc gộp, xóa Topic | FR-M07-01.01 |
| Dùng | M08 | Sự kiện kết quả báo cáo (kèm người nhận), cảnh cáo, ban, gỡ ban; đường dẫn khiếu nại | FR-M07-02.01, FR-M07-02.02, FR-M07-02.13, FR-M07-04.08 |
| Dùng | M09 | Sự kiện kết luận khiếu nại; thông báo gộp bài bị AI từ chối và cảnh cáo AI | FR-M07-02.01, FR-M07-02.13 |
| Dùng | M10 | Sự kiện đề xuất làm Mod, đề xuất lại | FR-M07-02.14, FR-M07-02.30 |
| Dùng | M11 | Sự kiện mời, gia nhập, duyệt, thăng cấp, kick trong nhóm; quyền xem nội dung nhóm Private | FR-M07-02.01, FR-M07-02.11 |
| Dùng | M12 | Sự kiện upvote, bỏ upvote bài và bình luận, badge, mốc điểm, danh hiệu tuần | FR-M07-02.01, FR-M07-02.03, FR-M07-02.19 |
| Dùng | M16 | Tin nhắn mới, thành viên cuộc trò chuyện, mốc đã đọc tin nhắn, cuộc trò chuyện người dùng đang xem, hộp thư Chat | FR-M07-07.02, FR-M07-07.03, FR-M07-07.05, FR-M07-07.06, FR-M07-09.05 |
| Cung cấp | M01 | Quan hệ theo dõi để xếp danh sách gợi ý nhắc tên | FR-M07-01.01 |
| Cung cấp | M02 | Quan hệ theo dõi và thời điểm bắt đầu theo dõi, để hiện số và danh sách người theo dõi, đang theo dõi | FR-M07-01.01 |
| Cung cấp | M03, M04 | Công tắc "Tắt thông báo cho bài này" trên mỗi bài; nó tắt thông báo bình luận mới, trả lời, upvote của bài | FR-M07-08.01, FR-M07-02.08 |
| Cung cấp | M06 | Quan hệ theo dõi (người dùng, Topic) cho bộ lọc chỉ nội dung đang theo dõi; không còn bài đang theo dõi (DEC-215) | FR-M07-01.01, FR-M07-01.02 |
| Cung cấp | M10 | Lựa chọn Chấp nhận, Từ chối của người được đề xuất làm Mod | FR-M07-02.15, FR-M07-02.16 |
| Cung cấp | M14 | Quan hệ theo dõi (người dùng, Topic) cho tab Following; không còn bài đang theo dõi (DEC-215) | FR-M07-01.01, FR-M07-01.02 |
| Cung cấp | Mọi module phát sinh sự kiện | Kênh thông báo trong ứng dụng và email theo danh sách sự kiện | FR-M07-02.01, FR-M07-04.01 |

### 5.14 AI hỗ trợ và hành vi khi tắt AI

Không áp dụng. M07 không gọi AI; việc AI ẩn bình luận, từ chối bài, ra cảnh cáo do M08, M13 quyết định, M07 chỉ gửi thông báo cho các sự kiện đó.

### 5.15 Yêu cầu HMI

Chưa có — chờ giai đoạn thiết kế.

### 5.16 Chuyển màn hình

Chưa có — chờ giai đoạn thiết kế.

## 6. Lịch sử sửa đổi

| Phiên bản | Ngày | Nội dung | Người sửa |
|---|---|---|---|
| 0.1 | 2026-10-20 | Tạo mới | Phạm Văn Đức |
| 0.2 | 2026-10-20 | Hoàn thành bước 1–6: 9 chức năng, 95 yêu cầu cấp dưới, 28 quy tắc; ghi DEC-215–DEC-220 (theo dõi người dùng và Topic, bỏ theo dõi bài viết, bỏ theo dõi, gộp upvote, chuông, người nhận, popup tin nhắn) | Phạm Văn Đức |
| 1.0 | 2026-10-21 | Bỏ các yêu cầu viết trùng với module sở hữu (FR-M07-01.05–.07, 02.05, 02.06, 02.12, 04.05, 04.07, 05.08; BR-M07-16, 17, 19), trỏ tới FR-M01, M04, M05, M09; chốt tài liệu | Phạm Văn Đức |

## Phụ lục A. Truy vết

| ID | Nguồn | Căn cứ | Ghi chú |
|---|---|---|---|
| FR-M07-01 | DM-4.5, QA-043, DEC-215, DEC-220, DEC-159, DEC-212, DEC-125, DEC-126 | Nói thẳng | — |
| FR-M07-01.01 | DM-4.5, QA-043, DEC-215, DEC-176 | Nói thẳng | — |
| FR-M07-01.02 | QA-043, DEC-215 | Nói thẳng | — |
| FR-M07-01.03 | DEC-126, DEC-215 | Suy ra | Mọi tương tác cần đăng nhập (DEC-126) ⇒ bỏ theo dõi (DEC-215) cũng cần đăng nhập |
| FR-M07-01.04 | DEC-065, DEC-215 | Nói thẳng | — |
| FR-M07-01.05 | DEC-141 | Nói thẳng | Đã bỏ ở phiên bản 0.2: hành vi thuộc M05, xem FR-M05-07.06 |
| FR-M07-01.06 | DEC-141 | Nói thẳng | Đã bỏ ở phiên bản 0.2: hành vi thuộc M05, xem FR-M05-08.06 |
| FR-M07-01.07 | DEC-156, DEC-159 | Nói thẳng | Đã bỏ ở phiên bản 0.2: hành vi thuộc M01, xem FR-M01-12.08 |
| FR-M07-01.08 | DEC-215 | Nói thẳng | — |
| FR-M07-01.09 | DEC-215 | Nói thẳng | — |
| FR-M07-01.10 | DEC-215 | Nói thẳng | — |
| FR-M07-01.11 | DEC-220 | Nói thẳng | — |
| FR-M07-01.12 | DEC-220 | Nói thẳng | — |
| FR-M07-01.13 | DEC-220, DEC-172 | Nói thẳng | — |
| FR-M07-02 | DEC-065, DEC-066, DEC-069, DM-8.1, QA-017, DEC-045, DEC-153, DEC-010, DEC-147, DEC-151, DEC-180, DEC-091, DEC-198, DEC-070, DM-5.3 | Nói thẳng | — |
| FR-M07-02.01 | DEC-065, QA-017, DM-8.1 | Nói thẳng | — |
| FR-M07-02.02 | DEC-065, DEC-074, DEC-192, DEC-076 | Suy ra | DEC-065 chỉ quy định loại sự kiện và kênh; ai nhận và khi nào sự kiện xảy ra do module phát sinh quy định (ví dụ DEC-074, DEC-192 của M08) ⇒ M07 dùng thông tin đó |
| FR-M07-02.03 | DEC-066, DEC-216 | Nói thẳng | — |
| FR-M07-02.04 | DEC-066, DEC-216 | Nói thẳng | — |
| FR-M07-02.05 | DEC-045, DEC-153 | Nói thẳng | Đã bỏ ở phiên bản 0.2: hành vi thuộc M01, xem FR-M01-14.10 |
| FR-M07-02.06 | DEC-153 | Nói thẳng | Đã bỏ ở phiên bản 0.2: hành vi thuộc M01, xem FR-M01-14.10 |
| FR-M07-02.07 | DEC-070, DEC-045 | Nói thẳng | — |
| FR-M07-02.08 | DEC-070, DEC-220 | Nói thẳng | — |
| FR-M07-02.09 | DEC-070 | Suy ra | DEC-070 chỉ liệt kê bình luận, trả lời, upvote bị tắt ⇒ loại khác (bài bị ẩn, kết quả báo cáo, nhắc tên) vẫn gửi |
| FR-M07-02.10 | DEC-067 | Nói thẳng | — |
| FR-M07-02.11 | DM-5.3 | Suy ra | "chỉ lọc thêm theo quyền xem nếu Group ở chế độ private" ⇒ người không xem được nội dung không nhận thông báo về nó |
| FR-M07-02.12 | DEC-198 | Nói thẳng | Đã bỏ ở phiên bản 0.2: hành vi thuộc M09, xem FR-M09-01.19 |
| FR-M07-02.13 | DEC-197, DEC-192, DEC-194 | Nói thẳng | — |
| FR-M07-02.14 | DEC-091 | Nói thẳng | — |
| FR-M07-02.15 | DEC-091 | Nói thẳng | — |
| FR-M07-02.16 | DEC-091 | Nói thẳng | — |
| FR-M07-02.17 | DEC-142, DEC-196, DEC-176 | Nói thẳng | — |
| FR-M07-02.18 | DEC-216 | Nói thẳng | — |
| FR-M07-02.19 | DEC-216 | Nói thẳng | — |
| FR-M07-02.20 | DEC-216 | Nói thẳng | — |
| FR-M07-02.21 | DEC-215 | Nói thẳng | — |
| FR-M07-02.22 | DEC-215 | Nói thẳng | — |
| FR-M07-02.23 | DEC-215 | Nói thẳng | — |
| FR-M07-02.24 | DEC-215 | Nói thẳng | — |
| FR-M07-02.25 | DEC-218 | Nói thẳng | — |
| FR-M07-02.26 | DEC-218 | Nói thẳng | — |
| FR-M07-02.27 | DEC-218 | Nói thẳng | — |
| FR-M07-02.28 | DEC-220 | Nói thẳng | — |
| FR-M07-02.29 | DEC-220 | Nói thẳng | — |
| FR-M07-02.30 | DEC-220 | Nói thẳng | — |
| FR-M07-03 | DEC-069, DEC-135, DEC-017 | Nói thẳng | — |
| FR-M07-03.01 | DEC-069 | Nói thẳng | — |
| FR-M07-03.02 | DEC-069, DEC-135, DEC-017 | Nói thẳng | — |
| FR-M07-03.03 | DEC-069 | Nói thẳng | — |
| FR-M07-03.04 | DEC-069 | Nói thẳng | — |
| FR-M07-04 | DEC-065, DEC-068, DEC-149, DEC-085, ISS-165 | Nói thẳng | — |
| FR-M07-04.01 | DEC-065, DEC-068, DEC-147, DEC-151 | Nói thẳng | — |
| FR-M07-04.02 | DEC-068 | Nói thẳng | — |
| FR-M07-04.03 | DEC-068 | Nói thẳng | — |
| FR-M07-04.04 | DEC-065, ISS-165 | Nói thẳng | — |
| FR-M07-04.05 | DEC-149 | Nói thẳng | Đã bỏ ở phiên bản 0.2: hành vi thuộc M01, xem FR-M01-12.05, BR-M01-32 |
| FR-M07-04.06 | DEC-065 | Nói thẳng | — |
| FR-M07-04.07 | DEC-149 | Suy ra | Đã bỏ ở phiên bản 0.2: hành vi thuộc M01, xem FR-M01-12.05, BR-M01-32 |
| FR-M07-04.08 | DEC-085, QA-019 | Nói thẳng | — |
| FR-M07-04.09 | DEC-220 | Nói thẳng | — |
| FR-M07-04.10 | DEC-220 | Nói thẳng | — |
| FR-M07-05 | DEC-067, DM-8.2, DEC-069 | Nói thẳng | — |
| FR-M07-05.01 | DEC-067, DEC-217 | Nói thẳng | — |
| FR-M07-05.02 | DEC-067, DEC-217 | Nói thẳng | — |
| FR-M07-05.03 | DM-8.2 | Nói thẳng | — |
| FR-M07-05.04 | DEC-127 | Nói thẳng | — |
| FR-M07-05.05 | DEC-065 | Suy ra | Mỗi thông báo gửi cho một người nhận; nguồn không có ai xem thông báo của người khác |
| FR-M07-05.06 | DEC-126 | Suy ra | Mọi tương tác cần đăng nhập (DEC-126) nên không có thông báo ⇒ trang Thông báo cần đăng nhập |
| FR-M07-05.07 | DEC-071, DEC-129 | Nói thẳng | — |
| FR-M07-05.08 | DEC-179, DEC-180, DEC-184 | Nói thẳng | Đã bỏ ở phiên bản 0.2: hành vi thuộc M03, M04, xem FR-M04-06.01 |
| FR-M07-05.09 | DEC-085 | Suy ra | Tài khoản BANNED chỉ thấy màn hình khóa, mọi chức năng khác bị chặn trừ khiếu nại (DEC-085) |
| FR-M07-05.10 | DEC-217 | Nói thẳng | — |
| FR-M07-05.11 | DEC-217 | Nói thẳng | — |
| FR-M07-05.12 | DEC-218 | Nói thẳng | — |
| FR-M07-05.13 | DEC-220, DEC-174 | Nói thẳng | — |
| FR-M07-06 | DEC-067, DM-8.2 | Nói thẳng | — |
| FR-M07-06.01 | DEC-067, DM-8.2 | Nói thẳng | — |
| FR-M07-06.02 | DEC-067 | Nói thẳng | — |
| FR-M07-06.03 | DEC-067, DM-8.2 | Nói thẳng | — |
| FR-M07-06.04 | DM-8.2 | Suy ra | Nguồn chỉ có chuyển chưa đọc → đã đọc, không có chuyển ngược |
| FR-M07-06.05 | DEC-067 | Suy ra | Tin nhắn không thuộc chuông, có số chưa đọc riêng (DEC-067) ⇒ nút ở chuông không đổi tin nhắn |
| FR-M07-06.06 | DEC-126 | Suy ra | Guest không có thông báo (xem FR-M07-05.06) |
| FR-M07-07 | DEC-067, DEC-065, DEC-219, DEC-220 | Nói thẳng | — |
| FR-M07-07.01 | DEC-067 | Nói thẳng | — |
| FR-M07-07.02 | DEC-067, DEC-219, DEC-220 | Nói thẳng | — |
| FR-M07-07.03 | DEC-067 | Nói thẳng | — |
| FR-M07-07.04 | DEC-067 | Suy ra | Guest không nhắn tin được (QA-011: MSG Không) ⇒ không có tin nhắn để báo |
| FR-M07-07.05 | DEC-219 | Nói thẳng | — |
| FR-M07-07.06 | DEC-219 | Nói thẳng | — |
| FR-M07-07.07 | DEC-219 | Nói thẳng | — |
| FR-M07-08 | DEC-070, DEC-220 | Nói thẳng | — |
| FR-M07-08.01 | DEC-070 | Nói thẳng | — |
| FR-M07-08.02 | DEC-070 | Nói thẳng | — |
| FR-M07-08.03 | DEC-070 | Nói thẳng | — |
| FR-M07-08.04 | DEC-070 | Suy ra | Công tắc là cài đặt của từng người, thay cho cài đặt cá nhân (DEC-070) ⇒ không ảnh hưởng người khác |
| FR-M07-08.05 | DEC-126 | Suy ra | Guest không có thông báo để tắt |
| FR-M07-09 | DEC-070, DEC-219 | Nói thẳng | — |
| FR-M07-09.01 | DEC-070, DEC-219 | Nói thẳng | — |
| FR-M07-09.02 | DEC-070, DEC-219 | Nói thẳng | — |
| FR-M07-09.03 | DEC-070, DEC-219 | Nói thẳng | — |
| FR-M07-09.04 | DEC-070, DEC-219 | Nói thẳng | — |
| FR-M07-09.05 | DEC-070 | Suy ra | "mute individual DM/Group chat threads" của chính người dùng ⇒ chỉ thành viên |
| FR-M07-09.06 | DEC-126 | Suy ra | Guest không nhắn tin được (QA-011) |
| FR-M07-09.07 | DEC-219 | Nói thẳng | — |
| BR-M07-01 | DEC-065, DEC-147, DEC-151, DEC-180, DEC-091, DEC-215, DM-8.1 | Suy ra | DEC-065 ghi "Appeal — post/comment/warn-related"; bình luận không có khiếu nại (DEC-180) nên chỉ còn bài viết, cảnh cáo. "Đề xuất làm Mod" thêm từ DEC-091, "bài mới của người đang theo dõi" từ DEC-215 |
| BR-M07-02 | DEC-065, DEC-067, ISS-165, DEC-219, DEC-220 | Nói thẳng | — |
| BR-M07-03 | DEC-065, DEC-147, DEC-151, ISS-165 | Nói thẳng | — |
| BR-M07-04 | DEC-065, DEC-149 | Nói thẳng | — |
| BR-M07-05 | DEC-066, DEC-216 | Nói thẳng | — |
| BR-M07-06 | DEC-045, DEC-153, DEC-070 | Nói thẳng | — |
| BR-M07-07 | DEC-070, DEC-220 | Suy ra | DEC-070 chỉ liệt kê bình luận, trả lời, upvote bị tắt ⇒ các thông báo khác về bài vẫn gửi; phạm vi upvote theo DEC-220 |
| BR-M07-08 | DEC-070, DEC-219 | Nói thẳng | — |
| BR-M07-09 | DEC-069, DEC-135 | Nói thẳng | — |
| BR-M07-10 | DEC-017 | Nói thẳng | — |
| BR-M07-11 | DEC-068 | Nói thẳng | — |
| BR-M07-12 | DEC-067, DEC-217 | Nói thẳng | — |
| BR-M07-13 | DEC-071, DEC-129 | Nói thẳng | — |
| BR-M07-14 | DEC-067, DM-8.2 | Nói thẳng | — |
| BR-M07-15 | QA-043, DM-4.5, DEC-215, DEC-220, DEC-126 | Nói thẳng | — |
| BR-M07-16 | DEC-141 | Nói thẳng | Đã bỏ ở phiên bản 0.2: quy tắc thuộc M05, xem FR-M05-07.06, FR-M05-08.06 |
| BR-M07-17 | DEC-156, DEC-159, DEC-215 | Nói thẳng | Đã bỏ ở phiên bản 0.2: quy tắc thuộc M01, xem BR-M01-47 |
| BR-M07-18 | DM-5.3 | Suy ra | "chỉ lọc thêm theo quyền xem nếu Group ở chế độ private" ⇒ người không xem được nội dung không nhận thông báo về nó |
| BR-M07-19 | DEC-198 | Nói thẳng | Đã bỏ ở phiên bản 0.2: quy tắc thuộc M09, xem FR-M09-01.19 |
| BR-M07-20 | DEC-091, DEC-220 | Nói thẳng | — |
| BR-M07-21 | DEC-142, DEC-196, DEC-176 | Nói thẳng | — |
| BR-M07-22 | DEC-127 | Nói thẳng | — |
| BR-M07-23 | DEC-215, DM-5.3 | Nói thẳng | — |
| BR-M07-24 | DEC-218, DEC-149, DEC-156 | Nói thẳng | — |
| BR-M07-25 | DEC-215 | Nói thẳng | — |
| BR-M07-26 | DEC-220 | Nói thẳng | — |
| BR-M07-27 | DEC-220, DEC-174, DEC-071 | Nói thẳng | — |
| BR-M07-28 | DEC-219 | Nói thẳng | — |

## Phụ lục B. Câu hỏi, giả định và TBD

### B.1 Câu hỏi đã hỏi

| Mã | Loại | Câu hỏi | Trả lời | Ghi vào register |
|---|---|---|---|---|
| Q-01 | Mâu thuẫn | QA-043 cho theo dõi User, Topic, Post và nhận thông báo khi người đang theo dõi đăng bài, khi Topic có bài mới, khi bài đang theo dõi có cập nhật/bình luận; DM-8.1 cũng có các sự kiện này. DEC-065 ("full event list", Phase 5) không có các sự kiện đó, và QA-127 nói không có theo dõi bài kiểu đăng ký nhận thông báo; trong khi DEC-159, DEC-212 vẫn coi bài viết là đối tượng theo dõi. Theo dõi có sinh thông báo nội dung mới không, cho loại đối tượng nào? | Theo dõi người dùng: có thông báo khi người đó có bài mới (công khai lần đầu; không với bài ẩn danh, bài nhóm Private với người ngoài nhóm, bài bị từ chối, sửa, khôi phục). Theo dõi Topic: không có thông báo. Bỏ theo dõi bài viết. | ISS-345, QA-405, DEC-215 |
| Q-02 | Cần cân nhắc | Nguồn chỉ có hành động theo dõi (DM-4.5, QA-043), không nhắc tới bỏ theo dõi. Người dùng có bỏ theo dõi được người dùng, Topic, bài viết không (mở rộng phạm vi)? | Cho bỏ theo dõi người dùng, Topic; "có người theo dõi mới" chỉ một lần mỗi cặp. Mở rộng phạm vi được chấp nhận (CC-01). | ISS-346, QA-406, DEC-215 |
| Q-03 | Mơ hồ | DEC-066: "Batch upvotes (post + comment) within a 5-minute rolling window into one notification ("A và N người khác đã upvote...")". Cửa sổ tính từ upvote nào và có trượt khi có upvote mới không; gộp theo từng bài/bình luận hay chung; "A" là người nào, N đếm gì; bỏ upvote trong cửa sổ thì sao? | W2: báo ngay lượt đầu; cửa sổ 5 phút từ lượt đầu; gộp theo từng bài, từng bình luận; A là người mới nhất, N là số người khác nhau còn lại; bỏ upvote không đổi thông báo. | ISS-347, QA-407, DEC-216 |
| Q-04 | Mơ hồ | DEC-067: chuông là "dropdown (5-10 most recent)". Chuông hiện đúng bao nhiêu thông báo, xếp theo thứ tự nào, chuông có số chưa đọc không, trang Thông báo tải thế nào? | Chuông 10 thông báo, mới nhất trước theo lần cập nhật cuối, có số chưa đọc riêng; mở chuông không đánh dấu đã đọc; trang Thông báo tải 20 mỗi lần. | ISS-348, QA-408, DEC-217 |
| Q-05 | Mơ hồ | DEC-070: "Tắt thông báo cho toàn bộ Chat … coexists with per-conversation mute for finer override". Khi đã tắt toàn bộ Chat, có bật riêng được một cuộc trò chuyện không; tin nhắn của cuộc đã tắt còn tăng số chưa đọc ở biểu tượng Tin nhắn không? | A: tắt toàn bộ là tắt hết; bỏ tắt toàn bộ thì cuộc đã tắt riêng vẫn tắt. Tắt chỉ ẩn popup tin nhắn; số trên biểu tượng Tin nhắn vẫn tính đủ. Popup không hiện khi đang xem đúng cuộc đó. | ISS-350, QA-410, DEC-219 |
| Q-06 | Thiếu chi tiết | FR-M07-01: người dùng có theo dõi được chính mình không; có theo dõi được tài khoản DEACTIVATED, BANNED không (DEC-172 không hiện các tài khoản này trong danh sách theo dõi)? Đề xuất: không theo dõi chính mình; không theo dõi tài khoản không ACTIVE, theo cách DEC-172 ẩn chúng. | Theo đề xuất (X1). | ISS-351, QA-411, DEC-220 |
| Q-07 | Thiếu chi tiết | FR-M07-02.14–.16 (DEC-091): sau khi đã chọn Chấp nhận hoặc Từ chối, thông báo đề xuất còn cho chọn lại không; đề xuất chưa trả lời có hết hạn không; Admin đề xuất lại thì đề xuất cũ ra sao? Đề xuất: chọn một lần, sau đó thông báo hiện kết quả đã chọn; đề xuất không hết hạn; đề xuất mới là thông báo mới. | Theo đề xuất (X2). | ISS-351, QA-411, DEC-220 |
| Q-08 | Thiếu chi tiết | FR-M07-02: có tạo thông báo cho người nhận DEACTIVATED, BANNED, DELETED không; người gây sự kiện cũng là người nhận (bình luận vào bài của mình, trả lời bình luận của mình, tự nhắc tên mình) có tạo thông báo không; tên người gây sự kiện hiện thế nào khi tài khoản đó DEACTIVATED, DELETED? Đề xuất: tạo cho DEACTIVATED, BANNED (thấy khi trở lại ACTIVE), không tạo cho DELETED; không báo cho chính người gây sự kiện; tên hiện như DEC-149, DEC-156 ("Tài khoản tạm thời vô hiệu hoá", "[Người dùng đã xóa]"). | A: không báo cho chính người gây sự kiện; vẫn tạo cho người nhận BANNED, DEACTIVATED; không tạo cho DELETED; tên người gây sự kiện theo DEC-149, DEC-156. | ISS-349, QA-409, DEC-218 |
| Q-09 | Thiếu chi tiết | FR-M07-04 (DEC-068): gửi email không thành công thì có gửi lại ở các lần quét sau không, tối đa mấy lần? Đề xuất: email lỗi ở lại hàng đợi và được gửi lại ở lần quét kế tiếp, tối đa 3 lần, rồi dừng. | Theo đề xuất (X3). | ISS-351, QA-411, DEC-220 |
| Q-10 | Thiếu chi tiết | FR-M07-05, FR-M07-06: bấm một thông báo khi nội dung liên quan đã bị xóa, ẩn, hoặc người dùng không còn quyền xem (ví dụ đã rời nhóm Private), ngoài các trường hợp chủ nội dung xem chỉ đọc (DEC-179, DEC-180, DEC-184)? Đề xuất: thông báo vẫn giữ (DEC-071), bấm vào thì thành đã đọc và hiện trang "nội dung không tồn tại" như M03 đang dùng. | Theo đề xuất (X4). | ISS-351, QA-411, DEC-220 |
| Q-11 | Thiếu chi tiết | FR-M07-07 (DEC-067 "own unread badge"): số chưa đọc trên biểu tượng Tin nhắn đếm số tin nhắn chưa đọc hay số cuộc trò chuyện có tin chưa đọc? Đề xuất: số cuộc trò chuyện có tin chưa đọc, tính theo mốc đã đọc của M16 (QA-209). | Theo đề xuất (X5): số cuộc trò chuyện có tin chưa đọc. | ISS-351, QA-411, DEC-220 |
| Q-12 | Thiếu chi tiết | FR-M07-08 (DEC-070 "toggle on each post"): công tắc hiện trên mọi bài hay chỉ bài người dùng có liên quan (bài của mình, bài mình đã bình luận); "upvote" bị tắt có gồm upvote bình luận của người dùng trong bài đó? Đề xuất: hiện trên mọi bài cho người đã đăng nhập; tắt cả upvote bài và upvote bình luận phát sinh trong bài. | Theo đề xuất (X6). | ISS-351, QA-411, DEC-220 |

### B.2 TBD

Không có TBD sinh từ OPEN: không mục OPEN nào (OPEN-001 … OPEN-012) chạm hành vi của M07.

### B.3 Cần cân nhắc (ngoài dữ liệu hiện có)

| Mã | Điểm cần cân nhắc | Vì sao cần | Quyết định |
|---|---|---|---|
| CC-01 | Mở rộng phạm vi: bỏ theo dõi người dùng, Topic (Q-02). | Nguồn chỉ có hành động theo dõi; không bỏ được thì một lượt theo dõi là vĩnh viễn và thông báo bài mới của người đang theo dõi không dừng được. | Chấp nhận: cho bỏ theo dõi (DEC-215) |

## Phụ lục C. Sổ nguồn

**Owner keywords:** notification, notifications, notify, notified, notifies, thông báo, bell, chuông, mark as read, mark all as read, đánh dấu đã đọc, đã đọc, chưa đọc, read/unread, unread, email_queue, email queue, mute, muted, tắt thông báo, batched, batching, in-app, SSE, WebSocket, push, digest, retention, Message icon, follow, follows, followed, follower, followers, following, unfollow, theo dõi, bỏ theo dõi, warning email, invite, kick, accepted answer
**Dependency keywords:** upvote, star, comment, bình luận, reply, @mention, mention, post, bài viết, badge, milestone, weekly top, chat, DM, group, nhóm, report, warning, ban, unban, appeal, khiếu nại, password, mật khẩu, DEACTIVATED, Google, poll, accepted answer, timezone, AI_ENABLED, email, cron, topic, promote
**Mục draft của module:** DM-8.1, DM-8.2
**Loại khỏi bảng nguồn (khớp nhầm):** DEC-015 ("muted" là kiểu chữ trong danh sách nhắc tên, M01); DEC-064, ISS-337, QA-397 (câu nhắc khi tải đủ 120 kết quả, M06); DEC-090 ("notify" khi đổi hằng số qua triển khai, M10); DEC-108, DEC-138, DEC-154 ("retention" là giữ bài trong feed nhóm, lưu giữ dữ liệu cá nhân); DEC-134, QA-256 (mô tả công nghệ frontend, SSR); DEC-104, DEC-139, DEC-205, DEC-208, QA-006, QA-047 ("follow" là từ thường); DG-5, DG-7, DM-13, DM-x04, DM-6.4, QA-046 (kênh thời gian thực của Nhắn tin, M16); DM-6.2, ISS-155, QA-209, QA-210, QA-211, QA-212 (đã đọc của tin nhắn, M16); DM-4.1, DM-11.5, QA-192 ("theo dõi" nghĩa là đo đếm); QA-031, QA-061, QA-249, QA-389, QA-390, QA-393 ("thông báo" là thông điệp trên màn hình); MR-A03 ("batched" là cách tính M15); ISS-162, QA-220, ISS-164, QA-222, MR-M16 (nhắn tin không cần theo dõi, M16); ISS-166, ISS-177, QA-230, QA-237, ISS-342 (tab, banner feed M14 và bộ lọc M06, không quy định việc theo dõi); QA-037, DM-11, DM-9.1, DM-10.2, DG-8, DM-x03, GL:Accepted Answer, DM-4.2.1 (Accepted Answer ở module khác, không nói tới thông báo; DEC-169 đủ); ISS-134, QA-183 (nội dung của thành viên bị kick, M11)

### C.1 Bảng nguồn

| Nguồn | Nhãn | Trạng thái | Dùng ở | Ghi chú |
|---|---|---|---|---|
| DEC-065 | Sở hữu | Sửa một phần bởi DEC-147, DEC-151, DEC-180, DEC-091, DEC-198, DEC-215, DEC-218 | FR-M07-01.04, FR-M07-02, FR-M07-02.01, FR-M07-02.02, FR-M07-04, FR-M07-04.01, FR-M07-04.04, FR-M07-04.06, FR-M07-05.05, FR-M07-07, BR-M07-01, BR-M07-02, BR-M07-03, BR-M07-04 | Nhóm A. Danh sách sự kiện và kênh (trong ứng dụng, email); không có email tổng hợp. DEC-091, DEC-198 sửa không có dấu (xem C.2) |
| DEC-066 | Sở hữu | Sửa một phần bởi DEC-216 | FR-M07-02, FR-M07-02.03, FR-M07-02.04, BR-M07-05 | Nhóm A. Gộp thông báo upvote trong cửa sổ 5 phút |
| DEC-067 | Sở hữu | Sửa một phần bởi DEC-217, DEC-219, DEC-220 | FR-M07-02.10, FR-M07-05, FR-M07-05.01, FR-M07-05.02, FR-M07-06, FR-M07-06.01, FR-M07-06.02, FR-M07-06.03, FR-M07-06.05, FR-M07-07, FR-M07-07.01, FR-M07-07.02, FR-M07-07.03, FR-M07-07.04, BR-M07-02, BR-M07-12, BR-M07-14 | Nhóm A. Chuông: danh sách gần nhất + trang /notifications; biểu tượng Tin nhắn riêng; đánh dấu đã đọc |
| DEC-068 | Sở hữu | Sửa một phần bởi DEC-220 | FR-M07-04, FR-M07-04.01, FR-M07-04.02, FR-M07-04.03, BR-M07-11 | Nhóm A. Email gửi bất đồng bộ qua hàng đợi, quét mỗi phút |
| DEC-069 | Sở hữu | Sửa một phần bởi DEC-135 | FR-M07-02, FR-M07-03, FR-M07-03.01, FR-M07-03.02, FR-M07-03.03, FR-M07-03.04, FR-M07-05, BR-M07-09 | Nhóm A. Thông báo lưu là nguồn chính; đẩy tới người đang online theo kiểu cố gắng. Chỉ đổi kênh đẩy |
| DEC-070 | Sở hữu | Sửa một phần bởi DEC-219, DEC-220 | FR-M07-02, FR-M07-02.07, FR-M07-02.08, FR-M07-02.09, FR-M07-08, FR-M07-08.01, FR-M07-08.02, FR-M07-08.03, FR-M07-08.04, FR-M07-09, FR-M07-09.01, FR-M07-09.02, FR-M07-09.03, FR-M07-09.04, FR-M07-09.05, BR-M07-06, BR-M07-07, BR-M07-08 | Nhóm A. Không có trang cài đặt theo loại; tắt theo bài, theo cuộc trò chuyện, toàn bộ Chat |
| DEC-071 | Sở hữu | Hiện hành | FR-M07-05.07, BR-M07-13, BR-M07-27 | Nhóm A. Không tự xóa thông báo |
| DM-8.1 | Sở hữu | Sửa một phần bởi DEC-065, DEC-169, DEC-215 | FR-M07-02, FR-M07-02.01, BR-M07-01 | Nhóm A. Draft: danh sách sự kiện thông báo. Sự kiện nội dung mới từ đối tượng theo dõi: |
| DM-8.2 | Sở hữu | Hiện hành | FR-M07-05, FR-M07-05.03, FR-M07-06, FR-M07-06.01, FR-M07-06.03, FR-M07-06.04, BR-M07-14 | Nhóm A. Draft: đã đọc/chưa đọc, đánh dấu đã đọc, đánh dấu tất cả |
| ISS-098 | Sở hữu | Trùng với DEC-065 | — | Nhóm A. Câu hỏi đã có DEC-065, DEC-066 trả lời |
| ISS-099 | Sở hữu | Trùng với DEC-067 | — | Nhóm A. Câu hỏi đã có DEC-067 trả lời |
| ISS-100 | Sở hữu | Trùng với DEC-068 | — | Nhóm A. Câu hỏi đã có DEC-068 trả lời |
| ISS-101 | Sở hữu | Trùng với DEC-070 | — | Nhóm A. Câu hỏi đã có DEC-070 trả lời |
| ISS-102 | Sở hữu | Trùng với DEC-069 | — | Nhóm A. Câu hỏi đã có DEC-069 trả lời |
| ISS-103 | Sở hữu | Trùng với DEC-071 | — | Nhóm A. Câu hỏi đã có DEC-071 trả lời |
| QA-123 | Sở hữu | Trùng với DEC-065 | — | Nhóm A. Câu trả lời của DEC-065 |
| QA-124 | Sở hữu | Trùng với DEC-065 | — | Nhóm A. Sự kiện có email |
| QA-125 | Sở hữu | Trùng với DEC-065 | — | Nhóm A. Không có email tổng hợp |
| QA-126 | Sở hữu | Trùng với DEC-066 | — | Nhóm A. Upvote báo theo lượt, gộp trong 5 phút |
| QA-127 | Sở hữu | Trùng với DEC-215 | — | Nhóm A. Không có theo dõi bài kiểu đăng ký nhận tin; bookmark chỉ để lưu. |
| QA-128 | Sở hữu | Trùng với DEC-067 | — | Nhóm A. Chuông: danh sách + trang riêng |
| QA-129 | Sở hữu | Trùng với DEC-067 | — | Nhóm A. Thông báo chat ở biểu tượng Tin nhắn riêng |
| QA-130 | Sở hữu | Trùng với DEC-068 | — | Nhóm A. Email bất đồng bộ, mỗi phút |
| QA-131 | Sở hữu | Trùng với DEC-069 | — | Nhóm A. Lưu + đẩy theo kiểu cố gắng; người dùng tải lại khi mở trang |
| QA-132 | Sở hữu | Trùng với DEC-070 | — | Nhóm A. Không có cài đặt chi tiết; thay bằng tắt theo bài và chat |
| QA-133 | Sở hữu | Trùng với DEC-071 | — | Nhóm A. Giữ thông báo vô thời hạn |
| MR-M07 | Sở hữu | Sửa một phần bởi DEC-135 | Không áp dụng: tóm tắt module, nội dung đã có ở DEC-065–DEC-071 | Nhóm A. Dòng module M07 |
| DEC-215 | Sở hữu | Hiện hành | FR-M07-01, FR-M07-01.01, FR-M07-01.02, FR-M07-01.03, FR-M07-01.04, FR-M07-01.08, FR-M07-01.09, FR-M07-01.10, FR-M07-02.21, FR-M07-02.22, FR-M07-02.23, FR-M07-02.24, BR-M07-01, BR-M07-15, BR-M07-23, BR-M07-25 | Nhóm A. Đối tượng theo dõi là người dùng, Topic; thông báo bài mới của người đang theo dõi; bỏ theo dõi (mở rộng phạm vi) |
| DEC-216 | Sở hữu | Hiện hành | FR-M07-02.03, FR-M07-02.04, FR-M07-02.18, FR-M07-02.19, FR-M07-02.20, BR-M07-05 | Nhóm A. Chi tiết gộp upvote |
| DEC-217 | Sở hữu | Hiện hành | FR-M07-05.01, FR-M07-05.02, FR-M07-05.10, FR-M07-05.11, BR-M07-12 | Nhóm A. Chuông và trang Thông báo |
| DEC-218 | Sở hữu | Hiện hành | FR-M07-02.25, FR-M07-02.26, FR-M07-02.27, FR-M07-05.12, BR-M07-24 | Nhóm A. Người nhận, người gây sự kiện, tên hiển thị |
| DEC-219 | Sở hữu | Hiện hành | FR-M07-07, FR-M07-07.02, FR-M07-07.05, FR-M07-07.06, FR-M07-07.07, FR-M07-09, FR-M07-09.01, FR-M07-09.02, FR-M07-09.03, FR-M07-09.04, FR-M07-09.07, BR-M07-02, BR-M07-08, BR-M07-28 | Nhóm A. Popup tin nhắn; tắt thông báo Chat chỉ ẩn popup |
| DEC-220 | Sở hữu | Hiện hành | FR-M07-01, FR-M07-01.11, FR-M07-01.12, FR-M07-01.13, FR-M07-02.08, FR-M07-02.28, FR-M07-02.29, FR-M07-02.30, FR-M07-04.09, FR-M07-04.10, FR-M07-05.13, FR-M07-07, FR-M07-07.02, FR-M07-08, BR-M07-02, BR-M07-07, BR-M07-15, BR-M07-20, BR-M07-26, BR-M07-27 | Nhóm A. Danh sách xác nhận X1–X6 |
| ISS-345 | Sở hữu | Trùng với DEC-215 | — | Nhóm A. Câu hỏi của DEC-215 |
| ISS-346 | Sở hữu | Trùng với DEC-215 | — | Nhóm A. Câu hỏi của DEC-215 |
| ISS-347 | Sở hữu | Trùng với DEC-216 | — | Nhóm A. Câu hỏi của DEC-216 |
| ISS-348 | Sở hữu | Trùng với DEC-217 | — | Nhóm A. Câu hỏi của DEC-217 |
| ISS-349 | Sở hữu | Trùng với DEC-218 | — | Nhóm A. Câu hỏi của DEC-218 |
| ISS-350 | Sở hữu | Trùng với DEC-219 | — | Nhóm A. Câu hỏi của DEC-219 |
| ISS-351 | Sở hữu | Trùng với DEC-220 | — | Nhóm A. Câu hỏi của DEC-220 |
| QA-405 | Sở hữu | Trùng với DEC-215 | — | Nhóm A. Câu trả lời của DEC-215 |
| QA-406 | Sở hữu | Trùng với DEC-215 | — | Nhóm A. Câu trả lời của DEC-215 |
| QA-407 | Sở hữu | Trùng với DEC-216 | — | Nhóm A. Câu trả lời của DEC-216 |
| QA-408 | Sở hữu | Trùng với DEC-217 | — | Nhóm A. Câu trả lời của DEC-217 |
| QA-409 | Sở hữu | Trùng với DEC-218 | — | Nhóm A. Câu trả lời của DEC-218 |
| QA-410 | Sở hữu | Trùng với DEC-219 | — | Nhóm A. Câu trả lời của DEC-219 |
| QA-411 | Sở hữu | Trùng với DEC-220 | — | Nhóm A. Câu trả lời của DEC-220 |
| DEC-174 | Phụ thuộc | Hiện hành | FR-M07-05.13, BR-M07-27 | Nhóm C. M02: bookmark tới bài không còn xem được hiện "Nội dung không tồn tại"; DEC-220 dùng cùng cách |
| DEC-010 | Sở hữu | Sửa một phần bởi DEC-147 | FR-M07-02 | Nhóm B. Thông báo sau khi tự liên kết Google |
| DEC-016 | Nhắc tới | Sửa một phần bởi DEC-151 | Chuyển M01 | Nhóm B. M01: luồng email xác minh, quên/đổi mật khẩu; phần thông báo do DEC-151 quy định |
| DEC-017 | Phụ thuộc | Sửa một phần bởi DEC-151 | FR-M07-03, FR-M07-03.02, BR-M07-10 | Nhóm B. M01: mỗi thiết bị một kết nối nhận đẩy; nhiều thiết bị cùng lúc. Sửa hạn làm mới phiên, không chạm M07 |
| DEC-020 | Nhắc tới | Sửa một phần bởi DEC-153 | Chuyển M01 | Nhóm B. M01: thứ tự gợi ý nhắc tên dùng quan hệ theo dõi. DEC-214 (ngoài bảng nguồn) cũng sửa |
| DEC-025 | Nhắc tới | Sửa một phần bởi DEC-171, DEC-172 | Chuyển M02 | Nhóm B. M02: hiện số và danh sách người theo dõi |
| DEC-045 | Sở hữu | Sửa một phần bởi DEC-153 | FR-M07-02, FR-M07-02.07, BR-M07-06 | Nhóm B. Nhắc tên luôn sinh thông báo, ở bài hay bình luận |
| DEC-056 | Nhắc tới | Sửa một phần bởi DEC-212 | Chuyển M06 | Nhóm B. M06: bộ lọc chỉ nội dung đang theo dõi. DEC-211 (ngoài bảng nguồn) cũng làm rõ |
| DEC-074 | Phụ thuộc | Sửa một phần bởi DEC-192 | FR-M07-02.02 | Nhóm B. M08: nội dung thông báo kết quả báo cáo tách theo người nhận |
| DEC-076 | Phụ thuộc | Hiện hành | FR-M07-02.02 | Nhóm B. M08: mọi người báo cáo trong vụ nhận cùng kết quả |
| DEC-085 | Phụ thuộc | Sửa một phần bởi DEC-197 | FR-M07-04, FR-M07-04.08, FR-M07-05.09 | Nhóm B. M09: email ban kèm đường dẫn khiếu nại |
| DEC-091 | Phụ thuộc | Sửa một phần bởi DEC-220 | FR-M07-02, FR-M07-02.14, FR-M07-02.15, FR-M07-02.16, BR-M07-01, BR-M07-20 | Nhóm B. M10: người dùng nhận thông báo "Đề xuất làm Mod" có Chấp nhận/Từ chối |
| DEC-102 | Phụ thuộc | Hiện hành | Chuyển M11 | Nhóm B. M11: ai được kick, promote trong nhóm (nguồn sự kiện nhóm) |
| DEC-110 | Phụ thuộc | Hiện hành | Chuyển M11 | Nhóm B. M11: mời vào nhóm Private qua lời mời/link; không có lời mời có Chấp nhận/Từ chối. DEC-210 (ngoài bảng nguồn) làm rõ phần tìm kiếm, không chạm M07 |
| DEC-121 | Phụ thuộc | Hiện hành | Chuyển M12 | Nhóm B. M12: thông báo trao danh hiệu tuần, trễ tối đa 60 phút |
| DEC-125 | Nhắc tới | Sửa một phần bởi DEC-215 | FR-M07-01 | Nhóm B. M14: tab Following dùng đối tượng theo dõi của M07 |
| DEC-126 | Phụ thuộc | Hiện hành | FR-M07-01, FR-M07-01.03, FR-M07-05.06, FR-M07-06.06, FR-M07-08.05, FR-M07-09.06, BR-M07-15 | Nhóm B. M14: theo dõi cần đăng nhập |
| DEC-129 | Phụ thuộc | Sửa một phần bởi DEC-156 | FR-M07-05.07, BR-M07-13 | Nhóm B. Dùng chung: nguyên tắc giữ dữ liệu, nhất quán DEC-071 |
| DEC-135 | Sở hữu | Hiện hành | FR-M07-03, FR-M07-03.02, BR-M07-09 | Nhóm B. Kênh đẩy thời gian thực cho thông báo (thay WebSocket) |
| DEC-137 | Nhắc tới | Hiện hành | Không áp dụng: công nghệ đã chốt, không đưa vào FR | Nhóm B. Công nghệ đã chốt (kênh đẩy, email) |
| DEC-141 | Phụ thuộc | Hiện hành | Chuyển M05 | Nhóm B. M05: gộp Topic chuyển người theo dõi sang Topic đích; xóa Topic bỏ lượt theo dõi |
| DEC-142 | Phụ thuộc | Hiện hành | FR-M07-02.17, BR-M07-21 | Nhóm B. M05: Mod/Admin đổi Topic, Tag thì tác giả không được thông báo |
| DEC-147 | Sở hữu | Hiện hành | FR-M07-02, FR-M07-04.01, BR-M07-01, BR-M07-03 | Nhóm B. Thêm sự kiện "Đã liên kết Google" (trong ứng dụng + email) |
| DEC-149 | Phụ thuộc | Hiện hành | FR-M07-04, BR-M07-04, BR-M07-24 | Nhóm B. M01: một email cảnh báo 24 giờ trước khi tự xóa |
| DEC-151 | Sở hữu | Hiện hành | FR-M07-02, FR-M07-04.01, BR-M07-01, BR-M07-03 | Nhóm B. Đặt lại mật khẩu cũng gửi "mật khẩu đã đổi" (trong ứng dụng + email); chỉ ý thứ ba |
| DEC-153 | Sở hữu | Hiện hành | FR-M07-02, BR-M07-06 | Nhóm B. Thông báo nhắc tên gửi khi nội dung công khai; sửa chỉ báo người mới được nhắc; chỉ ý thứ năm |
| DEC-156 | Phụ thuộc | Sửa một phần bởi DEC-159 | BR-M07-24 | Nhóm B. M01: khi DELETED xóa quan hệ theo dõi hai chiều |
| DEC-159 | Phụ thuộc | Sửa một phần bởi DEC-215 | FR-M07-01 | Nhóm B. M01: khi DELETED xóa theo dõi người dùng, Topic, bài; giảm số người theo dõi |
| DEC-169 | Phụ thuộc | Hiện hành | Không áp dụng: MS1 không có Accepted Answer, sự kiện tương ứng ghi ở Ngoài phạm vi (mục 1.2) | Nhóm B. M03: không có Accepted Answer ở MS1 (bỏ sự kiện tương ứng của draft) |
| DEC-171 | Nhắc tới | Hiện hành | Chuyển M02 | Nhóm B. M02: Guest phải đăng nhập mới xem danh sách theo dõi |
| DEC-172 | Nhắc tới | Hiện hành | FR-M07-01.13 | Nhóm B. M02: danh sách theo dõi chỉ người dùng, không hiện DEACTIVATED, BANNED |
| DEC-176 | Sở hữu | Hiện hành | FR-M07-01.01, FR-M07-02.17, BR-M07-21 | Nhóm B. Không có thông báo nhắc cập nhật Lớp/Khối ở MS1; chỉ ý thứ nhất, các ý khác thuộc M02 |
| DEC-179 | Phụ thuộc | Hiện hành | Chuyển M04 | Nhóm B. M04: chủ nội dung mở bình luận đã xử lý từ thông báo kết quả báo cáo |
| DEC-180 | Sở hữu | Hiện hành | FR-M07-02, BR-M07-01 | Nhóm B. Thêm sự kiện "Bình luận của bạn đã bị ẩn" (chỉ trong ứng dụng) |
| DEC-184 | Phụ thuộc | Hiện hành | Chuyển M03 | Nhóm B. M03: chủ bài mở bài đã xóa hẳn từ thông báo kết quả báo cáo |
| DEC-192 | Phụ thuộc | Sửa một phần bởi DEC-197 | FR-M07-02.02, FR-M07-02.13 | Nhóm B. M08: ai nhận thông báo khi kết luận vụ; vụ do AI tạo không báo người báo cáo; đường dẫn khiếu nại |
| DEC-194 | Phụ thuộc | Hiện hành | FR-M07-02.13 | Nhóm B. M08: Owner nhóm nhận thông báo kết quả, không kèm đường dẫn khiếu nại |
| DEC-196 | Phụ thuộc | Hiện hành | FR-M07-02.17, BR-M07-21 | Nhóm B. M09: không có thông báo chuyển khiếu nại lên ADMIN |
| DEC-197 | Phụ thuộc | Hiện hành | FR-M07-02.13 | Nhóm B. M09: mọi thông báo về xử lý khiếu nại được đều kèm đường dẫn khiếu nại |
| DEC-198 | Phụ thuộc | Hiện hành | FR-M07-02 | Nhóm B. M09: một thông báo gộp bài bị AI từ chối và cảnh cáo AI |
| DEC-212 | Nhắc tới | Sửa một phần bởi DEC-215 | FR-M07-01 | Nhóm B. M06: "đang theo dõi" gồm ba loại đối tượng theo dõi |
| DG-4 | Nhắc tới | Hiện hành | Không áp dụng: danh sách module | Nhóm B. Draft: danh sách module có Notification |
| DM-1.2 | Nhắc tới | Hiện hành | Chuyển M02 | Nhóm B. Draft M02: hồ sơ có Followers/Following |
| DM-4.5 | Sở hữu | Sửa một phần bởi QA-043, DEC-215 | FR-M07-01, FR-M07-01.01, BR-M07-15 | Nhóm B. Draft: Follow và thông báo khi có hoạt động; đối tượng theo dõi. Bỏ Tag, Group khỏi đối tượng theo dõi |
| DM-5.3 | Sở hữu | Hiện hành | FR-M07-02, FR-M07-02.11, BR-M07-18, BR-M07-23 | Nhóm B. Draft: thông báo trong Group dùng chung cơ chế, lọc theo quyền xem nhóm Private |
| DM-7.1 | Nhắc tới | Bị thay bởi DEC-125 | — | Nhóm B. Draft M14: feed Following, Personalized theo Topic/Group đang theo dõi |
| DM-8 | Nhắc tới | Hiện hành | Không áp dụng: tiêu đề mục draft | Nhóm B. Draft: tiêu đề mục Notification |
| DM-9.3 | Nhắc tới | Hiện hành | Chuyển M12 | Nhóm B. Draft M12: thống kê có Followers/Following |
| DM-x02 | Nhắc tới | Hiện hành | Không áp dụng: danh sách phạm vi dự án | Nhóm B. Draft: phạm vi có Follow, Notification |
| ISS-051 | Sở hữu | Trùng với QA-043 | — | Nhóm B. Câu hỏi đã có QA-043 trả lời |
| ISS-059 | Nhắc tới | Trùng với DEC-025 | — | Nhóm B. Câu hỏi M02 đã có DEC-025 trả lời |
| ISS-077 | Sở hữu | Trùng với DEC-045 | — | Nhóm B. Câu hỏi đã có DEC-045 trả lời |
| ISS-088 | Nhắc tới | Trùng với DEC-056 | — | Nhóm B. Câu hỏi M06 đã có DEC-056 trả lời |
| ISS-105 | Phụ thuộc | Trùng với DEC-074 | — | Nhóm B. Câu hỏi M08 đã có DEC-074 trả lời |
| ISS-131 | Phụ thuộc | Trùng với DEC-102 | — | Nhóm B. Câu hỏi M11 đã có DEC-102 trả lời |
| ISS-140 | Phụ thuộc | Trùng với DEC-110 | — | Nhóm B. Câu hỏi M11 đã có DEC-110 trả lời |
| ISS-165 | Sở hữu | Hiện hành | FR-M07-04, FR-M07-04.04, BR-M07-02, BR-M07-03 | Nhóm B. Tin nhắn mới chỉ báo trong ứng dụng, không email |
| ISS-168 | Nhắc tới | Trùng với DEC-125 | — | Nhóm B. Câu hỏi M14 đã có DEC-125 trả lời |
| ISS-169 | Nhắc tới | Trùng với QA-228 | — | Nhóm B. M14: tab Following rỗng dẫn sang tìm ba loại đối tượng theo dõi |
| ISS-191 | Phụ thuộc | Trùng với DEC-129 | — | Nhóm B. Câu hỏi đã có DEC-129 trả lời |
| ISS-198 | Sở hữu | Trùng với DEC-135 | — | Nhóm B. Câu hỏi đã có DEC-135 trả lời |
| ISS-199 | Nhắc tới | Trùng với DEC-136 | — | Nhóm B. Câu hỏi đã có DEC-136 trả lời; phạm vi email theo M07 không đổi |
| ISS-220 | Phụ thuộc | Trùng với DEC-141 | — | Nhóm B. Câu hỏi M05 đã có DEC-141 trả lời |
| ISS-229 | Phụ thuộc | Trùng với DEC-142 | — | Nhóm B. Câu hỏi M05 đã có DEC-142 trả lời |
| ISS-232 | Sở hữu | Trùng với DEC-147 | — | Nhóm B. Câu hỏi đã có DEC-147 trả lời |
| ISS-241 | Sở hữu | Trùng với DEC-153 | — | Nhóm B. Câu hỏi đã có DEC-153 trả lời |
| ISS-242 | Sở hữu | Trùng với DEC-149, DEC-151 | — | Nhóm B. Câu hỏi đã có DEC-149, DEC-151 trả lời |
| ISS-259 | Phụ thuộc | Trùng với DEC-159 | — | Nhóm B. Câu hỏi M01 đã có DEC-159 trả lời |
| ISS-272 | Phụ thuộc | Trùng với DEC-169 | — | Nhóm B. Câu hỏi M03 đã có DEC-169 trả lời |
| ISS-275 | Nhắc tới | Trùng với DEC-171 | — | Nhóm B. Câu hỏi M02 đã có DEC-171 trả lời |
| ISS-276 | Nhắc tới | Trùng với DEC-172 | — | Nhóm B. Câu hỏi M02 đã có DEC-172 trả lời |
| ISS-302 | Phụ thuộc | Trùng với DEC-192 | — | Nhóm B. Câu hỏi M08 đã có DEC-192 trả lời |
| ISS-314 | Phụ thuộc | Trùng với DEC-197 | — | Nhóm B. Câu hỏi M09 đã có DEC-197 trả lời |
| ISS-340 | Nhắc tới | Trùng với DEC-212 | — | Nhóm B. Câu hỏi M06 đã có DEC-212 trả lời |
| QA-017 | Sở hữu | Hiện hành | FR-M07-02, FR-M07-02.01 | Nhóm B. Tác nhân hệ thống gửi thông báo theo sự kiện. DEC-203 (ngoài bảng nguồn) làm rõ phần vòng phản hồi AI, không chạm M07 |
| QA-019 | Phụ thuộc | Sửa một phần bởi DEC-197 | FR-M07-04.08 | Nhóm B. M08/M09: ban gửi email kèm đường dẫn khiếu nại. DEC-187, DEC-189 (ngoài bảng nguồn) sửa phần ban, không chạm M07 |
| QA-026 | Sở hữu | Trùng với DEC-010 | — | Nhóm B. Gửi thông báo sau khi liên kết Google |
| QA-034 | Sở hữu | Bị thay bởi DEC-176 | — | Nhóm B. Thông báo nhắc cập nhật Lớp/Khối đầu năm ("có thể") |
| QA-043 | Sở hữu | Sửa một phần bởi DEC-215 | FR-M07-01, FR-M07-01.01, FR-M07-01.02, BR-M07-15 | Nhóm B. Đối tượng theo dõi: User, Topic, Post (không Group) và thông báo tương ứng. |
| QA-044 | Phụ thuộc | Sửa một phần bởi DEC-110 | Chuyển M11 | Nhóm B. M11: vào nhóm qua link mời hoặc xin gia nhập |
| QA-058 | Phụ thuộc | Trùng với DEC-017 | — | Nhóm B. M01: nhiều thiết bị, mỗi thiết bị một kết nối |
| QA-067 | Nhắc tới | Hiện hành | Chuyển M02 | Nhóm B. M02: hồ sơ có số và danh sách theo dõi. DEC-173 (ngoài bảng nguồn) thêm trường hồ sơ, không chạm M07 |
| QA-069 | Nhắc tới | Trùng với DEC-025 | — | Nhóm B. M02: danh sách theo dõi công khai |
| QA-099 | Sở hữu | Trùng với DEC-045 | — | Nhóm B. Nhắc tên trong bình luận luôn sinh thông báo |
| QA-113 | Nhắc tới | Trùng với DEC-056 | — | Nhóm B. M06: bộ lọc Following-only |
| QA-180 | Phụ thuộc | Trùng với DEC-102 | — | Nhóm B. M11: quyền kick, promote trong nhóm |
| QA-188 | Phụ thuộc | Trùng với DEC-110 | — | Nhóm B. M11: mời vào nhóm Private; không có thực thể lời mời riêng |
| QA-203 | Phụ thuộc | Trùng với DEC-121 | — | Nhóm B. M12: trao danh hiệu và gửi thông báo sau khi chu kỳ đóng |
| QA-223 | Sở hữu | Trùng với ISS-165 | — | Nhóm B. Tin nhắn mới không gửi email |
| QA-225 | Nhắc tới | Trùng với DEC-125 | — | Nhóm B. M14: tab Following theo Follow của M07 |
| QA-227 | Phụ thuộc | Trùng với DEC-126 | — | Nhóm B. M14: mọi tương tác, gồm theo dõi, cần đăng nhập |
| QA-228 | Nhắc tới | Hiện hành | Chuyển M14 | Nhóm B. M14: ba loại đối tượng theo dõi (M07) |
| QA-239 | Nhắc tới | Hiện hành | Chuyển M14 | Nhóm B. M14: banner bài mới dùng polling, không dùng kênh đẩy |
| QA-250 | Phụ thuộc | Trùng với DEC-129 | — | Nhóm B. Câu trả lời của DEC-129 |
| QA-257 | Sở hữu | Trùng với DEC-135 | — | Nhóm B. Thống nhất kênh đẩy cho thông báo; sửa QA-131 |
| QA-280 | Phụ thuộc | Trùng với DEC-141 | — | Nhóm B. M05: người theo dõi Topic nguồn chuyển sang Topic đích; xóa Topic bỏ lượt theo dõi |
| QA-289 | Phụ thuộc | Trùng với DEC-142 | — | Nhóm B. M05: không thông báo khi Mod/Admin đổi Topic, Tag |
| QA-292 | Sở hữu | Trùng với DEC-147 | — | Nhóm B. Thông báo liên kết Google: trong ứng dụng + email |
| QA-301 | Sở hữu | Trùng với DEC-153 | — | Nhóm B. Thời điểm gửi thông báo nhắc tên |
| QA-302 | Sở hữu | Trùng với DEC-149, DEC-151 | — | Nhóm B. Email cảnh báo 24 giờ trước khi tự xóa; đặt lại mật khẩu gửi "mật khẩu đã đổi" |
| QA-311 | Phụ thuộc | Trùng với DEC-156 | — | Nhóm B. M01: DELETED xóa quan hệ theo dõi |
| QA-319 | Phụ thuộc | Trùng với DEC-159 | — | Nhóm B. M01: DELETED xóa theo dõi Topic, bài |
| QA-332 | Phụ thuộc | Trùng với DEC-169 | — | Nhóm B. M03: MS1 không có Accepted Answer |
| QA-335 | Nhắc tới | Trùng với DEC-171 | — | Nhóm B. M02: Guest xem danh sách theo dõi cần đăng nhập |
| QA-336 | Nhắc tới | Trùng với DEC-172 | — | Nhóm B. M02: "đang theo dõi" chỉ người dùng |
| QA-345 | Phụ thuộc | Trùng với DEC-180 | — | Nhóm B. M04: chủ bình luận bị ẩn chỉ xem khi mở từ thông báo |
| QA-349 | Phụ thuộc | Trùng với DEC-179 | — | Nhóm B. M04: chủ nội dung xem lại khi mở từ thông báo xử lý |
| QA-362 | Phụ thuộc | Trùng với DEC-192 | — | Nhóm B. M08: thông báo khi kết luận vụ |
| QA-374 | Phụ thuộc | Trùng với DEC-197 | — | Nhóm B. M09: thông báo xử lý khiếu nại được kèm nút Khiếu nại |
| QA-375 | Phụ thuộc | Trùng với DEC-198 | — | Nhóm B. M09: thông báo gộp bài bị từ chối và cảnh cáo AI |
| QA-400 | Nhắc tới | Trùng với DEC-212 | — | Nhóm B. M06: "đang theo dõi" gồm ba loại đối tượng |
| QA-402 | Nhắc tới | Hiện hành | Chuyển M06 | Nhóm B. M06: danh sách xác nhận X1–X7 (bộ lọc theo dõi cho Guest) |
| F-GRP-07 | Phụ thuộc | Hiện hành | Chuyển M11 | Nhóm B. M11: link mời vào thẳng nhóm |
| MR-A01 | Nhắc tới | Hiện hành | Không áp dụng: tóm tắt đợt sửa M16 | Nhóm B. Đợt sửa M16: có thông báo tin nhắn |
| MR-A02 | Nhắc tới | Hiện hành | Chuyển M14 | Nhóm B. Đợt sửa M14: tab Following dùng đối tượng theo dõi của M07 |
| MR-A04 | Nhắc tới | Hiện hành | Không áp dụng: tóm tắt đợt sửa Phase 6 | Nhóm B. Đợt sửa Phase 6: khung thông báo đã có ở M07 |
| MR-A05 | Nhắc tới | Trùng với DEC-135 | — | Nhóm B. Đợt sửa tech stack: kênh đẩy thay WebSocket ở M07 |
| MR-M02 | Nhắc tới | Hiện hành | Chuyển M02 | Nhóm B. Dòng module M02: theo dõi công khai. DEC-170 (ngoài bảng nguồn) sửa dòng này, không chạm M07 |
| MR-M06 | Nhắc tới | Hiện hành | Chuyển M06 | Nhóm B. Dòng module M06: bộ lọc following. DEC-208 (đã loại) sửa dòng này, không chạm M07 |
| MR-M14 | Nhắc tới | Hiện hành | Chuyển M14 | Nhóm B. Dòng module M14: tab Following |
| DEC-127 | Phụ thuộc | Hiện hành | FR-M07-05.04, BR-M07-22 | Nhóm D. Dùng chung: múi giờ Asia/Ho_Chi_Minh cho tính và hiển thị thời gian |
| DEC-128 | Phụ thuộc | Hiện hành | Không áp dụng: câu chữ thông báo chốt khi thiết kế, theo khóa i18n tiếng Việt | Nhóm D. Dùng chung: chuỗi giao diện, thông điệp hệ thống qua khóa i18n, chỉ tiếng Việt |
| DEC-130 | Nhắc tới | Hiện hành | Không áp dụng: dùng chung, không quy định hành vi M07 | Nhóm D. Dùng chung; không quy định hành vi M07. DEC-160 (ngoài bảng nguồn) sửa, không chạm M07 |
| DEC-131 | Nhắc tới | Hiện hành | Không áp dụng: dùng chung, không quy định hành vi M07 | Nhóm D. Dùng chung; không quy định hành vi M07. DEC-146 (ngoài bảng nguồn), DEC-154 (đã loại) sửa, không chạm M07 |
| DEC-132 | Nhắc tới | Sửa một phần bởi DEC-141 | Không áp dụng: dùng chung, không quy định hành vi M07 | Nhóm D. Dùng chung; không quy định hành vi M07. DEC-144 (ngoài bảng nguồn) cũng sửa |
| DEC-133 | Nhắc tới | Hiện hành | Không áp dụng: dùng chung, không quy định hành vi M07 | Nhóm D. Dùng chung; không quy định hành vi M07. DEC-207 (ngoài bảng nguồn) làm rõ, không chạm M07 |
| DEC-136 | Phụ thuộc | Hiện hành | Không áp dụng: công nghệ gửi email, không đưa vào FR | Nhóm D. Dùng chung: gửi email; phạm vi email theo M07 |
| ISS-189 | Nhắc tới | Trùng với DEC-127 | — | Nhóm D. Dùng chung; không quy định hành vi M07 |
| ISS-190 | Nhắc tới | Trùng với DEC-128 | — | Nhóm D. Dùng chung; không quy định hành vi M07 |
| ISS-192 | Nhắc tới | Trùng với DEC-130 | — | Nhóm D. Dùng chung; không quy định hành vi M07 |
| ISS-193 | Nhắc tới | Trùng với DEC-131 | — | Nhóm D. Dùng chung; không quy định hành vi M07 |
| ISS-194 | Nhắc tới | Trùng với DEC-132 | — | Nhóm D. Dùng chung; không quy định hành vi M07 |
| ISS-195 | Nhắc tới | Trùng với DEC-133 | — | Nhóm D. Dùng chung; không quy định hành vi M07 |
| ISS-196 | Nhắc tới | Trùng với QA-255 | — | Nhóm D. Dùng chung; không quy định hành vi M07 |
| ISS-197 | Nhắc tới | Hiện hành | Không áp dụng: dùng chung, không quy định hành vi M07 | Nhóm D. Dùng chung; không quy định hành vi M07 |
| ISS-200 | Nhắc tới | Hiện hành | Không áp dụng: dùng chung, không quy định hành vi M07 | Nhóm D. Dùng chung; không quy định hành vi M07 |
| ISS-201 | Nhắc tới | Trùng với QA-260 | — | Nhóm D. Dùng chung; không quy định hành vi M07 |
| ISS-202 | Nhắc tới | Trùng với QA-261 | — | Nhóm D. Dùng chung; không quy định hành vi M07 |
| ISS-203 | Nhắc tới | Trùng với DEC-137 | — | Nhóm D. Dùng chung; không quy định hành vi M07 |
| ISS-204 | Nhắc tới | Hiện hành | Không áp dụng: dùng chung, không quy định hành vi M07 | Nhóm D. Dùng chung; không quy định hành vi M07 |
| QA-248 | Nhắc tới | Trùng với DEC-127 | — | Nhóm D. Dùng chung; không quy định hành vi M07 |
| QA-251 | Nhắc tới | Trùng với DEC-130 | — | Nhóm D. Dùng chung; không quy định hành vi M07 |
| QA-252 | Nhắc tới | Trùng với DEC-131 | — | Nhóm D. Dùng chung; không quy định hành vi M07 |
| QA-253 | Nhắc tới | Trùng với DEC-132 | — | Nhóm D. Dùng chung; không quy định hành vi M07 |
| QA-254 | Nhắc tới | Trùng với DEC-133 | — | Nhóm D. Dùng chung; không quy định hành vi M07 |
| QA-255 | Nhắc tới | Hiện hành | Không áp dụng: dùng chung, không quy định hành vi M07 | Nhóm D. Dùng chung; không quy định hành vi M07 |
| QA-258 | Nhắc tới | Trùng với DEC-136 | — | Nhóm D. Dùng chung; không quy định hành vi M07 |
| QA-259 | Nhắc tới | Hiện hành | Không áp dụng: dùng chung, không quy định hành vi M07 | Nhóm D. Dùng chung; không quy định hành vi M07 |
| QA-260 | Nhắc tới | Hiện hành | Không áp dụng: dùng chung, không quy định hành vi M07 | Nhóm D. Dùng chung; không quy định hành vi M07 |
| QA-261 | Nhắc tới | Hiện hành | Không áp dụng: dùng chung, không quy định hành vi M07 | Nhóm D. Dùng chung; không quy định hành vi M07 |
| QA-262 | Nhắc tới | Hiện hành | Không áp dụng: dùng chung, không quy định hành vi M07 | Nhóm D. Dùng chung; không quy định hành vi M07 |
| QA-263 | Nhắc tới | Trùng với DEC-137 | — | Nhóm D. Dùng chung; không quy định hành vi M07 |
| QA-264 | Nhắc tới | Hiện hành | Không áp dụng: dùng chung, không quy định hành vi M07 | Nhóm D. Dùng chung; không quy định hành vi M07 |

<!-- Nhãn: Sở hữu · Phụ thuộc · Nhắc tới · Loại (khớp nhầm)
     Trạng thái: Hiện hành · Sửa một phần bởi X · Bị thay bởi X · Trùng với X · Mâu thuẫn với X
     Dùng ở: ID trong tài liệu · "Chuyển Myy" · "Không áp dụng: <lý do>" · "—" (chỉ khi Nhãn là Loại hoặc Trạng thái là Bị thay/Trùng) -->

### C.2 Chuỗi quyết định

| Chuỗi | Nội dung hiện hành |
|---|---|
| DEC-065 → DEC-147, DEC-151, DEC-180, DEC-215, DEC-218; DEC-091, DEC-198 (không có dấu) | Bảng sự kiện và kênh của DEC-065 còn hiệu lực, có thêm: "Đã liên kết Google" (trong ứng dụng + email, DEC-147); đặt lại mật khẩu cũng là "mật khẩu đã đổi" (DEC-151); "Bình luận của bạn đã bị ẩn" (chỉ trong ứng dụng, DEC-180); "Đề xuất làm Mod" có Chấp nhận/Từ chối (DEC-091, chỉ trong ứng dụng); "người bạn theo dõi có bài mới" (chỉ trong ứng dụng, DEC-215). Bài bị AI từ chối kèm cảnh cáo AI chỉ có một thông báo gộp (DEC-198). Không báo cho chính người gây sự kiện; vẫn tạo cho người nhận BANNED, DEACTIVATED, không tạo cho DELETED; tên người gây sự kiện theo DEC-149, DEC-156 (DEC-218). Email chỉ gồm: đổi/đặt lại mật khẩu, liên kết Google, cảnh báo trước khi tự xóa, ban/gỡ ban, khiếu nại liên quan ban; không có email tổng hợp. |
| DEC-065 + DEC-149 (làm rõ, không có dấu) | Email cảnh báo tự xóa: đúng một email, 24 giờ trước khi tài khoản DEACTIVATED tự chuyển DELETED; không có thông báo trong ứng dụng. |
| DM-8.1 → DEC-065, DEC-169, DEC-215 | "Post nhận star" là upvote, gồm cả upvote bình luận, gộp theo DEC-066, DEC-216. Sự kiện Accepted Answer bị bỏ (MS1 không có Accepted Answer). "Report được xử lý", "Post hoàn tất moderation" ứng với các dòng kết quả báo cáo và bài được đăng/bị từ chối/bị ẩn của DEC-065. "Post mới từ user đang follow" còn hiệu lực (DEC-215). "Nội dung mới trong topic/tag/group đang follow" bị bỏ: Topic đang theo dõi không sinh thông báo, Tag và Group không theo dõi được. |
| DM-4.5 → QA-043 → DEC-215 (QA-127 trùng) | Đối tượng theo dõi là người dùng và Topic; theo dõi bài viết bị bỏ; Tag, Group không theo dõi được. Theo dõi người dùng sinh thông báo bài mới; theo dõi Topic không sinh thông báo. Người dùng bỏ theo dõi được; "có người theo dõi mới" chỉ một lần mỗi cặp. Không theo dõi chính mình, không bắt đầu theo dõi tài khoản BANNED (DEC-220). |
| DEC-069 → DEC-135 (QA-257); ISS-102, QA-131, MR-M07 | Thông báo được lưu trước và là nguồn chính; việc đẩy tới người đang online là cố gắng, không thử lại; người dùng tải danh sách khi mở trang hoặc bấm chuông. DEC-135 chỉ đổi công nghệ kênh đẩy (không đưa vào FR). |
| DEC-010 → DEC-147 | Liên kết Google tự động cả khi email chưa xác minh; sau khi liên kết, chủ tài khoản nhận thông báo trong ứng dụng và email. QA-026 trùng DEC-010. |
| DEC-045 → DEC-153 | Nhắc tên luôn sinh thông báo, trong bài hay bình luận, kể cả khi bài đã bị tắt thông báo (DEC-070). Thông báo gửi khi nội dung chứa lượt nhắc hiển thị công khai (sau quét trước khi đăng); sửa nội dung chỉ báo người mới được nhắc. |
| QA-034 → DEC-176 | Không có thông báo nhắc cập nhật Lớp/Khối đầu năm học ở MS1. |
| DEC-074 → DEC-192 → DEC-197 | Nội dung thông báo kết quả báo cáo do M08 quy định: người báo cáo nhận kết quả chung ("đã có biện pháp xử lý" / "không phát hiện vi phạm"), vụ do AI tạo không báo người báo cáo; người bị báo cáo chỉ nhận khi Có xử lý; mọi thông báo về xử lý khiếu nại được kèm đường dẫn khiếu nại (trừ bình luận bị ẩn, nhóm bị ẩn/khóa). |
| QA-019 → DEC-197; DEC-187, DEC-189 (ngoài bảng nguồn) | Phần còn hiệu lực cho M07: ban gửi email kèm đường dẫn khiếu nại. DEC-187, DEC-189 sửa cách ra ban (lần vi phạm thứ 7, chỉ Admin xử lý Mod), không chạm M07. |
| DEC-085 → DEC-197 | Email ban kèm đường dẫn trang khiếu nại; trong lúc bị ban chỉ khiếu nại được chính lệnh ban. |
| QA-044 → DEC-110 | Vào nhóm Private qua lời mời hoặc link; không có lời mời riêng có Chấp nhận/Từ chối, vào nhóm theo luồng gia nhập DEC-103. Sự kiện "Group: invite" của DEC-065 được đọc là thông báo cho người được mời, không phải một lời mời phải chấp nhận (chi tiết hành vi mời thuộc M11; điểm còn thiếu gom ở bước 5–6). |
| DEC-129 → DEC-156; DEC-156 → DEC-159 → DEC-215 | Dữ liệu dạng nhật ký giữ vĩnh viễn, nhất quán DEC-071. Khi DELETED: xóa mọi quan hệ theo dõi hai chiều (người dùng, Topic; không còn theo dõi bài), giảm số người theo dõi tương ứng. |
| DEC-016 → DEC-151; DEC-017 → DEC-151 | Phần chạm M07: đặt lại mật khẩu gửi "mật khẩu đã đổi" (đã ghi ở chuỗi DEC-065). Phần còn lại thuộc M01. |
| QA-017 → DEC-203 (ngoài bảng nguồn) | DEC-203 làm rõ vòng phản hồi AI chỉ đánh giá gợi ý Topic; phần "Notification Worker gửi thông báo theo sự kiện" của QA-017 còn hiệu lực. |
| DEC-132 → DEC-141 | Dùng chung (M05): Topic Suggestion đối chiếu danh mục Topic hiện tại; không chạm M07. |
| DEC-025 → DEC-171, DEC-172; DEC-056 → DEC-212 → DEC-215; DM-7.1 → DEC-125 → DEC-215 | Nơi dùng quan hệ theo dõi của M07: hồ sơ (M02, chỉ người dùng, không hiện DEACTIVATED/BANNED), bộ lọc "đang theo dõi" (M06) và tab Following (M14), nay gồm người dùng và Topic, không còn bài đang theo dõi (DEC-215); feed Personalized của draft bị bỏ (DEC-125). |
| DEC-066 → DEC-216 | Báo ngay lượt upvote đầu; cửa sổ 5 phút từ lượt đầu, riêng từng bài và bình luận; lượt sau cập nhật cùng thông báo ("A và N người khác"), về chưa đọc, lên đầu; bỏ upvote không đổi thông báo. |
| DEC-067 → DEC-217, DEC-219, DEC-220 | Chuông 10 thông báo, mới nhất trước theo lần cập nhật cuối, có số chưa đọc riêng; mở chuông không đánh dấu đã đọc; trang Thông báo tải 20 mỗi lần. Tin nhắn báo bằng popup và biểu tượng Tin nhắn; số trên biểu tượng là số cuộc trò chuyện có tin chưa đọc, gồm cả cuộc đã tắt. |
| DEC-068 → DEC-220 | Email qua hàng đợi quét mỗi 1 phút; email lỗi gửi lại ở lần quét kế tiếp, tối đa 3 lần rồi dừng. |
| DEC-070 → DEC-219, DEC-220 | Công tắc tắt thông báo bài có trên mọi bài, tắt bình luận mới, trả lời, upvote bài và upvote bình luận của người dùng trong bài; nhắc tên vẫn gửi. Tắt thông báo Chat (một cuộc hoặc toàn bộ) chỉ ẩn popup tin nhắn; tắt toàn bộ không có ngoại lệ; bỏ tắt toàn bộ thì cuộc đã tắt riêng vẫn tắt. |
| DEC-091 → DEC-220 | Thông báo "Đề xuất làm Mod" trả lời một lần, sau đó hiện lựa chọn; không có hạn; đề xuất lại là thông báo mới. Chấp nhận thì MOD ngay (M10). |

**Cạnh bị bác bỏ:** DEC-180 ← OPEN-012 (dấu ghi DEC-201 đóng OPEN-012; OPEN-012 không sửa DEC-180); DEC-020 ← DEC-209 (DEC-209 chỉ được trích làm chuẩn khớp tên; mục sửa là DEC-214). Các cạnh còn lại của tool tác động lên mục ngoài bảng nguồn (DEC-008, DEC-011, DEC-019, DEC-030, DEC-038, DEC-043, DEC-048–050, DEC-064, DEC-072, DEC-077, DEC-082, DEC-088, DEC-090, DEC-115, DEC-162, DEC-166, F-GRP-06, GL:Accepted Answer, GL:Topic, MR-M01, MR-M03, MR-M11, QA-011, QA-018, QA-021, QA-107, QA-160, QA-328): đúng nhưng không chạm M07.
