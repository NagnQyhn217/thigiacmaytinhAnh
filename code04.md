```mermaid
flowchart LR
    %% CSS Styling
    classDef header fill:#2b5c8f,color:#fff,stroke:#1d3d5f,stroke-width:2px,font-weight:bold;
    classDef io fill:#34495e,color:#fff,stroke:#2c3e50,stroke-width:2px,font-weight:bold;
    classDef step fill:#ffffff,color:#2c3e50,stroke:#34495e,stroke-width:1.5px,text-align:left;

    subgraph HANG1 [" hàng 1: Dự đoán & Tính toán "]
        direction LR
        IN_OUT1["<b>INPUT</b><br/>Detections & Tracks"]:::io
        
        STEP1["<b>BƯỚC 1: Dự đoán (Kalman)</b><br/>$\hat{x}_{k\vert{}k-1} = F_k \hat{x}_{k-1\vert{}k-1} + B_k u_k$"]:::step
        
        STEP2["<b>BƯỚC 2: Ma trận chi phí</b><br/>$\text{Cost} = \lambda \times \text{Mahalanobis} + (1-\lambda) \times \text{Cosine}$"]:::step

        IN_OUT1 --> STEP1 --> STEP2
    end

    subgraph HANG2 [" hàng 2: Phân công & Cập nhật "]
        direction LR
        STEP3["<b>BƯỚC 3: Ghép nối (Hungarian)</b><br/>• Phân phối tối ưu chi phí<br/>• Ngưỡng <code>max_cosine = 0.3</code>"]:::step
        
        STEP4["<b>BƯỚC 4: Cập nhật Tracks</b><br/>• Gán: Cập nhật detection<br/>• Không gán: Dự đoán (tăng age)<br/>• Mới: Tạo track từ unassigned"]:::step
        
        STEP5["<b>BƯỚC 5: Vòng đời Track</b><br/>• Xóa khi <code>age > 30</code><br/>• Xác nhận khi đủ <code>n_init=3</code>"]:::step
        
        IN_OUT2["<b>OUTPUT</b><br/>Tracks & ID"]:::io

        STEP3 --> STEP4 --> STEP5 --> IN_OUT2
    end

    %% Nối hàng 1 xuống hàng 2
    STEP2 ==> STEP3
