---
module: M06
ten_module: Search
ma_tai_lieu: FR-M06
phien_ban: 1.5
trang_thai: Đã chốt
ngay: 2026-10-24
tac_gia: Phạm Văn Đức
moc_nguon: DEC-213, QA-403, ISS-343, OPEN-012
steps_completed: [1, 2, 3, 4, 5, 6, 7]
---
# Tài liệu yêu cầu chức năng — M06 Search

| Mã tài liệu | FR-M06 |
|---|---|
| Dự án | iShare |
| Module | M06 — Search |
| Trạng thái | Đã chốt |
| Phiên bản | 1.5 |
| Ngày | 2026-10-24 |
| Tác giả | Phạm Văn Đức |

<!-- Quy ước chung cho mọi bảng dưới đây:
     - Thân tài liệu không ghi nguồn. Nguồn của mọi ID nằm ở Phụ lục A.
     - Ô không có nội dung ghi "—". Không xóa cột.
     - Mục chưa tới bước làm thì để dòng "(Chưa làm — bước N)". -->

## 1. Tổng quan

### 1.1 Mục đích

Module Search giúp người dùng, kể cả Guest, tìm bài viết theo ý nghĩa nội dung (tìm kiếm ngữ nghĩa) và tìm
người dùng, Tag, Topic, Group theo tên, trên một trang kết quả chung. Khi AI tắt hoặc lỗi, người dùng vẫn tìm
được bài theo từ khóa, kể cả khi gõ tiếng Việt không dấu.

### 1.2 Phạm vi

**Trong phạm vi:**

- Tìm bài viết: theo ngữ nghĩa ("Tìm kiếm thông minh") cho người đã đăng nhập khi AI bật; tìm full-text theo
  từ khóa (bỏ dấu tiếng Việt) cho Guest, khi AI tắt, hoặc khi AI lỗi với riêng truy vấn đó. Tìm bài chỉ chạy khi
  người dùng gửi truy vấn.
- Xếp hạng kết quả bài theo độ liên quan và mức tương tác; giảm hạng nội dung của người đang ở mức cảnh cáo HEAVY.
- Lọc và sắp xếp kết quả bài: Topic, Tag, khoảng thời gian, chỉ nội dung từ người/đối tượng đang theo dõi,
  sắp xếp. Xem các bài của một Topic hoặc Tag được làm qua bộ lọc này, kể cả khi không có truy vấn.
- Tìm người dùng (display_name, username), Tag, Topic, Group theo tiền tố hoặc gần đúng; gợi ý tự động khi gõ
  và tìm khi gửi.
- Trang kết quả hỗn hợp: bài là kết quả chính; người dùng, Tag, Topic, Group là kết quả phụ.
- Đoạn trích nội dung bài trong kết quả (không tô sáng từ khóa).
- Tải thêm kết quả khi cuộn, có giới hạn tổng số kết quả.
- Lịch sử tìm kiếm lưu trên thiết bị của người dùng; xóa khi người dùng đăng xuất.
- Quyền tìm theo vai trò (Guest, User, Mod, Admin), theo thành viên nhóm Private, và theo trạng thái tài khoản của người được tìm.
- Giới hạn tần suất tìm kiếm.

**Ngoài phạm vi:**

- Tìm bình luận — đã quyết là không làm.
- Tạo embedding cho bài và cho truy vấn, thời gian chờ và thử lại khi gọi AI, tạo bù embedding — M13 AI Layer.
- Công tắc AI tổng và công tắc Search — M10 Admin Panel.
- Gợi ý người dùng khi @mention — M01 Authentication & Account (M06 dùng chung cách so khớp tên).
- Danh sách Topic, Tag; vô hiệu hóa và kích hoạt lại Tag — M05 Topic & Tag.
- Quy tắc bài nào đang hiển thị công khai, nội dung chữ của bài — M03 Post & Content.
- Mức cảnh cáo của người dùng — M08 Moderation.
- Nhóm Public/Private, thành viên nhóm, bài ẩn danh trong nhóm — M11 Group.
- Quan hệ theo dõi — M07 Notification.
- Số sao (bình chọn) của bài — M12 Gamification. Số bình luận của bài — M04 Comment.
- Feed (Trending, Following, Group, Newest) và sắp xếp feed — M14 Feed & Discovery.
- Gợi ý bài liên quan (Related Posts) — không nằm trong phạm vi chính thức.
- Tối ưu để công cụ tìm kiếm bên ngoài lập chỉ mục (SEO/SSR) — hoãn có chủ đích ở MS1.

## 2. Thuật ngữ và viết tắt

### 2.1 Thuật ngữ

| Thuật ngữ | Định nghĩa |
|---|---|
| Truy vấn | Chuỗi người dùng gõ vào ô tìm kiếm, cùng bộ lọc và cách sắp xếp đang chọn. |
| Gửi truy vấn | Người dùng nhấn Enter hoặc bấm nút tìm. Tìm bài viết chỉ chạy khi gửi truy vấn. |
| Gợi ý khi gõ | Danh sách người dùng, Tag, Topic, Group khớp với chuỗi đang gõ (từ ký tự đầu tiên), hiện khi người dùng ngừng gõ 300 mili giây, trước khi gửi truy vấn; mỗi loại tối đa 3 mục. |
| Truy vấn rỗng | Truy vấn không có chữ nào trong ô tìm kiếm, ví dụ khi mở trang bài của một Topic hay Tag. |
| Tìm kiếm ngữ nghĩa | Tìm bài viết theo ý nghĩa: so ý nghĩa của truy vấn với ý nghĩa của tiêu đề và nội dung chữ của bài, nên ra được bài cùng ý dù khác chữ. Dùng embedding do M13 tạo. Tên hiển thị với người dùng: "Tìm kiếm thông minh". Chỉ người đã đăng nhập dùng được. |
| Tìm full-text | Tìm bài viết theo từ khóa có trong tiêu đề và nội dung chữ, bỏ dấu tiếng Việt khi so; bài chứa ít nhất một từ của truy vấn là khớp. Dùng cho Guest, khi AI tắt, hoặc khi AI lỗi với riêng một truy vấn. |
| Từ (của truy vấn) | Chuỗi ký tự giữa hai khoảng trắng; mỗi âm tiết tiếng Việt là một từ. "phương trình bậc hai" có 4 từ. |
| Embedding | Biểu diễn ý nghĩa của một bài viết hoặc một truy vấn, do M13 tạo. |
| Công tắc AI tổng, công tắc Search | Hai công tắc ở cấu hình hệ thống (M10). Tìm kiếm ngữ nghĩa chỉ chạy khi cả hai đều bật. |
| Nội dung chữ | Phần văn bản thuần của bài viết, không gồm định dạng và tệp đính kèm (M03). |
| Bài đang hiển thị công khai | Bài có trạng thái đăng Đã đăng và trạng thái kiểm duyệt Bình thường; bài trong nhóm Private chỉ hiển thị cho thành viên nhóm (M03, M11). |
| Thời điểm đăng | Lúc bài viết chuyển sang trạng thái Đã đăng (M03). |
| Upvote | Lượt đánh giá tích cực cho một bài viết (Post Star, M12). |
| Số bình luận | Số bình luận gốc cộng số trả lời đang hiển thị bình thường của bài, theo cách tính của M04. |
| Điểm liên quan | Mức bài khớp với truy vấn, trong khoảng 0–1. Tìm ngữ nghĩa: độ tương đồng giữa embedding truy vấn và embedding bài, đổi về 0–1 theo thang cố định. Tìm full-text: số từ của truy vấn có trong bài chia cho số từ của truy vấn. |
| Điểm tương tác | Điểm tính từ số upvote và số bình luận của bài, chuẩn hóa về khoảng 0–1 trong tập ứng viên. |
| Điểm cuối | Điểm dùng để xếp kết quả bài khi sắp xếp theo Liên quan: Điểm liên quan × 0,8 + Điểm tương tác × 0,2. |
| Tập ứng viên | 120 bài có Điểm liên quan cao nhất với một truy vấn có chữ, được lấy ra trước khi xếp lại theo cách sắp xếp đang chọn. |
| Mức HEAVY | Mức cảnh cáo cao nhất của người dùng, trong thời gian thử thách của mức đó (M08). Hai mức thấp hơn là LIGHT và MEDIUM. |
| Trạng thái tài khoản | ACTIVE, DEACTIVATED (tự tạm vô hiệu hóa), DELETED, BANNED (M01). Bước 3 là bước cuối của đăng ký (M01). |
| Topic, Tag | Topic là lĩnh vực nội dung lấy từ danh mục Topic; Tag là từ khóa tự do của bài, có thể bị Mod, Admin vô hiệu hóa (M05). |
| Nhóm Public, nhóm Private | Hai loại Group (M11). Nhóm Private chỉ vào được qua lời mời hoặc link; bài của nhóm Private chỉ thành viên xem được. |
| Đối tượng đang theo dõi | Người dùng và Topic mà người tìm đang theo dõi (M07). Bài viết không phải đối tượng theo dõi. |
| Kết quả chính, kết quả phụ | Trên trang kết quả, kết quả bài viết là kết quả chính; người dùng, Tag, Topic, Group là kết quả phụ. |
| Đoạn trích | Phần đầu của nội dung chữ, hiện dưới mỗi kết quả bài. |
| Lịch sử tìm kiếm | Các truy vấn gần đây lưu trên trình duyệt của thiết bị đang dùng, không lưu trên hệ thống. |
| Lượt gợi ý, lượt gửi | Đơn vị đếm của giới hạn tần suất: mỗi lần hệ thống trả gợi ý khi gõ là một lượt gợi ý; mỗi lần gửi truy vấn, đổi bộ lọc, đổi cách sắp xếp, mở trang bài của Topic hay Tag, hoặc chọn một mục lịch sử là một lượt gửi. Tải thêm khi cuộn không là lượt nào. |
| Tài khoản tìm được | Tài khoản ACTIVE đã xong Bước 3 đăng ký (M01). |
| Hôm nay, Tuần này, Tháng này | Khoảng theo lịch, giờ Asia/Ho_Chi_Minh: từ 00:00 hôm nay; từ 00:00 thứ Hai tuần này; từ 00:00 ngày 1 tháng này; tới lúc tìm. |

### 2.2 Viết tắt

| Viết tắt | Đầy đủ |
|---|---|
| FR | Functional Requirement — yêu cầu chức năng |
| BR | Business Rule — quy tắc nghiệp vụ |
| AI | Trí tuệ nhân tạo; trong tài liệu này là dịch vụ AI của bên thứ ba mà iShare gọi tới (M13) |
| IP | Địa chỉ mạng của thiết bị; dùng để tính giới hạn tần suất cho Guest |
| MS1 | Milestone 1 — mốc demo của đồ án |
| TBD | To Be Determined — điểm chưa chốt |

## 3. Thông tin đầu vào

### 3.1 Tài liệu đầu vào

| Tài liệu | Phiên bản / mốc |
|---|---|
| Draft: docs/_temp/iShare_modules.md (mục 7.3, 7.4, 11.3), iShare_specs_general.md (mục 6) | Theo ngày sửa tệp |
| Register: decisions, qa-log, issue-queue, open-issues, glossary, module-registry | DEC-213, QA-403, ISS-343, OPEN-012 (khớp `moc_nguon`) |

### 3.2 Tài liệu liên quan

| Module | Liên quan ở điểm nào |
|---|---|
| M01 Authentication & Account | Tìm người dùng theo display_name, username; chỉ tài khoản ACTIVE đã xong Bước 3; nhãn "Tài khoản đã bị khóa" của tài khoản BANNED. |
| M03 Post & Content | Bài nào đang hiển thị công khai; nội dung chữ của bài dùng để tìm và làm đoạn trích. |
| M04 Comment | Số bình luận của bài dùng để xếp hạng; bình luận không được tìm. |
| M05 Topic & Tag | Topic, Tag để tìm, gợi ý khi gõ và lọc bài; Tag bị vô hiệu hóa không hiện trong gợi ý; xem bài theo Topic/Tag qua bộ lọc M06. |
| M07 Notification | Quan hệ theo dõi cho bộ lọc chỉ nội dung đang theo dõi. |
| M08 Moderation | Mức cảnh cáo HEAVY làm giảm hạng tìm kiếm nội dung hiện có. |
| M10 Admin Panel | Công tắc AI tổng và công tắc Search quyết định tìm ngữ nghĩa hay full-text. |
| M11 Group | Nhóm Private không hiện trong tìm kiếm với người ngoài nhóm; bài của nhóm Private chỉ thành viên thấy; nhóm đổi Public sang Private. |
| M12 Gamification | Số sao (bình chọn) của bài dùng để xếp hạng. |
| M13 AI Layer | Embedding của bài và của truy vấn; báo AI tắt hoặc lỗi để M06 tìm full-text. |
| M14 Feed & Discovery | Tab Following rỗng dẫn người dùng sang trang tìm kiếm. |

## 4. Tổng quan chức năng

### 4.1 Luật, tiêu chuẩn liên quan

Không có.

### 4.2 Vai trò

| Vai trò | Mô tả trong module này |
|---|---|
| Guest | Người chưa đăng nhập. Tìm kiếm trên nội dung công khai, với giới hạn tần suất chặt hơn User. Tìm bài chỉ bằng full-text; thấy lựa chọn "Tìm kiếm thông minh" và bộ lọc chỉ nội dung đang theo dõi, bấm vào thì được nhắc đăng nhập. |
| User | Người dùng đã đăng nhập. Dùng gợi ý khi gõ, tìm bài viết, tìm người dùng, Tag, Topic, Group, lọc và sắp xếp kết quả, dùng lịch sử tìm kiếm. |
| Mod | Tìm kiếm như User. Nguồn không cho Mod quyền tìm thêm. |
| Admin | Tìm kiếm như User. Nguồn không cho Admin quyền tìm thêm. |
| Thành viên nhóm | Vai trò theo ngữ cảnh: User, Mod hoặc Admin là thành viên của một nhóm Private, nên thấy nhóm đó và bài của nhóm đó trong kết quả tìm. |

### 4.3 Ma trận quyền

| Hành động | Guest | User | Mod | Admin | Yêu cầu |
|---|---|---|---|---|---|
| Nhận gợi ý người dùng, Tag, Topic, Group khi gõ | ✓ | ✓ | ✓ | ✓ | FR-M06-01.01, FR-M06-01.06 |
| Tìm bài viết theo ngữ nghĩa | ✗ | ✓ | ✓ | ✓ | FR-M06-02.03, FR-M06-02.23, FR-M06-02.25 |
| Tìm bài viết bằng full-text (khi AI tắt hoặc lỗi) | ✓ | ✓ | ✓ | ✓ | FR-M06-02.04, FR-M06-02.05 |
| Tìm người dùng, Tag, Topic, Group | ✓ | ✓ | ✓ | ✓ | FR-M06-03.01 |
| Thấy bài của nhóm Private trong kết quả tìm bài | ✗ | ✓ (thành viên nhóm) | ✓ (thành viên nhóm) | ✓ (thành viên nhóm) | FR-M06-02.08 |
| Thấy nhóm Private trong kết quả tìm Group | ✗ | ✓ (thành viên nhóm) | ✓ (thành viên nhóm) | ✓ (thành viên nhóm) | FR-M06-03.08, FR-M06-03.09, FR-M06-01.13 |
| Lọc kết quả bài theo Topic, Tag, khoảng thời gian; sắp xếp kết quả bài | ✓ | ✓ | ✓ | ✓ | FR-M06-04.01, FR-M06-04.02, FR-M06-04.03, FR-M06-04.05, FR-M06-04.06, FR-M06-04.07 |
| Lọc kết quả bài chỉ theo người, đối tượng đang theo dõi | ✗ | ✓ | ✓ | ✓ | FR-M06-04.04, FR-M06-04.13 |
| Xem, chọn lại, xóa lịch sử tìm kiếm trên thiết bị | ✓ | ✓ | ✓ | ✓ | FR-M06-05.01, FR-M06-05.04, FR-M06-05.05 |

<!-- Ô suy ra: Guest ở hàng "gợi ý khi gõ" (giới hạn tần suất có mức riêng cho gợi ý của Guest);
     Guest ở hàng "lịch sử tìm kiếm" (Guest được tìm, lịch sử nằm trên thiết bị, nguồn không giới hạn theo vai trò);
     Guest ✗ ở hàng "bài của nhóm Private" (Guest không là thành viên nhóm nào);
     cột Mod, Admin (nguồn không cho Mod, Admin quyền tìm khác User). -->


### 4.4 Danh sách chức năng

| ID | Chức năng | Tác nhân chính | Kích hoạt |
|---|---|---|---|
| FR-M06-01 | Gợi ý người dùng, Tag, Topic, Group khi gõ | Guest, User, Mod, Admin | Người dùng gõ vào ô tìm kiếm rồi ngừng gõ |
| FR-M06-02 | Tìm bài viết | Guest, User, Mod, Admin | Người dùng gửi truy vấn (nhấn Enter hoặc bấm tìm) |
| FR-M06-03 | Tìm người dùng, Tag, Topic, Group | Guest, User, Mod, Admin | Người dùng gửi truy vấn; kết quả hiện cùng trang với kết quả bài |
| FR-M06-04 | Lọc và sắp xếp kết quả bài viết | Guest, User, Mod, Admin | Người dùng chọn bộ lọc hoặc cách sắp xếp trên trang kết quả, hoặc mở xem các bài của một Topic hay một Tag |
| FR-M06-05 | Dùng lịch sử tìm kiếm | Guest, User, Mod, Admin | Người dùng đặt con trỏ vào ô tìm kiếm, chọn một mục lịch sử, hoặc bấm xóa lịch sử |

