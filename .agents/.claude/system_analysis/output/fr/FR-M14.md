---
module: M14
ten_module: Feed & Discovery
ma_tai_lieu: FR-M14
phien_ban: 1.1
trang_thai: Đã chốt
ngay: 2026-10-24
tac_gia: Phạm Văn Đức
moc_nguon: DEC-271, QA-477, ISS-415, OPEN-012
steps_completed: [1, 2, 3, 4, 5, 6, 7]
---
# Tài liệu yêu cầu chức năng — M14 Feed & Discovery

| Mã tài liệu | FR-M14 |
|---|---|
| Dự án | iShare |
| Module | M14 — Feed & Discovery |
| Trạng thái | Đã chốt |
| Phiên bản | 1.1 |
| Ngày | 2026-10-24 |
| Tác giả | Phạm Văn Đức |

<!-- Quy ước chung cho mọi bảng dưới đây:
     - Thân tài liệu không ghi nguồn. Nguồn của mọi ID nằm ở Phụ lục A.
     - Ô không có nội dung ghi "—". Không xóa cột.
     - Mục chưa tới bước làm thì để dòng "(Chưa làm — bước N)". -->

## 1. Tổng quan

### 1.1 Mục đích

Feed & Discovery là trang chủ của iShare, nơi người dùng, kể cả khách chưa đăng nhập, khám phá nội dung qua bốn tab:
Trending (bài viết, Topic và Tag đang được quan tâm), Following (bài từ người dùng và Topic đang theo dõi), Group (bài từ
các nhóm đã tham gia) và Newest (bài mới nhất của toàn site). Các tab xếp bài theo thời gian hoặc theo điểm Trending,
không có tab cá nhân hóa bằng thuật toán.

### 1.2 Phạm vi

**Trong phạm vi:**

- Trang chủ feed gồm bốn tab Trending, Following, Group, Newest; tab Trending có ba mục con Trending Post, Trending
  Topic, Trending Tag.
- Trending Post: điểm theo upvote, bình luận, bookmark, giảm dần theo tuổi bài (nửa chu kỳ 7 ngày), loại bài quá 28 ngày;
  một danh sách chung, không lọc theo Topic, không ngưỡng tối thiểu; tính lại theo chu kỳ; có bài nhóm Public.
- Hiển thị Trending Topic và Trending Tag trong tab Trending (danh sách do M05 cung cấp).
- Tab Following: bài của người dùng và Topic đang theo dõi, kể cả bài nhóm Public, không gồm bài nhóm Private, theo thời
  gian; bài ẩn danh chỉ vào qua Topic đang theo dõi; trạng thái rỗng dẫn sang trang tìm kiếm.
- Tab Group: bài từ mọi nhóm (Public, Private) người dùng đã tham gia, theo thời gian; trạng thái rỗng dẫn sang
  "Khám phá Group".
- Tab Newest: bài toàn site theo thời gian, không gồm bài thuộc nhóm.
- Quyền xem theo tab của Guest (Newest, Trending xem được; Following, Group yêu cầu đăng nhập) và tab mặc định khi mở trang chủ.
- Tải bài kiểu cuộn vô hạn, mỗi lần 20 bài, cho cả bốn tab.
- Banner "có bài mới" cho Newest, Following, Group (kiểm tra định kỳ): bấm vào thì chèn bài mới lên đầu, giữ vị trí cuộn;
  Trending không có banner, mỗi lần mở tab hiện kết quả của lần tính gần nhất.
- Bài của tài khoản BANNED hoặc đang ở mức cảnh cáo HEAVY vẫn có mặt trong feed và Trending như bài thường.
- Hiển thị của feed khi cờ tính năng của module khác tắt (Group, Gamification).

**Ngoài phạm vi:**

- Tính điểm và thứ tự Trending Topic, Trending Tag — M05 Topic & Tag.
- Tìm kiếm, bộ lọc và sắp xếp kết quả (kể cả bộ lọc "đang theo dõi"; draft mục 7.3, 7.4) — M06 Search.
- Theo dõi, bỏ theo dõi người dùng và Topic; thông báo bài mới của người đang theo dõi — M07 Notification.
- Điều kiện một bài được hiển thị (trạng thái đăng, kiểm duyệt, xóa mềm) — M03 Post & Content; ẩn bài của tài khoản
  DEACTIVATED, DELETED — M01 Authentication & Account.
- Trang nhóm, bài nhóm ra feed chính, đổi chế độ Public↔Private, trang danh sách nhóm (đích của "Khám phá Group") —
  M11 Group.
- Upvote — M12 Gamification; bình luận — M04 Comment; bookmark — M02 User Profile; báo cáo — M08 Moderation. Feed chỉ
  hiển thị bài và dẫn tới các thao tác này.
- Nhãn "Tài khoản đã bị khóa" — M12 Gamification. Trạng thái cảnh cáo — M08 Moderation.
- Cờ tính năng — M10 Admin Panel (M14 là trang chủ, không có cờ riêng).
- Đã quyết không làm: tab "For You" xếp hạng cá nhân hóa (kéo theo không phụ thuộc M13 AI Layer); cập nhật feed thời
  gian thực; ngưỡng tối thiểu để vào Trending; lọc Trending Post theo Topic; SEO và dựng trang phía máy chủ ở MS1.

## 2. Thuật ngữ và viết tắt

### 2.1 Thuật ngữ

| Thuật ngữ | Định nghĩa |
|---|---|
| Feed | Trang chủ của iShare, gồm bốn tab Trending, Following, Group, Newest. |
| Tab | Một luồng bài trong feed. Tab Trending có ba mục con: Trending Post, Trending Topic, Trending Tag. |
| Bài đủ điều kiện hiển thị | Bài viết đang hiển thị với người xem theo M03 (trạng thái Đã đăng, kiểm duyệt Bình thường, chưa bị xóa mềm) và không bị ẩn vì tác giả ở trạng thái DEACTIVATED hoặc DELETED (M01). |
| Feed chính | Tập bài viết chung ngoài trang nhóm: bài đủ điều kiện hiển thị, kể cả bài của nhóm Public, không gồm bài của nhóm Private, kể cả với thành viên nhóm. |
| Bài nhóm | Bài viết đăng trong một nhóm (M11). Nhóm có chế độ Public hoặc Private. |
| Nhóm đã tham gia | Nhóm mà người xem đang là thành viên (M11) tại lúc tải tab. |
| Đối tượng đang theo dõi | Người dùng và Topic mà người xem đang theo dõi (M07). Bài viết, Tag, nhóm không theo dõi được. |
| Thời điểm đăng | Lúc bài viết chuyển sang trạng thái Đã đăng (M03). |
| Tuổi bài | Thời gian đã trôi từ thời điểm đăng của bài tới lúc tính điểm Trending Post, tính bằng ngày: 24 giờ là một ngày, giữ phần lẻ, không làm tròn theo ngày hay theo ngày lịch. |
| Lượt xem tab Trending | Khoảng từ lúc người xem mở tab Trending tới khi rời tab hoặc tải lại trang. |
| Điểm Trending Post | Điểm của một bài trong mục con Trending Post, tính theo BR-M14-10 ở mỗi lần tính lại. |
| Lần tính | Một lần hệ thống tính lại điểm Trending Post cho mọi bài trong phạm vi; kết quả dùng cho tới lần tính kế tiếp. |
| Lần tải | Một lần hệ thống trả thêm tối đa 20 bài cho tab đang xem. Lần tải đầu xảy ra khi mở tab. |
| Vị trí tải tiếp | Bài cuối cùng đã tải của một tab; lần tải sau bắt đầu ngay sau bài này. |
| Banner "có bài mới" | Thông báo trên đầu tab Newest, Following, Group cho biết đã có bài mới thuộc tab, mới hơn bài mới nhất đang hiện. |
| Bài ẩn danh | Bài nhóm mà tác giả chọn đăng ẩn danh (M11); chỉ bài nhóm mới đăng ẩn danh được; tên tác giả không hiện với người khác. |
| Trạng thái rỗng | Nội dung tab hiển thị khi tab không có bài nào, kèm một nút dẫn sang trang khác. |
| BANNED | Trạng thái tài khoản bị khóa (M08). Tên tài khoản hiện kèm nhãn "Tài khoản đã bị khóa" (M12). |
| HEAVY | Mức cảnh cáo cao nhất (M08); trạng thái cảnh cáo không hiện công khai. |
| Cờ tính năng | Công tắc của Admin bật, tắt một module (M10). Chỉ có cờ Group, Chat, Gamification. |

### 2.2 Viết tắt

| Viết tắt | Đầy đủ |
|---|---|
| FR | Functional Requirement — yêu cầu chức năng |
| BR | Business Rule — quy tắc nghiệp vụ |
| TBD | To Be Determined — điểm chưa chốt |
| MS1 | Milestone 1 — mốc phát hành đầu tiên |
| SEO | Search Engine Optimization — tối ưu để công cụ tìm kiếm lập chỉ mục |
| SSR | Server-Side Rendering — dựng sẵn trang ở máy chủ |
| CRUD | Create, Read, Update, Delete — tạo, đọc, sửa, xóa |

## 3. Thông tin đầu vào

### 3.1 Tài liệu đầu vào

| Tài liệu | Phiên bản / mốc |
|---|---|
| Draft: docs/_temp/iShare_modules.md, iShare_specs_general.md | Theo ngày sửa tệp |
| Register: decisions, qa-log, issue-queue, open-issues, glossary, module-registry | DEC-271, QA-477, ISS-415, OPEN-012 (khớp `moc_nguon`) |

### 3.2 Tài liệu liên quan

| Module | Liên quan ở điểm nào |
|---|---|
| M01 Authentication & Account | Đăng nhập để xem tab Following, Group; bài của tài khoản DEACTIVATED, DELETED bị ẩn. |
| M02 User Profile | Số bookmark của bài dùng cho điểm Trending Post. |
| M03 Post & Content | Bài đang hiển thị công khai là nguồn của mọi tab; thời điểm đăng; bài đã xóa mềm không hiện. |
| M04 Comment | Số bình luận dùng cho điểm Trending Post. |
| M05 Topic & Tag | Trending Topic, Trending Tag hiển thị trong tab Trending; nền công thức điểm Trending. |
| M06 Search | Trang tìm kiếm là đích khi tab Following rỗng. |
| M07 Notification | Quan hệ theo dõi (người dùng, Topic) cho tab Following. |
| M08 Moderation | Trạng thái cảnh cáo riêng tư, không ảnh hưởng feed. |
| M10 Admin Panel | M14 không có cờ tính năng; quy tắc chung khi cờ của module khác tắt. |
| M11 Group | Bài nhóm cho tab Group; bài nhóm Public cho Trending Post, không cho Newest; bài nhóm Public cho tab Following; bài nhóm đăng ẩn danh; trang danh sách nhóm; cờ Group tắt. |
| M12 Gamification | Upvote dùng cho điểm Trending Post; nhãn "Tài khoản đã bị khóa"; cờ Gamification tắt. |
| M13 AI Layer | Không còn phụ thuộc (không có feed cá nhân hóa bằng AI). |

## 4. Tổng quan chức năng

### 4.1 Luật, tiêu chuẩn liên quan

Không có.

### 4.2 Vai trò

| Vai trò | Mô tả trong module này |
|---|---|
| Guest | Người chưa đăng nhập. Xem tab Trending (cả ba mục con) và tab Newest. Thấy tab Following, Group nhưng phải đăng nhập mới xem được nội dung. |
| User | Người dùng đã đăng nhập. Xem cả bốn tab; tab Following theo người dùng và Topic mình đang theo dõi, tab Group theo các nhóm mình đã tham gia. |
| Mod | Có mọi quyền của User trong module này; không có quyền riêng trên feed. |
| Admin | Có mọi quyền của User trong module này; không có quyền riêng trên feed. |
| Thành viên nhóm | Vai trò theo ngữ cảnh: User, Mod hoặc Admin đã tham gia một nhóm; bài của nhóm đó vào tab Group của người này. |
| Hệ thống | Tác nhân của việc tính điểm Trending Post định kỳ. |

### 4.3 Ma trận quyền

| Hành động | Guest | User | Mod | Admin | Yêu cầu |
|---|---|---|---|---|---|
| Xem tab Trending (Trending Post, Trending Topic, Trending Tag) | ✓ | ✓ | ✓ | ✓ |FR-M14-02.01, FR-M14-02.02 |
| Xem tab Newest | ✓ | ✓ | ✓ | ✓ |FR-M14-06.01, FR-M14-06.04 |
| Xem tab Following | ✗ | ✓ (của mình) | ✓ (của mình) | ✓ (của mình) |FR-M14-04.01, FR-M14-04.04 |
| Xem tab Group | ✗ | ✓ (của mình) | ✓ (của mình) | ✓ (của mình) |FR-M14-05.01, FR-M14-05.05 |
| Tải thêm bài khi cuộn trong tab đang xem được | ✓ | ✓ | ✓ | ✓ |FR-M14-07.01, FR-M14-07.02 |
| Bấm banner "có bài mới" để xem bài mới | ✓ | ✓ | ✓ | ✓ |FR-M14-08.02, FR-M14-08.03 |

<!-- "(của mình)": tab Following theo đối tượng chính người xem đang theo dõi; tab Group theo nhóm chính người xem đã tham gia.
     Ô suy ra: cột Mod/Admin ở mọi hàng (nguồn không cho Mod/Admin quyền riêng trên feed; vai trò cao hơn xem được những gì User xem được);
     hàng 5 (tải thêm áp cho cả bốn tab, nên ai xem được tab nào thì tải thêm được ở tab đó);
     hàng 6 cột Guest (banner có ở Newest, Guest xem được Newest). Các hàng 1–4 cột Guest, User nói thẳng. -->

### 4.4 Danh sách chức năng

