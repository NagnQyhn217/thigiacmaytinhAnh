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

subgraph MAIN["QUY TRÌNH TTS VỚI EDGE-TTS"]
direction TB

A["INPUT<br/><b>Văn bản cần chuyển đổi (Text)</b><br/><br/>Ví dụ: 'Có người phía trước, khoảng cách 2.5 mét'"]

B["<b>BƯỚC 1. Tạo kết nối với dịch vụ Edge-TTS</b><br/><br/>
communicate = edge_tts.Communicate(text=text, voice=VOICE)"]

C["<b>BƯỚC 2. Tạo file âm thanh tạm thời</b><br/><br/>
await communicate.save(filename)<br/>
filename = tempfile.gettempdir() + 'speech.mp3'"]

D["<b>BƯỚC 3. Phát âm thanh</b><br/><br/>
playsound(filename)<br/>
• Phát âm thanh thông qua loa/headphone"]

E["<b>BƯỚC 4. Xóa file tạm thời</b><br/><br/>
os.remove(filename)"]

F["OUTPUT<br/><b>Âm thanh phát ra thông qua loa/headphone</b>"]

A --> B
B --> C
C --> D
D --> E
E --> F

end

classDef input fill:#2348A5,color:#ffffff,stroke:#1B3D91,stroke-width:2px;
classDef process fill:#A65A17,color:#ffffff,stroke:#7A3F0F,stroke-width:2px;
classDef output fill:#5B2BB5,color:#ffffff,stroke:#47208F,stroke-width:2px;

class A input
class B,C,D,E process
class F output

style MAIN fill:#F7F7F7,stroke:#666666,stroke-width:2px