### 4.5 Mốc và ưu tiên

Toàn bộ yêu cầu của module thuộc MS1, ưu tiên **Must** (bảng MoSCoW Summary của module-registry: Must gồm M01–M10, M13;
dòng M06 của bảng Module List bị lệch cột, không có giá trị MoSCoW nên không dùng). Không có yêu cầu ngoại lệ về ưu tiên.

## 5. Yêu cầu chức năng

### 5.1 FR-M06-01 Gợi ý người dùng, Tag, Topic, Group khi gõ

**Yêu cầu cấp trên:** Hệ thống phải gợi ý người dùng, Tag, Topic, Group khớp với chuỗi đang gõ trong ô tìm kiếm, trước khi người dùng gửi truy vấn.

**Lý do:** Tìm bài viết tốn nhiều tính toán nên chỉ chạy khi gửi truy vấn; vì vậy gợi ý khi gõ chỉ gồm người dùng, Tag, Topic, Group, không gồm tiêu đề bài viết. Tên người Việt có tên gọi đứng cuối, nên tên được khớp ở bất kỳ vị trí, không chỉ phần đầu.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M06-01.01 | Khi người dùng ngừng gõ trong ô tìm kiếm 300 mili giây (BR-M06-03), hệ thống phải hiện danh sách gợi ý gồm người dùng, Tag, Topic, Group khớp với chuỗi đang gõ (BR-M06-04). |
| FR-M06-01.02 | Khi người dùng gõ tiếp trước khi đủ 300 mili giây, hệ thống phải không gợi ý cho chuỗi trước đó. |
| FR-M06-01.03 | Hệ thống phải không đưa tiêu đề bài viết vào danh sách gợi ý. |
| FR-M06-01.04 | Hệ thống phải không đưa Tag bị vô hiệu hóa vào danh sách gợi ý (BR-M06-10). |
| FR-M06-01.05 | Hệ thống phải khớp người dùng cho danh sách gợi ý theo display_name và username (BR-M06-09). |
| FR-M06-01.06 | Hệ thống phải cho Guest dùng gợi ý khi gõ như người đã đăng nhập. |
| FR-M06-01.07 | Nếu người tìm đã dùng hết số lượt gợi ý trong 60 giây gần nhất theo BR-M06-21, hệ thống phải từ chối lượt gợi ý đó và báo quá nhiều yêu cầu. |
| FR-M06-01.08 | Trong khi công tắc AI tổng hoặc công tắc Search tắt, hệ thống phải vẫn gợi ý khi gõ như khi AI bật (BR-M06-22). |
| FR-M06-01.09 | Hệ thống phải gợi ý cả khi chuỗi đang gõ chỉ có một ký tự, sau cùng thời gian chờ 300 mili giây (BR-M06-03). |
| FR-M06-01.10 | Hệ thống phải hiện tối đa 3 mục cho mỗi loại người dùng, Tag, Topic, Group trong danh sách gợi ý. |
| FR-M06-01.11 | Hệ thống phải khớp chuỗi đang gõ với tên người dùng, Tag, Topic, Group theo BR-M06-09 và xếp mục giống chuỗi gõ hơn lên trước trong mỗi loại. |
| FR-M06-01.12 | Hệ thống phải chỉ đưa vào danh sách gợi ý những tài khoản tìm được (BR-M06-24). |
| FR-M06-01.13 | Nếu người gõ không là thành viên của một nhóm Private, kể cả Guest, hệ thống phải không đưa nhóm đó vào danh sách gợi ý (BR-M06-25). |

### 5.2 FR-M06-02 Tìm bài viết

**Yêu cầu cấp trên:** Hệ thống phải tìm bài viết theo truy vấn người dùng gửi, theo ngữ nghĩa khi người đã đăng nhập tìm lúc AI bật và bằng full-text trong các trường hợp còn lại, rồi hiện kết quả bài đã xếp hạng, có đoạn trích và được tải dần khi cuộn.

**Lý do:** Tìm kiếm ngữ nghĩa là một năng lực AI bắt buộc của dự án: tìm theo ý nghĩa, không chỉ theo từ khóa khớp nguyên văn. Guest không dùng tìm kiếm ngữ nghĩa để bảo vệ chi phí AI. Hệ thống phải hoạt động độc lập khi AI tắt, nên khi đó bài được tìm bằng full-text theo từ khóa, bỏ dấu để tìm được khi gõ không dấu. Tìm bài tốn nhiều tính toán nên chỉ chạy khi gửi truy vấn. Trong xếp hạng, upvote có trọng số gấp đôi bình luận, nhất quán với công thức Trending. Không tô sáng từ khóa vì tìm theo ngữ nghĩa không có từ khóa khớp nguyên văn để tô.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M06-02.01 | Khi người dùng gửi truy vấn, hệ thống phải tìm bài viết theo truy vấn đó. |
| FR-M06-02.02 | Hệ thống phải không tìm bài viết khi người dùng đang gõ mà chưa gửi truy vấn (BR-M06-02). |
| FR-M06-02.03 | Ở nơi công tắc AI tổng và công tắc Search đều bật, khi người dùng đã đăng nhập gửi truy vấn, hệ thống phải tìm bài theo ngữ nghĩa trên tiêu đề và nội dung chữ (BR-M06-05), dùng embedding của truy vấn do M13 tạo. |
| FR-M06-02.04 | Trong khi công tắc AI tổng hoặc công tắc Search tắt, hệ thống phải tìm bài bằng full-text trên tiêu đề và nội dung chữ (BR-M06-06). |
| FR-M06-02.05 | Nếu M13 báo việc tạo embedding cho truy vấn thất bại sau hai lần thử, hệ thống phải tìm full-text cho riêng truy vấn đó (BR-M06-07). |
| FR-M06-02.06 | Khi tìm full-text, hệ thống phải bỏ dấu tiếng Việt ở cả truy vấn và nội dung bài trước khi so (BR-M06-08). |
| FR-M06-02.07 | Hệ thống phải chỉ đưa vào kết quả những bài đang hiển thị công khai với người tìm (BR-M06-11). |
| FR-M06-02.08 | Nếu bài thuộc một nhóm Private mà người tìm không là thành viên nhóm đó, kể cả Guest, hệ thống phải không đưa bài vào kết quả. |
| FR-M06-02.09 | Khi một nhóm đổi từ Public sang Private, hệ thống phải không đưa bài của nhóm vào kết quả của các lần tìm sau đó của người không là thành viên nhóm. |
| FR-M06-02.10 | Khi tìm theo ngữ nghĩa và sắp xếp theo Liên quan, hệ thống phải xếp tập ứng viên theo Điểm cuối giảm dần, tính theo BR-M06-13. |
| FR-M06-02.11 | Trong khi tác giả của một bài đang ở mức HEAVY và kết quả được sắp xếp theo Liên quan, hệ thống phải nhân Điểm cuối của bài đó với 0,5 (BR-M06-14). |
| FR-M06-02.12 | Hệ thống phải không hiện cho người tìm dấu hiệu nào cho thấy một bài bị giảm hạng vì mức cảnh cáo của tác giả. |
| FR-M06-02.13 | Hệ thống phải giữ bài của tài khoản BANNED trong kết quả như bài khác, không loại và không giảm hạng (BR-M06-12). |
| FR-M06-02.14 | Khi kết quả bài hiện tên một tác giả đang bị BANNED, hệ thống phải hiện nhãn "Tài khoản đã bị khóa" cạnh tên đó. |
| FR-M06-02.15 | Hệ thống phải hiện dưới mỗi kết quả bài một đoạn trích theo BR-M06-18, không tô sáng từ khóa, như nhau khi tìm theo ngữ nghĩa và full-text. |
| FR-M06-02.16 | Hệ thống phải hiện kết quả bài làm kết quả chính trên một trang cuộn chung với kết quả phụ, không chia tab (BR-M06-17). |
| FR-M06-02.17 | Khi người dùng cuộn tới cuối các kết quả bài đã tải, hệ thống phải tải thêm tối đa 15 kết quả tiếp theo (BR-M06-19). |
| FR-M06-02.18 | Hệ thống phải không lặp lại và không bỏ sót kết quả giữa các lần tải thêm. |
| FR-M06-02.19 | Nếu truy vấn có chữ, đã tải 120 kết quả bài và người dùng cuộn tiếp, hệ thống phải dừng tải thêm và hiện "Thu hẹp tìm kiếm để có kết quả chính xác hơn". |
| FR-M06-02.20 | Nếu người tìm đã dùng hết số lượt gửi trong 60 giây gần nhất theo BR-M06-21, hệ thống phải từ chối lượt gửi đó và báo quá nhiều yêu cầu. |
| FR-M06-02.21 | Nếu một lượt gợi ý hoặc lượt gửi bị từ chối vì vượt giới hạn tần suất, hệ thống phải chỉ từ chối lượt đó, không yêu cầu captcha và không khóa quyền tìm kiếm của người tìm. |
| FR-M06-02.22 | Hệ thống phải không tìm trong bình luận (BR-M06-01). |
| FR-M06-02.23 | Nếu người gửi truy vấn là Guest, hệ thống phải tìm bài bằng full-text, kể cả khi công tắc AI tổng và công tắc Search đều bật (BR-M06-23). |
| FR-M06-02.24 | Hệ thống phải chỉ hiện lựa chọn "Tìm kiếm thông minh" cho Guest. |
| FR-M06-02.25 | Khi Guest bấm "Tìm kiếm thông minh", hệ thống phải hiện thông báo yêu cầu đăng nhập và giữ nguyên kết quả full-text, kể cả khi công tắc AI tổng hoặc công tắc Search đang tắt. |
| FR-M06-02.26 | Khi tìm full-text, hệ thống phải coi bài có ít nhất một từ của truy vấn trong tiêu đề hoặc nội dung chữ là khớp (BR-M06-08). |
| FR-M06-02.27 | Khi tìm full-text và sắp xếp theo Liên quan, hệ thống phải xếp tập ứng viên theo Điểm cuối giảm dần, với Điểm liên quan tính bằng tỷ lệ từ khớp (BR-M06-13). |
| FR-M06-02.28 | Khi truy vấn có chữ, hệ thống phải lấy tập ứng viên là 120 bài có Điểm liên quan cao nhất (BR-M06-13). |
| FR-M06-02.29 | Nếu hai bài bằng Điểm cuối, hệ thống phải xếp bài có Điểm liên quan cao hơn lên trước, và nếu vẫn bằng thì xếp bài đăng sau lên trước (BR-M06-13). |
| FR-M06-02.30 | Hệ thống phải không tính lượt gửi khi người dùng tải thêm kết quả bằng cách cuộn (BR-M06-21). |
| FR-M06-02.31 | Nếu người dùng gửi truy vấn rỗng mà không có bộ lọc nào, hệ thống phải không tìm. |
| FR-M06-02.32 | Nếu bài không có nội dung chữ, hệ thống phải không hiện đoạn trích cho bài đó (BR-M06-18). |

### 5.3 FR-M06-03 Tìm người dùng, Tag, Topic, Group

**Yêu cầu cấp trên:** Hệ thống phải tìm người dùng, Tag, Topic, Group khớp với truy vấn đã gửi và hiện tối đa 3 kết quả mỗi loại làm kết quả phụ trên trang kết quả.

**Lý do:** Tên người Việt có tên gọi đứng cuối, nên tên được khớp ở bất kỳ vị trí, không chỉ phần đầu. Nhóm Private chỉ vào được qua lời mời hoặc link, nên không hiện với người ngoài nhóm khi tìm kiếm.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M06-03.01 | Khi người dùng gửi truy vấn có chữ, hệ thống phải tìm người dùng, Tag, Topic, Group khớp với truy vấn đó. |
| FR-M06-03.02 | Hệ thống phải hiện tối đa 3 kết quả cho mỗi loại người dùng, Tag, Topic, Group, làm kết quả phụ trên cùng trang với kết quả bài (BR-M06-17). |
| FR-M06-03.03 | Hệ thống phải tìm người dùng theo display_name và username (BR-M06-09). |
| FR-M06-03.04 | Hệ thống phải không đưa Tag bị vô hiệu hóa vào kết quả tìm Tag (BR-M06-10). |
| FR-M06-03.05 | Trong khi công tắc AI tổng hoặc công tắc Search tắt, hệ thống phải vẫn tìm người dùng, Tag, Topic, Group như khi AI bật (BR-M06-22). |
| FR-M06-03.06 | Hệ thống phải khớp truy vấn với tên người dùng, Tag, Topic, Group theo BR-M06-09 và xếp kết quả giống truy vấn hơn lên trước trong mỗi loại. |
| FR-M06-03.07 | Hệ thống phải chỉ đưa vào kết quả tìm người dùng những tài khoản tìm được (BR-M06-24). |
| FR-M06-03.08 | Nếu người tìm không là thành viên của một nhóm Private, kể cả Guest, hệ thống phải không đưa nhóm đó vào kết quả tìm Group (BR-M06-25). |
| FR-M06-03.09 | Khi thành viên của một nhóm Private gửi truy vấn khớp tên nhóm, hệ thống phải đưa nhóm đó vào kết quả tìm Group (BR-M06-25). |
| FR-M06-03.10 | Hệ thống phải không so truy vấn với mô tả của Group (BR-M06-09). |

### 5.4 FR-M06-04 Lọc và sắp xếp kết quả bài viết

**Yêu cầu cấp trên:** Hệ thống phải cho người dùng lọc kết quả bài theo Topic, Tag, khoảng thời gian và nội dung đang theo dõi, chọn cách sắp xếp kết quả bài, và xem mọi bài khớp bộ lọc khi không có truy vấn.

**Lý do:** Bộ lọc của M06 cũng là cách xem các bài của một Topic hay một Tag; M05 chỉ có danh sách Topic, Tag, không có trang liệt kê bài riêng. Giới hạn 120 kết quả có lý do là các kết quả càng về sau càng ít liên quan; lý do đó không đúng khi chỉ lọc theo Topic hay Tag, nên khi không có truy vấn thì không giới hạn.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M06-04.01 | Khi người dùng chọn lọc theo Topic, hệ thống phải chỉ giữ trong kết quả những bài có Topic đó. |
| FR-M06-04.02 | Khi người dùng chọn lọc theo Tag, hệ thống phải chỉ giữ trong kết quả những bài có Tag đó. |
| FR-M06-04.03 | Khi người dùng chọn Hôm nay, Tuần này hoặc Tháng này, hệ thống phải chỉ giữ trong kết quả những bài có thời điểm đăng trong khoảng đó, tính theo lịch giờ Việt Nam (BR-M06-15). |
| FR-M06-04.04 | Khi người dùng đã đăng nhập bật bộ lọc chỉ nội dung đang theo dõi, hệ thống phải chỉ giữ trong kết quả bài của người dùng người đó đang theo dõi và bài thuộc Topic người đó đang theo dõi; bài ẩn danh chỉ được giữ nếu thuộc Topic người đó đang theo dõi, không giữ nhờ việc theo dõi tác giả (BR-M06-15). |
| FR-M06-04.05 | Hệ thống phải sắp xếp kết quả bài theo Liên quan khi truy vấn có chữ và người dùng chưa chọn cách sắp xếp khác (BR-M06-15). |
| FR-M06-04.06 | Khi người dùng chọn sắp xếp Mới nhất, hệ thống phải xếp kết quả bài theo thời điểm đăng, bài đăng sau đứng trước (BR-M06-15). |
| FR-M06-04.07 | Khi người dùng chọn sắp xếp Nhiều upvote nhất, hệ thống phải xếp kết quả bài theo số upvote, bài nhiều upvote hơn đứng trước (BR-M06-15). |
| FR-M06-04.08 | Khi người dùng mở xem các bài của một Topic hay một Tag, hệ thống phải hiện trang kết quả tìm bài với bộ lọc Topic hay Tag đó và truy vấn rỗng (BR-M06-16). |
| FR-M06-04.09 | Khi người dùng đổi bộ lọc hoặc cách sắp xếp, hệ thống phải tính lại kết quả bài theo lựa chọn mới, vẫn áp các yêu cầu về hiển thị, xếp hạng và tải dần của FR-M06-02. |
| FR-M06-04.10 | Hệ thống phải cho chọn tối đa một giá trị cho mỗi loại bộ lọc: một Topic, một Tag, một khoảng thời gian. |
| FR-M06-04.11 | Khi người dùng dùng nhiều bộ lọc cùng lúc, hệ thống phải chỉ giữ những bài thỏa mọi bộ lọc đó. |
| FR-M06-04.12 | Hệ thống phải áp bộ lọc cho kết quả bài, không áp cho kết quả phụ người dùng, Tag, Topic, Group. |
| FR-M06-04.13 | Khi Guest bấm bộ lọc chỉ nội dung đang theo dõi, hệ thống phải hiện thông báo yêu cầu đăng nhập và không áp bộ lọc. |
| FR-M06-04.14 | Khi truy vấn có chữ và người dùng chọn Mới nhất hoặc Nhiều upvote nhất, hệ thống phải sắp lại chính tập ứng viên của truy vấn đó (BR-M06-15). |
| FR-M06-04.15 | Nếu hai bài bằng nhau theo cách sắp xếp Mới nhất hoặc Nhiều upvote nhất, hệ thống phải xếp bài đăng sau lên trước. |
| FR-M06-04.16 | Hệ thống phải không giảm hạng bài của tác giả ở mức HEAVY khi sắp xếp Mới nhất hoặc Nhiều upvote nhất (BR-M06-14). |
| FR-M06-04.17 | Khi truy vấn rỗng và có ít nhất một bộ lọc, hệ thống phải liệt kê mọi bài đang hiển thị công khai với người xem khớp bộ lọc, không giới hạn 120 kết quả (BR-M06-16). |
| FR-M06-04.18 | Khi truy vấn rỗng, hệ thống phải mặc định sắp xếp Mới nhất và không cho chọn sắp xếp Liên quan (BR-M06-16). |
| FR-M06-04.19 | Khi truy vấn rỗng, hệ thống phải không gọi AI. |
| FR-M06-04.20 | Hệ thống phải tính một lượt gửi mỗi khi người dùng đổi bộ lọc, đổi cách sắp xếp hoặc mở trang bài của một Topic hay Tag (BR-M06-21). |