| ID | Chức năng | Tác nhân chính | Kích hoạt |
|---|---|---|---|
| FR-M14-01 | Mở trang chủ feed | Guest, User, Mod, Admin | Người xem truy cập trang chủ iShare |
| FR-M14-02 | Xem tab Trending | Guest, User, Mod, Admin | Người xem chọn tab Trending, hoặc trang chủ mở ở tab Trending |
| FR-M14-03 | Tính điểm Trending Post | Hệ thống | Đến chu kỳ tính lại định kỳ |
| FR-M14-04 | Xem tab Following | User, Mod, Admin | Người xem chọn tab Following |
| FR-M14-05 | Xem tab Group | Thành viên nhóm | Người xem chọn tab Group |
| FR-M14-06 | Xem tab Newest | Guest, User, Mod, Admin | Người xem chọn tab Newest |
| FR-M14-07 | Tải thêm bài khi cuộn | Guest, User, Mod, Admin | Người xem cuộn tới cuối danh sách bài đã tải của một tab |
| FR-M14-08 | Xem bài mới qua banner | Guest, User, Mod, Admin | Hệ thống phát hiện có bài mới khi kiểm tra định kỳ; người xem bấm banner "có bài mới" |

### 4.5 Mốc và ưu tiên

Toàn bộ yêu cầu của module thuộc MS1, ưu tiên **Could** (dòng M14 của bảng Module List và bảng MoSCoW Summary của
module-registry khớp nhau: Could gồm M14, M15). Không có yêu cầu ngoại lệ về ưu tiên.

## 5. Yêu cầu chức năng

### 5.1 FR-M14-01 Mở trang chủ feed

**Yêu cầu cấp trên:** Hệ thống phải cung cấp trang chủ feed gồm bốn tab Trending, Following, Group, Newest cho mọi người xem, kể cả Guest.

**Lý do:** Feed là trang chủ của iShare. Cấu trúc bốn tab, không có tab xếp hạng cá nhân hóa, giúp giản lược phạm vi và không phụ thuộc AI. Guest được xem Newest và Trending để nhất quán với quyền duyệt bài của Guest và mục tiêu giúp nội dung dễ được khám phá.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M14-01.01 | Khi người xem truy cập trang chủ, hệ thống phải hiển thị feed gồm bốn tab Trending, Following, Group, Newest (BR-M14-01). |
| FR-M14-01.02 | Khi Guest truy cập trang chủ, hệ thống phải mở feed ở tab Trending (BR-M14-03). |
| FR-M14-01.03 | Hệ thống phải hiển thị cả bốn tab với Guest, kể cả tab Following và tab Group (BR-M14-02). |
| FR-M14-01.04 | Hệ thống phải không cung cấp tab xếp hạng bài theo cá nhân hóa ngoài bốn tab của feed (BR-M14-01). |
| FR-M14-01.05 | Hệ thống phải chỉ hiển thị bài đủ điều kiện hiển thị ở mọi tab của feed (BR-M14-04). |
| FR-M14-01.06 | Hệ thống phải hiển thị ở mọi tab bài của tài khoản BANNED hoặc đang ở mức HEAVY như bài khác, với tên tài khoản BANNED kèm nhãn "Tài khoản đã bị khóa" và không hiện mức cảnh cáo (BR-M14-15). |
| FR-M14-01.07 | Hệ thống phải cho truy cập feed bất kể trạng thái các cờ tính năng (BR-M14-22). |
| FR-M14-01.08 | Khi người dùng đã đăng nhập truy cập trang chủ, hệ thống phải mở feed ở tab Trending như với Guest (BR-M14-03). |
| FR-M14-01.09 | Khi feed mở ở tab Trending, hệ thống phải hiện mục con Trending Post trước (BR-M14-03). |


### 5.2 FR-M14-02 Xem tab Trending

**Yêu cầu cấp trên:** Hệ thống phải cho mọi người xem, kể cả Guest, xem tab Trending với ba mục con Trending Post, Trending Topic, Trending Tag.

**Lý do:** Trending xếp hạng theo độ được quan tâm nên gộp mọi nguồn bài của feed chính. Trending Post là một danh sách chung vì đã có Trending Topic riêng để xem theo chủ đề; lọc thêm theo Topic là dư thừa. Guest xem được cả ba mục con vì Trending Topic, Trending Tag còn công khai hơn cả bài viết.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M14-02.01 | Khi người xem chọn tab Trending, hệ thống phải hiển thị ba mục con Trending Post, Trending Topic, Trending Tag (BR-M14-01). |
| FR-M14-02.02 | Hệ thống phải cho Guest xem tab Trending với đủ ba mục con như người đã đăng nhập (BR-M14-02). |
| FR-M14-02.03 | Khi người xem mở mục con Trending Post, hệ thống phải hiển thị bài theo kết quả của lần tính gần nhất tại lúc mở tab, xếp theo điểm Trending Post giảm dần (BR-M14-13, BR-M14-14). |
| FR-M14-02.04 | Hệ thống phải hiển thị cùng một danh sách Trending Post cho mọi người xem và không cho lọc danh sách này theo Topic (BR-M14-13). |
| FR-M14-02.05 | Nếu một bài có trong kết quả đang dùng của lượt xem nhưng không còn đủ điều kiện hiển thị lúc tải, hệ thống phải không hiển thị bài đó trong Trending Post (BR-M14-04). |
| FR-M14-02.06 | Khi người xem mở mục con Trending Topic hoặc Trending Tag, hệ thống phải hiển thị danh sách và thứ tự do M05 cung cấp (BR-M14-24). |
| FR-M14-02.07 | Hệ thống phải không hiển thị banner "có bài mới" ở tab Trending (BR-M14-19). |
| FR-M14-02.08 | Trong khi cờ Group tắt, hệ thống phải tiếp tục hiển thị bài nhóm Public trong Trending Post; việc mở bài nhóm do M11 xử lý (BR-M14-22). |
| FR-M14-02.09 | Khi một nhóm đổi từ Public sang Private, hệ thống phải không đưa bài của nhóm đó vào Trending Post của người ngoài nhóm từ lần tải kế tiếp; bài đang hiện trên màn hình đã tải do M11 xử lý (BR-M14-23). |
| FR-M14-02.10 | Hệ thống phải hiển thị trong mục con Trending Topic, Trending Tag mọi mục có điểm lớn hơn 0, mỗi lần tải tối đa 20 mục, tải thêm khi người xem cuộn (BR-M14-24). |
| FR-M14-02.11 | Trong khi người xem còn ở một lượt xem tab Trending, hệ thống phải giữ kết quả của lần tính hiện hành lúc người xem mở tab, kể cả khi đã có lần tính mới (BR-M14-19). |
| FR-M14-02.12 | Khi người xem mở lại tab Trending hoặc tải lại trang, hệ thống phải hiển thị kết quả của lần tính gần nhất (BR-M14-19). |



### 5.3 FR-M14-03 Tính điểm Trending Post

**Yêu cầu cấp trên:** Hệ thống phải tính định kỳ điểm Trending Post cho các bài của feed chính trong 28 ngày gần nhất, theo tương tác và tuổi bài.

**Lý do:** Trending Post dùng công thức giảm dần mượt hơn cửa sổ cứng của Trending Topic/Tag. Mốc 28 ngày là bội số của nửa chu kỳ 7 ngày: trọng số còn khoảng 6,25% nên không đáng kể, tránh việc bài bị cắt đột ngột khi trọng số còn lớn. Không đặt ngưỡng tối thiểu vì dữ liệu demo nhỏ, đặt ngưỡng dễ khiến Trending trống.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M14-03.01 | Khi đến chu kỳ tính lại, hệ thống phải tính điểm Trending Post cho mọi bài của feed chính có tuổi không quá 28 ngày (BR-M14-05, BR-M14-11). |
| FR-M14-03.02 | Hệ thống phải tính điểm Trending Post của một bài bằng 0,5^(t / 7) × (1 + 2 × số upvote + 1 × số bình luận + 1 × số bookmark), với t là tuổi bài (BR-M14-10). |
| FR-M14-03.03 | Hệ thống phải tính lại điểm Trending Post định kỳ, mỗi lần cách nhau 15–30 phút (BR-M14-14). |
| FR-M14-03.04 | Trong khi chưa đến lần tính kế tiếp, hệ thống phải cung cấp kết quả của lần tính gần nhất (BR-M14-14). |
| FR-M14-03.05 | Nếu bài có tuổi lớn hơn 28 ngày, hệ thống phải loại bài khỏi Trending Post bất kể điểm (BR-M14-11). |
| FR-M14-03.06 | Hệ thống phải đưa vào Trending Post mọi bài trong phạm vi, kể cả bài chưa có tương tác, không áp ngưỡng tối thiểu (BR-M14-12). |
| FR-M14-03.07 | Hệ thống phải không tính lượt xem bài vào điểm Trending Post (BR-M14-10). |
| FR-M14-03.08 | Hệ thống phải không loại, không chỉnh điểm bài của tài khoản BANNED hoặc đang ở mức HEAVY (BR-M14-15). |
| FR-M14-03.09 | Nếu bài thuộc nhóm Private, hệ thống phải không đưa bài vào Trending Post, kể cả với thành viên của nhóm (BR-M14-05). |
| FR-M14-03.10 | Khi tính điểm, hệ thống phải dùng số upvote, số bình luận và số bookmark bài đang có tại lúc tính; upvote đã rút, bình luận đã xóa và bookmark đã bỏ không được tính (BR-M14-10). |
| FR-M14-03.11 | Trong khi cờ Gamification tắt, hệ thống phải tiếp tục tính điểm Trending Post với số upvote bài đang có (BR-M14-22). |
| FR-M14-03.12 | Hệ thống phải tính tuổi bài liên tục bằng thời gian đã trôi từ thời điểm đăng, 24 giờ là một ngày, giữ phần lẻ, không làm tròn theo ngày (BR-M14-10). |
| FR-M14-03.13 | Khi tính số bình luận của bài, hệ thống phải tính cả trả lời (BR-M14-10). |
| FR-M14-03.14 | Nếu hai bài có cùng điểm Trending Post, hệ thống phải xếp bài có thời điểm đăng sau đứng trước (BR-M14-13). |
| FR-M14-03.15 | Hệ thống phải đưa mỗi upvote, bình luận và bookmark vào điểm Trending Post chậm nhất 30 phút sau khi xảy ra (BR-M14-14). |






### 5.4 FR-M14-04 Xem tab Following

**Yêu cầu cấp trên:** Hệ thống phải cho người dùng đã đăng nhập xem tab Following gồm bài của người dùng và Topic mình đang theo dõi, theo thời gian.

**Lý do:** Feed không có tab xếp hạng cá nhân hóa; tab Following lấy bài theo đúng các đối tượng người dùng đã chọn theo dõi. Khi tab rỗng, nút dẫn sang trang tìm kiếm vì tìm kiếm đúng các loại đối tượng theo dõi được, còn Trending có cả Tag là thứ không theo dõi được.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M14-04.01 | Khi người dùng đã đăng nhập chọn tab Following, hệ thống phải hiển thị bài đủ điều kiện hiển thị có tác giả là người dùng đang theo dõi hoặc có ít nhất một Topic đang theo dõi (BR-M14-08). |
| FR-M14-04.02 | Hệ thống phải hiển thị mỗi bài một lần trong tab Following, kể cả khi bài thỏa cả hai điều kiện (BR-M14-08). |
| FR-M14-04.03 | Hệ thống phải xếp bài trong tab Following theo thời điểm đăng, bài đăng sau đứng trước (BR-M14-09). |
| FR-M14-04.04 | Nếu Guest chọn tab Following, hệ thống phải yêu cầu đăng nhập và không hiển thị bài (BR-M14-02). |
| FR-M14-04.05 | Nếu người xem chưa theo dõi người dùng hay Topic nào, hệ thống phải hiển thị trạng thái rỗng kèm nút dẫn sang trang tìm kiếm (BR-M14-20). |
| FR-M14-04.06 | Khi người xem bỏ theo dõi một người dùng hoặc Topic, hệ thống phải không đưa vào tab Following từ lần tải kế tiếp các bài chỉ thỏa điều kiện nhờ đối tượng đó (BR-M14-08). |
| FR-M14-04.07 | Hệ thống phải đưa vào tab Following bài nhóm Public của đối tượng đang theo dõi, dù người xem có là thành viên nhóm hay không (BR-M14-08). |
| FR-M14-04.08 | (Đã bỏ ở phiên bản 0.1 — bài nhóm Private không vào tab Following, kể cả với thành viên; xem FR-M14-04.13) |
| FR-M14-04.09 | Nếu bài là bài ẩn danh, hệ thống phải không đưa bài vào tab Following nhờ việc người xem theo dõi tác giả (BR-M14-08). |
| FR-M14-04.10 | Khi bài ẩn danh thuộc một Topic người xem đang theo dõi, hệ thống phải đưa bài vào tab Following và hiển thị bài ở dạng ẩn danh (BR-M14-08). |
| FR-M14-04.11 | Nếu người xem có đối tượng đang theo dõi nhưng tab Following không có bài nào, hệ thống phải hiển thị trạng thái rỗng kèm nút dẫn sang trang tìm kiếm (BR-M14-20). |
| FR-M14-04.12 | Trong khi cờ Group tắt, hệ thống phải tiếp tục đưa bài nhóm vào tab Following như một lối vào; việc mở bài và tương tác do M11 xử lý (BR-M14-22). |
| FR-M14-04.13 | Nếu bài thuộc nhóm Private, hệ thống phải không đưa bài vào tab Following, kể cả khi người xem là thành viên của nhóm đó (BR-M14-08). |



### 5.5 FR-M14-05 Xem tab Group

**Yêu cầu cấp trên:** Hệ thống phải cho thành viên nhóm xem tab Group gồm bài của mọi nhóm mình đã tham gia, theo thời gian.

