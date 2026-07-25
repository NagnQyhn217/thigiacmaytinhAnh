# thigiacmaytinhAnh

graph TD
    %% Styling
    classDef mainApp stroke:#2563eb,stroke-width:2px,fill:#eff6ff,rx:8px,ry:8px;
    classDef module stroke:#059669,stroke-width:1.5px,fill:#ecfdf5,rx:6px,ry:6px;
    classDef subModule stroke:#d97706,stroke-width:1.5px,fill:#fffbeb,rx:6px,ry:6px;
    classDef output stroke:#7c3aed,stroke-width:1.5px,fill:#f5f3ff,rx:6px,ry:6px;

    subgraph MAIN ["CHƯƠNG TRÌNH CHÍNH (main.py)"]
        A["Khởi tạo và điều phối các module"] ::: mainApp

        %% Primary Modules
        A --> B["detector<br><b>(YOLOv8)</b>"] ::: module
        A --> C["tracker<br><b>(Kalman / IoU / Cosine / Maha)</b>"] ::: module
        A --> D["tts<br><b>(Edge-TTS)</b>"] ::: module

        %% Secondary Modules
        B --> E["distance.py<br><b>(Ước lượng khoảng cách)</b>"] ::: subModule
        C --> F["face_recognition.py<br><b>(Haar + Template Matching)</b>"] ::: subModule

        %% Output Stage
        E --> G["Hiển thị kết quả & Phát âm thanh"] ::: output
        F --> G
        D --> G
    end
