```mermaid
%%{init:{
'theme':'base',
'themeVariables':{
'background':'#FFFFFF',
'primaryTextColor':'#222222',
'fontFamily':'Times New Roman',
'fontSize':'16px',
'lineColor':'#555555'
}
}}%%

flowchart TB

subgraph MAIN["LƯU ĐỒ HOẠT ĐỘNG HỆ THỐNG"]
direction TB

START(["<b>BẮT ĐẦU</b>"])

INIT["<b>Khởi tạo hệ thống</b><br/><br/>• Detector (YOLOv8)<br/>• Tracker (DeepSORT)<br/>• FaceNet & MTCNN<br/>• Edge-TTS"]

READ["<b>Đọc khung hình từ camera</b>"]

subgraph PROCESS["XỬ LÝ KHUNG HÌNH"]
direction TB
P1["<b>Phát hiện vật thể bằng YOLOv8</b><br/><br/>• Detect: 7 lớp đối tượng<br/>• Ngưỡng: conf ≥ 0.4, iou ≤ 0.45"]
P2["<b>Cập nhật tracker với DeepSORT</b><br/><br/>• Kalman Filter dự đoán trạng thái<br/>• Hungarian Algorithm gán track-detection<br/>• max_age = 30, max_cosine_distance = 0.3"]
P3["<b>Nhận diện khuôn mặt (nếu là người)</b><br/><br/>• MTCNN phát hiện khuôn mặt<br/>• FaceNet embedding 512 chiều<br/>• Euclidean Distance với threshold = 0.8"]
P4["<b>Ước lượng khoảng cách</b><br/><br/>• d = base_size / √area_ratio<br/>• Giới hạn: 0.3m ≤ d ≤ 8.0m"]

P1 --> P2
P2 --> P3
P3 --> P4
end

DECIDE["<b>QUYẾT ĐỊNH THÔNG BÁO (TTS)</b><br/><br/>• Có người? ──▶ 'Có người phía trước'<br/>• Có người quen? ──▶ 'Chào [tên]'<br/>• Có vật thể khác? ──▶ '[Tên] ở khoảng [d]m'"]

SHOW["<b>Hiển thị kết quả lên màn hình</b>"]

CHECK{"<b>Nhấn ESC?</b>"}

FINISH(["<b>KẾT THÚC</b>"])

START --> INIT
INIT --> READ
READ --> PROCESS
PROCESS --> DECIDE
DECIDE --> SHOW
SHOW --> CHECK
CHECK -- "CÓ" --> FINISH
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
style PROCESS fill:#FFFFFF,stroke:#A65A17,stroke-width:1.5px,stroke-dasharray: 5 5