### 5.5 FR-M06-05 Dùng lịch sử tìm kiếm

**Yêu cầu cấp trên:** Hệ thống phải lưu tối đa 10 truy vấn gần nhất trên trình duyệt của thiết bị đang dùng, hiện chúng khi người dùng đặt con trỏ vào ô tìm kiếm, cho chọn lại, xóa toàn bộ, và xóa lịch sử khi người dùng đăng xuất.

**Lý do:** Lịch sử chỉ lưu trên trình duyệt, không gắn với tài khoản, nên trên máy dùng chung người dùng sau có thể thấy truy vấn của người trước; xóa lịch sử khi đăng xuất để bảo vệ quyền riêng tư của học sinh.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M06-05.01 | Khi người dùng gửi truy vấn có chữ, hệ thống phải lưu truy vấn đó vào lịch sử tìm kiếm trên trình duyệt của thiết bị đang dùng. |
| FR-M06-05.02 | Hệ thống phải không lưu lịch sử tìm kiếm trên hệ thống và không gắn lịch sử với tài khoản (BR-M06-20). |
| FR-M06-05.03 | Nếu lịch sử đã có 10 truy vấn, khi lưu một truy vấn mới, hệ thống phải bỏ truy vấn cũ nhất. |
| FR-M06-05.04 | Khi người dùng đặt con trỏ vào ô tìm kiếm, hệ thống phải hiện lịch sử tìm kiếm, truy vấn gần nhất đứng trước. |
| FR-M06-05.05 | Khi người dùng bấm xóa lịch sử, hệ thống phải xóa toàn bộ lịch sử tìm kiếm trên trình duyệt đó. |
| FR-M06-05.06 | Hệ thống phải không thêm vào lịch sử khi người dùng chọn một mục trong danh sách gợi ý hoặc mở trang bài của một Topic hay Tag. |
| FR-M06-05.07 | Nếu truy vấn vừa gửi đã có trong lịch sử, hệ thống phải đưa truy vấn đó lên đầu lịch sử thay vì thêm bản trùng. |
| FR-M06-05.08 | Khi người dùng chọn một truy vấn trong lịch sử, hệ thống phải gửi ngay truy vấn đó. |
| FR-M06-05.09 | Hệ thống phải chỉ cho xóa toàn bộ lịch sử, không cho xóa từng truy vấn. |
| FR-M06-05.10 | Khi người dùng đăng xuất, hệ thống phải xóa toàn bộ lịch sử tìm kiếm trên trình duyệt đó. |

### 5.6 Quy tắc nghiệp vụ

| ID | Loại | Quy tắc | Ví dụ |
|---|---|---|---|
| BR-M06-01 | Sự kiện | Đối tượng tìm được gồm bài viết, người dùng, Tag, Topic, Group. Bình luận không tìm được. | — |
| BR-M06-02 | Ràng buộc | Tìm bài viết chỉ chạy khi gửi truy vấn, không chạy khi đang gõ. Người dùng, Tag, Topic, Group được gợi ý khi gõ và cũng được tìm khi gửi truy vấn. | Gõ "đạo hàm" rồi dừng: chỉ có gợi ý người dùng, Tag, Topic, Group, chưa có kết quả bài. Nhấn Enter: có kết quả bài và kết quả phụ. |
| BR-M06-03 | Kích hoạt | Gợi ý khi gõ chạy khi người dùng ngừng gõ 300 mili giây, từ ký tự đầu tiên. | Gõ "t" rồi dừng 300 mili giây: có gợi ý cho "t". Gõ "toa" lúc 10:00:00,000, gõ thêm "n" lúc 10:00:00,200: không gợi ý cho "toa". Không gõ gì tới 10:00:00,500: gợi ý cho "toan". |
| BR-M06-04 | Ràng buộc | Gợi ý khi gõ chỉ gồm người dùng, Tag, Topic, Group khớp với chuỗi đang gõ theo BR-M06-09, mỗi loại tối đa 3 mục; không gợi ý tiêu đề bài viết. | Gõ "toán": có thể gợi ý Topic Toán học, Tag #toánhình; bài "Toán hình 12 khó quá" không được gợi ý. Có 5 Tag khớp: chỉ hiện 3 Tag giống chuỗi gõ nhất. |
| BR-M06-05 | Suy diễn | Khi công tắc AI tổng và công tắc Search đều bật, bài viết của người đã đăng nhập được tìm theo ngữ nghĩa: so ý nghĩa của truy vấn với ý nghĩa của tiêu đề và nội dung chữ của bài. | User gõ "cách nhớ từ vựng lâu": ra được bài "Mẹo ghi nhớ tiếng Anh" dù bài không có chữ "từ vựng". |
| BR-M06-06 | Suy diễn | Khi công tắc AI tổng hoặc công tắc Search tắt, bài viết được tìm full-text theo từ khóa trên tiêu đề và nội dung chữ. | Tổng bật, Search bật: ngữ nghĩa (người đã đăng nhập). Tổng bật, Search tắt: full-text. Tổng tắt, Search bật: full-text. Tổng tắt, Search tắt: full-text. |
| BR-M06-07 | Suy diễn | Khi AI đang bật mà việc tạo embedding cho truy vấn thất bại sau hai lần thử (M13), riêng truy vấn đó được tìm full-text; truy vấn gửi sau vẫn tìm theo ngữ nghĩa. | Truy vấn lúc 10:00 lỗi cả hai lần: kết quả full-text. Truy vấn lúc 10:01, AI trả lời bình thường: kết quả ngữ nghĩa. |
| BR-M06-08 | Ràng buộc | Tìm full-text không phân biệt dấu tiếng Việt: dấu được bỏ ở cả truy vấn và nội dung bài trước khi so. Bài có ít nhất một từ của truy vấn trong tiêu đề hoặc nội dung chữ là khớp. | "phuong trinh", "phương trình", "phương trinh" đều khớp bài có chữ "phương trình". Truy vấn "phương trình bậc hai": bài chỉ có "bậc hai" vẫn khớp; bài không có từ nào trong 4 từ thì không khớp. |
| BR-M06-09 | Ràng buộc | Người dùng, Tag, Topic, Group khớp với chuỗi gõ khi chuỗi có ở bất kỳ vị trí nào trong tên, không phân biệt chữ hoa, chữ thường, bỏ dấu tiếng Việt khi so, và cho khớp gần đúng khi gõ sai nhẹ. Chỉ so với tên: người dùng theo display_name và username; Group theo tên, không theo mô tả. Trong mỗi loại, mục giống chuỗi gõ hơn đứng trước. | "Nam" khớp người dùng "Nguyễn Văn Nam". "toan" và "tóan" khớp Topic "Toán học". "hàm" khớp #đạo_hàm. "duc_pv" khớp username "Duc_PV". "HSG" không khớp Group "CLB Hóa học" dù mô tả có "ôn thi HSG". Gõ "Toán": Topic "Toán học" đứng trước Tag #toánhìnhkhônggian. |
| BR-M06-10 | Suy diễn | Tag bị vô hiệu hóa không xuất hiện trong gợi ý khi gõ và trong kết quả tìm Tag; Tag được kích hoạt lại thì xuất hiện lại. | #abc bị vô hiệu hóa: gõ "ab" không gợi ý #abc. #abc được kích hoạt lại: gõ "ab" gợi ý #abc. |
| BR-M06-11 | Ràng buộc | Kết quả bài chỉ gồm bài đang hiển thị công khai với người tìm. Bài trong nhóm Private chỉ có trong kết quả của thành viên nhóm đó; nhóm đổi từ Public sang Private thì từ lúc đổi, kết quả tìm của người không phải thành viên không còn bài của nhóm. | Bài nháp, chờ duyệt, tự ẩn, đã xóa: không có trong kết quả. Bài trong nhóm Private X: thành viên X thấy, Guest và người ngoài X không thấy. Nhóm Y đổi sang Private lúc 10:00: người ngoài Y tìm lúc 10:05 không thấy bài của Y. |
| BR-M06-12 | Suy diễn | Bài của tài khoản BANNED vẫn có trong kết quả như bài khác, không bị loại, không bị giảm hạng; tên tác giả hiện kèm nhãn "Tài khoản đã bị khóa". | — |
| BR-M06-13 | Tính toán | Với truy vấn có chữ: tập ứng viên là 120 bài có Điểm liên quan cao nhất. Điểm liên quan khi tìm ngữ nghĩa = (độ tương đồng cosine giữa embedding truy vấn và embedding bài + 1) ÷ 2; khi tìm full-text = số từ của truy vấn có trong bài ÷ số từ của truy vấn. Điểm tương tác thô = log(1 + số upvote) × 2 + log(1 + số bình luận) × 1. Điểm tương tác = (thô − thô nhỏ nhất) ÷ (thô lớn nhất − thô nhỏ nhất) trong tập ứng viên; mọi ứng viên cùng điểm thô thì Điểm tương tác của tất cả bằng 0. Điểm cuối = Điểm liên quan × 0,8 + Điểm tương tác × 0,2. Sắp xếp theo Liên quan: Điểm cuối giảm dần; bằng nhau thì Điểm liên quan cao hơn trước, vẫn bằng thì bài đăng sau trước. | Ngữ nghĩa: độ tương đồng 0,8 → Điểm liên quan 0,9. Full-text: "phương trình bậc hai", bài có cả 4 từ → 1,0; bài có "phương trình" → 0,5. Tập ứng viên có A (thô 3, liên quan 0,9), B (thô 1, 0,9), C (thô 5, 0,7): Điểm tương tác A 0,5, B 0, C 1; Điểm cuối A 0,82, C 0,76, B 0,72 → thứ tự A, C, B. Hai bài cùng Điểm cuối 0,80, liên quan 0,9 và 0,8: bài 0,9 trước. |
| BR-M06-14 | Tính toán | Khi sắp xếp theo Liên quan, Điểm cuối của bài có tác giả đang ở mức HEAVY được nhân với 0,5, ở cả tìm ngữ nghĩa và full-text, trong suốt thời gian tác giả ở mức đó; mức LIGHT, MEDIUM không bị. Sắp xếp Mới nhất, Nhiều upvote nhất không giảm hạng. Kết quả không hiện dấu hiệu nào cho thấy bài bị giảm hạng. | Ở ví dụ BR-M06-13, tác giả của A đang ở mức HEAVY: A còn 0,82 × 0,5 = 0,41 → thứ tự C, B, A. Cùng truy vấn, sắp xếp Mới nhất: A vẫn ở vị trí theo thời điểm đăng. |
| BR-M06-15 | Ràng buộc | Bộ lọc kết quả bài: Topic, Tag, khoảng thời gian (Hôm nay, Tuần này, Tháng này, Tất cả), chỉ nội dung đang theo dõi; mỗi loại chọn tối đa một giá trị; nhiều bộ lọc thì bài phải thỏa tất cả; bộ lọc không áp cho kết quả phụ. Hôm nay, Tuần này, Tháng này tính theo lịch giờ Việt Nam trên thời điểm đăng. "Đang theo dõi" gồm bài của người dùng đang theo dõi và bài thuộc Topic đang theo dõi. Bài ẩn danh chỉ được giữ nếu thuộc Topic đang theo dõi, không giữ nhờ việc theo dõi tác giả (như tab Following, M14). Cách sắp xếp: Liên quan (mặc định khi truy vấn có chữ), Mới nhất (thời điểm đăng, mới trước), Nhiều upvote nhất (số upvote, nhiều trước); với truy vấn có chữ, Mới nhất và Nhiều upvote nhất sắp lại chính tập ứng viên; bằng nhau thì bài đăng sau trước. | Thứ Tư 15/10 lúc 10:00: Hôm nay = đăng từ 15/10 00:00; Tuần này = từ thứ Hai 13/10 00:00; Tháng này = từ 01/10 00:00. Lọc Toán học + #đạohàm + Tuần này: bài phải đủ cả ba. User theo dõi Minh và Topic Tin học: bài của Minh ở Ngữ văn và bài của người khác ở Tin học đều qua bộ lọc. A đăng 09:00, B đăng 11:00: Mới nhất xếp B trên A. A có 5 upvote, B có 3: Nhiều upvote nhất xếp A trên B; cùng 5 upvote thì bài đăng sau trước. Theo dõi B và Topic Toán: bài ẩn danh của B trong nhóm Public gắn Topic Văn → bị loại; gắn Topic Toán → được giữ, hiện ẩn danh. |
| BR-M06-16 | Suy diễn | Xem các bài của một Topic hoặc một Tag là trang kết quả tìm bài với bộ lọc Topic hoặc Tag đó và truy vấn rỗng. Truy vấn rỗng có ít nhất một bộ lọc: liệt kê mọi bài khớp bộ lọc, mặc định Mới nhất, đổi được sang Nhiều upvote nhất, không có Liên quan, không giới hạn 120 kết quả, không gọi AI. Truy vấn rỗng không có bộ lọc: không tìm. | Bấm Topic "Toán học" có 300 bài: liệt kê cả 300, mới nhất trước, cuộn tới bài cuối. Đang ở trang đó gõ "đạo hàm" rồi Enter: tìm bình thường trong Toán học, có giới hạn 120. Gửi ô trống, chỉ chọn "Tuần này": liệt kê mọi bài đăng tuần này. Gửi ô trống không có bộ lọc: không tìm. |
| BR-M06-17 | Ràng buộc | Trang kết quả là một trang cuộn, không chia tab. Kết quả bài là kết quả chính, theo cách sắp xếp đang chọn; người dùng, Tag, Topic, Group là kết quả phụ, mỗi loại tối đa 3. | Truy vấn "toán" khớp 40 bài, 7 người dùng, 2 Tag, 1 Topic, 0 Group: trang có kết quả bài, 3 người dùng, 2 Tag, 1 Topic. |
| BR-M06-18 | Ràng buộc | Mỗi kết quả bài có đoạn trích là 150 ký tự đầu của nội dung chữ, không tô sáng từ khóa, như nhau khi tìm theo ngữ nghĩa và full-text. Nếu ký tự thứ 150 nằm giữa một từ thì cắt trước từ đó và thêm "…". Nội dung chữ không quá 150 ký tự thì hiện nguyên, không thêm "…". Bài không có nội dung chữ thì không có đoạn trích. | Nội dung 400 ký tự, ký tự 150 nằm giữa từ "phương" (ký tự 146–151): đoạn trích là 145 ký tự đầu + "…". Nội dung 120 ký tự: hiện cả 120 ký tự. Bài chỉ có poll: không có đoạn trích. |
| BR-M06-19 | Ràng buộc | Kết quả bài được tải dần khi cuộn, 15 kết quả mỗi lần. Với truy vấn có chữ, tối đa 120 kết quả (8 lần tải); đã có 120 kết quả mà người dùng cuộn tiếp thì hệ thống hiện "Thu hẹp tìm kiếm để có kết quả chính xác hơn". Các lần tải sau không lặp lại hay bỏ sót kết quả của lần trước. | Có 50 kết quả: tải 15, 15, 15, 5 (4 lần), không hiện thông báo. Tập ứng viên đủ 120: sau lần tải thứ 8, cuộn tiếp thì hiện thông báo, không tải thêm. |
| BR-M06-20 | Ràng buộc | Lịch sử tìm kiếm lưu trên trình duyệt của thiết bị đang dùng, không lưu trên hệ thống, không gắn với tài khoản. Lịch sử giữ tối đa 10 truy vấn có chữ gần nhất, mới nhất trước, không có bản trùng; chỉ thêm khi gửi truy vấn có chữ; chọn một mục thì gửi ngay truy vấn đó; chỉ xóa được toàn bộ; bị xóa toàn bộ khi người dùng đăng xuất. | Lịch sử có 10 truy vấn; gửi truy vấn thứ 11: truy vấn cũ nhất bị bỏ, còn 10. Gửi lại "đạo hàm" đang ở vị trí 5: "đạo hàm" lên đầu, vẫn 10 mục. Chọn một gợi ý Topic: lịch sử không đổi. Đăng xuất: còn 0. |
| BR-M06-21 | Ràng buộc | Giới hạn tần suất tính trong 60 giây gần nhất. Guest tính theo địa chỉ IP: tối đa 30 lượt gợi ý và 10 lượt gửi; người đã đăng nhập (User, Mod, Admin) tính theo tài khoản: tối đa 45 lượt gợi ý và 20 lượt gửi. Lượt gửi gồm gửi truy vấn, đổi bộ lọc, đổi cách sắp xếp, mở trang bài của Topic hay Tag, chọn một mục lịch sử; tải thêm khi cuộn không tính. Vượt giới hạn thì yêu cầu đó bị từ chối với thông báo quá nhiều yêu cầu; không có captcha, không chặn lâu dài. | User gửi 20 lần trong 10:00:00–10:00:40: đều được; lần thứ 21 lúc 10:00:45: bị từ chối; lúc 10:01:01, lượt đầu tiên (10:00:00) đã ra khỏi 60 giây gần nhất: được. Cuộn tải thêm 7 lần: không tính lượt. Guest đổi sắp xếp là lượt gửi thứ 11 trong 60 giây: bị từ chối. Hai Guest khác IP: mỗi người được 10 lượt gửi. |
| BR-M06-22 | Sự kiện | AI tắt hoặc lỗi chỉ đổi cách tìm bài viết; gợi ý khi gõ và tìm người dùng, Tag, Topic, Group không dùng AI nên chạy như nhau dù AI bật hay tắt. | — |
| BR-M06-23 | Ràng buộc | Guest luôn tìm bài bằng full-text. Chỉ Guest thấy lựa chọn "Tìm kiếm thông minh"; bấm vào thì hiện thông báo yêu cầu đăng nhập, kết quả vẫn là full-text, kể cả khi công tắc AI đang tắt. Bộ lọc chỉ nội dung đang theo dõi cũng hiện với Guest và bấm vào thì hiện cùng thông báo. Người đã đăng nhập không có lựa chọn bật, tắt tìm kiếm thông minh. | Guest gõ "cách nhớ từ vựng lâu": kết quả full-text. Guest bấm "Tìm kiếm thông minh": thông báo yêu cầu đăng nhập. Admin tắt công tắc Search, Guest bấm: vẫn chỉ thông báo yêu cầu đăng nhập. User đăng nhập: không thấy lựa chọn này, kết quả ngữ nghĩa khi AI bật. |
| BR-M06-24 | Ràng buộc | Tìm người dùng (gợi ý khi gõ và kết quả phụ) chỉ gồm tài khoản ACTIVE đã xong Bước 3 đăng ký. | Gõ "Lan" khớp Lan A (ACTIVE), Lan B (BANNED), Lan C (DEACTIVATED), Lan D (DELETED), Lan E (ACTIVE, chưa xong Bước 3): chỉ hiện Lan A. |
| BR-M06-25 | Ràng buộc | Nhóm Private không xuất hiện trong gợi ý khi gõ và kết quả tìm Group với người không là thành viên, kể cả Guest; thành viên của nhóm vẫn tìm thấy nhóm. | Nhóm Private "Ôn thi HSG Toán 12": người ngoài nhóm gõ "HSG Toán": không thấy. Guest gõ: không thấy. Thành viên gõ: thấy. |

