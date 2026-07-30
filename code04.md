```mermaid
graph TD
    %% Tối ưu giao diện sáng
    style DEEPSORT_FLOW fill:#f8fafc,stroke:#475569,stroke-width:1.5px,color:#0f172a

    %% Tăng cỡ chữ lên to rõ (font-size: 16px - 18px)
    classDef inputNode stroke:#2563eb,stroke-width:2px,fill:#1e3a8a,color:#ffffff,rx:6px,ry:6px,font-size:16px;
    classDef stepNode stroke:#059669,stroke-width:2px,fill:#064e3b,color:#ffffff,rx:6px,ry:6px,font-size:16px;
    classDef subStepNode stroke:#d97706,stroke-width:2px,fill:#78350f,color:#ffffff,rx:6px,ry:6px,font-size:15px;
    classDef outputNode stroke:#7c3aed,stroke-width:2px,fill:#4c1d95,color:#ffffff,rx:6px,ry:6px,font-size:16px;

    subgraph DEEPSORT_FLOW ["QUY TRÌNH THEO DÕI DEEPSORT"]
        
        %% Hàng 1: Input và Bước 1
        In["<b>INPUT</b><br/>Detections & Tracks"] --> S1["<b>Bước 1: Dự đoán (Kalman)</b><br/>x̂ₖ|ₖ₋₁ = Fₖ x̂ₖ₋₁|ₖ₋₁ + Bₖ uₖ"]
        
        %% Xuống hàng 2: Bước 2 và Bước 3
        S1 --> S2["<b>Bước 2: Tính Ma trận Chi phí</b><br/>Cost = λ×Mahalanobis + (1-λ)×Cosine"]
        S2 --> S3["<b>Bước 3: Gán (Hungarian Alg.)</b><br/>• Tối ưu tổng chi phí<br/>• Ngưỡng max_cosine = 0.3"]
        
        %% Xuống hàng 3: Bước 4, Bước 5 và Output
        S3 --> S4["<b>Bước 4: Cập nhật Tracks</b><br/>• Được gán: Update<br/>• Không gán: Tăng age<br/>• Chưa gán: Tạo mới"]
        S4 --> S5["<b>Bước 5: Vòng đời Tracks</b><br/>• Xóa: age > 30<br/>• Xác nhận: n_init = 3"]
        S5 --> Out["<b>OUTPUT</b><br/>Tracks đã cập nhật"]

    end

    class In inputNode;
    class S1,S2 stepNode;
    class S3,S4,S5 subStepNode;
    class Out outputNode;
