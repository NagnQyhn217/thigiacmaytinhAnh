```mermaid
graph TD
    %% Style nền sáng
    style SYSTEM fill:#f8fafc,stroke:#475569,stroke-width:1.5px,color:#0f172a
    style MAIN_FLOW fill:#ffffff,stroke:#94a3b8,stroke-width:1px,color:#1e293b
    style MODULE_SUPPORT fill:#ffffff,stroke:#94a3b8,stroke-width:1px,color:#1e293b

    %% Class định hình kích thước nhỏ gọn
    classDef mainApp stroke:#2563eb,stroke-width:1.5px,fill:#1e3a8a,color:#ffffff,rx:4px,ry:4px;
    classDef module stroke:#059669,stroke-width:1.5px,fill:#064e3b,color:#ffffff,rx:4px,ry:4px;
    classDef subModule stroke:#d97706,stroke-width:1.5px,fill:#78350f,color:#ffffff,rx:4px,ry:4px;
    classDef output stroke:#7c3aed,stroke-width:1.5px,fill:#4c1d95,color:#ffffff,rx:4px,ry:4px;

    subgraph SYSTEM ["HỆ THỐNG CHÍNH"]
        
        subgraph MAIN_FLOW ["LUỒNG XỬ LÝ CHÍNH"]
            Cam["Camera"] --> Pre["Preprocess"]
            Pre --> Yolo["YOLOv8"] --> Sort["DeepSORT"]
            
            Yolo --> Det["Detection"]
            Sort --> Track["Tracking"]
            
            Det --> Dist["Distance Est."]
            Track --> Dist
            
            Dist --> Face["Face Recog.<br/>(MTCNN+FaceNet)"]
            Dist --> TTS["TTS Output<br/>(Edge-TTS)"]
            
            Face --> Disp["Display Output"]
            TTS --> Disp
        end

        subgraph MODULE_SUPPORT ["MODULE SUPPORT"]
            M1["YOLOv8"] --- M2["DeepSORT"]
            M3["MTCNN + FaceNet"] --- M4["Distance Est."]
            M5["Edge-TTS"] --- M6["encodings.pkl"]
        end

    end

    class Cam mainApp;
    class Pre,Yolo,Sort module;
    class Det,Track,Dist subModule;
    class Face,TTS,Disp output;
    class M1,M2,M3,M4,M5,M6 module;
