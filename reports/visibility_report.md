# Visibility report

- Thư mục nhãn: `dataset\labels\train`
- 20 ảnh, 29 skeleton, trung bình 15.83 khớp có v > 0 mỗi người
- Tổng: v=2 354 | v=1 105 | v=0 34

| # | Khớp | v=2 | v=1 | v=0 | %v=1 |
| ---: | --- | ---: | ---: | ---: | ---: |
| 0 | nose | 26 | 3 | 0 | 10% |
| 1 | left_eye | 21 | 8 | 0 | 28% |
| 2 | right_eye | 22 | 7 | 0 | 24% |
| 3 | left_ear | 14 | 15 | 0 | 52% |
| 4 | right_ear | 16 | 13 | 0 | 45% |
| 5 | left_shoulder | 25 | 4 | 0 | 14% |
| 6 | right_shoulder | 27 | 2 | 0 | 7% |
| 7 | left_elbow | 24 | 5 | 0 | 17% |
| 8 | right_elbow | 25 | 4 | 0 | 14% |
| 9 | left_wrist | 20 | 9 | 0 | 31% |
| 10 | right_wrist | 21 | 7 | 1 | 24% |
| 11 | left_hip | 22 | 7 | 0 | 24% |
| 12 | right_hip | 22 | 6 | 1 | 21% |
| 13 | left_knee | 18 | 4 | 7 | 14% |
| 14 | right_knee | 18 | 4 | 7 | 14% |
| 15 | left_ankle | 17 | 3 | 9 | 10% |
| 16 | right_ankle | 16 | 4 | 9 | 14% |

## Đọc bảng này thế nào

1. Khớp nào có **%v=1 cao**: khớp hay bị che. Cổ tay và hông thường là hai vị trí cần xem lại guideline trước khi kết luận.
2. Khớp nào có **v=0 cao bất thường**: mọi người đang dùng Outside ở chỗ đáng lẽ là Occluded. Đó là lỗi số 3 của slide 46, và nó xoá thẳng khớp đó khỏi bảng điểm OKS.
3. Khi so hai người: **lệch lớn = bất đồng về guideline**, không phải về bức ảnh. Sửa guideline trước, sửa nhãn sau.