**Lý do:** Tab Group tổng hợp bài từ mọi nhóm đã tham gia trong một nơi, khác với việc vào từng nhóm riêng lẻ đã có ở trang nhóm.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M14-05.01 | Khi người dùng đã đăng nhập chọn tab Group, hệ thống phải hiển thị bài đủ điều kiện hiển thị của mọi nhóm đã tham gia, cả nhóm Public lẫn nhóm Private (BR-M14-07). |
| FR-M14-05.02 | Hệ thống phải xếp bài trong tab Group theo thời điểm đăng, bài đăng sau đứng trước (BR-M14-09). |
| FR-M14-05.03 | Hệ thống phải không hiển thị trong tab Group bài của nhóm mà người xem không tham gia, kể cả nhóm Public (BR-M14-07). |
| FR-M14-05.04 | Khi người xem rời một nhóm, hệ thống phải không đưa bài của nhóm đó vào tab Group từ lần tải kế tiếp (BR-M14-07). |
| FR-M14-05.05 | Nếu Guest chọn tab Group, hệ thống phải yêu cầu đăng nhập và không hiển thị bài (BR-M14-02). |
| FR-M14-05.06 | Nếu người xem chưa tham gia nhóm nào, hệ thống phải hiển thị trạng thái rỗng kèm nút "Khám phá Group" dẫn sang trang danh sách nhóm (BR-M14-21). |
| FR-M14-05.07 | Nếu người xem đã tham gia nhóm nhưng tab Group không có bài nào, hệ thống phải hiển thị trạng thái rỗng kèm nút "Khám phá Group" (BR-M14-21). |
| FR-M14-05.08 | Trong khi cờ Group tắt, hệ thống phải tiếp tục hiển thị tab Group và liệt kê bài nhóm như một lối vào; việc mở bài và tương tác do M11 xử lý (BR-M14-22). |



### 5.6 FR-M14-06 Xem tab Newest

**Yêu cầu cấp trên:** Hệ thống phải cho mọi người xem, kể cả Guest, xem tab Newest gồm bài mới nhất của toàn site không thuộc nhóm.

**Lý do:** Newest là dòng thời gian nội dung chung của site nên giữ thuần bài không thuộc nhóm.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M14-06.01 | Khi người xem chọn tab Newest, hệ thống phải hiển thị bài đủ điều kiện hiển thị không thuộc nhóm nào (BR-M14-06). |
| FR-M14-06.02 | Hệ thống phải xếp bài trong tab Newest theo thời điểm đăng, bài đăng sau đứng trước (BR-M14-09). |
| FR-M14-06.03 | Hệ thống phải không hiển thị trong tab Newest bài nhóm, cả nhóm Public lẫn nhóm Private (BR-M14-06). |
| FR-M14-06.04 | Hệ thống phải cho Guest xem tab Newest như người đã đăng nhập (BR-M14-02). |

### 5.7 FR-M14-07 Tải thêm bài khi cuộn

**Yêu cầu cấp trên:** Hệ thống phải cho người xem tải dần bài của mọi tab bằng cách cuộn, mỗi lần tối đa 20 bài.

**Lý do:** Cách tải nhất quán với cách tải lịch sử tin nhắn đã dùng ở Chat.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M14-07.01 | Khi người xem mở một trong bốn tab, hệ thống phải tải tối đa 20 bài đầu tiên của tab (BR-M14-16). |
| FR-M14-07.02 | Khi người xem cuộn tới cuối danh sách đã tải, hệ thống phải tải tối đa 20 bài tiếp theo, bắt đầu ngay sau vị trí tải tiếp (BR-M14-16). |
| FR-M14-07.03 | Nếu tab không còn bài nào sau vị trí tải tiếp, hệ thống phải dừng tải thêm (BR-M14-16). |
| FR-M14-07.04 | Khi có bài mới đăng sau lần tải đầu, hệ thống phải không lặp bài và không bỏ sót bài ở các lần tải sau (BR-M14-16). |
| FR-M14-07.05 | Trong khi người xem còn ở một lượt xem tab Trending, hệ thống phải tải thêm theo cùng kết quả đã dùng lúc mở tab, không lặp và không bỏ sót bài, kể cả khi đã có lần tính mới (BR-M14-19). |


### 5.8 FR-M14-08 Xem bài mới qua banner

**Yêu cầu cấp trên:** Hệ thống phải báo cho người xem tab Newest, Following, Group khi có bài mới và cho chèn bài mới lên đầu mà không mất vị trí đang đọc.

**Lý do:** Không tự chèn bài để người xem không bị đổi chỗ đang đọc. Dùng kiểm tra định kỳ thay vì thời gian thực vì Following và Group phải lọc riêng theo quan hệ theo dõi và thành viên của từng người, phức tạp hơn nhiều so với lợi ích ở một module ưu tiên Could.

**Yêu cầu cấp dưới:**

| ID | Yêu cầu |
|---|---|
| FR-M14-08.01 | Trong khi người xem ở tab Newest, Following hoặc Group, hệ thống phải kiểm tra định kỳ, mỗi lần cách nhau không quá 60 giây, xem có bài mới hơn bài mới nhất đang hiện không (BR-M14-17). |
| FR-M14-08.02 | Khi phát hiện có bài mới, hệ thống phải hiện banner "có bài mới" và không tự chèn bài vào danh sách (BR-M14-17). |
| FR-M14-08.03 | Khi người xem bấm banner "có bài mới", hệ thống phải chỉ tải các bài mới hơn bài mới nhất đang hiện và chèn chúng lên đầu danh sách (BR-M14-18). |
| FR-M14-08.04 | Khi chèn bài mới từ banner, hệ thống phải giữ nguyên vị trí người xem đang đọc và không tải lại toàn bộ tab (BR-M14-18). |
| FR-M14-08.05 | Hệ thống phải chỉ tính là bài mới những bài thuộc phạm vi của tab đang xem (BR-M14-17). |
| FR-M14-08.06 | Hệ thống phải hiện banner "có bài mới" chậm nhất 60 giây sau khi một bài mới thuộc tab được đăng (BR-M14-17). |
| FR-M14-08.07 | Khi người xem bấm banner "có bài mới", hệ thống phải chèn tất cả các bài mới đó lên đầu danh sách (BR-M14-18). |


### 5.9 Quy tắc nghiệp vụ

| ID | Loại | Quy tắc | Ví dụ |
|---|---|---|---|
| BR-M14-01 | Sự kiện | Feed gồm đúng bốn tab: Trending, Following, Group, Newest. Tab Trending có ba mục con: Trending Post, Trending Topic, Trending Tag. Không có tab xếp hạng cá nhân hóa. | — |
| BR-M14-02 | Ràng buộc | Guest xem được tab Trending (cả ba mục con) và tab Newest. Tab Following, Group vẫn hiện với Guest; Guest chọn vào thì được yêu cầu đăng nhập, không thấy bài. | — |
| BR-M14-03 | Sự kiện | Mọi người xem, kể cả Guest và người đã đăng nhập, mở trang chủ thì feed mở ở tab Trending, mục con Trending Post. | — |
| BR-M14-04 | Ràng buộc | Feed chỉ hiện bài đủ điều kiện hiển thị. | Bài A Đã đăng, Bình thường → hiện. Bài B đã xóa mềm → không hiện. Bài C của tài khoản DEACTIVATED → không hiện. Bài D bị Mod ẩn → không hiện. |
| BR-M14-05 | Ràng buộc | Trending Post lấy bài của feed chính: bài không thuộc nhóm và bài nhóm Public; không lấy bài nhóm Private, kể cả với thành viên nhóm đó. | P1 bài thường, P2 bài nhóm Public N1, P3 bài nhóm Private N2 → Trending Post có P1, P2; không có P3 với mọi người xem. |
| BR-M14-06 | Ràng buộc | Newest lấy bài đủ điều kiện hiển thị không thuộc nhóm nào; bài nhóm Public và Private đều không vào Newest. | Với P1, P2, P3 ở BR-M14-05 → Newest chỉ có P1. |
| BR-M14-07 | Ràng buộc | Tab Group lấy bài đủ điều kiện hiển thị của mọi nhóm đã tham gia, cả Public lẫn Private. Bài của nhóm người xem không tham gia hoặc đã rời không vào tab Group. | Người xem là thành viên N2, không là thành viên N1 → tab Group có P3, không có P2. Người xem rời N2 → lần tải sau tab Group không còn P3. |
| BR-M14-08 | Ràng buộc | Tab Following lấy bài đủ điều kiện hiển thị có tác giả là người dùng đang theo dõi, hoặc có ít nhất một Topic đang theo dõi, kể cả bài nhóm Public; bài nhóm Private không vào tab Following, kể cả với thành viên nhóm (thành viên xem ở tab Group). Bài ẩn danh (chỉ có ở bài nhóm) không vào tab nhờ việc theo dõi tác giả; chỉ vào nhờ Topic đang theo dõi và hiện ở dạng ẩn danh. Bài thỏa nhiều điều kiện chỉ hiện một lần. | Người xem A theo dõi người dùng U và Topic Toán; A là thành viên nhóm Private 12A1. Bài Q1 của U về Văn → có. Bài Q2 của V về Toán → có. Bài Q3 của U về Toán → có, một lần. Bài Q4 của V về Văn → không. Bài của U trong nhóm Public CLB Toán → có. Bài của U trong 12A1 → không (A xem ở tab Group). Bài ẩn danh của U trong CLB Toán gắn Topic Văn → không. Bài ẩn danh của U trong CLB Toán gắn Topic Toán → có, hiện ẩn danh. |
| BR-M14-09 | Sự kiện | Tab Newest, Following, Group xếp bài theo thời điểm đăng, bài đăng sau đứng trước. | Bài đăng 10:00 và 10:05 cùng ngày → bài 10:05 đứng trước. |
| BR-M14-10 | Tính toán | Điểm Trending Post của một bài = 0,5^(t / 7) × (1 + 2 × U + C + B), với t là tuổi bài (ngày, liên tục, giữ phần lẻ), U là số upvote, C là số bình luận (kể cả trả lời), B là số bookmark bài đang có tại lúc tính. Upvote đã rút, bình luận đã xóa, bookmark đã bỏ không tính. Trọng số giảm một nửa sau mỗi 7 ngày. Không tính lượt xem. | Bài 0 ngày, chưa có tương tác → 1 × 1 = 1. Bài 7 ngày, 3 upvote, 2 bình luận → 0,5 × 9 = 4,5. Bài 14 ngày, 10 upvote, 4 bình luận, 2 bookmark → 0,25 × 27 = 6,75. Bài đúng 28 ngày, 20 upvote → 0,0625 × 41 = 2,5625. Bài đăng 01/10 08:00, tính lúc 04/10 20:00 → t = 3,5, trọng số 0,707; có 2 upvote, 1 bình luận, 3 bookmark → 0,707 × 9 ≈ 6,36. |
| BR-M14-11 | Ràng buộc | Bài có tuổi lớn hơn 28 ngày bị loại khỏi Trending Post, bất kể điểm. | Bài đăng 01/10 08:00: lần tính 29/10 08:00 → t = 28, còn (trọng số 0,0625); lần tính kế tiếp 29/10 08:20 → t > 28, bị loại. Bài 29 ngày, 100 upvote → bị loại. |
| BR-M14-12 | Ràng buộc | Trending Post không có ngưỡng tối thiểu: mọi bài trong phạm vi BR-M14-05 có tuổi không quá 28 ngày đều có mặt, kể cả bài chưa có tương tác. | Bài 3 ngày, 0 upvote, 0 bình luận → điểm 0,5^(3/7) ≈ 0,743, vẫn có trong danh sách. |
| BR-M14-13 | Sự kiện | Trending Post là một danh sách chung cho mọi người xem, không lọc theo Topic, xếp theo điểm Trending Post giảm dần; hai bài bằng điểm thì bài có thời điểm đăng sau đứng trước. | P1: 1 ngày, 2 upvote, 1 bình luận → 0,906 × 6 ≈ 5,43. P2: 10 ngày, 8 upvote, 3 bình luận → 0,372 × 20 ≈ 7,43. P3: 0 ngày, chưa tương tác → 1. Thứ tự: P2, P1, P3. Bằng điểm: P4 7 ngày, 1 upvote → 0,5 × 3 = 1,5; P5 14 ngày, 2 upvote, 1 bình luận → 0,25 × 6 = 1,5 → P4 (đăng sau) đứng trước P5. |
| BR-M14-14 | Kích hoạt | Điểm Trending Post được tính lại định kỳ, mỗi lần cách nhau 15–30 phút; mỗi upvote, bình luận, bookmark có mặt trong điểm chậm nhất 30 phút sau khi xảy ra. Giữa hai lần tính, Trending Post dùng kết quả của lần tính gần nhất. | Lần tính lúc 10:00, lần kế 10:20. Bài nhận thêm 5 upvote lúc 10:05 → điểm của bài đổi từ lần tính 10:20, trong mốc 30 phút (trước 10:35). |
| BR-M14-15 | Sự kiện | Bài của tài khoản BANNED hoặc đang ở mức HEAVY không bị loại, không bị chỉnh điểm ở mọi tab. Tên tài khoản BANNED hiện kèm nhãn "Tài khoản đã bị khóa" (M12); mức cảnh cáo không hiện gì. | Bài của X (BANNED) có điểm 7,43 → vẫn đứng đúng thứ hạng theo 7,43, tên X kèm nhãn. Bài của Y (HEAVY) → hiện như bài thường. |
| BR-M14-16 | Ràng buộc | Cả bốn tab tải bài kiểu cuộn vô hạn: mỗi lần tải tối đa 20 bài, bắt đầu ngay sau vị trí tải tiếp; hết bài thì dừng. Bài mới xuất hiện sau lần tải đầu không làm lặp hay mất bài ở các lần tải sau. | Tab có 45 bài: lần 1 bài 1–20, lần 2 bài 21–40, lần 3 bài 41–45, sau đó không tải nữa. Newest đã tải bài 1–20, có 3 bài mới đăng → lần tải 2 vẫn trả bài 21–40 theo thứ tự cũ. |
| BR-M14-17 | Kích hoạt | Trong khi người xem ở tab Newest, Following hoặc Group, hệ thống kiểm tra định kỳ, mỗi lần cách nhau không quá 60 giây, xem có bài mới thuộc tab, mới hơn bài mới nhất đang hiện không; có thì hiện banner "có bài mới", chậm nhất 60 giây sau khi bài được đăng. Bài mới không tự chèn vào danh sách. | Đang xem Newest, bài mới nhất đang hiện đăng 10:00; bài mới đăng 10:01:00 → banner hiện chậm nhất 10:02:00, danh sách chưa đổi. |
| BR-M14-18 | Sự kiện | Người xem bấm banner thì hệ thống chỉ tải các bài mới hơn bài mới nhất đang hiện, chèn tất cả các bài đó lên đầu danh sách, giữ nguyên vị trí đang đọc; không tải lại toàn bộ tab. | Đang đọc bài thứ 35, có 3 bài mới → bấm banner: 3 bài vào đầu danh sách, màn hình vẫn ở bài đang đọc. Có 30 bài mới → chèn cả 30. |
| BR-M14-19 | Sự kiện | Tab Trending không có banner "có bài mới". Một lượt xem tab Trending giữ kết quả của lần tính hiện hành lúc mở tab; mọi lần tải thêm trong lượt xem dùng cùng kết quả nên không lặp, không bỏ sót bài (bài không còn đủ điều kiện hiển thị vẫn bị bỏ). Kết quả mới hiện khi người xem mở lại tab hoặc tải lại trang. | 10:10 A mở Trending Post (kết quả lần tính 10:00), thấy hạng 1–20; X ở hạng 21. 10:20 có lần tính mới, X lên hạng 5. 10:22 A cuộn → nhận hạng 21–40 của lần tính 10:00, có X ở đầu. A tải lại trang lúc 10:25 → thấy kết quả lần tính 10:20, X ở hạng 5. |
| BR-M14-20 | Kích hoạt | Người xem đã đăng nhập chưa theo dõi người dùng hay Topic nào, hoặc có theo dõi nhưng tab không có bài nào, thì tab Following hiện trạng thái rỗng kèm nút dẫn sang trang tìm kiếm (M06). | — |
| BR-M14-21 | Kích hoạt | Người xem đã đăng nhập chưa tham gia nhóm nào, hoặc đã tham gia nhưng tab không có bài nào, thì tab Group hiện trạng thái rỗng kèm nút "Khám phá Group" dẫn sang trang danh sách nhóm (M11). | — |
| BR-M14-22 | Sự kiện | M14 không có cờ tính năng. Khi cờ Group tắt: bài nhóm vẫn hiện ở Trending và tab Following, tab Group vẫn hiện và vẫn liệt kê bài nhóm như một lối vào; mở bài nhóm ra thì báo "Hệ thống đang bận, vui lòng thử lại sau" và mọi tương tác bị từ chối (M11). Khi cờ Gamification tắt: số upvote vẫn hiện trên bài, điểm Trending Post vẫn tính như thường. | — |
| BR-M14-23 | Suy diễn | Nếu nhóm đổi từ Public sang Private, bài của nhóm đang hiện trên màn hình đã tải của người ngoài nhóm vẫn đọc được nhưng không tương tác được; từ lần tải sau, bài không còn ở Trending Post của người ngoài nhóm (M11). | Người ngoài nhóm đang xem P2 ở Trending Post; N1 đổi sang Private → P2 vẫn đọc được trên màn hình đó, bấm upvote bị từ chối; tải lại → không còn P2. |
| BR-M14-24 | Sự kiện | Mục con Trending Topic, Trending Tag hiện mọi mục có điểm lớn hơn 0, theo thứ tự do M05 cung cấp; mỗi lần tải tối đa 20 mục, tải thêm khi cuộn. | Có 23 Tag điểm > 0 → lần tải 1 hiện Tag hạng 1–20, cuộn tiếp hiện hạng 21–23. |