### 5.7 Dữ liệu nghiệp vụ

| Thực thể | Thuộc tính nguồn đã nêu | Quan hệ |
|---|---|---|
| Truy vấn tìm kiếm | Chuỗi truy vấn; bộ lọc (Topic, Tag, khoảng thời gian, chỉ nội dung đang theo dõi); cách sắp xếp; người tìm (Guest: địa chỉ IP; người đã đăng nhập: tài khoản); cách tìm bài (ngữ nghĩa hoặc full-text) | Sinh ra một Kết quả tìm kiếm; không lưu trên hệ thống |
| Kết quả tìm kiếm | Kết quả bài (bài viết, Điểm liên quan, Điểm tương tác, Điểm cuối, đoạn trích), tối đa 120; kết quả phụ người dùng, Tag, Topic, Group, mỗi loại tối đa 3 | Thuộc một Truy vấn tìm kiếm; trỏ tới Bài viết (M03), Người dùng (M01), Tag, Topic (M05), Group (M11) |
| Danh sách gợi ý | Chuỗi đang gõ; người dùng, Tag, Topic, Group khớp | Không lưu trên hệ thống |
| Mục lịch sử tìm kiếm | Chuỗi truy vấn; thứ tự gần đây | Lưu trên trình duyệt của thiết bị, tối đa 10 mục, không trùng; không thuộc tài khoản nào; bị xóa toàn bộ khi đăng xuất |
| Lượt tìm kiếm (để tính giới hạn) | Loại (lượt gợi ý hoặc lượt gửi); người tìm (địa chỉ IP hoặc tài khoản); thời điểm | Dùng để áp giới hạn tần suất |

Thực thể của module khác mà M06 chỉ đọc: Bài viết và nội dung chữ (M03), embedding bài và truy vấn (M13), Người dùng
(M01), Tag và Topic (M05), Group và thành viên nhóm (M11), quan hệ theo dõi (M07), mức cảnh cáo (M08), upvote (M12),
số bình luận (M04).

**Ma trận CRUD:**

| Thực thể | Tạo | Đọc | Sửa | Xóa |
|---|---|---|---|---|
| Truy vấn tìm kiếm | FR-M06-02.01, FR-M06-03.01 | FR-M06-02.01, FR-M06-03.01 | FR-M06-04.09 | Không có (không lưu trên hệ thống) |
| Kết quả tìm kiếm | FR-M06-02.01, FR-M06-03.01 | FR-M06-02.16, FR-M06-03.02 | FR-M06-04.09, FR-M06-02.17 | Không có (không lưu trên hệ thống) |
| Danh sách gợi ý | FR-M06-01.01 | FR-M06-01.01 | Không có | Không có (không lưu trên hệ thống) |
| Mục lịch sử tìm kiếm | FR-M06-05.01 | FR-M06-05.04 | FR-M06-05.07 (đưa lên đầu) | FR-M06-05.05, FR-M06-05.10 (xóa toàn bộ); FR-M06-05.03 (bỏ mục cũ nhất); xóa từng mục: Không có (FR-M06-05.09) |
| Lượt tìm kiếm (để tính giới hạn) | FR-M06-01.07, FR-M06-02.20, FR-M06-04.20 | FR-M06-01.07, FR-M06-02.20 | Không có | Không có (chỉ dùng trong cửa sổ đếm, BR-M06-21) |

### 5.8 Chuyển trạng thái

Không áp dụng: nguồn không nêu trạng thái cho thực thể nào của M06. Trạng thái của bài viết, Tag, tài khoản và nhóm do
M03, M05, M01, M11 quản lý; M06 chỉ đọc các trạng thái đó.

### 5.9 Giao tiếp với module khác

| Hướng | Module | Nội dung ở mức nghiệp vụ | Yêu cầu |
|---|---|---|---|
| Dùng | M01 | Người dùng (display_name, username) với cách khớp tên dùng chung với danh sách gợi ý nhắc tên; trạng thái tài khoản và việc đã xong Bước 3; tài khoản BANNED; sự kiện đăng xuất | FR-M06-01.05, FR-M06-03.03, FR-M06-01.12, FR-M06-03.07, FR-M06-02.13, FR-M06-02.14, FR-M06-05.10 |
| Dùng | M03 | Bài đang hiển thị công khai; tiêu đề, nội dung chữ và thời điểm đăng của bài | FR-M06-02.07, FR-M06-02.03, FR-M06-02.04, FR-M06-04.06 |
| Dùng | M04 | Số bình luận của bài để tính Điểm tương tác | FR-M06-02.10 |
| Dùng | M05 | Topic, Tag và trạng thái hoạt động, bị vô hiệu hóa của Tag | FR-M06-01.04, FR-M06-03.04, FR-M06-04.01, FR-M06-04.02 |
| Dùng | M07 | Quan hệ theo dõi (người dùng, Topic) của người tìm | FR-M06-04.04 |
| Dùng | M08 | Mức cảnh cáo HEAVY của tác giả | FR-M06-02.11 |
| Dùng | M10 | Công tắc AI tổng và công tắc Search | FR-M06-02.03, FR-M06-02.04 |
| Dùng | M11 | Nhóm, loại nhóm (Public, Private), thành viên nhóm, việc nhóm đổi từ Public sang Private; Mod, Admin không là thành viên cũng không thấy nhóm Private; khi cờ Group tắt, nhóm và bài nhóm vẫn hiện trong kết quả, mở ra thì báo hệ thống đang bận (M11 sở hữu) | FR-M06-02.08, FR-M06-02.09, FR-M06-03.01, FR-M06-03.08, FR-M06-01.13 |
| Dùng | M12 | Số upvote của bài; nhãn "Tài khoản đã bị khóa" | FR-M06-02.10, FR-M06-04.07, FR-M06-02.14 |
| Dùng | M13 | Embedding của truy vấn và của bài; báo AI lỗi để tìm full-text | FR-M06-02.03, FR-M06-02.05 |
| Cung cấp | M05 | Xem các bài của một Topic hay một Tag qua bộ lọc | FR-M06-04.08 |
| Cung cấp | M10 | Cách khớp tên người dùng (username, display_name ở bất kỳ vị trí, bỏ dấu, chấp nhận gõ sai nhẹ), dùng lại cho tìm người dùng trong Admin Panel | BR-M06-09 |
| Cung cấp | M13 | Truy vấn tìm bài của người dùng đã đăng nhập; giới hạn tần suất tìm kiếm | FR-M06-02.03, FR-M06-02.20 |
| Cung cấp | M14 | Trang tìm kiếm mà tab Following rỗng dẫn người dùng tới | FR-M06-02.01 |

### 5.10 AI hỗ trợ và hành vi khi tắt AI

- Khi công tắc AI tổng và công tắc Search đều bật, bài viết của người đã đăng nhập được tìm theo ngữ nghĩa: FR-M06-02.03, xếp hạng FR-M06-02.10. Guest luôn tìm full-text và được nhắc đăng nhập khi bấm "Tìm kiếm thông minh": FR-M06-02.23, FR-M06-02.25.
- Khi một trong hai công tắc tắt, bài viết được tìm bằng full-text: FR-M06-02.04, FR-M06-02.06, FR-M06-02.26, xếp hạng FR-M06-02.27.
- Khi AI lỗi với một truy vấn, riêng truy vấn đó được tìm bằng full-text: FR-M06-02.05.
- Gợi ý khi gõ, tìm người dùng, Tag, Topic, Group và xem bài khi truy vấn rỗng không dùng AI, chạy như nhau khi AI tắt: FR-M06-01.08, FR-M06-03.05, FR-M06-04.19.

### 5.11 Yêu cầu HMI

Chưa có — chờ giai đoạn thiết kế.

### 5.12 Chuyển màn hình

Chưa có — chờ giai đoạn thiết kế.

## 6. Lịch sử sửa đổi

| Phiên bản | Ngày | Nội dung | Người sửa |
|---|---|---|---|
| 0.1 | 2026-10-19 | Tạo mới | Phạm Văn Đức |
| 1.0 | 2026-10-20 | Chốt sau 7 bước; câu trả lời ghi vào register (DEC-208–213) | Phạm Văn Đức |
| 1.1 | 2026-10-20 | Đối chiếu sau khi chốt: @mention của M01 dùng cùng cách khớp tên (DEC-214); giao tiếp M01 thêm sự kiện đăng xuất. Chốt bản 1.1 | Phạm Văn Đức |
| 1.2 | 2026-10-21 | Đối chiếu với FR-M07 (DEC-215): bộ lọc "đang theo dõi" chỉ gồm bài của người dùng và bài thuộc Topic đang theo dõi, bỏ "bài đang theo dõi" (FR-M06-04.04, BR-M06-15, 2.1, C.2). Chốt bản 1.2 | Phạm Văn Đức |
| 1.3 | 2026-10-21 | Đối chiếu với FR-M10 (DEC-228): thêm dòng "Cung cấp M10" (cách khớp tên người dùng dùng lại ở Admin Panel); C.1. Không đổi yêu cầu. Chốt bản 1.3 | Phạm Văn Đức |
| 1.4 | 2026-10-21 | Đối chiếu với FR-M11 (DEC-233, DEC-236): "Dùng M11" ghi thêm Mod, Admin không là thành viên không thấy nhóm Private; hành vi khi cờ Group tắt (M11 sở hữu); không đổi yêu cầu. Chốt bản 1.4 | Phạm Văn Đức |
| 1.5 | 2026-10-24 | Đối chiếu với FR-M14 (DEC-263): bộ lọc chỉ nội dung đang theo dõi không giữ bài ẩn danh nhờ việc theo dõi tác giả, chỉ giữ nhờ Topic đang theo dõi (FR-M06-04.04, BR-M06-15). Chốt bản 1.5 | Phạm Văn Đức |

## Phụ lục A. Truy vết

