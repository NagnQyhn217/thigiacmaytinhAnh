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

subgraph MAIN["QUY TRÌNH NHẬN DIỆN KHUÔN MẶT VỚI MTCNN + FaceNet"]
direction TB

A["INPUT<br/><b>Khung hình (frame) và encodings.pkl (database)</b>"]

B["<b>BƯỚC 1: Phát hiện khuôn mặt bằng MTCNN</b><br/><br/>
• Phát hiện các khuôn mặt trong ảnh<br/>
• Trả về bounding box và 5 điểm đặc trưng<br/>
• Tham số: margin = 20, min_face_size = 60"]

C["<b>BƯỚC 2: Cắt và tiền xử lý khuôn mặt</b><br/><br/>
• Crop vùng khuôn mặt dựa trên bounding box<br/>
• Resize về kích thước 160×160 pixel<br/>
• Chuẩn hóa giá trị pixel về [-1, 1]"]

D["<b>BƯỚC 3: Trích xuất embedding bằng FaceNet (InceptionResnetV1)</b><br/><br/>
• Đưa ảnh khuôn mặt qua mạng InceptionResnetV1<br/>
• Trả về vector embedding 512 chiều<br/>
• Chuẩn hóa L2 để sử dụng với Euclidean Distance"]

E["<b>BƯỚC 4: So sánh với database bằng Euclidean Distance</b><br/><br/>
distance = √∑(emb_query − emb_db)²<br/>
• Tính khoảng cách với tất cả embeddings trong database<br/>
• Tìm người có khoảng cách nhỏ nhất<br/>
• Ngưỡng threshold = 0.8"]

F["<b>BƯỚC 5: Quyết định</b><br/><br/>
• Nếu min_distance < 0.8: Trả về tên người tương ứng<br/>
• Ngược lại: Trả về 'Unknown'"]

G["OUTPUT<br/><b>Bounding box + Tên người + Khoảng cách</b>"]

A --> B
B --> C
C --> D
D --> E
E --> F
F --> G

end

classDef input fill:#2348A5,color:#ffffff,stroke:#1B3D91,stroke-width:2px;
classDef process fill:#A65A17,color:#ffffff,stroke:#7A3F0F,stroke-width:2px;
classDef output fill:#5B2BB5,color:#ffffff,stroke:#47208F,stroke-width:2px;

class A input
class B,C,D,E,F process
class G output

style MAIN fill:#F7F7F7,stroke:#666666,stroke-width:2px