### 5.10 Dữ liệu nghiệp vụ

| Thực thể | Thuộc tính nguồn đã nêu | Quan hệ |
|---|---|---|
| Điểm Trending Post | Bài viết, điểm, lần tính | Thuộc một bài viết; dùng số upvote (M12), số bình luận (M04), số bookmark (M02) của bài |
| Bài viết (M03) | Thời điểm đăng, tác giả, Topic, nhóm (nếu là bài nhóm), đăng ẩn danh hay không, trạng thái hiển thị, số upvote, số bình luận, số bookmark | Thuộc người dùng; có thể thuộc một nhóm (M11) |
| Quan hệ theo dõi (M07) | Người theo dõi, đối tượng được theo dõi (người dùng hoặc Topic) | Nối người dùng với người dùng hoặc Topic |
| Thành viên nhóm (M11) | Người dùng, nhóm, chế độ của nhóm (Public, Private) | Nối người dùng với nhóm |
| Trending Topic, Trending Tag (M05) | Topic hoặc Tag, điểm, thứ tự | Do M05 tính |

**Ma trận CRUD:**

| Thực thể | Tạo | Đọc | Sửa | Xóa |
|---|---|---|---|---|
| Điểm Trending Post | FR-M14-03.01 | FR-M14-02.03 | FR-M14-03.03 | Không có (được thay ở lần tính kế tiếp; bài quá 28 ngày rời danh sách, BR-M14-11) |
| Bài viết | M03 | FR-M14-02.03, FR-M14-04.01, FR-M14-05.01, FR-M14-06.01 | M03 | M03 |
| Quan hệ theo dõi | M07 | FR-M14-04.01 | M07 | M07 |
| Thành viên nhóm | M11 | FR-M14-05.01 | M11 | M11 |
| Trending Topic, Trending Tag | M05 | FR-M14-02.06 | M05 | M05 |

### 5.11 Chuyển trạng thái

Không áp dụng: nguồn không nêu trạng thái cho thực thể nào của M14. Trạng thái của bài viết, tài khoản, nhóm do M03,
M01, M11 quản lý; M14 chỉ đọc các trạng thái đó để chọn bài cho từng tab (BR-M14-04 đến BR-M14-08).

### 5.12 Giao tiếp với module khác

| Hướng | Module | Nội dung ở mức nghiệp vụ | Yêu cầu |
|---|---|---|---|
| Dùng | M01 | Trạng thái đăng nhập của người xem; ẩn bài của tài khoản DEACTIVATED, DELETED (FR-M01-13.01) | FR-M14-01.05, FR-M14-04.04, FR-M14-05.05 |
| Dùng | M02 | Số bookmark của bài, bookmark đã bỏ không còn tính | FR-M14-03.02, FR-M14-03.10 |
| Dùng | M03 | Bài đủ điều kiện hiển thị (FR-M03-07.01) và thời điểm đăng; bài đã xóa mềm không hiện | FR-M14-01.05, FR-M14-03.01, FR-M14-03.12, FR-M14-04.03, FR-M14-06.02 |
| Dùng | M04 | Số bình luận của bài, bình luận đã xóa không còn tính | FR-M14-03.02, FR-M14-03.10 |
| Dùng | M05 | Danh sách Trending Topic, Trending Tag kèm thứ tự | FR-M14-02.06 |
| Dùng | M06 | Trang tìm kiếm, đích của nút ở trạng thái rỗng của tab Following; bộ lọc "đang theo dõi" của M06 dùng cùng định nghĩa và cùng quy tắc bài ẩn danh với tab Following (M06 sở hữu bộ lọc) | FR-M14-04.05, FR-M14-04.09 |
| Dùng | M07 | Quan hệ theo dõi người dùng, Topic; bỏ theo dõi | FR-M14-04.01, FR-M14-04.06 |
| Dùng | M08 | Trạng thái BANNED, mức cảnh cáo HEAVY (riêng tư, không ảnh hưởng feed) | FR-M14-01.06 |
| Dùng | M10 | Không có cờ tính năng cho M14; trạng thái cờ Group, Gamification | FR-M14-01.07 |
| Dùng | M11 | Bài nhóm và chế độ Public, Private của nhóm; bài nhóm đăng ẩn danh; thành viên nhóm; trang danh sách nhóm; đổi chế độ nhóm; xử lý khi mở bài nhóm lúc cờ Group tắt | FR-M14-02.08, FR-M14-02.09, FR-M14-03.09, FR-M14-04.07, FR-M14-04.09, FR-M14-04.12, FR-M14-04.13, FR-M14-05.01, FR-M14-05.06, FR-M14-05.08 |
| Dùng | M12 | Số upvote của bài, upvote đã rút không còn tính; nhãn "Tài khoản đã bị khóa" | FR-M14-03.02, FR-M14-03.11, FR-M14-01.06 |
| Dùng | M02, M04, M07, M08, M11, M12 | Tương tác trên bài hiện trong feed (bookmark, bình luận, theo dõi, báo cáo, tham gia nhóm, upvote); Guest được yêu cầu đăng nhập theo quy định của module đó | — |

### 5.13 AI hỗ trợ và hành vi khi tắt AI

Không áp dụng. Module không dùng AI (không có feed cá nhân hóa bằng AI), nên không có hành vi riêng khi tắt AI.

### 5.14 Yêu cầu HMI

Chưa có — chờ giai đoạn thiết kế.

### 5.15 Chuyển màn hình

Chưa có — chờ giai đoạn thiết kế.

## 6. Lịch sử sửa đổi

| Phiên bản | Ngày | Nội dung | Người sửa |
|---|---|---|---|
| 0.1 | 2026-10-24 | Tạo mới | Phạm Văn Đức |
| 1.0 | 2026-10-24 | Chốt sau 7 bước; câu trả lời bước 6 ghi ở DEC-258–261; ở bước 7 rút bài nhóm Private khỏi tab Following (DEC-262) và áp quy tắc bài ẩn danh cho bộ lọc đang theo dõi của M06 (DEC-263) | Phạm Văn Đức |
| 1.1 | 2026-10-24 | Rà soát chéo toàn bộ FR (review-cross-module.md): ghi vào C.2 DEC-271 (làm rõ DEC-237 mà M14 trích); không đổi yêu cầu. Chốt bản 1.1 | Phạm Văn Đức |

## Phụ lục A. Truy vết

