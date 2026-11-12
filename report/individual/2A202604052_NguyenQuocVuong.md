# Báo cáo cá nhân — NguyenQuocVuong-2A202604052

Dữ liệu: 12 ảnh người COCO 2017 (Lin et al., 2014) và 8 ảnh khuôn mặt cắt từ ảnh COCO 2017 (CC BY / CC BY-SA), chỉ dùng trong lớp.

## 0. Thông tin học viên

- Họ tên: Nguyễn Quốc Vương
- MSSV: 2A202604052
- Email: vug10032004@gmail.com
- Link repository: https://github.com/vuomg/K5-L2-NguyenQuocVuong-2A202604052-KeypointPose
- Phiên bản CVAT (Help → About): 2.81.1
- Máy: Windows 11 Home · RAM 32 GB · CVAT chế độ đầy đủ
- Bộ ảnh (`src/exports/assignment.json` do `lab.py setup` tạo): có
- Giờ bắt đầu: 16:30
- Giờ kết thúc: 19:20

## 1. Kiểm tra label (CP0)

| Label | Kiểu | Số điểm | Tên điểm đúng bảng của lab? | Đúng thứ tự? | Số cạnh |
|---|---|---:|---|---|---:|
| `person` | Skeleton | 17 | Có | Có | 19 |
| `face` | Skeleton | 13 | Có | Có | 13 |

Mẫu `person` dựng theo người quay mặt về camera (các điểm `left_*` nằm bên phải khung mẫu)? Có

Cách đổi cờ `occluded` / `outside` cho **một điểm** trên phiên bản CVAT này (một câu):

Chuột phải vào đúng điểm rồi chọn `occluded` hoặc `outside` trong menu (hoặc rê chuột vào điểm, bấm `Q` / `O`); chỉ điểm đó đổi.

## 2. Số lượng đã gán và thời gian (CP1, CP2)

| Nhóm ảnh | Số ảnh | Số skeleton đã gán | Số người dưới 60 px (không gán) | Số poster / gương / màn hình bỏ qua | Thời gian (phút) |
|---|---:|---:|---:|---:|---:|
| `easy` | 5 | 5 | 1 | 0 | 25 |
| `occluded` | 3 | 6 | 1 | 0 | 25 |
| `back` | 2 | 4 | 0 | 0 | 25 |
| `small` | 1 | 2 | 1 | 0 | 10 |
| `crowd` | 1 | 3 | 0 | 0 | 15 |
| `faces` | 8 | 8 | — | 0 | 25 |

Tổng: 20 skeleton `person` trên 12 ảnh, 8 skeleton `face` trên 8 ảnh.

Người dưới 60 px (không gán): người đi bộ ở nền `000000294379.jpg`; người ở xa trên dốc `000000302102.jpg`; người cầm máy ảnh ở góc trên trái `000000100510.jpg` (lúc đầu gán nhầm, đã xóa).

- Số ảnh người đã xong ở mốc phút 105: 8 / 10
- Thời gian thực tế (phút): CP1 100 · CP2 25 · CP3 15
- Ảnh tốn thời gian nhất là ảnh nào, vì sao?

`000000054909.jpg` (back): hai người quay lưng, đầu bị ô che, phải cân nhắc cờ cho các điểm mặt; đây cũng là ảnh đầu tiên nên còn đang làm quen với thao tác skeleton.

## 3. Bảng ca khó (CP1, CP2)

| Ảnh | Người / mặt | Điểm | Cờ đã chọn | Phân vân giữa | Lý do chọn |
|---|---|---|---:|---|---|
| `000000054909.jpg` (back) | #1, #2 | `nose`, mắt, tai | 0 | `v = 1` / `v = 0` | Quay lưng, đầu bị ô che, không đoán chắc vị trí mặt |
| `000000542160.jpg` (crowd) | #2 (số 5, giữa) | `right_elbow`, `right_wrist` | 0 | `v = 1` / `v = 0` | Tay bị người số 4 che hẳn, không thấy đoạn chi nào để ước lượng |
| `000000521817.jpg` (occluded) | #1, #2 | `left_ankle`, `right_ankle` | 0 | `v = 1` / `v = 0` | Cổ chân nằm ngoài khung ảnh, không kéo về mép |

