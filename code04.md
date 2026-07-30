```mermaid
flowchart TD
    %% Định nghĩa font chữ chuẩn, bo góc mượt và màu sắc dễ nhìn
    classDef header fill:#2b5c8f,color:#ffffff,stroke:#1d3d5f,stroke-width:2px,font-family:sans-serif,font-weight:bold;
    classDef io fill:#34495e,color:#ffffff,stroke:#2c3e50,stroke-width:2px,font-family:sans-serif,font-weight:bold;
    classDef step fill:#ffffff,color:#2c3e50,stroke:#34495e,stroke-width:1.5px,font-family:sans-serif,text-align:left;

    TITLE["QUY TRÌNH THEO DÕI ĐỐI TƯỢNG VỚI DeepSORT"]:::header

    IN_OUT1["INPUT: Detections từ YOLOv8 và Tracks hiện tại"]:::io

    STEP1["<b>BƯỚC 1: Dự đoán trạng thái mới bằng Kalman Filter</b><br/>• Dự đoán: x̂(k|k-1) = F(k) * x̂(k-1|k-1) + B(k) * u(k)"]:::step

    STEP2["<b>BƯỚC 2: Tính ma trận chi phí giữa Tracks và Detections</b><br/>• Cost = λ × Mahalanobis + (1-λ) × Cosine Distance"]:::step

    STEP3["<b>BƯỚC 3: Gán Tracks với Detections bằng Hungarian Algorithm</b><br/>• Phân phối tối ưu để tổng chi phí nhỏ nhất<br/>• Áp dụng ngưỡng chi phí (<code>max_cosine_distance = 0.3</code>)"]:::step

    STEP4["<b>BƯỚC 4: Cập nhật trạng thái Tracks</b><br/>• <b>Tracks được gán:</b> Cập nhật với detection mới<br/>• <b>Tracks không gán:</b> Tiếp tục dự đoán (tăng age)<br/>• <b>Tracks mới:</b> Tạo mới từ detection chưa gán"]:::step

    STEP5["<b>BƯỚC 5: Quản lý vòng đời Tracks</b><br/>• Xóa track khi <code>age > max_age (30)</code><br/>• Xác nhận track khi <code>n_init (3)</code> frame liên tiếp"]:::step

    IN_OUT2["OUTPUT: Danh sách Tracks đã cập nhật với ID ổn định"]:::io

    TITLE --- IN_OUT1
    IN_OUT1 --> STEP1
    STEP1 --> STEP2
    STEP2 --> STEP3
    STEP3 --> STEP4
    STEP4 --> STEP5
    STEP5 --> IN_OUT2