| ID | Nguồn | Căn cứ | Ghi chú |
|---|---|---|---|
| FR-M06-01 | DEC-054, DEC-058, DEC-057, DEC-062, DEC-063, DEC-209, DEC-210 | Nói thẳng | — |
| FR-M06-01.01 | DEC-054, DEC-058, DEC-209 | Nói thẳng | — |
| FR-M06-01.02 | DEC-054 | Suy ra | "debounce (300ms)": chỉ gợi ý khi đã ngừng gõ đủ 300 mili giây ⇒ chuỗi bị gõ tiếp không được gợi ý |
| FR-M06-01.03 | DEC-058 | Nói thẳng | — |
| FR-M06-01.04 | DEC-051, DEC-143 | Nói thẳng | — |
| FR-M06-01.05 | DEC-053, DEC-209 | Nói thẳng | — |
| FR-M06-01.06 | DEC-062, DEC-063, DEC-208 | Nói thẳng | — |
| FR-M06-01.07 | DEC-063, DEC-213 | Nói thẳng | — |
| FR-M06-01.08 | DEC-053, DEC-057, DEC-008 | Suy ra | Như BR-M06-22 |
| FR-M06-01.09 | DEC-209 | Nói thẳng | — |
| FR-M06-01.10 | DEC-209 | Nói thẳng | — |
| FR-M06-01.11 | DEC-209 | Nói thẳng | — |
| FR-M06-01.12 | DEC-209 | Nói thẳng | — |
| FR-M06-01.13 | DEC-210, DEC-110 | Nói thẳng | — |
| FR-M06-02 | DEC-053, DEC-054, DEC-055, DEC-057, DEC-060, DEC-061, DEC-062, DEC-064, DEC-008, DEC-099, DEC-079, DEC-108, DM-11.3, DM-7.3, DG-6, QA-011, DEC-208, DEC-211, DEC-213 | Nói thẳng | — |
| FR-M06-02.01 | DEC-054, DEC-053 | Nói thẳng | — |
| FR-M06-02.02 | DEC-054 | Nói thẳng | — |
| FR-M06-02.03 | DEC-053, DM-11.3, DG-6, DEC-093, DEC-205, DEC-208 | Nói thẳng | — |
| FR-M06-02.04 | DEC-008, DEC-053, DEC-057, DEC-093 | Nói thẳng | — |
| FR-M06-02.05 | DEC-099 | Nói thẳng | — |
| FR-M06-02.06 | DEC-057 | Nói thẳng | — |
| FR-M06-02.07 | DEC-062 | Suy ra | DEC-062 "same as public browse" ⇒ kết quả theo đúng quy tắc hiển thị bài của M03 |
| FR-M06-02.08 | DEC-062, DEC-210 | Nói thẳng | — |
| FR-M06-02.09 | DEC-108 | Nói thẳng | — |
| FR-M06-02.10 | DEC-055, DEC-211, QA-112 | Nói thẳng | — |
| FR-M06-02.11 | DEC-079, DEC-211 | Nói thẳng | — |
| FR-M06-02.12 | DEC-079 | Suy ra | Trạng thái cảnh cáo "fully PRIVATE" (DEC-079) ⇒ kết quả tìm không được để lộ việc giảm hạng |
| FR-M06-02.13 | DEC-122 | Suy ra | Như BR-M06-12 |
| FR-M06-02.14 | DEC-122 | Suy ra | DEC-122: nhãn hiện "everywhere the banned user's name appears" ⇒ gồm cả kết quả tìm |
| FR-M06-02.15 | DEC-061, DEC-213, QA-118 | Nói thẳng | — |
| FR-M06-02.16 | DEC-060 | Nói thẳng | — |
| FR-M06-02.17 | DEC-064 | Nói thẳng | — |
| FR-M06-02.18 | DEC-064 | Suy ra | "cursor-based (not offset)" ⇒ lần tải sau tiếp đúng sau kết quả cuối của lần trước |
| FR-M06-02.19 | DEC-064, DEC-211 | Nói thẳng | — |
| FR-M06-02.20 | DEC-063, DEC-213, QA-121 | Nói thẳng | — |
| FR-M06-02.21 | DEC-063 | Nói thẳng | — |
| FR-M06-02.22 | DEC-053 | Nói thẳng | — |
| FR-M06-02.23 | DEC-208, QA-011 | Nói thẳng | — |
| FR-M06-02.24 | DEC-208 | Nói thẳng | — |
| FR-M06-02.25 | DEC-208 | Nói thẳng | — |
| FR-M06-02.26 | DEC-211 | Nói thẳng | — |
| FR-M06-02.27 | DEC-211 | Nói thẳng | — |
| FR-M06-02.28 | DEC-211, DEC-055 | Nói thẳng | — |
| FR-M06-02.29 | DEC-211 | Nói thẳng | — |
| FR-M06-02.30 | DEC-213 | Nói thẳng | — |
| FR-M06-02.31 | DEC-212 | Nói thẳng | — |
| FR-M06-02.32 | DEC-213 | Nói thẳng | — |
| FR-M06-03 | DEC-053, DEC-054, DEC-060, DEC-062, QA-035, QA-036, QA-044, QA-120, DEC-110, DEC-209, DEC-210 | Nói thẳng | — |
| FR-M06-03.01 | DEC-053, DEC-054 | Nói thẳng | — |
| FR-M06-03.02 | DEC-060 | Nói thẳng | — |
| FR-M06-03.03 | DEC-053, DEC-209 | Nói thẳng | — |
| FR-M06-03.04 | DEC-051, DEC-143 | Suy ra | Như BR-M06-10 |
| FR-M06-03.05 | DEC-053, DEC-057, DEC-008 | Suy ra | Như BR-M06-22 |
| FR-M06-03.06 | DEC-209 | Nói thẳng | — |
| FR-M06-03.07 | DEC-209 | Nói thẳng | — |
| FR-M06-03.08 | DEC-210, DEC-110 | Nói thẳng | — |
| FR-M06-03.09 | DEC-210 | Nói thẳng | — |
| FR-M06-03.10 | DEC-209 | Nói thẳng | — |
| FR-M06-04 | DEC-056, DEC-142, DEC-208, DEC-211, DEC-212, DEC-213 | Nói thẳng | — |
| FR-M06-04.01 | DEC-056 | Nói thẳng | — |
| FR-M06-04.02 | DEC-056 | Nói thẳng | — |
| FR-M06-04.03 | DEC-056, DEC-212, DEC-127 | Nói thẳng | — |
| FR-M06-04.04 | DEC-056, DEC-212, DEC-215, DEC-263 | Nói thẳng | — |
| FR-M06-04.05 | DEC-056 | Nói thẳng | — |
| FR-M06-04.06 | DEC-056 | Nói thẳng | — |
| FR-M06-04.07 | DEC-056 | Nói thẳng | — |
| FR-M06-04.08 | DEC-142, DEC-212 | Nói thẳng | — |
| FR-M06-04.09 | DEC-056, DEC-060 | Suy ra | Bộ lọc, sắp xếp áp cho kết quả bài (DEC-056 "Filters (Post search)") ⇒ kết quả sau khi lọc vẫn theo cùng quy tắc của tìm bài |
| FR-M06-04.10 | DEC-212 | Nói thẳng | — |
| FR-M06-04.11 | DEC-212 | Nói thẳng | — |
| FR-M06-04.12 | DEC-212 | Nói thẳng | — |
| FR-M06-04.13 | DEC-208 | Nói thẳng | — |
| FR-M06-04.14 | DEC-211 | Nói thẳng | — |
| FR-M06-04.15 | DEC-211 | Nói thẳng | — |
| FR-M06-04.16 | DEC-211 | Nói thẳng | — |
| FR-M06-04.17 | DEC-212 | Nói thẳng | — |
| FR-M06-04.18 | DEC-212 | Nói thẳng | — |
| FR-M06-04.19 | DEC-212 | Nói thẳng | — |
| FR-M06-04.20 | DEC-213 | Nói thẳng | — |
| FR-M06-05 | DEC-059, DEC-213 | Nói thẳng | — |
| FR-M06-05.01 | DEC-059, DEC-213 | Nói thẳng | — |
| FR-M06-05.02 | DEC-059 | Suy ra | Như BR-M06-20 |
| FR-M06-05.03 | DEC-059 | Suy ra | "Max 10 recent searches" ⇒ giữ 10 truy vấn gần nhất, bỏ truy vấn cũ nhất |
| FR-M06-05.04 | DEC-059, DEC-213 | Nói thẳng | — |
| FR-M06-05.05 | DEC-059 | Nói thẳng | — |
| FR-M06-05.06 | DEC-213 | Nói thẳng | — |
| FR-M06-05.07 | DEC-213 | Nói thẳng | — |
| FR-M06-05.08 | DEC-213 | Nói thẳng | — |
| FR-M06-05.09 | DEC-213 | Nói thẳng | — |
| FR-M06-05.10 | DEC-213 | Nói thẳng | — |
| BR-M06-01 | DEC-053 | Nói thẳng | — |
| BR-M06-02 | DEC-054 | Nói thẳng | — |
| BR-M06-03 | DEC-054, DEC-209 | Nói thẳng | — |
| BR-M06-04 | DEC-058, DEC-209 | Nói thẳng | — |
| BR-M06-05 | DEC-053, DM-11.3, DG-6, DEC-093, DEC-205, DEC-208 | Nói thẳng | — |
| BR-M06-06 | DEC-008, DEC-053, DEC-057, DEC-093 | Nói thẳng | — |
| BR-M06-07 | DEC-099 | Nói thẳng | — |
| BR-M06-08 | DEC-057, DEC-211 | Nói thẳng | — |
| BR-M06-09 | DEC-209, DEC-053, QA-036 | Nói thẳng | — |
| BR-M06-10 | DEC-051, DEC-143 | Suy ra | Nguồn nói ẩn khỏi autocomplete và browse ⇒ kết quả tìm Tag cũng không có Tag bị vô hiệu hóa |
| BR-M06-11 | DEC-062, DEC-108, DEC-110, DEC-210 | Suy ra | DEC-062 "same as public browse" ⇒ chỉ bài đang hiển thị công khai theo M03; phần nhóm Private nói thẳng |
| BR-M06-12 | DEC-122 | Suy ra | DEC-122: bài của tài khoản BANNED "remain visible to other users as normal", nhãn ở mọi nơi tên hiện ⇒ có trong kết quả, không giảm hạng |
| BR-M06-13 | DEC-055, DEC-211, QA-112 | Nói thẳng | — |
| BR-M06-14 | DEC-079, DEC-211 | Nói thẳng | "Không hiện dấu hiệu" suy từ việc trạng thái cảnh cáo hoàn toàn riêng tư (DEC-079) |
| BR-M06-15 | DEC-056, DEC-211, DEC-212, DEC-127, DEC-215, DEC-263 | Nói thẳng | — |
| BR-M06-16 | DEC-142, DEC-212 | Nói thẳng | — |
| BR-M06-17 | DEC-060 | Nói thẳng | — |
| BR-M06-18 | DEC-061, DEC-213, QA-118 | Nói thẳng | — |
| BR-M06-19 | DEC-064, DEC-211 | Suy ra | Câu "không lặp lại hay bỏ sót" suy từ "cursor-based (not offset)"; phần còn lại nói thẳng |
| BR-M06-20 | DEC-059, DEC-213 | Suy ra | "Không gắn với tài khoản" suy từ "localStorage only (no DB)"; phần còn lại nói thẳng |
| BR-M06-21 | DEC-063, DEC-213, QA-121 | Suy ra | Nguồn ghi "User (by user_id)" ⇒ Mod, Admin dùng mức của người đã đăng nhập; phần còn lại nói thẳng |
| BR-M06-22 | DEC-053, DEC-057, DEC-008 | Suy ra | Người dùng, Tag, Topic, Group tìm bằng khớp chuỗi, không qua embedding; dự phòng khi tắt AI chỉ nói cho bài viết ⇒ phần khác không đổi |
| BR-M06-23 | DEC-208, QA-011 | Nói thẳng | — |
| BR-M06-24 | DEC-209 | Nói thẳng | — |
| BR-M06-25 | DEC-210, DEC-110 | Nói thẳng | — |

## Phụ lục B. Câu hỏi, giả định và TBD

### B.1 Câu hỏi đã hỏi

| Mã | Loại | Câu hỏi | Trả lời | Ghi vào register |
|---|---|---|---|---|
| Q-01 | Mâu thuẫn | DEC-062 cho Guest "search normally (same as public browse)", QA-011 ghi Guest "Semantic Search: Không" (bảo vệ chi phí AI). Guest tìm bài theo ngữ nghĩa như User, hay chỉ tìm full-text theo từ khóa? | Guest tìm bài bằng full-text. Chỉ Guest thấy "Tìm kiếm thông minh" (tên hiển thị của tìm kiếm ngữ nghĩa); bấm thì nhắc đăng nhập, kể cả khi AI tắt. Người đã đăng nhập luôn tìm ngữ nghĩa khi AI bật. | QA-393, DEC-208 |
| Q-02 | Mâu thuẫn | QA-036 chọn so khớp chuỗi con cho tên người dùng ("Nam" phải ra "Nguyễn Văn Nam"), DEC-053 ghi User "exact/prefix match". Tìm User khớp cả phần giữa tên, hay chỉ phần đầu? | Khớp ở bất kỳ vị trí trong tên (giữ QA-036), không phân biệt hoa thường, bỏ dấu, gần đúng. | QA-394, DEC-209 |
| Q-03 | Mâu thuẫn | DEC-062, DEC-053, QA-044, QA-120 cho nhóm Private hiện trong kết quả tìm Group (tên, mô tả; nội dung khóa); DEC-110, QA-188 (sau, ở M11) ghi nhóm Private "fully hidden from search/discovery", chỉ vào qua lời mời/link. Nhóm Private có hiện trong kết quả tìm không? | Ẩn hoàn toàn với người không là thành viên, kể cả Guest; thành viên vẫn tìm thấy nhóm. | QA-395, DEC-210 |
| Q-04 | Thiếu chi tiết | Bộ lọc "Following-only" (DEC-056) lọc bài theo người, đối tượng đang theo dõi; Guest không theo dõi được ai (QA-011: không có tương tác). Với Guest, bộ lọc này bị ẩn, hay vẫn hiện và yêu cầu đăng nhập khi bấm (như tab Following của M14, QA-227)? | Bộ lọc vẫn hiện với Guest; bấm thì nhắc đăng nhập. | QA-402, DEC-208 |
| Q-05 | Mơ hồ | Tìm full-text (DEC-057: "to_tsvector(... title || content_text)") khi truy vấn có nhiều từ: bài phải chứa mọi từ hay chỉ cần một từ? Kết quả full-text xếp thế nào, khi Điểm liên quan của DEC-055 là "cosine similarity from embedding" và không có ở chế độ này? | Bài có ít nhất một từ là khớp; Điểm liên quan = tỷ lệ từ khớp; dùng chung công thức 0,8/0,2. | QA-396, DEC-211 |
| Q-06 | Thiếu chi tiết | Gợi ý khi gõ (DEC-058): phải gõ tối thiểu bao nhiêu ký tự mới gợi ý? Mỗi loại (người dùng, Tag, Topic, Group) hiện tối đa bao nhiêu mục? | Gợi ý từ ký tự đầu tiên; mỗi loại tối đa 3 mục. | QA-402, DEC-209 |
| Q-07 | Mơ hồ | Tag, Topic, Group khớp thế nào: DEC-053 ghi "exact/prefix match", DEC-057 ghi "prefix/fuzzy match". Chỉ khớp phần đầu, hay khớp gần đúng (gõ sai chính tả); có bỏ dấu không; Group có khớp mô tả không? Trong mỗi loại kết quả phụ (tối đa 3) xếp theo thứ tự nào? (Hỏi cùng Q-02 ở bước 6.) | Như Q-02 cho Tag, Topic, Group; chỉ so tên, Group không so mô tả; giống chuỗi gõ hơn thì đứng trước. | QA-394, DEC-209 |
| Q-08 | Thiếu chi tiết | Kết quả tìm người dùng có hiện tài khoản DEACTIVATED, DELETED, BANNED, hoặc chưa xong Bước 3 không? DEC-153 loại các tài khoản này khỏi gợi ý @mention (M06 dùng chung cách so khớp, QA-110); DEC-122 cho hồ sơ BANNED hiện bình thường. | Chỉ tài khoản ACTIVE đã xong Bước 3. | QA-401, QA-402, DEC-209 |
| Q-09 | Mơ hồ | Công thức xếp hạng (DEC-055): tập ứng viên "Top N" có bao nhiêu bài; "normalized 0-1" và "normalize ... within candidate set" làm thế nào; khi mọi ứng viên có cùng điểm tương tác thô thì Điểm tương tác bằng bao nhiêu; bằng Điểm cuối xếp sao; "search-downranked ×0.5" (DEC-079) nhân vào Điểm cuối hay Điểm liên quan; có đúng 120 kết quả thì có hiện thông báo "Thu hẹp tìm kiếm..." (DEC-064) không? | Tập ứng viên 120 bài; liên quan ngữ nghĩa (cosine + 1) ÷ 2; tương tác chuẩn hóa trong tập ứng viên, cùng thô thì 0; bằng điểm: liên quan cao hơn, rồi bài mới hơn; HEAVY: Điểm cuối × 0,5; thông báo khi đã tải 120 và cuộn tiếp. | QA-397, DEC-211 |
| Q-10 | Mơ hồ | Sắp xếp Mới nhất, Nhiều upvote nhất (DEC-056) khi tìm ngữ nghĩa: sắp lại tập ứng viên theo liên quan, hay mọi bài? Bằng nhau (cùng thời điểm đăng, cùng số upvote) xếp sao? Giảm hạng HEAVY có áp cho hai cách sắp xếp này không? | Sắp lại chính tập ứng viên; bằng nhau thì bài mới hơn trước; không giảm hạng HEAVY. | QA-398, DEC-211 |
| Q-11 | Mơ hồ | Khoảng thời gian "Today/This week/This month" (DEC-056) tính theo lịch (từ 00:00 hôm nay, từ thứ Hai, từ ngày 1, giờ Việt Nam theo DEC-127) hay cuốn chiếu (24 giờ, 7 ngày, 30 ngày gần nhất), và theo thời điểm đăng của bài? | Theo lịch, giờ Việt Nam, theo thời điểm đăng. | QA-402, DEC-212 |
| Q-12 | Thiếu chi tiết | Bộ lọc (DEC-056): chọn được nhiều Topic, nhiều Tag không; nếu được thì bài khớp một hay khớp tất cả? "Following-only" gồm bài của người đang theo dõi, bài thuộc Topic đang theo dõi, bài đang theo dõi (ba loại đối tượng theo dõi, QA-228), hay chỉ một phần? Bộ lọc có áp cho kết quả phụ không? | Mỗi loại một giá trị; nhiều bộ lọc thì phải thỏa tất cả; "đang theo dõi" gồm người dùng, Topic, bài; chỉ áp cho kết quả bài. | QA-400, DEC-212 |
| Q-13 | Mơ hồ | Đoạn trích "first ~150 chars of content_text" (DEC-061): đúng 150 ký tự hay cắt ở ranh giới từ, có dấu "…" không? Bài chỉ có poll, không có nội dung chữ, thì đoạn trích là gì? | 150 ký tự, cắt trước từ bị chia đôi và thêm "…"; không quá 150 thì hiện nguyên; không có nội dung chữ thì không có đoạn trích. | QA-402, DEC-213 |
| Q-14 | Thiếu chi tiết | Lịch sử tìm kiếm (DEC-059): thao tác nào thêm một mục (gửi truy vấn, chọn một gợi ý, mở bài theo Topic hay Tag)? Gửi lại truy vấn đã có trong lịch sử thì đưa nó lên đầu hay thêm bản trùng? Chọn một mục lịch sử thì hệ thống điền vào ô tìm kiếm hay gửi luôn truy vấn? Xóa được từng mục không? | Chỉ thêm khi gửi truy vấn có chữ; gửi lại thì lên đầu; mới nhất trước; chọn mục thì gửi luôn; không xóa từng mục. | QA-402, DEC-213 |
| Q-15 | Mơ hồ | Giới hạn "/min" (DEC-063): một phút theo đồng hồ hay 60 giây gần nhất (như DEC-144 cho gợi ý Topic)? Tải thêm khi cuộn, đổi bộ lọc, đổi sắp xếp có tính là một lượt gửi không? | 60 giây gần nhất; tải thêm không tính; đổi bộ lọc, đổi sắp xếp, mở trang Topic/Tag, chọn mục lịch sử tính một lượt gửi. | QA-402, DEC-213 |
| Q-16 | Thiếu chi tiết | Xem bài của một Topic hay Tag qua bộ lọc M06 (DEC-142) khi không có truy vấn (và gửi truy vấn rỗng, chỉ có bộ lọc): sắp xếp mặc định là gì (Liên quan cần có truy vấn); có giới hạn 120 kết quả không; có tính vào giới hạn tần suất không? | Liệt kê mọi bài khớp bộ lọc; mặc định Mới nhất, không có Liên quan; không giới hạn 120; không gọi AI; truy vấn rỗng không có bộ lọc thì không tìm. | QA-399, DEC-212 |

