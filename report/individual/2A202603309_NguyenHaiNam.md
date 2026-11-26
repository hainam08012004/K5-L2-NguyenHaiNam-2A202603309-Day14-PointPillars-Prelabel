# Báo cáo Day 14 — Nguyen Hai Nam — 2A202603309

> Sao chép file này thành `report/individual/<MSSV>_<HoTen>.md` (không dấu), ví dụ `2A20260000_NguyenVanAn.md`.

- Mã học viên dùng với `--student`: `2A202603309`
- `seed_tag` trong `frames_A.txt`: `82ac3100fd`

## 1. Dự đoán trước sweep (bước 5b)

Ghi **trước** khi chạy `scripts/pp_sweep.py`, rồi commit và push ngay (lịch sử commit là bằng chứng thời điểm viết). Không sửa phần này sau khi có kết quả.

- Tham số tôi nghĩ giảm công sửa nhiều nhất: tăng đồng thời cả `score_thr` và `min_points`.
- Vì sao (nhìn ảnh BEV tập A: box thừa nhiều hay box sót nhiều?):
  - Trên tập A, mô hình chủ yếu vẽ **thừa** hộp hơn là bỏ sót: tôi phải xóa 35 hộp nhưng chỉ thêm 4 hộp (85 hộp dự đoán so với 54 hộp trong nhãn tham chiếu).
  - `score_thr`: chỉ giữ các hộp mà mô hình đủ tự tin là một vật thể thật, nhờ đó loại bớt các dự đoán không chắc chắn.
  - `min_points`: khi sửa trên CVAT, tôi nhiều lần phải xóa các hộp chứa quá ít điểm LiDAR, đến mức nhìn bằng mắt cũng không xác định được đó là vật gì. Nhiều hộp người (Pedestrian/Cyclist) bị vẽ sai rơi vào trường hợp này. Lọc theo số điểm sẽ loại được nhóm hộp này.

## 2. Tập A: sửa tay và tune

| Cấu hình | Xóa | Thêm | Sửa | Chi phí |
|---|---:|---:|---:|---:|
| Gốc | 35 | 4 | 0 | 14.5 |
| `best_config.json` | | | | |

- Tham số đã đổi trong `best_config.json`: ...
- Kết quả leave-one-out (dán các dòng `scripts/pp_sweep.py` in ra): ...
- Cấu hình có ổn định trên từng frame không? Vì sao tôi vẫn chọn (hoặc không chọn) nó: ...

## 3. Trước/sau (bước 8)

![so sánh](../../d14_2A202603309/compare/<frame>.jpg)

- `scripts/pp_compare.py` báo giảm (hoặc tăng) ...% công sửa trên tập A.
- Dự đoán ở mục 1 đúng hay sai? Giải thích bằng số box xóa/thêm/sửa: ...

## 4. Tập B

Số đo từ `scripts/pp_prelabel.py --frames d14_2A202603309/frames_B.txt --config d14_2A202603309/best_config.json --gt d14_2A202603309/ref_B.json`:

| Xóa | Thêm | Sửa | Chi phí |
|---:|---:|---:|---:|
| | | | |

- Loại box tốn công sửa nhất ở tập B: ...

## 5. Giới hạn

- Nêu ít nhất 2 giới hạn (ví dụ: chỉ 3 frame tune; model KITTI không có Truck/Bus; chi phí là công thức, chưa phải thời gian sửa thật): ...
