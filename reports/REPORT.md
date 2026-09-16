# Báo cáo Ngày 4 - Keypoint & Pose

Họ tên: Nguyễn Công Thành   Nhóm:    Ngày: 16/09/20226

> Cách dùng: copy file này thành `reports/REPORT.md`. Điền bằng số liệu do công cụ sinh ra;
> không tự ước lượng hoặc sửa số trong file JSON.

## 1. Nhãn của tôi

<!-- Lấy số từ reports/visibility_report.md hoặc outputs/visibility_report.json sau Chặng 4.
Số ảnh phải là 20; số skeleton là tổng số người trong 20 ảnh. Thời gian trung bình = tổng
thời gian gán / 20. -->

| Chỉ số | Giá trị |
| --- | ---: |
| Số ảnh đã gán | 20 |
| Số skeleton | 29 |
| v=2 / v=1 / v=0 | 354/105/34 |
| Thời gian trung bình mỗi ảnh | 2 phút |

Ba khớp có `%v=1` cao nhất (chép từ `reports/visibility_report.md`):

1. left_ear 52%
2. right_ear 45%
3. left_wrist 31%

Chúng có đúng là những khớp bạn thấy khó gán nhất không? Nếu không, giải thích.

Đúng, đây là những khớp tôi thực sự thấy khó gán nhất. Các khớp tai (left_ear, right_ear) có tỷ lệ bị che lấp (v=1) cực kỳ cao vì thường xuyên bị tóc che khuất hoặc không nhìn rõ ở các góc chụp nghiêng, chụp từ phía sau lưng, buộc tôi phải ước lượng vị trí giải phẫu. Trong khi đó, khớp cổ tay (left_wrist) cử động rất linh hoạt, hay bị khuất sau thân người hoặc bị đồ vật che lấp (như trường hợp bế mèo ở ảnh train_11), làm cho việc xác định tọa độ chính xác trở nên khó khăn.

## 2. Chấm với gold

<!-- Lấy hai cột từ outputs/eval_vs_gold.json: một lần ngay khi protected release mở và một
lần sau rework. Đếm số phần tử trong từng danh sách lỗi, không tự làm tròn. -->

| Chỉ số | Trước rework | Sau rework |
| --- | ---: | ---: |
| OKS trung bình | 0.931 | |
| OKS@0.50 | 1.000 | |
| OKS@0.75 | 1.000 | |
| Lỗi `dao_trai_phai` | 2 | |
| Lỗi `nham_nguoi` | 1 | |
| Lỗi `xoa_khop_bi_che` | 24 | |

**Tôi đã sửa gì giữa hai lần chạy** (ghi cụ thể: ảnh nào, người thứ mấy, khớp nào):

<!-- Mỗi dòng phải có: tên ảnh + người thứ mấy + keypoint + thao tác sửa. Không viết “đã sửa
lại một số lỗi”. -->

- train_01.jpg - người 1 & 2 - 8 khớp tứ chi: Chuyển từ v=0 sang v=1 và ước lượng lại vị trí do người vẫn nằm gọn trong khung hình nhưng bị che khuất.
- train_10.jpg & train_11.jpg - người 1 - 8 khớp bị che: Chuyển từ v=0 sang v=1 vì lỗi dùng Outside thay cho Occluded.
- train_13.jpg - người 1 - 4 khớp tay: Đặt lại thành v=1 và chấm điểm dự đoán vị trí giải phẫu, xóa bỏ trạng thái v=0.

**Lỗi đảo trái/phải của tôi xảy ra ở ảnh nào?** Ảnh đó dễ hay khó? Nếu là ảnh dễ,
bạn nghĩ vì sao mình vẫn sai?

Lỗi đảo trái/phải của tôi xảy ra ở các ảnh chụp từ phía sau lưng. Về cơ bản ảnh không khó, nhưng do thói quen nhìn theo hướng tay của bản thân (người quan sát) nên tôi đã gán ngược trái/phải so với trục giải phẫu thực tế của người trong ảnh.

## 3. Kiểm chéo

Bạn cùng nhóm: ______

Khớp lệch `%v=1` nhiều nhất giữa hai bảng đếm:

| Khớp | Bạn | Họ | Lệch | Nguyên nhân (guideline hay gán sai?) |
| --- | ---: | ---: | ---: | --- |
| | | | | |
| | | | | |

Luật mới đã bổ sung vào `GUIDELINE_MINI.md` sau khi thống nhất:

<!-- Viết một rule kiểm chứng được: điều kiện nhìn thấy/căn cứ vị trí → chọn v=1 hoặc v=0.
Không chỉ ghi “cẩn thận hơn khi gán”. -->

-

## 4. Model

<!-- Chép số từ outputs/eval_model.json sau Chặng 6. “Chênh” = sau fine-tune trừ baseline;
đây là quan sát trên tập test, không phải chất lượng sản phẩm. -->