| ID | Nguồn | Căn cứ | Ghi chú |
|---|---|---|---|
| FR-M14-01 | DEC-125, DEC-126, QA-227, DEC-260, DEC-225, MR-M14, MR-A02, DM-7.1 | Nói thẳng | "Trang chủ" lấy từ DEC-225 "Feed (M14) is the home page"; bốn tab theo DEC-125; tab mặc định theo QA-227, DEC-260 |
| FR-M14-01.01 | DEC-125, DM-7.1 | Nói thẳng | — |
| FR-M14-01.02 | QA-227 | Nói thẳng | — |
| FR-M14-01.03 | DEC-126, QA-227 | Nói thẳng | — |
| FR-M14-01.04 | DEC-125, QA-225 | Nói thẳng | — |
| FR-M14-01.05 | DEC-038, DEC-145 | Suy ra | Điều kiện hiển thị của M03 (FR-M03-07.01) và ẩn bài của tài khoản DEACTIVATED, DELETED (FR-M01-13.01) áp cho mọi nơi hiện bài; DEC-038 "hidden from feed" |
| FR-M14-01.06 | QA-236, DEC-122, DEC-118, DEC-079, QA-205 | Suy ra | QA-236 nói cho Trending; tab khác suy ra vì ngoại lệ ẩn chỉ áp cho bảng xếp hạng (DEC-118, DEC-122); nhãn do M12 cung cấp |
| FR-M14-01.07 | DEC-225 | Nói thẳng | "Feed (M14) is the home page" — không có cờ riêng |
| FR-M14-01.08 | DEC-260 | Nói thẳng | — |
| FR-M14-01.09 | DEC-260, DEC-125 | Nói thẳng | — |
| FR-M14-02 | DEC-125, DEC-126, QA-227, QA-231, QA-237, DEC-260, DEC-261, DEC-052, DEC-145, DM-7.1 | Nói thẳng | Trending Topic, Trending Tag do M05 cung cấp (DEC-052 "dedicated Feed section", DEC-145) |
| FR-M14-02.01 | DEC-125 | Nói thẳng | — |
| FR-M14-02.02 | DEC-126, QA-227, QA-011 | Nói thẳng | — |
| FR-M14-02.03 | DEC-124, QA-231, DEC-260 | Nói thẳng | Xếp giảm dần theo "xếp hạng theo độ hot" (QA-233); "tại lúc mở tab" theo DEC-260 |
| FR-M14-02.04 | QA-231 | Nói thẳng | — |
| FR-M14-02.05 | DEC-038, DEC-145 | Suy ra | Kết quả lần tính có thể cũ hơn trạng thái bài; BR-M14-04 áp ở mọi lần hiển thị |
| FR-M14-02.06 | DEC-052, DEC-145 | Nói thẳng | DEC-052 "dedicated Feed section" |
| FR-M14-02.07 | QA-237 | Nói thẳng | — |
| FR-M14-02.08 | DEC-236 | Nói thẳng | — |
| FR-M14-02.09 | DEC-108, DEC-234 | Nói thẳng | "New feed/search queries by non-members exclude these posts" |
| FR-M14-02.10 | DEC-261 | Nói thẳng | — |
| FR-M14-02.11 | DEC-260 | Nói thẳng | — |
| FR-M14-02.12 | DEC-260 | Nói thẳng | — |
| FR-M14-03 | DEC-124, DEC-259, DEC-125, QA-231, QA-233, QA-235, DM-7.2, QA-271 | Nói thẳng | Bookmark chốt ở DEC-259 (đóng OPEN-009) |
| FR-M14-03.01 | DEC-124, DEC-125, DEC-111, QA-233 | Nói thẳng | — |
| FR-M14-03.02 | DEC-124, DEC-259 | Nói thẳng | Σ của DEC-124 thu về một bài; bookmark theo DEC-259 |
| FR-M14-03.03 | DEC-124 | Nói thẳng | — |
| FR-M14-03.04 | DEC-124 | Suy ra | "recalculated every 15-30 min" ⇒ điểm không đổi giữa hai lần tính |
| FR-M14-03.05 | DEC-124 | Nói thẳng | — |
| FR-M14-03.06 | QA-235 | Nói thẳng | — |
| FR-M14-03.07 | DEC-124, DM-7.2 | Suy ra | Công thức DEC-124 không có lượt xem; tín hiệu Views của draft DM-7.2 không còn |
| FR-M14-03.08 | QA-236 | Nói thẳng | — |
| FR-M14-03.09 | DEC-111, DEC-125 | Nói thẳng | "Private group posts never surface on the main feed" |
| FR-M14-03.10 | DEC-124, DEC-259 | Nói thẳng | DEC-259 "using the counts the post has at computation time" |
| FR-M14-03.11 | DEC-245 | Nói thẳng | "Trending … unchanged" |
| FR-M14-03.12 | DEC-259 | Nói thẳng | — |
| FR-M14-03.13 | DEC-259 | Nói thẳng | — |
| FR-M14-03.14 | DEC-259 | Nói thẳng | — |
| FR-M14-03.15 | DEC-259 | Nói thẳng | — |
| FR-M14-04 | DEC-125, DEC-215, DEC-258, DEC-262, DEC-126, QA-227, QA-228, QA-225, DEC-261, DM-7.1 | Nói thẳng | — |
| FR-M14-04.01 | DEC-125, DEC-215 | Nói thẳng | — |
| FR-M14-04.02 | DEC-125, DEC-215 | Suy ra | Tab là một danh sách bài ⇒ một bài không lặp |
| FR-M14-04.03 | DEC-125 | Suy ra | "chronological" ⇒ bài mới trước, như Newest |
| FR-M14-04.04 | DEC-126, QA-227 | Nói thẳng | — |
| FR-M14-04.05 | QA-228, DEC-215 | Nói thẳng | — |
| FR-M14-04.06 | DEC-215 | Suy ra | Bỏ theo dõi xóa quan hệ theo dõi (DEC-215) ⇒ bài không còn thỏa FR-M14-04.01 |
| FR-M14-04.07 | DEC-258 | Nói thẳng | — |
| FR-M14-04.08 | DEC-258, DEC-262 | Nói thẳng | Bị thay bởi DEC-262 |
| FR-M14-04.09 | DEC-258 | Nói thẳng | — |
| FR-M14-04.10 | DEC-258 | Nói thẳng | — |
| FR-M14-04.11 | DEC-261 | Nói thẳng | — |
| FR-M14-04.12 | DEC-225, DEC-236, DEC-258 | Suy ra | DEC-225 "entry points stay visible"; DEC-258 đưa bài nhóm vào tab Following ⇒ tab Following là một lối vào bài nhóm như Trending, tab Group |
| FR-M14-04.13 | DEC-262, DEC-111 | Nói thẳng | — |
| FR-M14-05 | DEC-125, QA-229, QA-230, QA-233, DEC-126, QA-227, DEC-111, DEC-261 | Nói thẳng | — |
| FR-M14-05.01 | DEC-125, QA-229 | Nói thẳng | — |
| FR-M14-05.02 | QA-229 | Suy ra | "chronological" ⇒ bài mới trước, như Newest |
| FR-M14-05.03 | DEC-111, QA-229 | Suy ra | Tab chỉ gồm nhóm đã tham gia; bài nhóm Public với người ngoài nhóm đi qua feed chính |
| FR-M14-05.04 | DEC-125 | Suy ra | "groups the user has joined" ⇒ chỉ nhóm đang là thành viên |
| FR-M14-05.05 | DEC-126, QA-230 | Nói thẳng | — |
| FR-M14-05.06 | QA-230, DEC-237 | Nói thẳng | Đích của nút theo DEC-237 L6 |
| FR-M14-05.07 | DEC-261 | Nói thẳng | — |
| FR-M14-05.08 | DEC-261, DEC-236 | Nói thẳng | — |
| FR-M14-06 | DEC-125, DEC-126, QA-227, QA-233, DM-7.1 | Nói thẳng | Newest thay cho Latest của draft |
| FR-M14-06.01 | DEC-125, QA-233 | Nói thẳng | — |
| FR-M14-06.02 | DEC-125, DM-7.1 | Suy ra | "chronological" kết hợp tên tab Newest (Latest của draft) |
| FR-M14-06.03 | QA-233 | Nói thẳng | — |
| FR-M14-06.04 | DEC-126, QA-227, QA-011 | Nói thẳng | — |
| FR-M14-07 | QA-234, DEC-260 | Nói thẳng | — |
| FR-M14-07.01 | QA-234 | Nói thẳng | "áp dụng cả 4 tab" (ISS-174) |
| FR-M14-07.02 | QA-234 | Nói thẳng | — |
| FR-M14-07.03 | QA-234 | Suy ra | Cuộn vô hạn trên danh sách hữu hạn ⇒ hết bài thì dừng |
| FR-M14-07.04 | QA-234 | Suy ra | "cursor-based" (tải tiếp từ bài cuối đã tải) ⇒ bài mới không đẩy lệch các lần tải sau |
| FR-M14-07.05 | DEC-260 | Nói thẳng | — |
| FR-M14-08 | QA-237, QA-238, QA-239, DEC-261 | Nói thẳng | — |
| FR-M14-08.01 | QA-237, QA-239, DEC-261 | Nói thẳng | — |
| FR-M14-08.02 | QA-237 | Nói thẳng | — |
| FR-M14-08.03 | QA-238 | Nói thẳng | — |
| FR-M14-08.04 | QA-238 | Nói thẳng | — |
| FR-M14-08.05 | QA-237, QA-239 | Suy ra | QA-239: banner của Following, Group phải lọc theo quan hệ theo dõi, thành viên của từng người ⇒ bài mới là bài mới của chính tab đó |
| FR-M14-08.06 | DEC-261 | Nói thẳng | — |
| FR-M14-08.07 | DEC-261 | Nói thẳng | — |
| BR-M14-01 | DEC-125, QA-225, QA-229, DM-7.1 | Nói thẳng | — |
| BR-M14-02 | DEC-126, QA-227 | Nói thẳng | — |
| BR-M14-03 | QA-227, DEC-260 | Nói thẳng | — |
| BR-M14-04 | DEC-038, DEC-145, DEC-125 | Suy ra | Điều kiện hiển thị của M03 (FR-M03-07.01) và ẩn bài của tài khoản DEACTIVATED, DELETED (FR-M01-13.01); DEC-038 "hidden from feed"; DEC-145 "only posts visible on the main feed" |
| BR-M14-05 | DEC-125, DEC-111, QA-233 | Nói thẳng | Bài nhóm Private không bao giờ ra feed chính (DEC-111) |
| BR-M14-06 | DEC-125, QA-233 | Nói thẳng | "Newest is kept as a pure non-group content stream" |
| BR-M14-07 | DEC-125, QA-229, DEC-111 | Suy ra | "groups the user has joined" ⇒ chỉ nhóm đang là thành viên; rời nhóm thì bài nhóm rời tab |
| BR-M14-08 | DEC-125, DEC-215, DEC-258, DEC-262 | Suy ra | Đối tượng theo dõi theo DEC-215, bài nhóm và bài ẩn danh theo DEC-258; bài thỏa nhiều điều kiện chỉ hiện một lần vì tab là một danh sách bài |
| BR-M14-09 | DEC-125, DM-7.1 | Suy ra | "chronological" kết hợp tên tab Newest ⇒ bài đăng sau đứng trước; áp cùng cách cho Following, Group |
| BR-M14-10 | DEC-124, DEC-259, DM-7.2 | Nói thẳng | Σ trong công thức của DEC-124 thu về một bài; bookmark, tuổi bài liên tục, bình luận gồm trả lời theo DEC-259 |
| BR-M14-11 | DEC-124, DEC-259 | Nói thẳng | "older than that are excluded"; DEC-259 "once t exceeds 28" |
| BR-M14-12 | QA-235 | Nói thẳng | — |
| BR-M14-13 | QA-231, DEC-124, DEC-259 | Nói thẳng | Xếp giảm dần suy từ "xếp hạng theo độ hot" (QA-233); bằng điểm theo DEC-259 |
| BR-M14-14 | DEC-124, DEC-259 | Nói thẳng | "recalculated every 15-30 min" ⇒ giữa hai lần tính dùng kết quả gần nhất; mốc 30 phút theo DEC-259 |
| BR-M14-15 | QA-236, DEC-122, DEC-118, DEC-079, QA-205 | Suy ra | QA-236 nói cho Trending; các tab khác suy ra vì ngoại lệ ẩn chỉ áp cho bảng xếp hạng (DEC-118, DEC-122) |
| BR-M14-16 | QA-234, DEC-261 | Nói thẳng | "cursor-based" ⇒ không lặp, không mất bài khi có bài mới |
| BR-M14-17 | QA-237, QA-239, DEC-261 | Nói thẳng | — |
| BR-M14-18 | QA-238, QA-237, DEC-261 | Nói thẳng | — |
| BR-M14-19 | QA-237, DEC-260 | Nói thẳng | — |
| BR-M14-20 | QA-228, DEC-215, DEC-261 | Nói thẳng | — |
| BR-M14-21 | QA-230, DEC-237, DEC-261 | Nói thẳng | Đích của nút theo DEC-237 L6 |
| BR-M14-22 | DEC-225, DEC-236, DEC-245, DEC-261, DEC-258 | Nói thẳng | Phần tab Following suy ra từ DEC-225 "entry points stay visible" và DEC-258 |
| BR-M14-23 | DEC-108, DEC-234 | Nói thẳng | Hành vi do M11 sở hữu; M14 là nơi người xem thấy |
| BR-M14-24 | DEC-052, DEC-145, DEC-125, DEC-261 | Nói thẳng | — |

## Phụ lục B. Câu hỏi, giả định và TBD

### B.1 Câu hỏi đã hỏi

| Mã | Loại | Câu hỏi | Trả lời | Ghi vào register |
|---|---|---|---|---|
| Q-01 | Thiếu chi tiết | Nguồn chỉ nói Guest mở trang chủ thì vào tab Trending. Người đã đăng nhập mở trang chủ thì vào tab nào? Vào tab Trending thì mục con nào hiện trước? | Mọi người, kể cả người đã đăng nhập, vào tab Trending, mục con Trending Post. | QA-461, DEC-260 |
| Q-02 | Thiếu chi tiết | Tab Following lấy bài của người dùng và Topic đang theo dõi. Bài ẩn danh của người dùng đang theo dõi có vào không (lộ tác giả)? Bài nhóm Public, bài nhóm Private (người xem là thành viên) của đối tượng đang theo dõi có vào không? | Bài ẩn danh: không vào nhờ theo dõi tác giả, chỉ vào nhờ Topic đang theo dõi (hiện ẩn danh). Bài nhóm: lấy bài nhóm Public; ban đầu chọn lấy cả bài nhóm Private khi người xem là thành viên, sau đó rút lại: bài nhóm Private không vào tab Following. | QA-456, QA-457, QA-463, DEC-258, DEC-262 |
| Q-03 | Mơ hồ | Tuổi bài trong công thức Trending Post (age_days) tính liên tục theo giờ phút hay theo số ngày nguyên? Bài đăng 01/10 08:00, tính lúc 04/10 20:00: 3,5 ngày (trọng số 0,707) hay 3 ngày (0,743)? | Liên tục: 24 giờ là một ngày, giữ phần lẻ; bài bị loại khi tuổi lớn hơn 28 ngày. | QA-459, DEC-259 |
| Q-04 | Thiếu chi tiết | Số bình luận trong điểm Trending Post có gồm trả lời không (Trending Topic/Tag ở M05 có gồm)? | Có, gồm cả trả lời. | QA-462, DEC-259 |
| Q-05 | Thiếu chi tiết | Hai bài có cùng điểm Trending Post xếp thế nào? | Bài đăng sau đứng trước. | QA-462, DEC-259 |
| Q-06 | Mơ hồ | Chu kỳ tính lại "15–30 phút" kiểm chứng bằng mốc nào? | Mỗi tương tác có mặt trong điểm chậm nhất 30 phút; chu kỳ trong 15–30 phút. | QA-462, DEC-259 |
| Q-07 | Thiếu chi tiết | Mục con Trending Topic, Trending Tag hiện bao nhiêu mục (20 mục mỗi lần tải chỉ nói cho bài)? | Mọi mục có điểm > 0, theo thứ tự M05, 20 mục mỗi lần tải. | QA-462, DEC-261 |
| Q-08 | Thiếu chi tiết | Trending Post được tính lại trong lúc người xem đang cuộn thì các lần tải sau theo kết quả cũ hay mới (có thể lặp hoặc mất bài)? | Một lượt xem giữ kết quả lúc mở tab; mọi lần tải thêm dùng kết quả đó. | QA-460, DEC-260 |
| Q-09 | Thiếu chi tiết | Chu kỳ kiểm tra bài mới "khoảng 30–60 giây" kiểm chứng bằng mốc nào? Có nhiều bài mới (ví dụ 30) thì bấm banner chèn tất cả hay tối đa 20? | Banner chậm nhất 60 giây (kiểm tra cách nhau không quá 60 giây); bấm thì chèn tất cả bài mới. | QA-462, DEC-261 |
| Q-10 | Mơ hồ | "Trending tự làm mới theo chu kỳ": thay danh sách đang hiện trên màn hình, hay chỉ khi người xem mở lại hoặc tải lại tab? | Không thay danh sách trên màn hình; kết quả mới hiện khi mở lại tab hoặc tải lại trang. | QA-460, DEC-260 |
| Q-11 | Thiếu chi tiết | Tab Following đã có đối tượng theo dõi nhưng không có bài nào, và tab Group đã tham gia nhóm nhưng không có bài nào, thì hiện gì? | Cùng trạng thái rỗng và cùng nút như khi chưa theo dõi, chưa tham gia nhóm. | QA-462, DEC-261 |
| Q-12 | Thiếu chi tiết | Khi cờ Group tắt, tab Group hiển thị thế nào (DEC-236 nêu các lối vào khác, chưa nêu tab Group)? | Tab Group vẫn hiện và liệt kê bài nhóm như lối vào; mở bài thì báo hệ thống đang bận; tương tác bị từ chối (M11). | QA-462, DEC-261 |
| Q-13 | Thiếu chi tiết | Điểm Trending Post có cộng bookmark trọng số 1 như Trending Topic/Tag không (OPEN-009, TBD-M14-01)? | Có: cộng bookmark trọng số 1, chỉ tính bookmark đang có; decay và mốc 28 ngày giữ nguyên. | QA-458, DEC-259 |

