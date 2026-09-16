# Mini guideline - nhóm: ______  |  người gán: ______  |  ngày: ______

> Điền file này **trong lúc** gán nhãn, không phải sau khi xong. Mỗi lần bạn dừng lại
> hơn 10 giây để phân vân, đó là một dòng phải ghi vào đây.

## 1. Luật bắt buộc (đã thống nhất cả lớp - không sửa)

- Bộ 17 điểm COCO, đúng tên, đúng thứ tự. Lấy từ file `.SVG` chung.
- Mọi người trong ảnh đều có **đủ 17 điểm**. Điểm không dùng được thì gắn cờ, không xoá.
- Trái/phải tính theo **cơ thể người**, không theo bức ảnh.
- Bị che, còn trong khung -> `v = 1`, **vẫn đặt chấm** ở vị trí ước lượng.
- Ra ngoài mép ảnh -> `v = 0`, **không** đặt chấm.
- Không dùng `Hidden` (`h`) - nó không được lưu vào file.

## 2. Luật của nhóm bạn (phải điền)

| Tình huống | Luật nhóm bạn chọn | Vì sao |
| --- | --- | --- |
| Hông của người mặc quần áo dài | Ước lượng vị trí khớp xương chậu dựa trên tỷ lệ cơ thể (chiều dài lưng/chân) và đánh cờ v = 1 | Để model học được cách suy luận cấu trúc khung xương ngay cả khi bị trang phục che khuất hoàn toàn |
| Tai bị tóc hoặc mũ bảo hiểm che một phần | Đặt điểm ở vị trí phỏng đoán của lỗ tai (ngang tầm mắt/mũi) và đánh cờ v = 1 | Khuôn mặt tuân theo tỷ lệ cố định, model có thể nội suy được vị trí tai từ các keypoint mắt, mũi |
| Người bị cắt ở mép ảnh (chỉ thấy từ hông trở lên) | Các điểm từ hông trở lên đánh v = 2 hoặc v = 1. Các điểm chân ra ngoài mép ảnh thì đặt v = 0 (không đặt chấm) | Tuân thủ tuyệt đối luật bắt buộc: "Ra ngoài mép ảnh -> v=0, không đặt chấm" |
| Cổ tay nằm sau tay lái / sau thân mình | Nội suy vị trí cổ tay dựa trên hướng của cẳng tay và góc gập của khuỷu tay, đánh cờ v = 1 | Cấu trúc cánh tay có giới hạn góc gập tĩnh học, có thể suy ra điểm kết thúc chính xác |
| Hai người chồng lên nhau | Gán đầy đủ cho người bị che lấp bằng cách ước lượng phần cơ thể bị che (v = 1). Phải chú ý gán đúng ID của người đó | Phân biệt rõ tư thế của từng cá thể, tránh để model học nhầm tay chân của người phía trước thành của người phía sau |
| Người nhỏ đến mức nào thì không gán nữa | Nếu diện tích của người trên ảnh quá nhỏ (không thể phân biệt được bằng mắt thường 3 khớp cơ bản như đầu, vai), thì bỏ qua không gán | Gán bừa vào các pixel mờ nhòe sẽ tạo ra nhiễu (noise) làm hỏng khả năng hội tụ của model |

Với mỗi luật, chèn **một ảnh mẫu** (screenshot từ CVAT) thay vì chỉ viết một câu.
Slide 12 nói rõ: khớp không có bề mặt nhìn thấy được thì phải có ảnh mẫu, không phải
một câu văn chung chung.

## 3. Ba ca mơ hồ đã gặp (bắt buộc, ghi ít nhất 3)

### Ca 1 - ảnh `train_20.jpg`, người thứ `1`, khớp `left_ear,right_ear,nose`

- Mơ hồ ở chỗ nào: Người đi xe máy bị thân xe phía trước che khuất hoàn toàn phần chân trái, không thấy nếp gấp quần để đoán vị trí.
- Bạn quyết thế nào: Suy luận góc đặt chân dựa trên vị trí để chân của loại xe máy đó. Chấm ở vị trí ước lượng và đặt v = 1.
- Vì sao: Đủ cơ sở ngữ cảnh (xe máy) để nội suy được không gian sinh học của chân.
- Nếu người khác quyết ngược lại thì model học sai cái gì: Nếu họ bỏ qua hoặc đặt v = 0, model sẽ mất khả năng nhận diện tư thế lái xe và nghĩ rằng người đi xe không có chân bên trái.

### Ca 2 - ảnh `train_14.jpg`, người thứ `1`, khớp `left_hip,left_knee,left_ankle`

- Mơ hồ ở chỗ nào: Người trong ảnh đang quay lưng lại hoàn toàn với camera (sau gáy), không thấy bất kỳ chi tiết nào của khuôn mặt.
- Bạn quyết thế nào: Vẫn chấm các điểm tai (Ear) ở hai bên rìa đầu (v = 1), nhưng không chấm mắt (Eye) và mũi (Nose) (để v = 0).
- Vì sao: Tai vẫn có thể suy đoán được vị trí dựa trên mép tóc/cổ, nhưng mắt và mũi đã hoàn toàn nằm ngoài không gian mặt phẳng 2D có thể nhìn thấy từ góc này.
- Nếu người khác quyết ngược lại thì model học sai cái gì: Nếu cố tình chấm mắt và mũi ở phía sau gáy, model sẽ bị nhiễu và học nhận diện sai các vùng tóc/gáy thành khuôn mặt người.

### Ca 3 - ảnh `train_11.jpg`, người thứ `1`, khớp `left_ear,right_ear,left_eye,right_eye,nose`

- Mơ hồ ở chỗ nào: Người phụ nữ hoàn toàn mất tỷ lệ thân dưới và cánh tay bên trái, bàn tay bên phảido bị chiếc bàn che
- Bạn quyết thế nào: Dựa vào điểm vai và điểm khuỷu tay, cánh tay lộ ra để vẽ dự đoán phần tay
- Vì sao: Khung xương con người là chuỗi liên kết. Khi biết điểm đầu (vai) và điểm giữa (khuỷu) và đường nối (cánh tay lộ ra), có thể giới hạn được vị trí của điểm cuổi (cổ tay).
- Nếu người khác quyết ngược lại thì model học sai cái gì: Nếu chấm đại ở mép ngoài của chiếc bàn, model sẽ học sai tỷ lệ khung xương và nghĩ rằng tay người có thể rộng ngang bằng chiếc bàn.

## 4. Sau khi so visibility report với bạn cùng nhóm

- Khớp lệch `%v=1` nhiều nhất: `left_ear` (bạn `48%` / họ `___%`)
- Nguyên nhân là **guideline chưa rõ** hay **một trong hai bên gán sai**: guideline chưa rõ
- Luật mới bổ sung vào mục 2 sau khi thống nhất: Tình huống 2