| Chỉ số | yolo26n-pose gốc | Sau fine-tune | Chênh |
| --- | ---: | ---: | ---: |
| pose_mAP50 | 0.8450 | 0.8450 | +0.0000 |
| pose_mAP50-95 | 0.6853 | 0.6908 | +0.0055 |
| pose_precision | 0.9734 | 0.9792 | +0.0058 |
| pose_recall | 0.8462 | 0.8462 | +0.0000 |
| box_mAP50-95 | 0.8119 | 0.8041 | -0.0078 |

### Trả lời năm câu hỏi ở cuối notebook

> Mỗi câu cần trỏ tới ảnh/chỉ số cụ thể. Một con số thấp không tự chứng minh nhãn sai;
> kiểm lại bằng bằng chứng thị giác và kết quả gold.

1. `pose_mAP50-95` thay đổi bao nhiêu? Nếu nó giảm, 20 ảnh của bạn dạy được model
pose_mAP50-95 tăng nhẹ +0.0055 (từ 0.6853 lên 0.6908). Tuy nhiên, box_mAP50-95 lại bị giảm -0.0078. Dù bộ data nhỏ (20 ảnh) không mang tính tổng quát hoá cao, nhưng nó đã giúp model nhận diện cấu trúc khớp (pose) chi tiết hơn một chút đối với các bối cảnh cụ thể trong tập train, đổi lại việc giới hạn bối cảnh hẹp đã làm giảm nhẹ khả năng phát hiện bounding box chung của người.

2. `box_mAP` và `pose_mAP` chênh nhau bao nhiêu? Model tìm *người* dễ hơn hay tìm
Model tìm người dễ hơn rất nhiều so với tìm khớp. Sau fine-tune, box_mAP50-95 là 0.8041, cao hơn đáng kể so với pose_mAP50-95 là 0.6908 (chênh lệch 0.1133). Việc xác định một vùng không gian (bounding box) chứa toàn bộ cơ thể luôn dễ hơn việc phải hồi quy chính xác toạ độ của 17 điểm giải phẫu nhỏ bé, đặc biệt là khi các khớp bị che khuất, trùng lặp hoặc uốn cong phức tạp.

3. Một ảnh test model đoán sai - gọi tên lỗi theo bốn loại của slide 43
Trong ảnh test_02, model bị lỗi nhầm người. Mặc dù ảnh chỉ có ít đối tượng chính, model lại bắt thêm các bounding box và khung xương vào bóng người hoặc các chi tiết nền không phải người thật (nhận diện thành 2 persons).
4. Ảnh nào có OKS thấp nhất giữa nhãn của bạn và model? Ai đúng, và bạn dựa vào đâu?
Ảnh có OKS thấp nhất là train_13 (OKS = 0.443). Trong trường hợp này, model đã đúng. Căn cứ vào cảnh báo ở bước 1, file train_13.txt:1 của tôi bị báo lỗi "có 4 khớp v=0 trong khi cả người nằm gọn giữa ảnh". Do tôi đã xóa khớp sai nguyên tắc, model (hiểu đúng luật) vẫn dự đoán vị trí các khớp đó, dẫn đến sự bất đồng lớn về điểm số.
5. Ảnh bạn gán tệ nhất có *cũng* là ảnh model đoán tệ nhất không? Nếu có, điều đó
Đúng vậy, train_13 (và train_06 với OKS = 0.564) là những ảnh tôi có chất lượng nhãn tệ nhất (do nhầm lẫn v=0 và v=1), đồng thời cũng là ảnh model và tôi bất đồng nhất. Điều này cho thấy đây là những bức ảnh có tư thế phức tạp và độ che khuất cực cao, khiến cả người gán (không tuân thủ được guideline khi bối cảnh khó) và máy móc đều lúng túng trong việc suy luận hình học.

## 5. Một rule evidence bạn đã dùng

Chọn một keypoint trong ảnh core mà bạn phải quyết định giữa `v=1` và `v=0`. Nêu ảnh, người,
khớp, bằng chứng nhìn thấy và lý do chọn trạng thái đó trong 3-5 câu.

Trong ảnh train_11.jpg, với người thứ nhất (ID 235), tôi phải quyết định v=1 hay v=0 cho các khớp cổ tay (WRIST) và khuỷu tay (ELBOW). Bằng chứng thị giác là phần vai (SHOULDER) vẫn thấy rõ, và tư thế của người này đang cúi xuống, áo khoác phồng lên để đỡ một con mèo to che lấp toàn bộ thân trước. Vì thân người vẫn nằm hoàn toàn trong khung hình (chưa bị cắt mép ảnh), tay không thể biến mất mà chỉ đang vòng ra sau con mèo, nên tôi bắt buộc phải chọn trạng thái bị che lấp. Do đó, tôi đặt v=1 và ước lượng vị trí cổ tay nằm ở phía dưới bụng con mèo (chỗ tay người đang bợ lấy mèo), tuyệt đối không dùng v=0.
