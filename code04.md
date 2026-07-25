```mermaid
graph TD
    classDef step stroke:#2563eb,stroke-width:2px,fill:#1e3a8a,color:#ffffff,rx:6px,ry:6px;
    classDef process stroke:#059669,stroke-width:1.5px,fill:#064e3b,color:#ffffff,rx:6px,ry:6px;
    classDef output stroke:#7c3aed,stroke-width:1.5px,fill:#4c1d95,color:#ffffff,rx:6px,ry:6px;

    subgraph HANG1 ["Giai đoạn 1: Phát hiện và Dự đoán"]
        direction LR
        A["Khung hình mới"] --> B["YOLO Detection"] --> C["Kalman Predict<br>• Dự đoán vị trí"]
    end

    subgraph HANG2 ["Giai đoạn 2: Khớp và Cập nhật"]
        direction LR
        D["Matching<br>• IoU + Cosine + Maha"] --> E["Kalman Update<br>• Cập nhật vị trí"] --> F["Track Management<br>• Tạo mới / Xóa già"]
    end

    C --> D
    F --> G["Tracking Result<br>• Hiển thị (age <= 3)"]

    class A,B step;
    class C,D,E,F process;
    class G output;
```
