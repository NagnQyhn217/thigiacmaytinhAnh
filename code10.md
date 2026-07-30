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

START(["<b>BẮT ĐẦU</b>"]) --> INIT["<b>Khởi tạo hệ thống</b><br/>(YOLOv8, DeepSORT, FaceNet, Edge-TTS)"]
INIT --> READ["<b>Đọc frame từ camera</b>"]

subgraph PROCESS["XỬ LÝ KHUNG HÌNH"]
direction TB
P1["<b>YOLOv8:</b> Detect vật thể (conf ≥ 0.4, iou ≤ 0.45)"]
P2["<b>DeepSORT:</b> Cập nhật tracking (Kalman, Hungarian)"]
P3["<b>FaceNet & MTCNN:</b> Nhận diện khuôn mặt (threshold = 0.8)"]
P4["<b>Ước lượng khoảng cách:</b> d = base_size / √area_ratio"]

P1 --> P2 --> P3 --> P4
end

READ --> PROCESS
PROCESS --> DECIDE["<b>QUYẾT ĐỊNH THÔNG BÁO (TTS)</b><br/>• Có người/vật thể? ──▶ Thông báo khoảng cách<br/>• Người quen? ──▶ 'Chào [Tên]'"]
DECIDE --> SHOW["<b>Hiển thị kết quả lên màn hình</b>"]
SHOW --> CHECK{"<b>Nhấn ESC?</b>"}

CHECK -- "CÓ" --> FINISH(["<b>KẾT THÚC</b>"])
CHECK -- "KHÔNG" --> READ

end

classDef start_end fill:#333333,color:#ffffff,stroke:#111111,stroke-width:2px;
classDef process_box fill:#A65A17,color:#ffffff,stroke:#7A3F0F,stroke-width:2px;
classDef decide_box fill:#2348A5,color:#ffffff,stroke:#1B3D91,stroke-width:2px;
classDef condition_box fill:#5B2BB5,color:#ffffff,stroke:#47208F,stroke-width:2px;

class START,FINISH start_end
class INIT,READ,P1,P2,P3,P4,SHOW process_box
class DECIDE decide_box
class CHECK condition_box

style MAIN fill:#F7F7F7,stroke:#666666,stroke-width:2px
style PROCESS fill:#FFFFFF,stroke:#A65A17,stroke-width:1.5px,stroke-dasharray: 4 4
