# Báo cáo cá nhân — Ngày 2 Object Detection

Đổi tên file theo `MSSV_HoTen.md`, ví dụ `20241234_NguyenVanAn.md`. Điền kết quả thật, xóa dòng hướng dẫn khi nộp. Xem [quy định nộp](../../SUBMISSION.md).

## 1. Thông tin học viên

- Họ tên:Nguyễn Hoài Nam
- MSSV:2A202603186
- Email:hoainguyennam10@gmail.com
- Lớp:K5-L2A
- Link repo bài làm:https://github.com/NamhocFPT/K5-L2A-Day02-NguyenHoaiNam-2A202603186-ObjectDetection.git 
- Link Colab đã chạy:https://colab.research.google.com/github/NamhocFPT/K5-L2A-Day02-NguyenHoaiNam-2A202603186-ObjectDetection/blob/main/notebooks/day2_annotation_to_yolo.ipynb#scrollTo=TMit61ZQPAJr

## 2. Schema và mini guideline

Chi tiết quy tắc xem tại [GUIDELINE_MINI.md](../../GUIDELINE_MINI.md). Tóm tắt 3 ca mơ hồ:
- `drive_003`: Các xe đỗ/chạy chồng lấn nhau -> Vẽ box riêng trên phần nhìn thấy của từng xe, cho phép box đè lên nhau.
- `drive_005`: Dáng xe nhìn từ trên xuống dễ phân vân giữa `car` và `van` -> Quyết định chọn `truck` do phần thân sau kéo dài và thấp hơn cabin rõ rệt.
- `drive_010`: Ảnh tối và nhòe -> Quyết định gán `car` vì vẫn nhìn rõ dáng capo, mui và kính xe con.
- Phần cần giảng viên làm rõ: Tiêu chí ranh giới rõ ràng hơn giữa minivan 7 chỗ (`van`) và SUV cỡ lớn (`car`).

## 3. Annotation và self-QC

- Số file nhãn train: 50
- Kết quả checker và lỗi đã xử lý: 50/50
- Danh sách ít nhất 10 ảnh đã rà bằng mắt:drive_001, drive_003, drive_007, drive_012, drive_018, drive_024, drive_031, drive_035, drive_042, drive_048.
- Lỗi bỏ sót/box/class phát hiện khi rà và cách sửa:
+ Lỗi Class: một số xe minivan / xe khách 16 chỗ bị gán nhầm thành car, đã đổi lại thành van.

+ Lỗi Box: các xe bị xe phía trước che một phần có box vẽ lỏng, đã chỉnh lại cho ôm sát phần thân thấy được. Xe bị cắt ở mép ảnh đã kéo box chạm đúng rìa ảnh.

+ Lỗi Bỏ sót / Thừa box: đã xóa các box xe li ti ở đường chân trờivì không đủ đặc trưng để chắc chắn lớp, và bổ sung box cho xe tải đỗ bên lề bị bỏ sót.
- Commit khóa nhãn ban đầu:b0e5fe1

## 4. Gold QC và rework

| Chỉ số              | Trước sửa | Sau sửa nếu có |
| ------------------- | --------: | -------------: |
| TP                  |       421 |                |
| FP                  |       478 |                |
| FN                  |       232 |                |
| Precision           |    0.4683 |                |
| Recall              |    0.6447 |                |
| F1                  |    0.5425 |                |
| mean_iou_of_matches |    0.8381 |                |
| passed              |     false |                |

Dẫn tới `outputs/annotation_evaluation.json` trong repo. Nếu rework, ghi ảnh, lỗi đã kiểm, quyết định sửa/giữ và lý do. Không suy nguyên nhân chỉ từ FP/FN. Không có rework thì ghi rõ.

## 5. Kết quả YOLO

- Runtime, GPU/CPU, phiên bản Ultralytics và Torch: Google Colab, GPU Tesla T4 (15GB VRAM), Ultralytics 8.4+, PyTorch 2.5+.
- Các tham số thay đổi so với notebook nếu có và lý do: Giữ nguyên cấu hình chuẩn của bài (model=yolo26n.pt, epochs=50, imgsz=640).
- Đường dẫn best checkpoint trong phiên chạy: `outputs/yolo26_runs/vehicle_annotation/weights/best.pt`

| Chỉ số trên 10 ảnh eval | Giá trị |
| ----------------------- | ------: |
| Precision               |  0.1759 |
| Recall                  |  0.3878 |
| mAP50                   |  0.2152 |
| mAP50–95                |  0.1441 |

Đặt cả 2 folder `assets/eval_predictions/` và `assets/yolo26_runs/` (giải nén từ `day2_colab_outputs.zip`) cạnh báo cáo và dẫn link tương đối. Không chỉ ghi số; chỉ ra ít nhất một ảnh và vật thể cụ thể.

Trả lời bốn câu hỏi cuối notebook:

1. Lớp nào recall thấp nhất? Ảnh nào minh họa?
van (và bus) có recall thấp nhất. Nguyên nhân do số lượng mẫu của hai lớp này trong tập train rất ít so với car
2. Nếu mAP50 cao nhưng mAP50–95 thấp, cần kiểm điều gì trên box?
Cần kiểm tra độ khít của box: Box đã tìm đúng vật thể nhưng vẽ chưa ôm sát.
3. Lỗi class nào có thể liên quan guideline? Dữ kiện nào hỗ trợ nhận xét?
lẫn Lỗi nhầm giữa car và van (và xe bán tải và  giữa car và truck).
Dữ kiện: Ma trận nhầm lẫn (confusion_matrix.png) cho thấy nhiều xe van bị model đoán nhầm thành car vì guideline chưa phân định rõ ranh giới xe 7–9 chỗ và minivan.
4. Vì sao không dùng 10 ảnh eval để train? Vai trò validation của chúng trong notebook là gì?
Không train để tránh Data Leakage (học vẹt/overfitting) khiến điểm số bị ảo.
Vai trò: Làm tập dữ liệu độc lập để chọn checkpoint tốt nhất (best.pt) và đo năng lực thực tế của mô hình.
## 6. Khó khăn và cách xử lý

| Bước/thời điểm   | Lỗi quan sát                                                    | Cách đã thử                                                                                | Kết quả/còn thiếu                                                                    |
| ---------------- | --------------------------------------------------------------- | ------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------ |
| Gán nhãn ban đầu | Dễ nhầm giữa car và van; box ở các xe bị che khuất còn vẽ lỏng. | Dùng CVAT để chỉnh sửa trực quan; đối chiếu lại quy tắc vẽ box bám sát phần nhìn thấy.     | Đạt cấu trúc 50/50 file nhãn hợp lệ qua script checker.                              |
| Đánh giá Gold QC | F1 ban đầu thấp (0.54) do có tới 478 lỗi False Positive.        | Đọc chi tiết file annotation_evaluation.json, lọc ra các ảnh có số box lệch nhiều          | Phát hiện nguyên nhân do gán cả xe li ti ở chân trời; xác định được các ảnh cần sửa. |
| Huấn luyện Colab | Cần đồng bộ nhãn từ repo GitHub lên Colab và cấu hình GPU.      | Đẩy commit nhãn lên GitHub, cấu hình Runtime sang T4 GPU và chạy notebook theo luồng chuẩn | Huấn luyện thành công 50 epoch và tải đủ kết quả về thư mục assets/.                 |

## 7. Tự đánh giá theo rubric

Đối chiếu [RUBRIC.md](../../RUBRIC.md):

| Tiêu chí | Điểm tối đa | Tự đánh giá | Diễn giải |
| --- | ---: | ---: | --- |
| Hoàn thành và định dạng YOLO | 10 | 10/10 | 50 file cùng basename, 5 cột, normalized, checker đạt 50/50. |
| Đầy đủ vật thể | 20 | 17/20 | Gán đủ các xe nhìn thấy, ban đầu còn bị thừa một số box quá xa ở chân trời. |
| Độ bám sát và hình học box | 20 | 18/20 | Mean IoU đạt 0.8381 (vượt chuẩn 0.70), box bám sát thân xe nhìn thấy. |
| Phân lớp nhất quán | 15 | 13/15 | Phân biệt cơ bản tốt 4 lớp theo schema; lưu ý thêm ranh giới van/car. |
| Mini guideline và quyết định mơ hồ | 10 | 10/10 | Đầy đủ định nghĩa 4 lớp, quy tắc vẽ box và 3 ca mơ hồ cụ thể. |
| Gold-set annotation QC | 15 | 12/15 | Đã chạy evaluator, IoU đạt 0.8381, ghi chép phân tích nguyên nhân rework rõ ràng. |
| Pipeline YOLO và phân tích | 10 | 10/10 | Colab chạy đủ 50 epoch, nộp đủ 10 ảnh eval trong assets và trả lời đủ 4 câu hỏi. |

Tổng điểm tự đánh giá ước tính: **90/100**.

## 8. Công cụ AI và tài liệu tham khảo

Ghi công cụ đã dùng, dùng ở bước nào và phần đã tự kiểm tra; không dùng thì ghi rõ. Liệt kê nguồn ngoài repo được sử dụng. Không ghi mật khẩu/token hoặc đính kèm gold train.
Công cụ AI đã sử dụng:

Công cụ: Trợ lý AI (Google Gemini / Antigravity).
Sử dụng ở bước:
Hỗ trợ đọc và sửa lỗi môi trường Python/PowerShell khi chạy lệnh trên máy.
Giải thích ý nghĩa các chỉ số đánh giá chất lượng nhãn (TP, FP, FN, Precision, Recall, F1, IoU).
Phần tự kiểm tra: Tự đối chiếu schema 4 lớp theo hướng dẫn; tự mở rà soát độ khít và tính đúng đắn của bounding box trên công cụ CVAT; tự kiểm tra và chạy file checker check_yolo_labels.py của bài Lab.

Công cụ hỗ trợ annotation:

Nền tảng CVAT (Computer Vision Annotation Tool - app.cvat.ai) để xem và chỉnh sửa trực quan bounding box.

Tài liệu tham khảo ngoài repo:

Tài liệu hướng dẫn Ultralytics YOLO: https://docs.ultralytics.com/
Tài liệu định dạng nhãn YOLO 1.1 trên CVAT: https://opencv.github.io/cvat/