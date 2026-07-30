```mermaid
flowchart TD
    %% Định nghĩa Style
    classDef header fill:#2b5c8f,color:#fff,stroke:#1d3d5f,stroke-width:2px,font-weight:bold;
    classDef inputOutput fill:#34495e,color:#fff,stroke:#2c3e50,stroke-width:2px,font-weight:bold;
    classDef stepNode fill:#ffffff,color:#2c3e50,stroke:#34495e,stroke-width:1px,text-align:left;

    TITLE["<b>QUY TRÌNH THEO DÕI ĐỐI TƯỢNG VỚI DeepSORT</b>"]:::header
    
    IN_OUT1["<b>INPUT:</b> Detections từ YOLOv8 và Tracks hiện tại"]:::inputOutput
    
    STEP1["<b>BƯỚC 1: Dự đoán trạng thái mới bằng Kalman Filter</b><br/>• $\hat{x}_{k|k-1} = F_k \hat{x}_{k-1|k-1} + B_k u_k$"]:::stepNode
    
    STEP2["<b>BƯỚC 2: Tính ma trận chi phí giữa Tracks và Detections</b><br/>• $\text{Cost} = \lambda \times \text{Mahalanobis} + (1-\lambda) \times \text{Cosine Distance}$"]:::stepNode
    
    STEP3["<b>BƯỚC 3: Gán Tracks với Detections bằng Hungarian Algorithm</b><br/>• Phân phối tối ưu để tổng chi phí nhỏ nhất<br/>• Áp dụng ngưỡng chi phí (<code>max_cosine_distance = 0.3</code>)"]:::stepNode
    
    STEP4["<b>BƯỚC 4: Cập nhật trạng thái Tracks</b><br/>• <b>Tracks được gán:</b> Cập nhật với detection mới<br/>• <b>Tracks không gán:</b> Tiếp tục dự đoán (tăng age)<br/>• <b>Tracks mới:</b> Tạo mới từ detection chưa gán"]:::stepNode
    
    STEP5["<b>BƯỚC 5: Quản lý vòng đời Tracks</b><br/>• Xóa track khi <code>age > max_age (30)</code><br/>• Xác nhận track khi <code>n_init (3)</code> frame liên tiếp"]:::stepNode
    
    IN_OUT2["<b>OUTPUT:</b> Danh sách Tracks đã cập nhật với ID ổn định"]:::inputOutput

    %% Điều hướng luồng
    TITLE --- IN_OUT1
    IN_OUT1 --> STEP1
    STEP1 --> STEP2
    STEP2 --> STEP3
    STEP3 --> STEP4
    STEP4 --> STEP5
    STEP5 --> IN_OUT2
