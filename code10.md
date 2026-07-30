```mermaid
%%{init:{
'theme':'base',
'themeVariables':{
'background':'#FFFFFF',
'primaryTextColor':'#222222',
'fontFamily':'Times New Roman',
'fontSize':'14px',
'lineColor':'#555555'
}
}}%%

flowchart TB

subgraph MAIN["LƯU ĐỒ HOẠT ĐỘNG HỆ THỐNG"]
direction TB

    %% Luồng chính hàng ngang
    A["<b>ACQUISITION</b><br/><br/>• Khởi tạo hệ thống:<br/>  - Detector<br/>  - DeepSORT<br/>  - FaceNet<br/>  - Edge-TTS<br/><br/>• Đọc Frame từ Camera"] 
    --> B["<b>VISION PROCESSING</b><br/><br/>• YOLOv8: Phát hiện vật thể<br/>• DeepSORT: Theo dõi đối tượng<br/>• FaceNet + MTCNN: Nhận diện khuôn mặt<br/>• Ước lượng khoảng cách"] 
    --> C["<b>OUTPUT</b><br/><br/>• Hiển thị Bounding Box<br/>• Hiển thị ID/Tên<br/>• Phát thông báo Edge-TTS"]

    %% Luồng kiểm tra bên dưới
    C --> CHECK{"<b>Nhấn ESC?</b>"}
    
    CHECK -- "Không (Quay lại Camera)" --> A
    CHECK -- "Có" --> END_NODE(["<b>KẾT THÚC</b>"])

end

classDef boxClass fill:#A65A17,color:#ffffff,stroke:#7A3F0F,stroke-width:2px;
classDef conditionClass fill:#5B2BB5,color:#ffffff,stroke:#47208F,stroke-width:2px;
classDef endClass fill:#333333,color:#ffffff,stroke:#111111,stroke-width:2px;

class A,B,C boxClass
class CHECK conditionClass
class END_NODE endClass

style MAIN fill:#F7F7F7,stroke:#666666,stroke-width:2px