### B.2 TBD

| ID | Nội dung | Ảnh hưởng | Lý do chưa chốt |
|---|---|---|---|
| TBD-M06-01 | Trang tìm kiếm công khai (Guest dùng được) chưa được tối ưu để công cụ tìm kiếm bên ngoài lập chỉ mục và hiển thị xem trước khi chia sẻ link. | Thấp | OPEN-006 hoãn có chủ đích (không làm SSR/SEO ở MS1) |

### B.3 Cần cân nhắc (ngoài dữ liệu hiện có)

| Mã | Điểm cần cân nhắc | Vì sao cần | Quyết định |
|---|---|---|---|
| CC-01 | Mở rộng phạm vi: xóa lịch sử tìm kiếm trên thiết bị khi người dùng đăng xuất. | Lịch sử lưu trên trình duyệt, không gắn tài khoản (BR-M06-20); trên máy dùng chung (ví dụ phòng máy của trường), người dùng sau thấy truy vấn của người trước. Chạm tới quyền riêng tư của học sinh. | Chấp nhận (mở rộng phạm vi): xóa lịch sử khi đăng xuất — QA-403, DEC-213 |

## Phụ lục C. Sổ nguồn

**Owner keywords:** M06, search, Search, tìm kiếm, tìm, semantic search, Semantic Search, full-text, FTS, tsvector, tsquery, unaccent, không dấu, pg_trgm, trigram, prefix match, autocomplete, debounce, search history, lịch sử tìm kiếm, ranking, relevance, relevance_score, final_score, cosine, snippet, highlight, infinite scroll, cursor-based, Following-only, date range, rate limit, rate limiting, 429, mixed results, suggestion list, Tài khoản đã bị khóa
**Dependency keywords:** post, bài viết, user, username, display_name, tag, topic, chủ đề, group, nhóm, private group, visible-but-gated, comment, bình luận, embedding, pgvector, HNSW, AI_ENABLED, AI off, AI master, per-module toggle, fallback, follow, upvote, star, timezone, BANNED, DEACTIVATED, anonymous, ẩn danh, HIDDEN, mod_state, publish_state, deleted, @mention, Lớp/Khối, grade_level
**Mục draft của module:** DM-7.3, DM-7.4, DM-11.3
**Loại khỏi bảng nguồn (khớp nhầm):** DEC-029 ("highlight" là định dạng chữ trong trình soạn, M03); DEC-101, ISS-130, QA-179 (giới hạn tạo nhóm, M11); DEC-121, DEC-123, ISS-149, QA-203, QA-047, GL:Leaderboard (xếp hạng bảng xếp hạng, M12); DEC-125, ISS-167 (xếp hạng feed, M14); ISS-174, QA-234, MR-A02 (phân trang feed, M14); ISS-155, QA-210, QA-212, ISS-162, QA-220, MR-A01 (chat, M16); ISS-182, QA-245, ISS-183, QA-246 (khoảng thời gian, cách tính của dashboard, M15); QA-214 ("không dấu vết"); QA-296 (username không dấu, M01); QA-055 (tô màu tên khi @mention, M01); QA-004 ("tự tìm lời giải" — hành vi học sinh); DEC-206 (tóm tắt bài, M13; chỉ nhắc giới hạn tần suất của DEC-100)

### C.1 Bảng nguồn

