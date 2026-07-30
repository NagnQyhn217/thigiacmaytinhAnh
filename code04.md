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
        
        %% --- HÀNG 1 (Từ Tới Sang Phải) ---
        In["<b>INPUT</b><br/>Detections & Tracks"] --> S1["<b>Bước 1: Dự đoán (Kalman)</b><br/>x̂ₖ|ₖ₋₁ = Fₖ x̂ₖ₋₁|ₖ₋₁ + Bₖ uₖ"]
        S1 --> S2["<b>Bước 2: Ma trận Chi phí</b><br/>Cost = λ×Mahalanobis + (1-λ)×Cosine"]
        
        %% Mối nối từ Hàng 1 xuống Hàng 2 (Chạy từ S2 xuống S3)
        S2 --> S3
        
        %% --- HÀNG 2 (Tới Sang Phải) ---
        S3["<b>Bước 3: Gán (Hungarian)</b><br/>• Tối ưu tổng chi phí<br/>• Ngưỡng max_cosine = 0.3"] --> S4["<b>Bước 4 & 5: Cập nhật & Vòng đời</b><br/>• Update / Tăng age / Tạo mới<br/>• Xóa (age > 30) | Xác nhận (n_init = 3)"]
        S4 --> Out["<b>OUTPUT</b><br/>Tracks đã cập nhật"]

    end

    class In inputNode;
    class S1,S2 stepNode;
    class S3,S4 subStepNode;
    class Out outputNode;
