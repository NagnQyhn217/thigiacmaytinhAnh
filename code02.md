```mermaid
graph TD
    %% Tùy chỉnh màu nền sáng cho các khung bao (Subgraph)
    style SYSTEM fill:#f8fafc,stroke:#475569,stroke-width:2px,color:#0f172a
    style MAIN_FLOW fill:#ffffff,stroke:#94a3b8,stroke-width:1.5px,color:#1e293b
    style MODULE_SUPPORT fill:#ffffff,stroke:#94a3b8,stroke-width:1.5px,color:#1e293b

    %% Định nghĩa các lớp màu cho nút
    classDef mainApp stroke:#2563eb,stroke-width:2px,fill:#1e3a8a,color:#ffffff,rx:6px,ry:6px;
    classDef module stroke:#059669,stroke-width:1.5px,fill:#064e3b,color:#ffffff,rx:6px,ry:6px;
    classDef subModule stroke:#d97706,stroke-width:1.5px,fill:#78350f,color:#ffffff,rx:6px,ry:6px;
    classDef output stroke:#7c3aed,stroke-width:1.5px,fill:#4c1d95,color:#ffffff,rx:6px,ry:6px;

    subgraph SYSTEM ["HỆ THỐNG CHÍNH"]
        
        subgraph MAIN_FLOW ["LUỒNG XỬ LÝ CHÍNH"]
            Cam["Camera"] --> Pre["Preprocess"]
            Pre --> Yolo["YOLOv8"]
            Yolo --> Sort["DeepSORT"]
            
            Yolo --> Det["Detection"]
            Sort --> Track["Tracking"]
            
            Det --> Dist["Distance Estimation"]
            Track --> Dist
            
            Dist --> Face["Face Recognition<br/>(MTCNN + FaceNet)"]
            Dist --> TTS["TTS Output<br/>(Edge-TTS)"]
            
            Face --> Disp["Display Output"]
            TTS --> Disp
        end

        subgraph MODULE_SUPPORT ["MODULE SUPPORT"]
            direction LR
            M1["Object Detection<br/>(YOLOv8)"] --- M2["Tracking<br/>(DeepSORT)"] --- M3["Face Recognition<br/>(MTCNN + FaceNet)"]
            M4["Distance<br/>Estimation"] --- M5["Text-to-Speech<br/>(TTS)"] --- M6["Database<br/>(encodings.pkl)"]
        end

    end

    %% Gán class màu cho từng nút
    class Cam mainApp;
    class Pre,Yolo,Sort module;
    class Det,Track,Dist subModule;
    class Face,TTS,Disp output;
    class M1,M2,M3,M4,M5,M6 module;
