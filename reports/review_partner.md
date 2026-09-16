| Ảnh | Người thứ | Khớp | Lỗi gì | Sửa thế nào |
| --- | ---: | --- | --- | --- |
| train_01.jpg | 1 | 4 khớp bị che (tay/chân) | Dùng v=0 (Outside) sai quy tắc, vì cả người vẫn nằm gọn trong khung hình. | Chuyển thành v=1 (Occluded) và kéo chấm về vị trí giải phẫu ước lượng. |
| train_01.jpg | 2 | 4 khớp bị che (tay/chân) | Nhầm lẫn giữa v=0 và v=1 khi khớp không hề ra khỏi viền ảnh. | Chuyển thành v=1 (Occluded) và kéo chấm về vị trí giải phẫu ước lượng. |
| train_04.jpg | 1 | 4 khớp bị che (tay/chân) | Xóa khớp (v=0) sai nguyên tắc khi khớp bị khuất lấp sau vật cản/cơ thể. | Đặt lại thành v=1 và chấm tọa độ dự đoán vị trí thực tế của khớp. |
| train_10.jpg | 1 | 4 khớp bị che (tay/chân) | (tay/chân)	Dùng v=0 (Outside) sai quy tắc, vì cả người vẫn nằm gọn trong khung hình. | Chuyển thành v=1 (Occluded) và kéo chấm về vị trí giải phẫu ước lượng. |
| train_11.jpg | 1 | 4 khớp bị che (tay/chân) | Dùng v=0 (Outside) sai quy tắc, vì cả người vẫn nằm gọn trong khung hình. | Chuyển thành v=1 (Occluded) và kéo chấm về vị trí giải phẫu ước lượng. |
| train_13.jpg | 1 | 4 khớp bị che (tay/chân) | Dùng v=0 trái quy định đối với người nằm hoàn toàn trong khung ảnh. | Đổi lại thành v=1 và ước lượng vị trí của khớp để đặt chấm. |