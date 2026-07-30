```mermaid
graph TD
    %% Styling nền sáng cho khung ngoài
    style DEEPSORT_FLOW fill:#f8fafc,stroke:#475569,stroke-width:1.5px,color:#0f172a

    %% Styling các lớp màu nút gọn gàng
    classDef inputNode stroke:#2563eb,stroke-width:1.5px,fill:#1e3a8a,color:#ffffff,rx:4px,ry:4px;
    classDef stepNode stroke:#059669,stroke-width:1.5px,fill:#064e3b,color:#ffffff,rx:4px,ry:4px;
    classDef subStepNode stroke:#d97706,stroke-width:1.5px,fill:#78350f,color:#ffffff,rx:4px,ry:4px;
    classDef outputNode stroke:#7c3aed,stroke-width:1.5px,fill:#4c1d95,color:#ffffff,rx:4px,ry:4px;

    subgraph DEEPSORT_FLOW ["QUY TRÌNH THEO DÕI ĐỐI TƯỢNG VỚI DeepSORT"]
        
        In["<b>INPUT:</b> Detections từ YOLOv8 & Tracks hiện tại"] --> S1
        
        subgraph S1 ["BƯỚC 1: Dự đoán trạng thái (Kalman Filter)"]
            Eq1["x̂ₖ|ₖ₋₁ = Fₖ x̂ₖ₋₁|ₖ₋₁ + Bₖ uₖ"]
        end
        
        S1 --> S2
        
        subgraph S2 ["BƯỚC 2: Tính ma trận chi phí (Cost Matrix)"]
            Eq2["Cost = λ × Mahalanobis + (1-λ) × Cosine Dist."]
        end
        
        S2 --> S3
        
        subgraph S3 ["BƯỚC 3: Gán Tracks bằng Hungarian Algorithm"]
            Details3["• Phân phối tối ưu chi phí nhỏ nhất<br/>• Áp dụng ngưỡng (max_cosine_distance = 0.3)"]
        end
        
        S3 --> S4
        
        subgraph S4 ["BƯỚC 4: Cập nhật trạng thái Tracks"]
            Details4["• Tracks được gán: Cập nhật detection mới<br/>• Tracks không gán: Dự đoán tiếp (tăng age)<br/>• Tracks mới: Tạo mới từ detection chưa gán"]
        end
        
        S4 --> S5
        
        subgraph S5 ["BƯỚC 5: Quản lý vòng đời Tracks"]
            Details5["• Xóa track khi age > max_age (30)<br/>• Xác nhận track khi n_init (3) frame liên tiếp"]
        end
        
        S5 --> Out["<b>OUTPUT:</b> Danh sách Tracks đã cập nhật (ID ổn định)"]

    end

    class In inputNode;
    class Eq1,Eq2 stepNode;
    class Details3,Details4,Details5 subStepNode;
    class Out outputNode;