## 4. Bảng tự review (CP3)

| Ảnh | Người / mặt | Điểm | Mã lỗi | Ghi chú | Đã sửa? |
|---|---|---|---|---|---|
| `000000542160.jpg` (crowd) | #3 (số 4) | cả người | `lr_swap` | Thấy mặt nhưng `left_*` nằm bên trái ảnh | Chưa |
| `000000542160.jpg` (crowd) | #1, #2 | `*_knee`, `*_ankle` | `lr_swap` | Cặp chân ngược phía so với vai, hông | Chưa |
| `000000521817.jpg` | #1 | `*_eye`, `*_ear` | `lr_swap` | Cặp mắt, tai ngược phía so với thân | Chưa |
| `000000469061.jpg` | #1 (người lớn) | cả người | `lr_swap` | Quay mặt nhưng gán như quay lưng | Chưa |
| `000000210604.jpg` (back) | #1 | cả người | `lr_swap` | Thấy mặt nhưng `left_*` nằm bên trái ảnh | Chưa |
| `000000100510.jpg` | #3 | cả người | `extra` | Người góc trên trái cao 48 px (< 60 px) | Có (đã xóa) |
| `face_309728.jpg` (kính râm) | mặt | 8 điểm mắt | `vis_flag` | Mắt sau kính râm tối đang `v = 2`, phải là `occluded` | Chưa |
| `face_155465.jpg` | mặt | — | `ok` | | — |
| `face_92028.jpg` | mặt | — | `ok` | | — |

Tổng hợp số lỗi theo mã:

| `lr_swap` | `vis_flag` | `position` | `missing` | `extra` | `ok` |
|---:|---:|---:|---:|---:|---:|
| 5 | 1 | 0 | 0 | 1 | 2 |

Điểm còn phân vân giữa `v = 1` và `v = 0`:

`000000542160.jpg` #2, tay phải: chọn `v = 0` thay vì `v = 1`, vì tay bị che hoàn toàn, nhiều người đoán sẽ ra các vị trí khác nhau.

## 5. Kiểm file xuất và kết quả tự kiểm (CP4)

| File | Người / mặt kiểm (ảnh, thứ tự) | Số phần tử `keypoints` | Điểm `outside` ra `v = 0`, `occluded` ra `v = 1`? | `num_keypoints` khớp? |
|---|---|---:|---|---|
| `NguyenQuocVuong_persons.zip` | `000000194027.jpg`, #1 (easy) | 51 | Không có điểm `outside` / `occluded`; 17 điểm `v = 2` | Có (17) |
| `NguyenQuocVuong_persons.zip` | `000000054909.jpg`, #1 (back) | 51 | Có: 5 điểm mặt `outside` ra `v = 0` | Có (12) |
| `NguyenQuocVuong_faces.zip` | `face_155465.jpg` (mặt thẳng) | 39 | Không có điểm `outside` / `occluded`; 13 điểm `v = 2` | Có (13) |

