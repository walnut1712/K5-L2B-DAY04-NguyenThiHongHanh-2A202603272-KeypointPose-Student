# Báo cáo cá nhân — NguyenThiHongHanh-2A202603272

Dữ liệu: 12 ảnh người COCO 2017 và 8 ảnh khuôn mặt theo bộ ảnh được tạo cho MSSV. Ảnh chỉ dùng trong lớp.

## 0. Thông tin học viên

- Họ tên: Nguyen Thi Hong Hanh
- MSSV: 2A202603272
- Email:  26ai.hanhnth@vinuni.edu.vn
- Link repository: https://github.com/walnut1712/K5-L2B-NguyenThiHongHanh-2A202603272-KeypointPose-Student
- Phiên bản CVAT (Help → About): 2.74.1
- Máy: Windows · RAM 16 · CVAT chế độ: Local
- Bộ ảnh (`src/exports/assignment.json` do `lab.py setup` tạo): Có
- Giờ bắt đầu: 16h00 13/11/2026
- Giờ kết thúc: 19h30 13/11/2026

## 1. Kiểm tra label (CP0)

| Label | Kiểu | Số điểm | Tên điểm đúng bảng của lab? | Đúng thứ tự? | Số cạnh |
|---|---|---:|---|---|---:|
| `person` | Skeleton | 17 | Có (checker không báo sai tên) | Có (checker không báo sai thứ tự) | 19 |
| `face` | Skeleton | 13 | Có (checker không báo sai tên) | Có (checker không báo sai thứ tự) | 13 |

Mẫu `person` dựng theo người quay mặt về camera (các điểm `left_*` nằm bên phải khung mẫu)?
- Có. Mẫu được kiểm tra trên CVAT đúng theo quy ước người quay mặt về camera, với `left_*` nằm ở phía phải khung mẫu.

Cách đổi cờ `occluded` / `outside` cho một điểm trên phiên bản CVAT này (một câu):
- Chọn skeleton, chọn đúng keypoint trên canvas hoặc trong danh sách Skeleton parts ở Objects Sidebar, sau đó bật thuộc tính Occluded hoặc Outside trong phần Properties của chính điểm đó.

## 2. Số lượng đã gán và thời gian (CP1, CP2)

| Nhóm ảnh | Số ảnh | Số skeleton đã gán | Số người dưới 60 px (không gán) | Số poster / gương / màn hình bỏ qua | Thời gian (phút) |
|---|---:|---:|---:|---:|---:|
| `easy` | 5 | 5 | 12 | 0 | Không ghi nhận riêng |
| `occluded` | 3 | 6 | 0 | 0 | Không ghi nhận riêng |
| `back` | 2 | 3 | 4 | 0 | Không ghi nhận riêng |
| `small` | 1 | 1 | 0 | 0 | Không ghi nhận riêng |
| `crowd` | 1 | 3 | 0 | 0 | Không ghi nhận riêng |
| `faces` | 8 | 8 | — | Không ghi nhận | Không ghi nhận riêng |
| **Tổng ảnh người** | **12** | **18** | **16** | **0** | — |

- Số ảnh người đã xong ở mốc phút 105: **10 / 10**
- Thời gian thực tế: **210 phút (16:00–19:30)**.
- CP1: **Không ghi nhận riêng** · CP2: **Không ghi nhận riêng** · CP3: **Không ghi nhận riêng**.
- Ảnh tốn thời gian nhất là `000000193879.jpg`, vì người trong ảnh đang thực hiện tư thế vận động phức tạp: một tay và chân chéo, thân người nghiêng, nên xác định `ankle`, `knee`, `hip` và `shoulder` mất nhiều thời gian hơn các tư thế đứng đơn giản.

## 3. Bảng ca khó (CP1, CP2)

Tự ghi các trường hợp phân vân khi gán; các dòng dưới là trường hợp thật xuất hiện trong job.

| Ảnh | Người / mặt | Điểm | Cờ đã chọn (`v`) | Phân vân giữa | Lý do chọn |
|---|---|---|---:|---|---|
| `000000193879.jpg` | Người | `ankle` | `v = 2` | Bên trái / bên phải | Chân bắt chéo; đối chiếu tư thế toàn thân và giữ nhãn theo bên thực của người. |
| `000000521817.jpg` | Người | `eye`, `knee` | `v = 2` | Bên trái / bên phải | Người nghiêng và quay mặt lệch; kiểm tra theo hướng cơ thể thay vì chiều khung hình. |

## 4. Bảng tự review (CP3)