| Nguồn | Nhãn | Trạng thái | Dùng ở | Ghi chú |
|---|---|---|---|---|
| DEC-053 | Sở hữu | Sửa một phần bởi DEC-209, DEC-210 | FR-M06-01.05, FR-M06-01.08, FR-M06-02, FR-M06-02.01, FR-M06-02.03, FR-M06-02.04, FR-M06-02.22, FR-M06-03, FR-M06-03.01, FR-M06-03.03, FR-M06-03.05, BR-M06-01, BR-M06-05, BR-M06-06, BR-M06-09, BR-M06-22 | Nhóm A. Phạm vi tìm; DEC-209 thay "exact/prefix" bằng khớp ở bất kỳ vị trí, DEC-210 bỏ "visible-but-gated" cho nhóm Private |
| DEC-054 | Sở hữu | Hiện hành | FR-M06-01, FR-M06-01.01, FR-M06-01.02, FR-M06-02, FR-M06-02.01, FR-M06-02.02, FR-M06-03, FR-M06-03.01, BR-M06-02, BR-M06-03 | Nhóm A. Cách kích hoạt: bài chỉ khi gửi; User/Tag/Topic/Group gợi ý khi gõ (300ms) và khi gửi |
| DEC-055 | Sở hữu | Sửa một phần bởi DEC-211 | FR-M06-02, FR-M06-02.10, FR-M06-02.28, BR-M06-13 | Nhóm A. Công thức xếp hạng kết quả bài: liên quan 0,8 + tương tác 0,2 |
| DEC-056 | Sở hữu | Sửa một phần bởi DEC-211, DEC-212 | FR-M06-04, FR-M06-04.01, FR-M06-04.02, FR-M06-04.03, FR-M06-04.04, FR-M06-04.05, FR-M06-04.06, FR-M06-04.07, FR-M06-04.09, BR-M06-15 | Nhóm A. Bộ lọc kết quả bài: Topic, Tag, khoảng thời gian, chỉ người đang theo dõi, sắp xếp |
| DEC-057 | Sở hữu | Sửa một phần bởi DEC-209, DEC-211 | FR-M06-01, FR-M06-01.08, FR-M06-02, FR-M06-02.04, FR-M06-02.06, FR-M06-03.05, BR-M06-06, BR-M06-08, BR-M06-22 | Nhóm A. Tìm full-text, bỏ dấu tiếng Việt, khớp gần đúng cho Tag/User/Topic/Group |
| DEC-058 | Sở hữu | Sửa một phần bởi DEC-209 | FR-M06-01, FR-M06-01.01, FR-M06-01.03, BR-M06-04 | Nhóm A. Gợi ý khi gõ: chỉ User/Tag/Topic/Group, không gợi ý tiêu đề bài |
| DEC-059 | Sở hữu | Sửa một phần bởi DEC-213 | FR-M06-05, FR-M06-05.01, FR-M06-05.02, FR-M06-05.03, FR-M06-05.04, FR-M06-05.05, BR-M06-20 | Nhóm A. Lịch sử tìm kiếm trên thiết bị, tối đa 10, có nút xóa |
| DEC-060 | Sở hữu | Hiện hành | FR-M06-02, FR-M06-02.16, FR-M06-03, FR-M06-03.02, FR-M06-04.09, BR-M06-17 | Nhóm A. Trang kết quả hỗn hợp; bài là chính, mỗi loại khác tối đa 3 |
| DEC-061 | Sở hữu | Sửa một phần bởi DEC-213 | FR-M06-02, FR-M06-02.15, BR-M06-18 | Nhóm A. Đoạn trích ~150 ký tự, không tô sáng từ khóa |
| DEC-062 | Sở hữu | Sửa một phần bởi DEC-208, DEC-210 | FR-M06-01, FR-M06-01.06, FR-M06-02, FR-M06-02.07, FR-M06-02.08, FR-M06-03, BR-M06-11 | Nhóm A. Quyền tìm; DEC-208: Guest chỉ tìm full-text; DEC-210: nhóm Private ẩn với người ngoài nhóm |
| DEC-063 | Sở hữu | Sửa một phần bởi DEC-213 | FR-M06-01, FR-M06-01.06, FR-M06-01.07, FR-M06-02.20, FR-M06-02.21, BR-M06-21 | Nhóm A. Giới hạn tần suất theo Guest/User, gợi ý khi gõ/gửi |
| DEC-064 | Sở hữu | Sửa một phần bởi DEC-211, DEC-212 | FR-M06-02, FR-M06-02.17, FR-M06-02.18, FR-M06-02.19, BR-M06-19 | Nhóm A. Tải thêm khi cuộn, 15 kết quả mỗi lần, tối đa 120 |
| DM-11.3 | Sở hữu | Hiện hành | FR-M06-02, FR-M06-02.03, BR-M06-05 | Nhóm A. Draft: luồng tìm ngữ nghĩa (truy vấn → embedding → tìm vector → bài liên quan) |
| DM-7.3 | Sở hữu | Sửa một phần bởi DEC-053, DEC-056 | FR-M06-02 | Nhóm A. Draft: tiêu chí tìm (Title, Content, Author, Topic, Tag, Lớp/Khối, ngữ nghĩa) |
| DM-7.4 | Sở hữu | Bị thay bởi DEC-056 | — | Nhóm A. Draft: lọc/sắp xếp (Newest, Oldest, Most starred/viewed/commented, Topic, Tag, Lớp/Khối, Author); mục 7 dùng chung với Feed (M14) |
| ISS-085 | Nhắc tới | Trùng với DEC-053 | — | Nhóm A. Câu hỏi đã có DEC-053 trả lời |
| ISS-086 | Nhắc tới | Trùng với DEC-054 | — | Nhóm A. Câu hỏi đã có DEC-054 trả lời |
| ISS-087 | Nhắc tới | Trùng với DEC-055 | — | Nhóm A. Câu hỏi đã có DEC-055 trả lời |
| ISS-088 | Nhắc tới | Trùng với DEC-056 | — | Nhóm A. Câu hỏi đã có DEC-056 trả lời |
| ISS-089 | Nhắc tới | Trùng với DEC-057 | — | Nhóm A. Câu hỏi đã có DEC-057 trả lời |
| ISS-090 | Nhắc tới | Trùng với DEC-058 | — | Nhóm A. Câu hỏi đã có DEC-058 trả lời |
| ISS-091 | Nhắc tới | Trùng với DEC-057 | — | Nhóm A. Câu hỏi đã có DEC-057 trả lời |
| ISS-092 | Nhắc tới | Trùng với DEC-059 | — | Nhóm A. Câu hỏi đã có DEC-059 trả lời |
| ISS-093 | Nhắc tới | Trùng với DEC-060 | — | Nhóm A. Câu hỏi đã có DEC-060 trả lời |
| ISS-094 | Nhắc tới | Trùng với DEC-061 | — | Nhóm A. Câu hỏi đã có DEC-061 trả lời |
| ISS-095 | Nhắc tới | Trùng với DEC-062 | — | Nhóm A. Câu hỏi đã có DEC-062 trả lời |
| ISS-096 | Nhắc tới | Trùng với DEC-063 | — | Nhóm A. Câu hỏi đã có DEC-063 trả lời |
| ISS-097 | Nhắc tới | Trùng với DEC-064 | — | Nhóm A. Câu hỏi đã có DEC-064 trả lời |
| QA-109 | Sở hữu | Trùng với DEC-053 | — | Nhóm A. Mở rộng phạm vi so với QA-022: thêm Topic, Group |
| QA-110 | Sở hữu | Trùng với DEC-053 | — | Nhóm A. User tìm theo display_name + username, dùng chung cách so khớp với @mention (M01) |
| QA-111 | Sở hữu | Trùng với DEC-054 | — | Nhóm A. Câu trả lời của stakeholder, nội dung nằm trong DEC-053–DEC-064 |
| QA-112 | Sở hữu | Hiện hành | FR-M06-02.10, BR-M06-13 | Nhóm A. Lý do trọng số 2:1 giữa bình chọn và bình luận: nhất quán công thức Trending |
| QA-113 | Sở hữu | Trùng với DEC-056 | — | Nhóm A. Câu trả lời của stakeholder, nội dung nằm trong DEC-053–DEC-064 |
| QA-114 | Sở hữu | Trùng với DEC-057 | — | Nhóm A. Câu trả lời của stakeholder, nội dung nằm trong DEC-053–DEC-064 |
| QA-115 | Sở hữu | Trùng với DEC-058 | — | Nhóm A. Câu trả lời của stakeholder, nội dung nằm trong DEC-053–DEC-064 |
| QA-116 | Sở hữu | Trùng với DEC-059 | — | Nhóm A. Câu trả lời của stakeholder, nội dung nằm trong DEC-053–DEC-064 |
| QA-117 | Sở hữu | Trùng với DEC-060 | — | Nhóm A. Câu trả lời của stakeholder, nội dung nằm trong DEC-053–DEC-064 |
| QA-118 | Sở hữu | Hiện hành | FR-M06-02.15, BR-M06-18 | Nhóm A. Lý do không tô sáng: tìm ngữ nghĩa không có từ khóa khớp nguyên văn |
| QA-119 | Sở hữu | Trùng với DEC-062 | — | Nhóm A. Câu trả lời của stakeholder, nội dung nằm trong DEC-053–DEC-064 |
| QA-120 | Sở hữu | Sửa một phần bởi DEC-210 | FR-M06-03 | Nhóm A. Phần bài nhóm Private chỉ cho thành viên còn hiệu lực; phần nhóm hiện trong tìm kiếm bị DEC-210 thay |
| QA-121 | Sở hữu | Hiện hành | FR-M06-02.20, BR-M06-21 | Nhóm A. Lý do Guest chặt hơn: khác biệt về trách nhiệm |
| QA-122 | Sở hữu | Trùng với DEC-064 | — | Nhóm A. Câu trả lời của stakeholder, nội dung nằm trong DEC-053–DEC-064 |
| MR-M06 | Sở hữu | Sửa một phần bởi DEC-208, DEC-209, DEC-210, DEC-211, DEC-212, DEC-213 | Mục 1.2, 4.5 | Nhóm A. Dòng module-registry của M06 |
| DEC-008 | Sở hữu | Hiện hành | FR-M06-01.08, FR-M06-02, FR-M06-02.04, FR-M06-03.05, BR-M06-06, BR-M06-22 | Nhóm B. Ngoài section. Cách dự phòng của M06 khi tắt AI: tìm full-text theo từ khóa. DEC-092, DEC-093 (làm rõ): công tắc nằm ở cấu hình hệ thống (M10) |
| DEC-015 | Phụ thuộc | Sửa một phần bởi DEC-148 | Không áp dụng: M01: username dùng cho @mention và tìm kiếm, không phải tên hiển thị chính | Nhóm B. M01: username dùng cho @mention và tìm kiếm, không phải tên hiển thị chính |
| DEC-020 | Phụ thuộc | Sửa một phần bởi DEC-153 | Không áp dụng: cách so khớp @mention thuộc M01; M06 có quy tắc khớp ở BR-M06-09, M01 áp cùng quy tắc cho @mention (DEC-214, ngoài bảng nguồn) | Nhóm B. M01: @mention so khớp display_name + username; DEC-214 (ngoài bảng nguồn, ghi sau khi chốt 1.0) cho @mention khớp tên như DEC-209 |
| DEC-030 | Phụ thuộc | Hiện hành | Không áp dụng: nội dung chữ của bài thuộc M03, ghi ở 5.9 | Nhóm B. M03: nội dung dạng chữ thuần của bài dùng cho tìm kiếm. DEC-164, DEC-169 (ngoài bảng nguồn) sửa phần bắt buộc, độ dài, ảnh bìa; phần nội dung chữ dùng để tìm không đổi |
| DEC-051 | Phụ thuộc | Sửa một phần bởi DEC-143 | FR-M06-01.04, FR-M06-03.04, BR-M06-10 | Nhóm B. M05: Tag bị vô hiệu hóa ẩn khỏi autocomplete và browse. DEC-146 (ngoài bảng nguồn) thêm ghi nhật ký |
| DEC-079 | Sở hữu | Sửa một phần bởi DEC-122, DEC-211 | FR-M06-02, FR-M06-02.11, FR-M06-02.12, BR-M06-14 | Nhóm B. Ngoài section (M08). Nội dung hiện có của người ở mức HEAVY bị giảm hạng tìm kiếm ×0,5; kết quả thấy ở M06. DEC-118, DEC-163, DEC-188 (ngoài bảng nguồn) sửa phần bảng xếp hạng, phạm vi tạo bài, cách hạ mức; giảm hạng ×0,5 không đổi |
| DEC-093 | Phụ thuộc | Sửa một phần bởi DEC-205 | FR-M06-02.03, FR-M06-02.04, BR-M06-05, BR-M06-06 | Nhóm B. M10: công tắc AI tổng và công tắc Search (embedding ngữ nghĩa) |
| DEC-099 | Sở hữu | Sửa một phần bởi DEC-205 | FR-M06-02, FR-M06-02.05, BR-M06-07 | Nhóm B. Ngoài section (M13). Phần M06: AI lỗi sau lần thử lại → tìm full-text cho riêng truy vấn đó. Thời gian chờ, thử lại thuộc M13. DEC-206, DEC-207 (ngoài bảng nguồn) làm rõ phần tóm tắt, nhật ký AI; phần tìm full-text cho riêng truy vấn lỗi không đổi |
| DEC-100 | Nhắc tới | Hiện hành | Không áp dụng: M13 không có giới hạn AI riêng, dựa vào giới hạn tìm kiếm DEC-063 | Nhóm B. M13 không có giới hạn AI riêng, dựa vào giới hạn tìm kiếm DEC-063. DEC-144 (ngoài bảng nguồn) chỉ sửa giới hạn gợi ý Topic |
| DEC-108 | Sở hữu | Hiện hành | FR-M06-02, FR-M06-02.09, BR-M06-11 | Nhóm B. Ngoài section (M11). Nhóm chuyển Private: truy vấn tìm mới của người không phải thành viên loại bài của nhóm |
| DEC-110 | Sở hữu | Sửa một phần bởi DEC-210 | FR-M06-01.13, FR-M06-03, FR-M06-03.08, BR-M06-11, BR-M06-25 | Nhóm B. M11: nhóm Private ẩn khỏi tìm kiếm (DEC-210 giữ, thêm: thành viên vẫn thấy) |
| DEC-122 | Phụ thuộc | Hiện hành | FR-M06-02.13, FR-M06-02.14, BR-M06-12 | Nhóm B. M12/M01: bài, bình luận, hồ sơ của tài khoản BANNED vẫn hiện bình thường; nhãn "Tài khoản đã bị khóa" ở mọi nơi tên hiện |
| DEC-131 | Nhắc tới | Hiện hành | Không áp dụng: M01: trang chính sách công bố nội dung được dịch vụ AI xử lý, gồm embedding cho tìm kiếm | Nhóm B. M01: trang chính sách công bố nội dung được dịch vụ AI xử lý, gồm embedding cho tìm kiếm. DEC-146, DEC-154 (ngoài bảng nguồn) sửa nội dung công bố |
| DEC-134 | Nhắc tới | Hiện hành | Không áp dụng: Công nghệ frontend/backend; SEO hoãn (OPEN-006) | Nhóm B. Công nghệ frontend/backend; SEO hoãn (OPEN-006) |
| DEC-137 | Nhắc tới | Hiện hành | Không áp dụng: Công nghệ đã chốt, gồm phần mở rộng tìm kiếm của CSDL (không đưa vào FR) | Nhóm B. Công nghệ đã chốt, gồm phần mở rộng tìm kiếm của CSDL (không đưa vào FR) |
| DEC-142 | Sở hữu | Hiện hành | FR-M06-04, FR-M06-04.08, BR-M06-16 | Nhóm B. Ngoài section (M05). Xem bài theo Topic/Tag làm qua bộ lọc của M06 |
| DEC-143 | Phụ thuộc | Hiện hành | FR-M06-01.04, FR-M06-03.04, BR-M06-10 | Nhóm B. M05: Tag kích hoạt lại xuất hiện lại trong autocomplete; tập ký tự Tag |
| DEC-148 | Phụ thuộc | Hiện hành | Không áp dụng: M01: username so không phân biệt hoa thường khi tìm @mention | Nhóm B. M01: username so không phân biệt hoa thường khi tìm @mention |
| DEC-153 | Phụ thuộc | Hiện hành | Không áp dụng: M01 (@mention); M06 chốt riêng ở DEC-209 | Nhóm B. M01: danh sách gợi ý @mention không hiện tài khoản DEACTIVATED, DELETED, BANNED, chưa xong Bước 3; sửa DEC-020 mà M06 dùng chung cách so khớp |
| DEC-205 | Phụ thuộc | Hiện hành | FR-M06-02.03, BR-M06-05 | Nhóm B. M13: embedding bài và truy vấn theo công tắc tổng và công tắc Search; bài thiếu embedding được tạo bù |
| DG-4 | Nhắc tới | Hiện hành | Không áp dụng: Bản đồ module: Discovery / Search | Nhóm B. Bản đồ module: Discovery / Search |
| DG-6 | Sở hữu | Hiện hành | FR-M06-02, FR-M06-02.03, BR-M06-05 | Nhóm B. Draft: Semantic Search là năng lực AI bắt buộc |
| DG-7 | Nhắc tới | Hiện hành | Không áp dụng: Kiến trúc: CSDL có pgvector cho Semantic Search | Nhóm B. Kiến trúc: CSDL có pgvector cho Semantic Search |
| DM-11.5 | Nhắc tới | Hiện hành | Không áp dụng: Related Posts không nằm trong phạm vi chính thức | Nhóm B. Related Posts không nằm trong phạm vi chính thức |
| DM-13 | Nhắc tới | Hiện hành | Không áp dụng: Sơ đồ kiến trúc tổng thể | Nhóm B. Sơ đồ kiến trúc tổng thể |
| DM-7 | Nhắc tới | Hiện hành | Không áp dụng: Tiêu đề mục 7 của draft | Nhóm B. Tiêu đề mục 7 của draft |
| DM-x02 | Nhắc tới | Hiện hành | Không áp dụng: Phạm vi dự án: Search / Filter / Sort, Semantic Search | Nhóm B. Phạm vi dự án: Search / Filter / Sort, Semantic Search |
| GL:Semantic Search | Sở hữu | Hiện hành | Mục 2.1 | Nhóm B. Thuật ngữ: tìm theo embedding, theo ý nghĩa chứ không chỉ từ khóa |
| GL:pgvector | Nhắc tới | Hiện hành | Không áp dụng: Thuật ngữ công nghệ | Nhóm B. Thuật ngữ công nghệ |
| ISS-040 | Nhắc tới | Bị thay bởi DEC-053 | — | Nhóm B. Câu hỏi đã có QA-022 trả lời |
| ISS-047 | Nhắc tới | Trùng với QA-035 | — | Nhóm B. Câu hỏi đã có QA-035, QA-036, QA-037 trả lời |
| ISS-122 | Nhắc tới | Trùng với DEC-093 | — | Nhóm B. Câu hỏi đã có QA-165, DEC-093 trả lời |
| ISS-129 | Nhắc tới | Trùng với DEC-100 | — | Nhóm B. Câu hỏi đã có QA-178, DEC-100 trả lời |
| ISS-140 | Nhắc tới | Trùng với DEC-110 | — | Nhóm B. Câu hỏi đã có QA-188, DEC-110 trả lời |
| ISS-154 | Nhắc tới | Trùng với DEC-122 | — | Nhóm B. Câu hỏi đã có DEC-122 trả lời |
| ISS-161 | Nhắc tới | Trùng với QA-219 | — | Nhóm B. Chat (M16): so sánh với mục đích giới hạn tần suất của Search |
| ISS-165 | Nhắc tới | Trùng với QA-224 | — | Nhóm B. Chat (M16): phân trang cùng kiểu Search, nhưng không giới hạn tổng |
| ISS-169 | Nhắc tới | Trùng với QA-228 | — | Nhóm B. M14: tab Following rỗng dẫn sang trang Search |
| ISS-193 | Nhắc tới | Trùng với DEC-131 | — | Nhóm B. Câu hỏi đã có DEC-131 trả lời |
| OPEN-006 | Phụ thuộc | Hiện hành | TBD-M06-01 | Nhóm B. Hoãn SEO/SSR; phạm vi ảnh hưởng ghi gồm "Search public" |
| QA-007 | Nhắc tới | Hiện hành | Không áp dụng: Quy mô demo ~200 lượt tìm ngữ nghĩa; chi phí AI | Nhóm B. Quy mô demo ~200 lượt tìm ngữ nghĩa; chi phí AI. DEC-206 (ngoài bảng nguồn) sửa phần tóm tắt |
| QA-011 | Sở hữu | Sửa một phần bởi DEC-208 | FR-M06-02, FR-M06-02.23, BR-M06-23 | Nhóm B. Guest "Semantic Search: Không" — giữ, DEC-208 làm rõ. DEC-171, DEC-206 (ngoài bảng nguồn) sửa phần Guest xem hồ sơ, tóm tắt |
| QA-022 | Sở hữu | Bị thay bởi DEC-053 | — | Nhóm B. Phạm vi tìm Phase 3 (Post, User, Tag); không tìm bình luận; full-text khi tắt AI |
| QA-024 | Nhắc tới | Hiện hành | Không áp dụng: M13 là Must vì M06, M08, M05 phụ thuộc; dẫn tới DEC-008 | Nhóm B. M13 là Must vì M06, M08, M05 phụ thuộc; dẫn tới DEC-008 |
| QA-035 | Sở hữu | Sửa một phần bởi DEC-053 | FR-M06-03 | Nhóm B. Phạm vi tìm Phase 4: Group dùng full-text (tên + mô tả); nói khác DEC-053 (xét ở bước 2) |
| QA-036 | Sở hữu | Sửa một phần bởi DEC-209 | FR-M06-03, BR-M06-09 | Nhóm B. Khớp chuỗi con cho tên người dùng — giữ, DEC-209 áp cho cả Tag, Topic, Group |
| QA-037 | Sở hữu | Bị thay bởi DEC-053 | — | Nhóm B. Phase 4: bình luận tìm bằng full-text; nói khác DEC-053 (xét ở bước 2) |
| QA-044 | Sở hữu | Sửa một phần bởi DEC-210 | FR-M06-03 | Nhóm B. Nhóm Private visible-but-gated khi tìm — DEC-210 thay phần tìm kiếm |
| QA-054 | Nhắc tới | Trùng với DEC-020 | — | Nhóm B. Câu trả lời của DEC-020 (M01) |
| QA-165 | Phụ thuộc | Trùng với DEC-093 | — | Nhóm B. M10: công tắc AI tổng + từng module |
| QA-178 | Nhắc tới | Trùng với DEC-100 | — | Nhóm B. Câu trả lời của DEC-100 |
| QA-186 | Sở hữu | Trùng với DEC-108 | — | Nhóm B. Câu trả lời của DEC-108 (M11) |
| QA-188 | Sở hữu | Trùng với DEC-110 | — | Nhóm B. Câu trả lời của DEC-110 (M11) |
| QA-205 | Phụ thuộc | Trùng với DEC-122 | — | Nhóm B. Nhãn "Tài khoản đã bị khóa" ở mọi nơi tên tác giả xuất hiện |
| QA-219 | Nhắc tới | Hiện hành | Không áp dụng: Chat (M16): giới hạn tần suất của Search nhằm giới hạn chi phí AI (so sánh) | Nhóm B. Chat (M16): giới hạn tần suất của Search nhằm giới hạn chi phí AI (so sánh) |
| QA-224 | Nhắc tới | Hiện hành | Không áp dụng: Chat (M16): phân trang cùng kiểu Search | Nhóm B. Chat (M16): phân trang cùng kiểu Search |
| QA-228 | Nhắc tới | Hiện hành | Không áp dụng: M14: tab Following rỗng dẫn sang trang Search (tìm User/Topic/Post) | Nhóm B. M14: tab Following rỗng dẫn sang trang Search (tìm User/Topic/Post) |
| QA-230 | Nhắc tới | Hiện hành | Không áp dụng: M14: tab Group rỗng dẫn sang trang danh sách/tìm Group | Nhóm B. M14: tab Group rỗng dẫn sang trang danh sách/tìm Group |
| QA-236 | Nhắc tới | Hiện hành | Không áp dụng: M14: Trending không loại, không chỉnh điểm bài của BANNED/HEAVY; ngoại lệ ẩn chỉ áp cho bảng xếp hạng | Nhóm B. M14: Trending không loại, không chỉnh điểm bài của BANNED/HEAVY; ngoại lệ ẩn chỉ áp cho bảng xếp hạng |
| QA-252 | Nhắc tới | Trùng với DEC-131 | — | Nhóm B. Câu trả lời của DEC-131 (M01) |
| QA-275 | Sở hữu | Trùng với DEC-142 | — | Nhóm B. Câu trả lời của DEC-142: xem bài theo Topic/Tag qua bộ lọc M06 |
| QA-388 | Phụ thuộc | Trùng với DEC-205 | — | Nhóm B. Câu trả lời của DEC-205 (M13) |
| MR-A04 | Nhắc tới | Hiện hành | Không áp dụng: Đợt sửa Phase 6: tìm kiếm đã được M06 xử lý | Nhóm B. Đợt sửa Phase 6: tìm kiếm đã được M06 xử lý |
| MR-FB-M06 | Sở hữu | Trùng với DEC-008 | — | Nhóm B. Bảng dự phòng AI: M06 → tìm full-text theo từ khóa |
| MR-M12 | Nhắc tới | Hiện hành | Không áp dụng: Dòng module-registry M12; nhắc DEC-079 được sửa (bảng xếp hạng) | Nhóm B. Dòng module-registry M12; nhắc DEC-079 được sửa (bảng xếp hạng) |
| DEC-127 | Phụ thuộc | Hiện hành | FR-M06-04.03, BR-M06-15 | Nhóm C. Múi giờ nghiệp vụ cho Hôm nay/Tuần này/Tháng này |
| DEC-128 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M06 | Nhóm D. Dùng chung; không quy định hành vi M06 |
| DEC-129 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M06 | Nhóm D. Dùng chung; không quy định hành vi M06. DEC-156 (ngoài bảng nguồn) |
| DEC-130 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M06 | Nhóm D. Dùng chung; không quy định hành vi M06. DEC-160 (ngoài bảng nguồn) |
| DEC-132 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M06 | Nhóm D. Dùng chung; không quy định hành vi M06. DEC-141, DEC-144 (ngoài bảng nguồn) |
| DEC-133 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M06 | Nhóm D. Dùng chung; không quy định hành vi M06. DEC-207 (ngoài bảng nguồn): nhật ký AI không ghi embedding truy vấn |
| DEC-135 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M06 | Nhóm D. Dùng chung; không quy định hành vi M06 |
| DEC-136 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M06 | Nhóm D. Dùng chung; không quy định hành vi M06 |
| DEC-138 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M06 | Nhóm D. Dùng chung; không quy định hành vi M06. DEC-155, DEC-157 (ngoài bảng nguồn) |
| ISS-189 | Nhắc tới | Trùng với DEC-127 | — | Nhóm D. Dùng chung; không quy định hành vi M06 |
| ISS-190 | Nhắc tới | Trùng với DEC-128 | — | Nhóm D. Dùng chung; không quy định hành vi M06 |
| ISS-191 | Nhắc tới | Trùng với DEC-129 | — | Nhóm D. Dùng chung; không quy định hành vi M06 |
| ISS-192 | Nhắc tới | Trùng với DEC-130 | — | Nhóm D. Dùng chung; không quy định hành vi M06 |
| ISS-194 | Nhắc tới | Trùng với DEC-132 | — | Nhóm D. Dùng chung; không quy định hành vi M06 |
| ISS-195 | Nhắc tới | Trùng với DEC-133 | — | Nhóm D. Dùng chung; không quy định hành vi M06 |
| ISS-196 | Nhắc tới | Trùng với QA-255 | — | Nhóm D. Dùng chung; không quy định hành vi M06 |
| ISS-197 | Nhắc tới | Trùng với DEC-134 | — | Nhóm D. Dùng chung; không quy định hành vi M06 |
| ISS-198 | Nhắc tới | Trùng với DEC-135 | — | Nhóm D. Dùng chung; không quy định hành vi M06 |
| ISS-199 | Nhắc tới | Trùng với DEC-136 | — | Nhóm D. Dùng chung; không quy định hành vi M06 |
| ISS-200 | Nhắc tới | Trùng với DEC-008 | — | Nhóm D. Dùng chung; không quy định hành vi M06 |
| ISS-201 | Nhắc tới | Trùng với QA-260 | — | Nhóm D. Dùng chung; không quy định hành vi M06 |
| ISS-202 | Nhắc tới | Trùng với QA-261 | — | Nhóm D. Dùng chung; không quy định hành vi M06 |
| ISS-203 | Nhắc tới | Trùng với DEC-137 | — | Nhóm D. Dùng chung; không quy định hành vi M06 |
| ISS-204 | Nhắc tới | Trùng với DEC-138 | — | Nhóm D. Dùng chung; không quy định hành vi M06 |
| QA-248 | Phụ thuộc | Trùng với DEC-127 | — | Nhóm D. Múi giờ (cùng nội dung DEC-127) |
| QA-249 | Nhắc tới | Trùng với DEC-128 | — | Nhóm D. Dùng chung; không quy định hành vi M06 |
| QA-250 | Nhắc tới | Trùng với DEC-129 | — | Nhóm D. Dùng chung; không quy định hành vi M06 |
| QA-251 | Nhắc tới | Trùng với DEC-130 | — | Nhóm D. Dùng chung; không quy định hành vi M06 |
| QA-253 | Nhắc tới | Trùng với DEC-132 | — | Nhóm D. Dùng chung; không quy định hành vi M06 |
| QA-254 | Nhắc tới | Trùng với DEC-133 | — | Nhóm D. Dùng chung; không quy định hành vi M06 |
| QA-255 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M06 | Nhóm D. Dùng chung; không quy định hành vi M06 |
| QA-256 | Nhắc tới | Trùng với DEC-134 | — | Nhóm D. Dùng chung; không quy định hành vi M06 |
| QA-257 | Nhắc tới | Trùng với DEC-135 | — | Nhóm D. Dùng chung; không quy định hành vi M06 |
| QA-258 | Nhắc tới | Trùng với DEC-136 | — | Nhóm D. Dùng chung; không quy định hành vi M06 |
| QA-259 | Phụ thuộc | Trùng với DEC-008 | — | Nhóm D. M10: cờ AI nằm ở cấu hình hệ thống |
| QA-260 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M06 | Nhóm D. Dùng chung; không quy định hành vi M06 |
| QA-261 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M06 | Nhóm D. Dùng chung; không quy định hành vi M06 |
| QA-262 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M06 | Nhóm D. Dùng chung; không quy định hành vi M06 |
| QA-263 | Nhắc tới | Trùng với DEC-137 | — | Nhóm D. Dùng chung; không quy định hành vi M06 |
| QA-264 | Nhắc tới | Trùng với DEC-138 | — | Nhóm D. Dùng chung; không quy định hành vi M06 |
| MR-A05 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung; không quy định hành vi M06 | Nhóm D. Dùng chung; không quy định hành vi M06 |
| DEC-208 | Sở hữu | Hiện hành | FR-M06-01.06, FR-M06-02, FR-M06-02.03, FR-M06-02.23, FR-M06-02.24, FR-M06-02.25, FR-M06-04, FR-M06-04.13, BR-M06-05, BR-M06-23 | Nhóm A. Guest tìm bài bằng full-text; "Tìm kiếm thông minh" nhắc Guest đăng nhập; bộ lọc theo dõi nhắc Guest đăng nhập |
| DEC-209 | Sở hữu | Hiện hành | FR-M06-01, FR-M06-01.01, FR-M06-01.05, FR-M06-01.09, FR-M06-01.10, FR-M06-01.11, FR-M06-01.12, FR-M06-03, FR-M06-03.03, FR-M06-03.06, FR-M06-03.07, FR-M06-03.10, BR-M06-03, BR-M06-04, BR-M06-09, BR-M06-24 | Nhóm A. Cách khớp người dùng, Tag, Topic, Group; chỉ tài khoản ACTIVE đã xong Bước 3; gợi ý từ ký tự đầu, mỗi loại tối đa 3 |
| DEC-210 | Sở hữu | Hiện hành | FR-M06-01, FR-M06-01.13, FR-M06-02.08, FR-M06-03, FR-M06-03.08, FR-M06-03.09, BR-M06-11, BR-M06-25 | Nhóm A. Nhóm Private ẩn khỏi tìm kiếm với người ngoài nhóm; thành viên vẫn thấy |
| DEC-211 | Sở hữu | Hiện hành | FR-M06-02, FR-M06-02.10, FR-M06-02.11, FR-M06-02.19, FR-M06-02.26, FR-M06-02.27, FR-M06-02.28, FR-M06-02.29, FR-M06-04, FR-M06-04.14, FR-M06-04.15, FR-M06-04.16, BR-M06-08, BR-M06-13, BR-M06-14, BR-M06-15, BR-M06-19 | Nhóm A. Chi tiết xếp hạng, full-text khớp ít nhất một từ, sắp xếp trên tập ứng viên, HEAVY |
| DEC-212 | Sở hữu | Sửa một phần bởi DEC-215, DEC-263 | FR-M06-02.31, FR-M06-04, FR-M06-04.03, FR-M06-04.04, FR-M06-04.08, FR-M06-04.10, FR-M06-04.11, FR-M06-04.12, FR-M06-04.17, FR-M06-04.18, FR-M06-04.19, BR-M06-15, BR-M06-16 | Nhóm A. Bộ lọc: một giá trị mỗi loại, kết hợp, "đang theo dõi", lịch; truy vấn rỗng |
| DEC-263 | Sở hữu | Hiện hành | FR-M06-04.04, BR-M06-15 | Nhóm B (đối chiếu FR-M14). Bộ lọc đang theo dõi không giữ bài ẩn danh nhờ theo dõi tác giả |
| DEC-213 | Sở hữu | Hiện hành | FR-M06-01.07, FR-M06-02, FR-M06-02.15, FR-M06-02.20, FR-M06-02.30, FR-M06-02.32, FR-M06-04, FR-M06-04.20, FR-M06-05, FR-M06-05.01, FR-M06-05.04, FR-M06-05.06, FR-M06-05.07, FR-M06-05.08, FR-M06-05.09, FR-M06-05.10, BR-M06-18, BR-M06-20, BR-M06-21 | Nhóm A. Đoạn trích, lịch sử, xóa khi đăng xuất, cách đếm giới hạn tần suất |
| F-GRP-06 | Phụ thuộc | Sửa một phần bởi DEC-210 | Chuyển M11 | Nhóm B. M11: nhóm Private visible-but-gated; DEC-210 làm rõ không hiện trong tìm kiếm với người ngoài nhóm |
| MR-M11 | Phụ thuộc | Sửa một phần bởi DEC-210 | Chuyển M11 | Nhóm B. Dòng module-registry M11; DEC-210 làm rõ phần tìm kiếm |
| DEC-144 | Nhắc tới | Hiện hành | Không áp dụng: tiền lệ cách đếm 60 giây, đã nằm trong DEC-213 | Nhóm C. M05: giới hạn gợi ý Topic tính theo 60 giây gần nhất; tiền lệ cho cách đếm của DEC-213 |
| QA-393 | Sở hữu | Trùng với DEC-208 | — | Nhóm A. Câu trả lời của stakeholder ở bước 6, nội dung nằm trong DEC |
| ISS-333 | Nhắc tới | Trùng với DEC-208 | — | Nhóm A. Câu hỏi bước 6, đã có DEC trả lời |
| QA-394 | Sở hữu | Trùng với DEC-209 | — | Nhóm A. Câu trả lời của stakeholder ở bước 6, nội dung nằm trong DEC |
| ISS-334 | Nhắc tới | Trùng với DEC-209 | — | Nhóm A. Câu hỏi bước 6, đã có DEC trả lời |
| QA-395 | Sở hữu | Trùng với DEC-210 | — | Nhóm A. Câu trả lời của stakeholder ở bước 6, nội dung nằm trong DEC |
| ISS-335 | Nhắc tới | Trùng với DEC-210 | — | Nhóm A. Câu hỏi bước 6, đã có DEC trả lời |
| QA-396 | Sở hữu | Trùng với DEC-211 | — | Nhóm A. Câu trả lời của stakeholder ở bước 6, nội dung nằm trong DEC |
| ISS-336 | Nhắc tới | Trùng với DEC-211 | — | Nhóm A. Câu hỏi bước 6, đã có DEC trả lời |
| QA-397 | Sở hữu | Trùng với DEC-211 | — | Nhóm A. Câu trả lời của stakeholder ở bước 6, nội dung nằm trong DEC |
| ISS-337 | Nhắc tới | Trùng với DEC-211 | — | Nhóm A. Câu hỏi bước 6, đã có DEC trả lời |
| QA-398 | Sở hữu | Trùng với DEC-211 | — | Nhóm A. Câu trả lời của stakeholder ở bước 6, nội dung nằm trong DEC |
| ISS-338 | Nhắc tới | Trùng với DEC-211 | — | Nhóm A. Câu hỏi bước 6, đã có DEC trả lời |
| QA-399 | Sở hữu | Trùng với DEC-212 | — | Nhóm A. Câu trả lời của stakeholder ở bước 6, nội dung nằm trong DEC |
| ISS-339 | Nhắc tới | Trùng với DEC-212 | — | Nhóm A. Câu hỏi bước 6, đã có DEC trả lời |
| QA-400 | Sở hữu | Trùng với DEC-212 | — | Nhóm A. Câu trả lời của stakeholder ở bước 6, nội dung nằm trong DEC |
| ISS-340 | Nhắc tới | Trùng với DEC-212 | — | Nhóm A. Câu hỏi bước 6, đã có DEC trả lời |
| QA-401 | Sở hữu | Trùng với DEC-209 | — | Nhóm A. Câu trả lời của stakeholder ở bước 6, nội dung nằm trong DEC |
| ISS-341 | Nhắc tới | Trùng với DEC-209 | — | Nhóm A. Câu hỏi bước 6, đã có DEC trả lời |
| QA-402 | Sở hữu | Trùng với DEC-213 | — | Nhóm A. Danh sách xác nhận X1–X7, nội dung nằm trong DEC-208, DEC-209, DEC-212, DEC-213 |
| ISS-342 | Nhắc tới | Trùng với DEC-213 | — | Nhóm A. Danh sách xác nhận, đã có DEC-208, DEC-209, DEC-212, DEC-213 trả lời |
| QA-403 | Sở hữu | Trùng với DEC-213 | — | Nhóm A. Câu trả lời của stakeholder ở bước 6, nội dung nằm trong DEC |
| ISS-343 | Nhắc tới | Trùng với DEC-213 | — | Nhóm A. Câu hỏi bước 6, đã có DEC trả lời |
| DEC-215 | Phụ thuộc | Hiện hành | FR-M06-04.04, BR-M06-15 | Nhóm B (đối chiếu FR-M07). M07: đối tượng theo dõi chỉ còn người dùng, Topic; bộ lọc "đang theo dõi" không còn bài đang theo dõi |
| DEC-228 | Phụ thuộc | Hiện hành | Chuyển M10 | Nhóm B (đối chiếu FR-M10). M10: tìm người dùng trong Admin Panel khớp tên như tìm người dùng M06 (BR-M06-09) |
| DEC-233 | Phụ thuộc | Hiện hành | Chuyển M11 | Nhóm B (đối chiếu FR-M11). M11: Mod, Admin không là thành viên chỉ xem nhóm Private trong vụ báo cáo |
| DEC-236 | Phụ thuộc | Hiện hành | Chuyển M11 | Nhóm B (đối chiếu FR-M11). M11: cờ Group tắt, lối vào vẫn hiện, mở ra thì báo hệ thống đang bận |