<!-- Loại: Mâu thuẫn · Mơ hồ · Thiếu chi tiết · Cần cân nhắc -->

### B.2 TBD

| ID | Nội dung | Ảnh hưởng | Lý do chưa chốt |
|---|---|---|---|
| TBD-M14-01 | (Đã đóng ở phiên bản 0.1 — DEC-259: điểm Trending Post cộng bookmark trọng số 1) | Thấp | Đã chốt |
| TBD-M14-02 | Lần tải đầu của Newest, Trending (Guest xem được) chưa được tối ưu để công cụ tìm kiếm lập chỉ mục và hiển thị xem trước khi chia sẻ link. | Thấp | OPEN-006 hoãn có chủ đích (không làm SSR/SEO ở MS1) |

<!-- Ảnh hưởng: Cao · Trung bình · Thấp. Bản chốt không được còn TBD ảnh hưởng Cao. -->

### B.3 Cần cân nhắc (ngoài dữ liệu hiện có)

| Mã | Điểm cần cân nhắc | Vì sao cần | Quyết định |
|---|---|---|---|

## Phụ lục C. Sổ nguồn

**Owner keywords:** M14, feed, Feed, bảng tin, Discovery, trending, Trending, Trending Post, decay, half-life, Newest, Latest, Popular, For You, Personalized, personalized, cá nhân hóa, tab Following, tab Group, Following tab, Group tab, có bài mới, bài mới, new-content, infinite scroll, cuộn vô hạn, cursor, empty state, Khám phá Group
**Dependency keywords:** post, bài viết, topic, Topic, tag, Tag, follow, Follow, theo dõi, group, Group, cross-post, Guest, upvote, comment, bình luận, bookmark, BANNED, HEAVY, Tài khoản đã bị khóa, search, Search, SSR, SEO, polling, timezone, Lớp/Khối, feature flag, cờ tính năng, ẩn danh, anonymous, mod_state, publish_state, removed, đã xóa
**Mục draft của module:** DM-7.1, DM-7.2
**Loại khỏi bảng nguồn (khớp nhầm):** DEC-032, DEC-065, ISS-262, QA-322, QA-030 ("bài mới" là bài vừa tạo, M03, M07); DEC-042 (sắp xếp bình luận, M04); DEC-056, DEC-064, DEC-211, DEC-213, ISS-097, QA-112, QA-122, QA-397, QA-398, MR-M06, DM-7.4 (bộ lọc, sắp xếp, phân trang của tìm kiếm, M06); DEC-110, ISS-140, QA-188 ("discovery" là tìm nhóm Private, M11); ISS-165, QA-224 (phân trang lịch sử chat, M16); DEC-254, DEC-255 ("latest message" của chat, M16); DEC-176, DEC-217, DEC-228, DEC-243, DEC-244 ("newest first" của danh sách khác); ISS-178, QA-241, MR-A03 (M15); QA-047 ("decay" của điểm, M12); DM-9.2, DM-9.5 ("popular" trong huy hiệu, thống kê); DM-13 (sơ đồ kiến trúc)

### C.1 Bảng nguồn