Tự review 5 ảnh người (ít nhất 2 ảnh `back` hoặc `crowd`) và 3 ảnh mặt. Dùng mã `lr_swap`, `vis_flag`, `position`, `missing`, `extra`, hoặc `ok`; nếu checker cảnh báo nhưng kiểm tra ảnh xác nhận nhãn đúng thì ghi `ok` và nêu lý do giữ nguyên.

| Ảnh | Người / mặt | Điểm | Mã lỗi | Ghi chú | Đã sửa? |
|---|---|---|---|---|---|
| `000000193879.jpg` | Người | `ankle` | `ok` | Checker cảnh báo cặp ankle ngược phía; kiểm tra lại trên CVAT xác nhận do chân bắt chéo thật, nên giữ nguyên nhãn. | Không (đã kiểm tra) |
| `000000521817.jpg` | Người | `eye`, `knee` | `ok` | Checker cảnh báo các cặp lệch phía; kiểm tra lại trên CVAT xác nhận do người nghiêng và quay mặt, nên giữ nguyên nhãn. | Không (đã kiểm tra) |
| `000000130816.jpg` | Người | `wrist` | `position` | Vị trí cổ tay lệch vì tay che thân và bị méo khi xem vội. | Có |
| `000000311497.jpg` | Người | `hip` | `position` | Hông lệch khá nhiều do ảnh có góc nghiêng; cần căn vuông góc với đường thân. | Có |
| `000000351176.jpg` | Người | `all` | `ok` | Hình ảnh tương đối rõ, vẫn giữ đúng vị trí và cờ. | Có |
| `face_137371.jpg` | Mặt | `left_eye` | `ok` | Mắt và mũi đúng vị trí, không có lỗi. | Có |
| `face_168953.jpg` | Mặt | `nose` | `position` | Mũi lệch nhẹ do góc khuôn mặt nghiêng; đã căn lại. | Có |
| `face_261458.jpg` | Mặt | `right_eye` | `ok` | Vị trí mắt ổn định, chỉ cần chú ý lúc cắt khuôn mặt. | Có |

Tổng hợp số lỗi theo mã:

| `lr_swap` | `vis_flag` | `position` | `missing` | `extra` | `ok` |
|---:|---:|---:|---:|---:|---:|
| 0 | 0 | 3 | 0 | 0 | 5 |

Điểm còn phân vân giữa `v = 1` và `v = 0` (ghi cả hai lựa chọn và lý do chọn): `000000193879.jpg` có thể chọn `v = 1` cho `ankle` bị che hoặc lệch ngoài khung, nhưng vì chân vẫn còn nhìn thấy rõ và nằm trong khung nên giữ `v = 2`; tương tự với `000000521817.jpg`, các điểm mắt và đầu gối gần như nhìn rõ nên ưu tiên `v = 2` thay vì `v = 0`/`v = 1`.

## 5. Kiểm file xuất và kết quả tự kiểm (CP4)

Kết quả kiểm cấu trúc cho biết mỗi annotation người có 51 số, mỗi annotation mặt có 39 số. Đã mở file JSON và đối chiếu thủ công các điểm cùng cờ trước khi xác nhận đạt.

| File | Người / mặt kiểm (ảnh, thứ tự) | Số phần tử `keypoints` | Điểm `outside` ra `v = 0`, `occluded` ra `v = 1`? | `num_keypoints` khớp? |
|---|---|---:|---|---|
| `NguyenThiHongHanh_persons.zip` | `000000193879.jpg`, người #1 | 51 | Có, cờ được kiểm tra theo quy tắc COCO: `outside` → `v = 0`, `occluded` → `v = 1` | Có |
| `NguyenThiHongHanh_persons.zip` | `000000521817.jpg`, người #2 | 51 | Có, cờ được kiểm tra theo quy tắc COCO: `outside` → `v = 0`, `occluded` → `v = 1` | Có |
| `NguyenThiHongHanh_faces.zip` | `face_137371.jpg`, mặt #1 | 39 | Có, các cờ mặt đều đối chiếu với quy tắc mặt đang dùng | Có |

Theo quy ước COCO của bài: `occluded` → `v = 1`; `outside` → `v = 0`. Checker ghi nhận các điểm `v = 0` trong file này vẫn có tọa độ cũ (CVAT 2.x); điểm `v = 0` không được dùng khi huấn luyện/chấm. Các cờ trên JSON đã được xác nhận.

Hai job đã chuyển sang completed trên CVAT: **Có**.

Dưới đây là phần tóm tắt checker đã chạy trên hai file xuất hiện có:

```text
----- TÓM TẮT (dán vào báo cáo mục 5) -----
- File person: NguyenThiHongHanh_persons.zip
  Số ảnh: 12 · số skeleton `person`: 18 · mỗi annotation 51 số
  Skeleton theo ảnh: 000000043719=1, 000000057978=1, 000000130816=3, 000000177889=1, 000000193879=2, 000000211458=1, 000000253584=1, 000000311497=2, 000000351176=2, 000000390585=1, 000000463932=1, 000000521817=2
  Cờ v: v=2 235 (77%) · v=1 37 (12%) · v=0 34 (11%)
  num_keypoints trung bình: 15.1
- File face: NguyenThiHongHanh_faces.zip
  Số ảnh: 8 · số skeleton `face`: 8 · mỗi annotation 39 số
  Skeleton theo ảnh: face_137371=1, face_168953=1, face_232598=1, face_261458=1, face_264124=1, face_309728=1, face_333134=1, face_92028=1
  Cờ v: v=2 96 (92%) · v=1 8 (8%) · v=0 0 (0%)
  num_keypoints trung bình: 13.0
- Ghi chú: 34 điểm v = 0 vẫn mang tọa độ cũ (CVAT 2.x xuất như vậy; chuẩn COCO ghi 0, 0). Không phải lỗi: điểm v = 0 bị bỏ qua khi huấn luyện và khi chấm.
- Số [LỖI]: 0 · số [CẢNH BÁO]: 2
Kết quả: ĐẠT (đọc lại từng cảnh báo ở trên)
```

Các `[CẢNH BÁO]` checker phát hiện; đã xem lại bằng mắt trên CVAT và giữ nguyên vì đó là trường hợp chân/tay bắt chéo hoặc người nghiêng thật, không phải lỗi label:

- `000000193879.jpg`, người #1: cặp `ankle` nằm ngược phía so với các cặp còn lại; sau kiểm tra, đây là chân bắt chéo thật nên không sửa.
- `000000521817.jpg`, người #2: cặp `eye`, `knee` ở phía ngược so với các cặp còn lại; sau kiểm tra, là tư thế nghiêng và quay mặt thật, không sửa.

## 6. Ảnh chụp màn hình

Các ảnh hiện có đang là JPG; yêu cầu nộp đúng tên PNG như dưới đây. Ảnh đầu tiên là label constructor, không phải các ảnh hiện có trong folder `report/individual/images/` vì cần cắt đúng vùng và lưu theo tên yêu cầu. Ảnh minh họa trong thư mục này có thể dùng làm dữ liệu tham khảo đầu vào để chụp lại đúng cách.

1. Label `person` trong label constructor (đủ 17 điểm có tên): cần chụp lại label constructor và lưu thành `images/1_label_person.png`.

2. Một người quay lưng đã gán, cờ đã đặt: `images/2_nguoi_quay_lung.jpg`.

   ![Người quay lưng](images/2_nguoi_quay_lung.jpg)
   Nguồn: COCO val2017 (ảnh trong bộ lab).

3. Một khuôn mặt đã gán 13 điểm, phóng to vùng mắt: `images/3_mat_phong_to.jpg`.

   ![Khuôn mặt phóng to](images/3_mat_phong_to.jpg)
   Nguồn: COCO val2017 (ảnh trong bộ lab).

4. Một đoạn JSON xuất của một người: cần chụp JSON có cả `keypoints` và `num_keypoints`, lưu thành `images/4_json_export.png`.

Nguồn ảnh minh họa: COCO 2017 (các ảnh trong bộ lab có nguồn Flickr ghi trong `src/lab/pool.json`). Ghi nguồn cụ thể dưới từng ảnh chụp khi hoàn thiện báo cáo.

## 7. Tự đánh giá

1. Lỗi mắc nhiều nhất hôm nay: nhầm trái-phải khi người nằm ở tư thế quay lưng, nghiêng hoặc chân tay bắt chéo. Cách tránh ở dự án thật: luôn kiểm tra từ trung tâm cơ thể (nose, neck, spine) rồi xác định `left/right` theo hướng mặt của người, không theo hướng của khung ảnh; nếu chưa chắc, đánh dấu `occluded` hoặc `outside` thay vì ép điểm vào vị trí không chắc chắn.

2. Quy tắc đề xuất thêm vào guideline: với người quay lưng hoặc bắt chéo, nên đánh dấu một cặp điểm rồi kiểm tra đối xứng cả toàn bộ thân trước khi gán tiếp. Nếu hình ảnh có góc xoay, không đánh dấu theo chiều của camera mà phải theo hướng mặt của người thật. Trong trường hợp điểm bị che rõ, ưu tiên `outside`/`occluded` thay vì cố ép vào tọa độ giả.

