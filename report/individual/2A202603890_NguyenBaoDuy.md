# Báo cáo cá nhân — Day 01: Lọc tin nhắn rác bằng ML, DL, Embedding và LLM

> Đổi tên file này thành `MSSV_HoTen.md` của bạn, ví dụ `2A20260000_NguyenVanAn.md`, rồi điền từng mục. Xoá các dòng hướng dẫn in nghiêng khi xong.

- **MSSV:**2A202603890
- **Họ và tên:**Nguyễn Bảo Duy
- **SEED** (in ở ô đầu notebook):986

## 1. Bằng chứng

| Tệp | Có? |
| --- | --- |
| [`day01_lab.ipynb`](day01_lab.ipynb) — notebook đã chạy, còn output | x |
| [`lab1_report.json`](lab1_report.json) — do ô "Báo cáo cuối" sinh ra | x |
| [`hand_calc.jpg`](hand_calc.jpg) — ảnh tính tay có các bước | x |

## 2. Kết quả chính

*Chép bảng so sánh cuối Phần 5 (F1 test, F1 SUB 40, p95 ms/tin, USD/1k tin) của chính bạn.*

## 3. Dự đoán và thực tế

*Chọn 3 dự đoán `predict(...)` lệch nhiều nhất so với kết quả. Mỗi cái: bạn đoán gì, ra gì, vì sao lệch.*

## 4. Phân tích 50 case khó

Bow+ mlp tụt nhiều nhất. 

## 5. Thử thách cá nhân
3: DL · Đổi lớp ẩn MLP thành 4 và 512 nơ-ron. Báo số tham số, F1 test, thời gian train. Khi nào nên chọn mạng nhỏ?
Sử dụng mô hình MLPClassifier của thư viện scikit-learn.

Thiết lập tham số hidden_layer_sizes=(4,) cho thí nghiệm 1 và hidden_layer_sizes=(512,) cho thí nghiệm 2
Mạng ẩn 4 nơ-ron:

Số tham số: ~1.545 tham số.

Thời gian train: Rất nhanh.

F1 Test: 0.9355
Mạng ẩn 512 nơ-ron:

Số tham số: ~197.633 tham số.

Thời gian train: Chậm hơn đáng kể.

F1 Test: 0.9418
Khi tăng số nơ-ron từ 4 lên 512, ma trận trọng số phình to khổng lồ khiến thời gian tính toán và cập nhật gradient tăng vọt. Tuy nhiên, điểm F1 không tăng tỷ lệ thuận vì bản thân dữ liệu vector đầu vào đã mang sẵn đặc trưng ngữ nghĩa rất tốt và dễ phân tách tuyến tính. Mạng 512 nơ-ron thậm chí mang rủi ro "học vẹt" các đặc trưng nhiễu của tập huấn luyện. Đặc biệt, như đã thấy ở phần đánh giá 50 case khó, khi kết hợp với đặc trưng thô, mô hình quá phức tạp sẽ "sụp đổ" mạnh nhất khi gặp dữ liệu biến đổi.

Khi nào nên chọn mạng nhỏ

Dữ liệu huấn luyện ít: Để tránh hiện tượng Overfitting. Mạng nhỏ ép mô hình chỉ chắt lọc những đặc trưng quan trọng nhất.

Yêu cầu độ trễ cực thấp: Mạng ít tham số sẽ có tốc độ suy luận tính bằng micro-giây, dễ dàng đáp ứng SLA thời gian thực (< 50ms) cho hàng chục ngàn tin nhắn.

Tài nguyên phần cứng hạn chế: Khi cần triển khai mô hình trực tiếp lên điện thoại di động hoặc các thiết bị biên có dung lượng RAM và pin yếu.
## 6. Phương án cho sản phẩm thật

*Với yêu cầu p95 < 50 ms/tin cho 10 triệu SMS/ngày: chọn phương án nào, dẫn số liệu nào, chấp nhận đánh đổi gì.*

## 7. AI log và điều đã học

*Mỗi lần dùng AI: hỏi gì, nhận gì, bạn sửa gì. Sau đó 2–3 câu: điều bạn hiểu ra hôm nay mà trước đó chưa hiểu.*