| Nguồn | Nhãn | Trạng thái | Dùng ở | Ghi chú |
|---|---|---|---|---|
| DEC-124 | Sở hữu | Sửa một phần bởi DEC-259 | FR-M14-02.03, FR-M14-03, FR-M14-03.01, FR-M14-03.02, FR-M14-03.03, FR-M14-03.04, FR-M14-03.05, FR-M14-03.07, FR-M14-03.10, BR-M14-10, BR-M14-11, BR-M14-13, BR-M14-14 | Nhóm A. Công thức Trending Post: decay nửa chu kỳ 7 ngày, cắt sau 28 ngày |
| DEC-125 | Sở hữu | Sửa một phần bởi DEC-215, DEC-258, DEC-260 | FR-M14-01, FR-M14-01.01, FR-M14-01.04, FR-M14-01.09, FR-M14-02, FR-M14-02.01, FR-M14-03, FR-M14-03.01, FR-M14-03.09, FR-M14-04, FR-M14-04.01, FR-M14-04.02, FR-M14-04.03, FR-M14-05, FR-M14-05.01, FR-M14-05.04, FR-M14-06, FR-M14-06.01, FR-M14-06.02, BR-M14-01, BR-M14-04, BR-M14-05, BR-M14-06, BR-M14-07, BR-M14-08, BR-M14-09, BR-M14-24 | Nhóm A. Cấu trúc 4 tab, không có tab cá nhân hóa; bài nhóm Public vào Trending Post, không vào Newest |
| DEC-126 | Sở hữu | Hiện hành | FR-M14-01, FR-M14-01.03, FR-M14-02, FR-M14-02.02, FR-M14-04, FR-M14-04.04, FR-M14-05, FR-M14-05.05, FR-M14-06, FR-M14-06.04, BR-M14-02 | Nhóm A. Guest xem Newest, Trending; Following, Group cần đăng nhập |
| DM-7.1 | Sở hữu | Sửa một phần bởi DEC-125 | FR-M14-01, FR-M14-01.01, FR-M14-02, FR-M14-04, FR-M14-06, FR-M14-06.02, BR-M14-01, BR-M14-09 | Nhóm A. Draft: các feed Latest, Popular, Trending, Following, Personalized |
| DM-7.2 | Sở hữu | Sửa một phần bởi DEC-124, DEC-259 | FR-M14-03, FR-M14-03.07, BR-M14-10 | Nhóm A. Draft: tín hiệu Trending/Popular |
| ISS-166 | Sở hữu | Trùng với QA-227 | — | Nhóm A. Guest xem feed |
| ISS-167 | Sở hữu | Trùng với DEC-125 | — | Nhóm A. Tín hiệu xếp hạng feed cá nhân hóa (N/A) |
| ISS-168 | Sở hữu | Trùng với DEC-125 | — | Nhóm A. Các tab của feed |
| ISS-169 | Sở hữu | Trùng với QA-228 | — | Nhóm A. Tab Following rỗng |
| ISS-170 | Sở hữu | Trùng với QA-240 | — | Nhóm A. Feed cá nhân hóa khi tắt AI (N/A) |
| ISS-171 | Sở hữu | Bị thay bởi ISS-185 | — | Nhóm A. Trending dùng lại công thức DEC-052 |
| ISS-172 | Sở hữu | Trùng với QA-231 | — | Nhóm A. Trending Post không lọc theo Topic |
| ISS-173 | Sở hữu | Trùng với QA-233 | — | Nhóm A. Bài nhóm Public trong Newest, Trending Post |
| ISS-174 | Sở hữu | Trùng với QA-234 | — | Nhóm A. Phân trang 4 tab |
| ISS-175 | Sở hữu | Trùng với QA-235 | — | Nhóm A. Không ngưỡng tối thiểu vào Trending |
| ISS-176 | Sở hữu | Trùng với QA-236 | — | Nhóm A. Bài của BANNED, HEAVY trong Trending |
| ISS-177 | Sở hữu | Trùng với QA-237, QA-239 | — | Nhóm A. Banner có bài mới |
| ISS-185 | Sở hữu | Trùng với DEC-124 | — | Nhóm A. Công thức Trending Post |
| ISS-186 | Sở hữu | Trùng với QA-240 | — | Nhóm A. Bỏ phụ thuộc M13 |
| ISS-187 | Sở hữu | Trùng với QA-229 | — | Nhóm A. Thêm tab Group |
| ISS-188 | Sở hữu | Trùng với QA-230 | — | Nhóm A. Hiện tab Group, tab Group rỗng |
| QA-225 | Sở hữu | Sửa một phần bởi QA-229 | FR-M14-01.04, FR-M14-04, BR-M14-01 | Nhóm A. Các tab ban đầu, không có For You |
| QA-226 | Sở hữu | Trùng với DEC-124 | — | Nhóm A. Công thức Trending Post, lý do 28 ngày |
| QA-227 | Sở hữu | Sửa một phần bởi DEC-260 | FR-M14-01, FR-M14-01.02, FR-M14-01.03, FR-M14-02, FR-M14-02.02, FR-M14-04, FR-M14-04.04, FR-M14-05, FR-M14-06, FR-M14-06.04, BR-M14-02, BR-M14-03 | Nhóm A. Guest: tab xem được, tab mặc định Trending |
| QA-228 | Sở hữu | Sửa một phần bởi DEC-215, DEC-261 | FR-M14-04, FR-M14-04.05, BR-M14-20 | Nhóm A. Tab Following rỗng dẫn sang Search |
| QA-229 | Sở hữu | Hiện hành | FR-M14-05, FR-M14-05.01, FR-M14-05.02, FR-M14-05.03, BR-M14-01, BR-M14-07 | Nhóm A. Thêm tab Group |
| QA-230 | Sở hữu | Sửa một phần bởi DEC-261 | FR-M14-05, FR-M14-05.05, FR-M14-05.06, BR-M14-21 | Nhóm A. Hiện tab Group; rỗng dẫn sang Khám phá Group |
| QA-231 | Sở hữu | Hiện hành | FR-M14-02, FR-M14-02.03, FR-M14-02.04, FR-M14-03, BR-M14-13 | Nhóm A. Trending Post một danh sách chung |
| QA-232 | Sở hữu | Bị thay bởi QA-233 | — | Nhóm A. Bài nhóm Public vào Newest, Trending (bản đầu) |
| QA-233 | Sở hữu | Hiện hành | FR-M14-03, FR-M14-03.01, FR-M14-05, FR-M14-06, FR-M14-06.01, FR-M14-06.03, BR-M14-05, BR-M14-06 | Nhóm A. Bài nhóm Public: vào Trending Post, tab Group; không vào Newest |
| QA-234 | Sở hữu | Sửa một phần bởi DEC-134, DEC-260 | FR-M14-07, FR-M14-07.01, FR-M14-07.02, FR-M14-07.03, FR-M14-07.04, BR-M14-16 | Nhóm A. Cuộn vô hạn, 20 bài/lần, theo con trỏ; SSR hoãn |
| QA-235 | Sở hữu | Hiện hành | FR-M14-03, FR-M14-03.06, BR-M14-12 | Nhóm A. Không ngưỡng tối thiểu vào Trending |
| QA-236 | Sở hữu | Hiện hành | FR-M14-01.06, FR-M14-03.08, BR-M14-15 | Nhóm A. Không loại bài BANNED, HEAVY khỏi Trending |
| QA-237 | Sở hữu | Sửa một phần bởi DEC-260, DEC-261 | FR-M14-02, FR-M14-02.07, FR-M14-08, FR-M14-08.01, FR-M14-08.02, FR-M14-08.05, BR-M14-17, BR-M14-18, BR-M14-19 | Nhóm A. Banner có bài mới cho Newest/Following/Group; Trending tự làm mới theo chu kỳ |
| QA-238 | Sở hữu | Sửa một phần bởi DEC-261 | FR-M14-08, FR-M14-08.03, FR-M14-08.04, BR-M14-18 | Nhóm A. Bấm banner chỉ chèn bài mới, giữ vị trí cuộn |
| QA-239 | Sở hữu | Hiện hành | FR-M14-08, FR-M14-08.01, FR-M14-08.05, BR-M14-17 | Nhóm A. Banner dùng polling, không thời gian thực |
| QA-240 | Sở hữu | Hiện hành | Không áp dụng: M14 không dùng AI, ghi ở mục 5.13 | Nhóm A. Bỏ phụ thuộc M13 |
| MR-A02 | Sở hữu | Sửa một phần bởi DEC-215, DEC-259 | FR-M14-01 | Nhóm A. Đợt sửa phạm vi Phase 5 của M14 |
| MR-M14 | Sở hữu | Sửa một phần bởi DEC-258, DEC-259, DEC-260, DEC-261, DEC-262 | FR-M14-01 | Nhóm A. Dòng module M14 |
| DEC-258 | Sở hữu | Sửa một phần bởi DEC-262 | FR-M14-04, FR-M14-04.07, FR-M14-04.08, FR-M14-04.09, FR-M14-04.10, FR-M14-04.12, BR-M14-08, BR-M14-22 | Nhóm A. Nội dung tab Following: bài nhóm Public; bài ẩn danh chỉ qua Topic (phần bài nhóm Private bị DEC-262 rút) |
| DEC-259 | Sở hữu | Hiện hành | FR-M14-03, FR-M14-03.02, FR-M14-03.10, FR-M14-03.12, FR-M14-03.13, FR-M14-03.14, FR-M14-03.15, BR-M14-10, BR-M14-11, BR-M14-13, BR-M14-14 | Nhóm A. Chi tiết điểm Trending Post: bookmark, tuổi bài liên tục, bình luận gồm trả lời, bằng điểm, mốc 30 phút |
| DEC-260 | Sở hữu | Hiện hành | FR-M14-01, FR-M14-01.08, FR-M14-01.09, FR-M14-02, FR-M14-02.03, FR-M14-02.11, FR-M14-02.12, FR-M14-07, FR-M14-07.05, BR-M14-03, BR-M14-19 | Nhóm A. Tab mặc định Trending, mục con Trending Post; lượt xem Trending giữ kết quả lúc mở tab |
| DEC-261 | Sở hữu | Hiện hành | FR-M14-02, FR-M14-02.10, FR-M14-04, FR-M14-04.11, FR-M14-05, FR-M14-05.07, FR-M14-05.08, FR-M14-08, FR-M14-08.01, FR-M14-08.06, FR-M14-08.07, BR-M14-16, BR-M14-17, BR-M14-18, BR-M14-20, BR-M14-21, BR-M14-22, BR-M14-24 | Nhóm A. Danh sách xác nhận: số mục Trending Topic/Tag, tab rỗng khi chưa có bài, tab Group khi cờ Group tắt, banner 60 giây |
| DEC-262 | Sở hữu | Hiện hành | FR-M14-04, FR-M14-04.08, FR-M14-04.13, BR-M14-08 | Nhóm A. Bài nhóm Private không vào tab Following; DEC-111 giữ nguyên |
| DEC-263 | Sở hữu | Hiện hành | Chuyển M06 | Nhóm A. Bộ lọc đang theo dõi của M06 dùng cùng quy tắc bài ẩn danh với tab Following |
| ISS-394 | Sở hữu | Trùng với DEC-258 | — | Nhóm A. Câu hỏi ở bước 6 FR M14; nội dung ghi ở DEC-258 |
| ISS-395 | Sở hữu | Trùng với DEC-258 | — | Nhóm A. Câu hỏi ở bước 6 FR M14; nội dung ghi ở DEC-258 |
| ISS-396 | Sở hữu | Trùng với DEC-259 | — | Nhóm A. Câu hỏi ở bước 6 FR M14; nội dung ghi ở DEC-259 |
| ISS-397 | Sở hữu | Trùng với DEC-259 | — | Nhóm A. Câu hỏi ở bước 6 FR M14; nội dung ghi ở DEC-259 |
| ISS-398 | Sở hữu | Trùng với DEC-260 | — | Nhóm A. Câu hỏi ở bước 6 FR M14; nội dung ghi ở DEC-260 |
| ISS-399 | Sở hữu | Trùng với DEC-260 | — | Nhóm A. Câu hỏi ở bước 6 FR M14; nội dung ghi ở DEC-260 |
| ISS-400 | Sở hữu | Trùng với DEC-261 | — | Nhóm A. Câu hỏi ở bước 6 FR M14; nội dung ghi ở DEC-261 |
| QA-456 | Sở hữu | Trùng với DEC-258 | — | Nhóm A. Câu trả lời ở bước 6 FR M14; nội dung ghi ở DEC-258 |
| QA-457 | Sở hữu | Trùng với DEC-258 | — | Nhóm A. Câu trả lời ở bước 6 FR M14; nội dung ghi ở DEC-258 (phần bài nhóm Private bị DEC-262 rút) |
| QA-458 | Sở hữu | Trùng với DEC-259 | — | Nhóm A. Câu trả lời ở bước 6 FR M14; nội dung ghi ở DEC-259 |
| QA-459 | Sở hữu | Trùng với DEC-259 | — | Nhóm A. Câu trả lời ở bước 6 FR M14; nội dung ghi ở DEC-259 |
| QA-460 | Sở hữu | Trùng với DEC-260 | — | Nhóm A. Câu trả lời ở bước 6 FR M14; nội dung ghi ở DEC-260 |
| QA-461 | Sở hữu | Trùng với DEC-260 | — | Nhóm A. Câu trả lời ở bước 6 FR M14; nội dung ghi ở DEC-260 |
| QA-462 | Sở hữu | Trùng với DEC-261 | — | Nhóm A. Câu trả lời ở bước 6 FR M14; nội dung ghi ở DEC-261 |
| ISS-401 | Sở hữu | Trùng với DEC-262 | — | Nhóm A. Câu hỏi ở bước 7 FR M14; xem DEC-262 |
| QA-463 | Sở hữu | Trùng với DEC-262 | — | Nhóm A. Câu trả lời ở bước 7 FR M14; nội dung ghi ở DEC-262 |
| ISS-402 | Sở hữu | Trùng với DEC-263 | — | Nhóm A. Câu hỏi ở bước 7 FR M14; xem DEC-263 |
| QA-464 | Sở hữu | Trùng với DEC-263 | — | Nhóm A. Câu trả lời ở bước 7 FR M14; nội dung ghi ở DEC-263 |
| DEC-038 | Phụ thuộc | Hiện hành | FR-M14-01.05, FR-M14-02.05, BR-M14-04 | Nhóm B. M03: bài đã xóa mềm ẩn khỏi feed; DEC-162, DEC-184 (M03) chỉ sửa phần khôi phục, hết hạn; phần ẩn khỏi feed giữ nguyên |
| DEC-051 | Nhắc tới | Sửa một phần bởi DEC-143 | Không áp dụng: M05: Tag vô hiệu hóa ẩn khỏi Trending Tag | Nhóm B. M05: Tag vô hiệu hóa ẩn khỏi Trending Tag |
| DEC-052 | Phụ thuộc | Sửa một phần bởi DEC-145 | FR-M14-02, FR-M14-02.06, BR-M14-24 | Nhóm B. M05: Trending Topic/Tag là một mục của feed (ghi chú cho M14) |
| DEC-079 | Phụ thuộc | Sửa một phần bởi DEC-118, DEC-122 | FR-M14-01.06, BR-M14-15 | Nhóm B. M08: trạng thái cảnh cáo riêng tư, chỉ ảnh hưởng bảng xếp hạng |
| DEC-108 | Phụ thuộc | Sửa một phần bởi DEC-234 | FR-M14-02.09, BR-M14-23 | Nhóm B. M11: đổi Public↔Private, bài đã hiện trên feed |
| DEC-111 | Phụ thuộc | Sửa một phần bởi DEC-234, DEC-258, DEC-262 | FR-M14-03.01, FR-M14-03.09, FR-M14-04.13, FR-M14-05, FR-M14-05.03, BR-M14-05, BR-M14-07 | Nhóm B. M11: bài nhóm hiện ở feed thành viên; bài nhóm Public ra feed chính |
| DEC-234 | Phụ thuộc | Hiện hành | FR-M14-02.09, BR-M14-23 | Nhóm B (bước 2). M11: làm rõ DEC-108, DEC-111 — "đã hiện" là bài đang hiện trên màn hình đã tải; người ngoài nhóm tương tác bài nhóm Public như bài thường |
| DEC-135 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung: banner feed giữ polling | Nhóm B. Dùng chung: banner feed giữ polling |
| DEC-143 | Nhắc tới | Hiện hành | Không áp dụng: M05: kích hoạt lại Tag, Tag hiện lại ở Trending Tag | Nhóm B. M05: kích hoạt lại Tag, Tag hiện lại ở Trending Tag |
| DEC-145 | Phụ thuộc | Hiện hành | FR-M14-01.05, FR-M14-02, FR-M14-02.05, FR-M14-02.06, BR-M14-04, BR-M14-24 | Nhóm B. M05: công thức Trending Topic/Tag, phạm vi bài của feed chính |
| DEC-212 | Nhắc tới | Sửa một phần bởi DEC-215 | Không áp dụng: M06: bộ lọc đang theo dõi như tab Following M14 | Nhóm B. M06: bộ lọc đang theo dõi như tab Following M14 |
| DEC-215 | Sở hữu | Hiện hành | FR-M14-04, FR-M14-04.01, FR-M14-04.02, FR-M14-04.05, FR-M14-04.06, BR-M14-08, BR-M14-20 | Nhóm B. M07: đối tượng theo dõi chỉ còn người dùng, Topic; tab Following bỏ bài đang theo dõi |
| DEC-225 | Phụ thuộc | Sửa một phần bởi DEC-236, DEC-245 | FR-M14-01, FR-M14-01.07, FR-M14-04.12, BR-M14-22 | Nhóm B. M10: M14 là trang chủ, không có cờ tính năng; quy tắc cờ tắt |
| DEC-236 | Phụ thuộc | Sửa một phần bởi DEC-261 | FR-M14-02.08, FR-M14-04.12, FR-M14-05.08, BR-M14-22 | Nhóm B. M11: cờ Group tắt, bài nhóm vẫn hiện ở Trending, mở ra thì báo bận |
| DEC-237 | Phụ thuộc | Hiện hành | FR-M14-05.06, BR-M14-21 | Nhóm B. M11: L6 trang danh sách nhóm là đích của Khám phá Group; DEC-240 sửa phần duyệt bài của Owner; L6 giữ nguyên |
| DEC-245 | Phụ thuộc | Hiện hành | FR-M14-03.11, BR-M14-22 | Nhóm B. M12: cờ Gamification tắt, số upvote vẫn hiện, Trending không đổi |
| DG-4 | Nhắc tới | Hiện hành | Không áp dụng: Bản đồ module: Discovery/Search gồm các luồng feed | Nhóm B. Bản đồ module: Discovery/Search gồm các luồng feed |
| DG-5 | Sở hữu | Sửa một phần bởi DEC-125 | Không áp dụng: phần cá nhân hóa feed bị DEC-125 thay; phần còn lại thuộc module khác | Nhóm B. Nguyên tắc: Personalized Feed theo Lớp/Khối và đang theo dõi |
| DM-1.2 | Sở hữu | Sửa một phần bởi DEC-125 | Không áp dụng: phần cá nhân hóa feed bị DEC-125 thay; phần còn lại thuộc M02 | Nhóm B. Draft hồ sơ: Lớp/Khối dùng để cá nhân hóa feed |
| DM-3.3 | Sở hữu | Sửa một phần bởi DEC-125 | Không áp dụng: phần Personalized Feed bị DEC-125 thay; phần còn lại thuộc M05 | Nhóm B. Draft Lớp/Khối: tiêu chí ưu tiên trong Personalized Feed |
| DM-7 | Nhắc tới | Hiện hành | Không áp dụng: Draft: tiêu đề mục Discovery / Search | Nhóm B. Draft: tiêu đề mục Discovery / Search |
| DM-x02 | Sở hữu | Sửa một phần bởi DEC-125 | Không áp dụng: danh sách feed của draft bị DEC-125 thay; phần còn lại thuộc module khác | Nhóm B. Draft phạm vi: Feed (Latest, Popular, Trending, Following, Personalized) |
| GL:Lớp/Khối | Sở hữu | Sửa một phần bởi DEC-125 | Không áp dụng: phần cá nhân hóa feed bị DEC-125 thay; Lớp/Khối thuộc M02, M03 | Nhóm B. Thuật ngữ: Lớp/Khối dùng để cá nhân hóa feed |
| ISS-082 | Nhắc tới | Hiện hành | Không áp dụng: M05: cửa sổ Trending Tag | Nhóm B. M05: cửa sổ Trending Tag |
| ISS-138 | Nhắc tới | Trùng với DEC-108 | — | Nhóm B. M11: đổi Public↔Private, bài trên feed |
| ISS-141 | Nhắc tới | Trùng với DEC-111 | — | Nhóm B. M11: bài nhóm ra feed chính |
| ISS-198 | Nhắc tới | Trùng với DEC-135 | — | Nhóm B. Dùng chung: banner feed là polling |
| ISS-211 | Nhắc tới | Trùng với QA-271 | — | Nhóm B. M05: đổi công thức Trending Topic/Tag; mở OPEN-009 |
| ISS-225 | Nhắc tới | Trùng với DEC-145 | — | Nhóm B. M05: Trending tính trên bài, tương tác nào |
| ISS-226 | Nhắc tới | Trùng với DEC-145 | — | Nhóm B. M05: chu kỳ tính lại Trending |
| ISS-227 | Nhắc tới | Trùng với DEC-145 | — | Nhóm B. M05: mục điểm 0, thứ tự bằng điểm |
| OPEN-006 | Phụ thuộc | Hiện hành | TBD-M14-02 | Nhóm B. Dùng chung: SEO/SSR cho feed của Guest hoãn ở MS1 |
| OPEN-009 | Sở hữu | Bị thay bởi DEC-259 | — | Nhóm B. Trending Post có thêm bookmark trọng số 1 không; đóng bởi DEC-259 (có thêm) |
| QA-043 | Phụ thuộc | Sửa một phần bởi DEC-215 | Chuyển M07 | Nhóm B. M07: phạm vi theo dõi (đã sửa bởi DEC-215) |
| QA-106 | Phụ thuộc | Sửa một phần bởi DEC-145 | Chuyển M05 | Nhóm B. M05: công thức gốc Trending, nền điểm của Trending Post |
| QA-186 | Phụ thuộc | Trùng với DEC-108 | — | Nhóm B. M11: đổi Public↔Private, bài trên feed |
| QA-189 | Phụ thuộc | Trùng với DEC-111 | — | Nhóm B. M11: bài nhóm ra feed chính |
| QA-257 | Nhắc tới | Trùng với DEC-135 | — | Nhóm B. Dùng chung: banner feed là polling |
| QA-271 | Sở hữu | Sửa một phần bởi DEC-259 | FR-M14-03 | Nhóm B. M05: công thức Trending Topic/Tag; Trending Post thêm bookmark để review ở M14 |
| QA-285 | Phụ thuộc | Trùng với DEC-145 | — | Nhóm B. M05: bài trên feed chính tính vào Trending |
| QA-286 | Phụ thuộc | Trùng với DEC-145 | — | Nhóm B. M05: mốc 30 phút đưa tương tác vào Trending |
| QA-287 | Phụ thuộc | Trùng với DEC-145 | — | Nhóm B. M05: chỉ hiện mục điểm > 0, thứ tự khi bằng điểm |
| QA-400 | Nhắc tới | Sửa một phần bởi DEC-215 | Không áp dụng: M06: bộ lọc đang theo dõi như tab Following M14 | Nhóm B. M06: bộ lọc đang theo dõi như tab Following M14 |
| QA-405 | Phụ thuộc | Trùng với DEC-215 | — | Nhóm B. M07: bỏ theo dõi bài viết; theo dõi Topic chỉ dùng cho tab Following, bộ lọc |
| QA-429 | Phụ thuộc | Trùng với DEC-236 | — | Nhóm B. M11: cờ Group tắt, bài nhóm vẫn hiện ở Trending |
| MR-M05 | Nhắc tới | Hiện hành | Không áp dụng: Dòng module M05: trending cửa sổ 7 ngày | Nhóm B. Dòng module M05: trending cửa sổ 7 ngày |
| DEC-118 | Phụ thuộc | Hiện hành | FR-M14-01.06, BR-M14-15 | Nhóm C. M12: ngoại lệ ẩn HEAVY chỉ áp cho bảng xếp hạng; DEC-242, DEC-246 chỉ làm rõ bảng xếp hạng (M12) |
| DEC-122 | Phụ thuộc | Hiện hành | FR-M14-01.06, BR-M14-15 | Nhóm C. M12: BANNED vẫn hiện bài, có nhãn Tài khoản đã bị khóa; DEC-242, DEC-246 chỉ làm rõ bảng xếp hạng (M12) |
| DEC-134 | Phụ thuộc | Hiện hành | TBD-M14-02 | Nhóm C. Dùng chung: SPA, không SSR ở MS1 |
| QA-011 | Phụ thuộc | Hiện hành | FR-M14-02.02, FR-M14-06.04 | Nhóm C. Quyền của Guest: xem bài, không tương tác; DEC-171, DEC-206, DEC-208 sửa phần hồ sơ, tóm tắt AI, tìm kiếm; không chạm feed |
| QA-205 | Phụ thuộc | Hiện hành | FR-M14-01.06, BR-M14-15 | Nhóm C. M12: nhãn Tài khoản đã bị khóa ở mọi nơi có tên tác giả |
| QA-256 | Phụ thuộc | Trùng với DEC-134 | — | Nhóm C. Dùng chung: không SSR, SEO ở MS1 (OPEN-006) |
| DEC-127 | Phụ thuộc | Hiện hành | Không áp dụng: tuổi bài tính liên tục (DEC-259), không theo ranh giới ngày | Nhóm D. Dùng chung: múi giờ UTC+7, tính tuổi bài theo ngày |
| DEC-128 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M14 |
| DEC-129 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M14 |
| DEC-130 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M14 |
| DEC-131 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M14 |
| DEC-132 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M14 |
| DEC-133 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M14 |
| DEC-136 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M14 |
| DEC-137 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M14 |
| DEC-138 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M14 |
| ISS-189 | Nhắc tới | Trùng với DEC-127 | — | Nhóm D. Dùng chung; không quy định hành vi M14 |
| ISS-190 | Nhắc tới | Trùng với DEC-128 | — | Nhóm D. Dùng chung; không quy định hành vi M14 |
| ISS-191 | Nhắc tới | Trùng với DEC-129 | — | Nhóm D. Dùng chung; không quy định hành vi M14 |
| ISS-192 | Nhắc tới | Trùng với DEC-130 | — | Nhóm D. Dùng chung; không quy định hành vi M14 |
| ISS-193 | Nhắc tới | Trùng với DEC-131 | — | Nhóm D. Dùng chung; không quy định hành vi M14 |
| ISS-194 | Nhắc tới | Trùng với DEC-132 | — | Nhóm D. Dùng chung; không quy định hành vi M14 |
| ISS-195 | Nhắc tới | Trùng với DEC-133 | — | Nhóm D. Dùng chung; không quy định hành vi M14 |
| ISS-196 | Nhắc tới | Trùng với QA-255 | — | Nhóm D. Dùng chung; không quy định hành vi M14 |
| ISS-197 | Nhắc tới | Trùng với DEC-134 | — | Nhóm D. Dùng chung; không quy định hành vi M14 |
| ISS-199 | Nhắc tới | Trùng với DEC-136 | — | Nhóm D. Dùng chung; không quy định hành vi M14 |
| ISS-200 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M14 |
| ISS-201 | Nhắc tới | Trùng với QA-260 | — | Nhóm D. Dùng chung; không quy định hành vi M14 |
| ISS-202 | Nhắc tới | Trùng với QA-261 | — | Nhóm D. Dùng chung; không quy định hành vi M14 |
| ISS-203 | Nhắc tới | Trùng với QA-263 | — | Nhóm D. Dùng chung; không quy định hành vi M14 |
| ISS-204 | Nhắc tới | Trùng với DEC-138 | — | Nhóm D. Dùng chung; không quy định hành vi M14 |
| QA-248 | Nhắc tới | Trùng với DEC-127 | — | Nhóm D. Dùng chung; không quy định hành vi M14 |
| QA-249 | Nhắc tới | Trùng với DEC-128 | — | Nhóm D. Dùng chung; không quy định hành vi M14 |
| QA-250 | Nhắc tới | Trùng với DEC-129 | — | Nhóm D. Dùng chung; không quy định hành vi M14 |
| QA-251 | Nhắc tới | Trùng với DEC-130 | — | Nhóm D. Dùng chung; không quy định hành vi M14 |
| QA-252 | Nhắc tới | Trùng với DEC-131 | — | Nhóm D. Dùng chung; không quy định hành vi M14 |
| QA-253 | Nhắc tới | Trùng với DEC-132 | — | Nhóm D. Dùng chung; không quy định hành vi M14 |
| QA-254 | Nhắc tới | Trùng với DEC-133 | — | Nhóm D. Dùng chung; không quy định hành vi M14 |
| QA-255 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M14 |
| QA-258 | Nhắc tới | Trùng với DEC-136 | — | Nhóm D. Dùng chung; không quy định hành vi M14 |
| QA-259 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M14 |
| QA-260 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M14 |
| QA-261 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M14 |
| QA-262 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M14 |
| QA-263 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M14 |
| QA-264 | Nhắc tới | Trùng với DEC-138 | — | Nhóm D. Dùng chung; không quy định hành vi M14 |
| MR-A04 | Nhắc tới | Hiện hành | Không áp dụng: Dùng chung | Nhóm D. Dùng chung; không quy định hành vi M14 |
| MR-A05 | Nhắc tới | Trùng với DEC-137 | — | Nhóm D. Dùng chung; không quy định hành vi M14 |

