```mermaid
graph TD
    style DEEPSORT_FLOW fill:#f8fafc,stroke:#475569,stroke-width:1.5px,color:#0f172a
    style LEFT_COL fill:#ffffff,stroke:#cbd5e1,stroke-width:1px
    style RIGHT_COL fill:#ffffff,stroke:#cbd5e1,stroke-width:1px

    classDef inputNode stroke:#2563eb,stroke-width:1.5px,fill:#1e3a8a,color:#ffffff,rx:4px,ry:4px;
    classDef stepNode stroke:#059669,stroke-width:1.5px,fill:#064e3b,color:#ffffff,rx:4px,ry:4px;
    classDef subStepNode stroke:#d97706,stroke-width:1.5px,fill:#78350f,color:#ffffff,rx:4px,ry:4px;
    classDef outputNode stroke:#7c3aed,stroke-width:1.5px,fill:#4c1d95,color:#ffffff,rx:4px,ry:4px;

    subgraph DEEPSORT_FLOW ["QUY TRÌNH THEO DÕI DeepSORT"]
        In["<b>INPUT:</b> Detections YOLOv8 & Tracks"] --> S1

        subgraph LEFT_COL ["GIAI ĐOẠN 1: DỰ ĐOÁN & GÁN"]
            subgraph S1 ["Bước 1: Dự đoán (Kalman)"]
                Eq1["x̂ₖ|ₖ₋₁ = Fₖ x̂ₖ₋₁|ₖ₋₁ + Bₖ uₖ"]
            end
            
            S1 --> S2
            
            subgraph S2 ["Bước 2: Tính Ma trận Chi phí"]
                Eq2["Cost = λ×Mahalanobis + (1-λ)×Cosine"]
            end
            
            S2 --> S3
            
            subgraph S3 ["Bước 3: Gán (Hungarian Alg.)"]
                Details3["• Tối ưu tổng chi phí<br/>• Ngưỡng: max_cosine = 0.3"]
            end
        end

        S3 --> S4

        subgraph RIGHT_COL ["GIAI ĐOẠN 2: CẬP NHẬT & XUẤT"]
            subgraph S4 ["Bước 4: Cập nhật Tracks"]
                Details4["• Được gán: Update detection<br/>• Không gán: Tăng age<br/>• Chưa gán: Tạo track mới"]
            end
            
            S4 --> S5
            
            subgraph S5 ["Bước 5: Vòng đời Tracks"]
                Details5["• Xóa track: age > 30<br/>• Xác nhận: n_init = 3 frames"]
            end
            
            S5 --> Out["<b>OUTPUT:</b> Tracks đã cập nhật (ID ổn định)"]
        end
    end

    class In inputNode;
    class Eq1,Eq2 stepNode;
    class Details3,Details4,Details5 subStepNode;
    class Out outputNode;