3. Nhãn đi vào model ở đâu? Trong trường hợp `000000193879.jpg`, nếu cặp `ankle` bị đảo trái-phải, heatmap ở chân sẽ học sai vị trí thực, dẫn đến các vùng loss chú trọng nhầm vào phía sai của cơ thể. Khi bản thân lật ảnh hoặc tính toán đồng bộ, trọng số trong loss của chân đó sẽ bị lệch, khiến model học nhầm hướng cơ thể và dễ sai ở các ảnh tương tự.

## 8. Khó khăn và lỗi kỹ thuật

Không gặp lỗi kỹ thuật nghiêm trọng trong quá trình làm bài. Chỉ có các cảnh báo checker về một số cặp `ankle`, `eye`, `knee` ở tư thế chéo hoặc nghiêng, sau khi xem lại trên CVAT đều được xác nhận là do tư thế thật chứ không phải lỗi kỹ thuật trong export.

## Bonus (nếu làm)

### B1 — 3 ảnh người khó thêm

| Ảnh | Số skeleton | Số người dưới 60 px | Ca khó nhất |
|---|---:|---:|---|
| `000000065350.jpg` | 3 | 0 | Chân tay bắt chéo và thân nghiêng |
| `000000357549.jpg` | 3 | 0 | Người ở góc chụp khó, tay và chân chồng lên nhau |
| `000000507223.jpg` | 3 | 0 | Cặp `wrist` lệch phía do tay nhấc rất cao |

Kết quả checker cho file bonus: `NguyenThiHongHanh_bonus_persons.zip`
- Số ảnh: 3 · số skeleton `person`: 9 · mỗi annotation 51 số
- Cờ v: v=2 92 (60%) · v=1 15 (10%) · v=0 46 (30%)
- Số [LỖI]: 0 · số [CẢNH BÁO]: 1
- Kết quả: ĐẠT (đọc lại cảnh báo `wrist` ở `000000507223.jpg`)

### B2 — 5 ảnh khuôn mặt đen trắng / hồng ngoại

Đã gán nhãn 13 điểm cho 5 ảnh khuôn mặt đen trắng trong `data/faces-extra/` và xuất `src/exports/NguyenThiHongHanh_bonus_faces.zip`.

- Kết quả checker: 5 ảnh, 5 skeleton `face`, mỗi annotation 39 số; 61 điểm `v = 2`, 0 điểm `v = 1`, 4 điểm `v = 0`; không có lỗi hoặc cảnh báo.
- Ảnh không có màu nên khó dựa vào sắc độ da để phân biệt ranh giới; cần dựa nhiều hơn vào hình dáng và tương phản quanh mắt, mũi, miệng. Ảnh `face_102517.jpg` có kính trong nhưng mắt vẫn nhìn thấy, nên các điểm mắt được gán `v = 2`.
- Bộ ảnh này không có ảnh hồng ngoại hoặc kính râm, nên không thể đánh giá trực tiếp trường hợp đó. Nếu kính râm che mắt nhưng vẫn ước lượng chắc vị trí, mắt là `v = 1`; nếu mắt thực sự nhìn thấy rõ qua ảnh thì là `v = 2`.

### B3 — Model so với nhãn của tôi (không tính điểm)

Đã thử demo Pixlane YOLOv26 Pose Estimation trên ảnh duy nhất do lab cung cấp: tượng ngồi nhiều tay.

Ảnh gốc: [image.png](images/image.png) · Kết quả model: [image-result.png](images/image-result.png)

1. Model đánh dấu tượng là `person` với confidence 4% và vẽ keypoint trên thân tượng. Ảnh kết quả không hiển thị confidence riêng cho từng keypoint, nên chưa thể kết luận model xử lý khớp bị che hoặc ngoài ảnh ra sao.
2. Ảnh này nhìn chính diện, không phải người quay lưng; vì vậy không kiểm tra được model có đảo trái/phải hay không.
3. Overlay có vẻ dùng bộ 17 keypoint kiểu COCO, nhưng với một kết quả confidence thấp và chưa có dữ liệu nhãn đối chiếu thì chưa xác nhận được đầy đủ sự tương ứng.

## 9. Tài liệu tham khảo và công cụ AI đã dùng

- Tài liệu lab: `README.md`, `CHECKPOINTS.md`, `SUBMISSION.md`, `docs/GUIDELINE.md`, `docs/COCO_KEYPOINTS.md`.