### C.2 Chuỗi quyết định

| Chuỗi | Nội dung hiện hành |
|---|---|
| DM-7.1, DM-x02 → QA-225 → QA-229 → DEC-125 → DEC-215 → DEC-258 → DEC-262, DEC-260 (ISS-167, ISS-168, QA-227) | Feed gồm bốn tab: Trending (mục con Post, Topic, Tag), Following, Group, Newest. Latest của draft thành Newest; Popular và Personalized của draft bỏ; thêm tab Group. Không có tab "For You". Mọi người mở trang chủ vào tab Trending, mục con Trending Post. Following lấy bài theo người dùng và Topic đang theo dõi (không còn bài đang theo dõi), kể cả bài nhóm Public, không gồm bài nhóm Private (DEC-262 rút phần này của DEC-258); bài ẩn danh chỉ vào nhờ Topic đang theo dõi, hiện ở dạng ẩn danh. |
| DG-5, DM-1.2, DM-3.3, GL:Lớp/Khối → DEC-125 (ISS-167) | Phần "Lớp/Khối dùng để cá nhân hóa feed, ưu tiên đúng lớp/khối" của draft hết hiệu lực: không tab nào ưu tiên bài theo Lớp/Khối. Các vai trò khác của Lớp/Khối thuộc module khác. |
| DM-7.2, QA-106 → DEC-052 → ISS-171 → ISS-185, DEC-124 (QA-226) → OPEN-009 (QA-271) → DEC-259 | Trending Post: điểm của bài = 0,5^(t / 7) × (1 + 2 × số upvote + số bình luận + số bookmark), t là tuổi bài tính liên tục bằng ngày (giữ phần lẻ); dùng số bài đang có, bình luận gồm trả lời, tương tác đã rút hoặc xóa không tính; bài có tuổi lớn hơn 28 ngày bị loại; bằng điểm thì bài đăng sau đứng trước; tính lại mỗi 15–30 phút, mỗi tương tác vào điểm chậm nhất 30 phút. Không tính lượt xem. Views, Stars, Comments, Bookmarks, Recency của draft còn upvote, bình luận, bookmark, tuổi bài. OPEN-009 đã đóng. |
| DEC-052 → DEC-145 → DEC-261 (QA-285, QA-286, QA-287) | Trending Topic, Trending Tag theo công thức DEC-145 của M05 (cửa sổ 7 ngày, không decay); M14 hiển thị mọi mục có điểm > 0 theo thứ tự M05, mỗi lần tải 20 mục. Ghi chú "tích hợp thành một mục của Feed" của DEC-052 còn hiệu lực. |
| QA-232 → QA-233 (DEC-125, ISS-173) | Bài nhóm Public vào Trending Post và tab Group (của thành viên), không vào Newest. Bản đầu của QA-232 (vào cả Newest) hết hiệu lực. Bài nhóm vào tab Following theo DEC-258. |
| QA-234 → DEC-134, QA-256, OPEN-006 → DEC-260 (ISS-174) | Cả bốn tab tải kiểu cuộn vô hạn theo con trỏ, mỗi lần 20 bài. Một lượt xem tab Trending tải thêm theo cùng kết quả lúc mở tab. Phần dựng sẵn lần tải đầu cho công cụ tìm kiếm (SSR) hoãn ở MS1 (TBD-M14-02). |
| QA-237 → QA-238 → QA-239 → DEC-260, DEC-261 (DEC-135, ISS-177) | Newest, Following, Group không tự chèn bài: kiểm tra định kỳ cách nhau không quá 60 giây, banner "có bài mới" hiện chậm nhất 60 giây sau khi bài thuộc tab được đăng; bấm vào chỉ tải và chèn tất cả bài mới lên đầu, giữ vị trí cuộn. Không thời gian thực. Trending không có banner: một lượt xem giữ kết quả lúc mở tab, kết quả mới hiện khi mở lại tab hoặc tải lại trang. |
| QA-228 → DEC-215 → DEC-261 (ISS-169, QA-230) | Tab Following chưa theo dõi gì hoặc không có bài: trạng thái rỗng kèm nút dẫn sang trang tìm kiếm; đối tượng theo dõi là người dùng và Topic. Tab Group chưa tham gia nhóm nào hoặc không có bài: trạng thái rỗng kèm nút "Khám phá Group". |
| QA-043 → DEC-212 → DEC-215 (QA-400, QA-405) | Đối tượng theo dõi: người dùng và Topic. Theo dõi bài viết bị bỏ; Tag, Group không theo dõi được. |
| DEC-079 → DEC-118, DEC-122 (QA-236, QA-205) | Bài của tài khoản HEAVY, BANNED không bị loại, không bị hạ điểm trong feed và Trending. BANNED có nhãn "Tài khoản đã bị khóa" (M12); mức cảnh cáo không hiện ra. Ngoại lệ ẩn chỉ áp cho bảng xếp hạng. |
| DEC-108, DEC-111 → DEC-234, DEC-258 → DEC-262 (QA-186, QA-189) | Bài nhóm luôn hiện với thành viên; bài nhóm Public còn ra feed chính (Trending Post, tab Following); bài nhóm Private không bao giờ ra feed chính, chỉ ở trang nhóm và tab Group của thành viên. Ngoại lệ tab Following của DEC-258 đã bị DEC-262 rút. Nhóm đổi sang Private: bài đang hiện trên màn hình đã tải vẫn đọc được, không tương tác; tải lại thì không còn với người ngoài nhóm. |
| DEC-225 → DEC-236, DEC-245, DEC-261 (QA-429) | M14 là trang chủ, không có cờ tính năng. Cờ Group tắt: bài nhóm vẫn hiện ở Trending, tab Following và tab Group như lối vào, mở ra báo "Hệ thống đang bận, vui lòng thử lại sau", mọi tương tác bị từ chối. Cờ Gamification tắt: số upvote vẫn hiện, Trending không đổi. |
| QA-225, ISS-170, ISS-186 → QA-240 | M14 không phụ thuộc M13; không có hành vi khi tắt AI. |
| DEC-038 → DEC-162, DEC-184; DEC-079 → DEC-163, DEC-188, DEC-211; DEC-118, DEC-122 → DEC-242, DEC-246; DEC-225 → DEC-256; DEC-237 → DEC-240; QA-011 → DEC-171, DEC-206, DEC-208 | Các sửa đổi này chỉ chạm phần M14 không dùng: khôi phục và hết hạn khôi phục bài (M03); hạn chế, thời gian thử thách, giảm hạng tìm kiếm của cảnh cáo (M08, M06); bảng xếp hạng (M12); cờ Chat (M16); duyệt bài của Owner (M11); hồ sơ, tóm tắt AI, tìm kiếm của Guest (M02, M13, M06). Phần M14 dùng giữ nguyên: bài đã xóa mềm ẩn khỏi feed; cảnh cáo riêng tư; nhãn BANNED; quy tắc chung khi cờ tắt; trang danh sách nhóm; Guest xem được bài công khai. |
| DEC-237 → DEC-271 | Không đổi hành vi M14: DEC-271 nói kết quả khiếu nại bài nhóm bị AI từ chối (M09, M11); phần L6 (trang danh sách nhóm cho nút "Khám phá Group") không đổi (rà soát chéo 2026-10-24). |