Sau khi xuất, CVAT ghi `occluded` thành `v = 1` và `outside` thành `v = 0`. Tọa độ của điểm `outside` là tọa độ cũ, không phải `0, 0` (ví dụ `nose` của `000000054909.jpg` #1 ra `453.52, 179.81, 0`).

Hai job đã chuyển sang completed trên CVAT? Có

Phần **TÓM TẮT** của `src/check_submission.py`:

```text
- File person: NguyenQuocVuong_persons.zip
  Số ảnh: 12 · số skeleton `person`: 20 · mỗi annotation 51 số
  Skeleton theo ảnh: 000000054909=2, 000000100510=2, 000000194027=1, 000000205650=1, 000000210604=2, 000000294329=1, 000000294379=1, 000000302102=2, 000000314154=1, 000000469061=2, 000000521817=2, 000000542160=3
  Cờ v: v=2 313 (92%) · v=1 0 (0%) · v=0 27 (8%)
  num_keypoints trung bình: 15.7
- File face: NguyenQuocVuong_faces.zip
  Số ảnh: 8 · số skeleton `face`: 8 · mỗi annotation 39 số
  Skeleton theo ảnh: face_155465=1, face_309728=1, face_359139=1, face_483667=1, face_505385=1, face_53580=1, face_556064=1, face_92028=1
  Cờ v: v=2 104 (100%) · v=1 0 (0%) · v=0 0 (0%)
  num_keypoints trung bình: 13.0
- Ghi chú: 27 điểm v = 0 vẫn mang tọa độ cũ (CVAT 2.x xuất như vậy; chuẩn COCO ghi 0, 0). Không phải lỗi: điểm v = 0 bị bỏ qua khi huấn luyện và khi chấm.
- Số [LỖI]: 0 · số [CẢNH BÁO]: 7
Kết quả: ĐẠT (đọc lại từng cảnh báo ở trên)
```

Các `[CẢNH BÁO]` còn giữ nguyên và lý do:

| Ảnh / người | Cảnh báo | Lý do |
|---|---|---|
| `000000210604.jpg` #1, `000000469061.jpg` #1, `000000542160.jpg` #3 | Thấy mặt nhưng `left_*` bên trái ảnh | Đã ghi `lr_swap` ở mục 4, chưa  sửa |
| `000000521817.jpg` #1; `000000542160.jpg` #1, #2 | Một cặp điểm ngược phía | Đã ghi `lr_swap` ở mục 4, chưa  sửa |
| `000000314154.jpg` #1 | `left_ankle` sát mép dưới | Cổ chân vẫn nằm trong ảnh, sát mép thật, nên giữ `v = 2` |

## 6. Ảnh chụp màn hình

1. Label `person` trong label constructor:

   ![Label person](images/1_label_person.png)

2. Một người quay lưng đã gán, cờ đã đặt:

   ![Người quay lưng](images/2_nguoi_quay_lung.png)

3. Một khuôn mặt đã gán 13 điểm, phóng to vùng mắt:

   ![Khuôn mặt phóng to](images/3_mat_phong_to.png)

4. Một đoạn JSON xuất của một người:

   ![JSON export](images/4_json_export.png)

Nguồn ảnh: COCO 2017.

## 7. Tự đánh giá

1. Lỗi bạn mắc nhiều nhất hôm nay, và cách bạn sẽ tránh ở dự án thật:

   `lr_swap`: quên đổi trái/phải khi hướng người khác mẫu.

2. Một quy tắc bạn đề xuất thêm vào guideline:

   Sau mỗi người, kiểm nhanh `left_shoulder` và `left_hip` có cùng phía với `left_eye` không; khác phía thì dừng lại kiểm hướng người.

3. Nhãn của bạn đi vào model ở đâu? Chọn một lỗi bạn đã sửa và nói nó sẽ làm model học sai thế nào:

   Skeleton `extra` ở `000000100510.jpg`: người 48 px quá nhỏ, điểm đặt không chính xác, nhưng vẫn có `v > 0` nên được tính vào loss. Model sẽ học heatmap ở những vị trí đoán bừa.

## 8. Khó khăn và lỗi kỹ thuật

Chưa quen cách đổi cờ cho từng điểm nên ít dùng.

## Bonus (nếu làm)


## 9. Tài liệu tham khảo và công cụ AI đã dùng

- Tài liệu của lab: `docs/GUIDELINE.md`, `docs/CVAT_CHEATSHEET.md`, `docs/COCO_KEYPOINTS.md`, `docs/HUONG_DAN_BANG_HINH.md`.
- Lin et al., 2014. Microsoft COCO: Common Objects in Context.
- Công cụ AI: Claude Code, dùng để đọc tài liệu lab.
