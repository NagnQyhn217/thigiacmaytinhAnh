```mermaid
graph TD
    %% Styling nền sáng cho các khung bao
    style YOLO_PRINCIPLE fill:#f8fafc,stroke:#475569,stroke-width:1.5px,color:#0f172a
    style INPUT_SEC fill:#ffffff,stroke:#94a3b8,stroke-width:1px,color:#1e293b
    style PRED_SEC fill:#ffffff,stroke:#94a3b8,stroke-width:1px,color:#1e293b
    style OUT_SEC fill:#ffffff,stroke:#94a3b8,stroke-width:1px,color:#1e293b

    %% Styling các nút gọn gàng
    classDef inputNode stroke:#2563eb,stroke-width:1.5px,fill:#1e3a8a,color:#ffffff,rx:4px,ry:4px;
    classDef cnnNode stroke:#059669,stroke-width:1.5px,fill:#064e3b,color:#ffffff,rx:4px,ry:4px;
    classDef predNode stroke:#d97706,stroke-width:1.5px,fill:#78350f,color:#ffffff,rx:4px,ry:4px;
    classDef outNode stroke:#7c3aed,stroke-width:1.5px,fill:#4c1d95,color:#ffffff,rx:4px,ry:4px;

    subgraph YOLO_PRINCIPLE ["NGUYÊN LÝ HOẠT ĐỘNG CỦA YOLO"]
        
        subgraph INPUT_SEC ["1. INPUT IMAGE & FEATURE EXTRACTION"]
            Img["Ảnh đầu vào"] --> CNN["CNN Backbone<br/>(Extract Features)"]
        end

        INPUT_SEC --> PRED_SEC

        subgraph PRED_SEC ["2. PREDICTION LAYER (Lưới S × S)"]
            Grid["Chia ảnh thành lưới S×S"] --> DetInfo["Mỗi ô dự đoán:<br/>• B bounding boxes<br/>• Confidence scores<br/>• Class probabilities"]
        end

        PRED_SEC --> OUT_SEC

        subgraph OUT_SEC ["3. OUTPUT (NMS - Non-Maximum Suppression)"]
            direction LR
            O1["Người: 0.92"] --- O2["Xe máy: 0.85"]
            O3["Ghế: 0.78"] --- O4["Bàn: 0.72"]
        end

    end

    class Img inputNode;
    class CNN cnnNode;
    class Grid,DetInfo predNode;
    class O1,O2,O3,O4 outNode;