### C.2 Chuỗi quyết định

| Chuỗi | Nội dung hiện hành |
|---|---|
| ISS-040 → QA-022 → QA-035, QA-036, QA-037 → QA-109 → DEC-053 → DEC-209, DEC-210 | Tìm được bài viết, người dùng, Tag, Topic, Group; không tìm bình luận (QA-037 bị thay). Người dùng, Tag, Topic, Group khớp chuỗi gõ ở bất kỳ vị trí trong tên, không phân biệt hoa thường, bỏ dấu, gần đúng; chỉ so tên (người dùng: display_name, username; Group: tên, không mô tả); trong mỗi loại mục giống chuỗi gõ hơn đứng trước (DEC-209 thay "exact/prefix" của DEC-053, giữ QA-036). Group không còn tìm full-text trên tên + mô tả (QA-035 bị thay phần này). |
| DM-7.3, DM-7.4 → DEC-053, DEC-056 → DEC-211, DEC-212 → DEC-215 → DEC-263 | Bộ lọc: Topic, Tag, Hôm nay/Tuần này/Tháng này/Tất cả (theo lịch, giờ Việt Nam, theo thời điểm đăng), chỉ nội dung đang theo dõi (bài của người dùng và bài thuộc Topic đang theo dõi; DEC-215 bỏ theo dõi bài viết); mỗi loại một giá trị, nhiều bộ lọc thì bài phải thỏa tất cả; chỉ áp cho kết quả bài. Sắp xếp: Liên quan (mặc định khi có truy vấn), Mới nhất, Nhiều upvote nhất; hai cách sau sắp lại chính tập ứng viên, bằng nhau thì bài đăng sau trước. Các mục của draft không được giữ: Oldest, Most viewed, Most commented; lọc Lớp/Khối, Author; tìm theo Author, Lớp/Khối. Bài ẩn danh chỉ được giữ nhờ Topic đang theo dõi, không nhờ theo dõi tác giả (DEC-263). |
| QA-011 (DEC-171, DEC-206 ngoài bảng nguồn) ↔ DEC-062, QA-119 → DEC-208 | Guest được tìm, nhưng tìm bài luôn bằng full-text. Chỉ Guest thấy lựa chọn "Tìm kiếm thông minh"; bấm thì nhắc đăng nhập, kể cả khi AI tắt; bộ lọc theo dõi cũng nhắc Guest đăng nhập. Người đã đăng nhập luôn tìm ngữ nghĩa khi AI bật. FR-M13-04.04 (Guest không có embedding truy vấn) khớp với chuỗi này. DEC-171, DEC-206 chỉ sửa phần Guest xem hồ sơ, xem tóm tắt của QA-011. |
| QA-044 → QA-120, DEC-053, DEC-062 ↔ DEC-110, QA-188 → DEC-210; MR-M11, F-GRP-06 | Nhóm Private không hiện trong gợi ý khi gõ và kết quả tìm Group với người không là thành viên, kể cả Guest; thành viên vẫn tìm thấy nhóm. "Visible-but-gated" không còn áp cho tìm kiếm. Bài của nhóm Private chỉ hiện với thành viên. |
| DEC-108, QA-186 | Nhóm đổi Public sang Private: truy vấn tìm mới của người không phải thành viên không còn trả bài của nhóm. |
| DEC-055 → DEC-211; QA-112 | Tập ứng viên 120 bài theo Điểm liên quan. Điểm liên quan: ngữ nghĩa (cosine + 1) ÷ 2; full-text = tỷ lệ từ của truy vấn có trong bài. Điểm tương tác = (thô − nhỏ nhất) ÷ (lớn nhất − nhỏ nhất) trong tập ứng viên, cùng thô thì 0. Điểm cuối = Điểm liên quan × 0,8 + Điểm tương tác × 0,2; bằng nhau thì Điểm liên quan cao hơn, rồi bài đăng sau. |
| DEC-057 → DEC-209, DEC-211 | Full-text bỏ dấu, bài có ít nhất một từ của truy vấn là khớp. Khớp tên cho người dùng, Tag, Topic, Group theo DEC-209. |
| DEC-079 → DEC-122, DEC-211 (DEC-118, DEC-163, DEC-188 ngoài bảng nguồn); QA-236 | Bài của tác giả đang ở mức HEAVY: Điểm cuối × 0,5 khi sắp xếp theo Liên quan, ở cả hai chế độ; không giảm hạng khi sắp xếp Mới nhất, Nhiều upvote nhất; không hiện dấu hiệu. Các sửa đổi khác chỉ chạm bảng xếp hạng, phạm vi tạo bài, cách hạ mức. Bài của tài khoản BANNED vẫn hiện bình thường, kèm nhãn "Tài khoản đã bị khóa" (DEC-122, QA-205; ISS-154 là câu hỏi DEC-122 trả lời). |
| DEC-008 → DEC-092, DEC-093 → DEC-205; MR-FB-M06 | Tắt AI thì tìm bài bằng full-text. Công tắc AI tổng và công tắc Search ở cấu hình hệ thống (M10); công tắc Search điều khiển cả embedding bài và embedding truy vấn. |
| DEC-099 → DEC-205 (DEC-206, DEC-207 ngoài bảng nguồn) | AI lỗi sau lần thử lại thì tìm full-text cho riêng truy vấn đó. DEC-205 thêm tạo bù embedding cho bài (M13). |
| DEC-015 → DEC-148; DEC-020 → DEC-153, DEC-214; QA-110 → DEC-209 | Tìm người dùng chỉ gồm tài khoản ACTIVE đã xong Bước 3 (DEC-209, cùng phạm vi với danh sách @mention của DEC-153). Cách khớp tên của M06 theo DEC-209; @mention của M01 dùng cùng cách khớp (DEC-214, ngoài bảng nguồn), nên "dùng chung" của QA-110 được giữ. |
| DEC-058 → DEC-209; DEC-054 | Gợi ý khi gõ chạy khi ngừng gõ 300 mili giây, từ ký tự đầu tiên, mỗi loại tối đa 3 mục; không gợi ý tiêu đề bài. |
| DEC-051 → DEC-143, DEC-146 | Tag bị vô hiệu hóa không hiện trong gợi ý khi gõ và kết quả tìm Tag; kích hoạt lại thì hiện lại. DEC-146 (ngoài bảng nguồn) chỉ thêm ghi nhật ký thao tác Tag. |
| DEC-142, QA-275 → DEC-212; DEC-064 → DEC-211, DEC-212 | Xem bài của một Topic hay Tag là trang tìm bài với bộ lọc đó và truy vấn rỗng: mọi bài khớp bộ lọc, mặc định Mới nhất, không có Liên quan, không giới hạn 120, không gọi AI. Truy vấn có chữ: tối đa 120 kết quả, 15 mỗi lần tải; đã tải 120 mà cuộn tiếp thì hiện "Thu hẹp tìm kiếm để có kết quả chính xác hơn". |
| DEC-061 → DEC-213; QA-118 | Đoạn trích 150 ký tự đầu của nội dung chữ, cắt trước từ bị chia đôi và thêm "…"; không quá 150 thì hiện nguyên; không có nội dung chữ thì không có đoạn trích; không tô sáng. |
| DEC-059 → DEC-213 | Lịch sử trên trình duyệt, tối đa 10, mới nhất trước, không trùng; chỉ thêm khi gửi truy vấn có chữ; chọn mục thì gửi luôn; chỉ xóa toàn bộ; xóa khi đăng xuất. |
| DEC-063 → DEC-213; DEC-144; QA-121 | Giới hạn tính trong 60 giây gần nhất: Guest theo IP 30 lượt gợi ý / 10 lượt gửi, người đã đăng nhập theo tài khoản 45 / 20. Tải thêm không tính; đổi bộ lọc, đổi sắp xếp, mở trang Topic/Tag, chọn mục lịch sử tính một lượt gửi. |
