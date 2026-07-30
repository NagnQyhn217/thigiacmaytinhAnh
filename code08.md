```mermaid
%%{init:{
'theme':'base',
'themeVariables':{
'background':'#FFFFFF',
'primaryTextColor':'#222222',
'fontFamily':'Times New Roman',
'fontSize':'15px',
'lineColor':'#555555'
}
}}%%

flowchart LR

subgraph MAIN["QUY TRÌNH TTS VỚI EDGE-TTS"]
direction LR

A["INPUT<br/><b>Văn bản (Text)</b><br/><br/><i>'Có người phía trước,<br/>khoảng cách 2.5m'</i>"]

B["<b>BƯỚC 1 & 2: KHỞI TẠO & LƯU</b><br/><br/>• Kết nối Edge-TTS:<br/><code>edge_tts.Communicate()</code><br/>• Lưu file tạm <code>speech.mp3</code>:<br/><code>await communicate.save()</code>"]

C["<b>BƯỚC 3 & 4: PHÁT & DỌN DẸP</b><br/><br/>• Phát qua loa/headphone:<br/><code>playsound(filename)</code><br/>• Xóa file âm thanh tạm:<br/><code>os.remove(filename)</code>"]

D["OUTPUT<br/><b>Âm thanh thông báo</b><br/><br/>Phát ra loa/headphone"]

A --> B
B --> C
C --> D

end

classDef input fill:#2348A5,color:#ffffff,stroke:#1B3D91,stroke-width:2px;
classDef process fill:#A65A17,color:#ffffff,stroke:#7A3F0F,stroke-width:2px;
classDef output fill:#5B2BB5,color:#ffffff,stroke:#47208F,stroke-width:2px;

class A input
class B,C process
class D output

style MAIN fill:#F7F7F7,stroke:#666666,stroke-width:2px
