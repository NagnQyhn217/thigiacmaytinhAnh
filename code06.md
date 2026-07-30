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

flowchart LR

subgraph MAIN["ƯỚC LƯỢNG KHOẢNG CÁCH DỰA TRÊN BOUNDING BOX"]
direction LR

A["INPUT<br/><b>Bounding box đối tượng</b><br/>(x1, y1, x2, y2)<br/><br/>Frame: 640 × 480"]

B["<b>CÔNG THỨC TÍNH KHOẢNG CÁCH</b><br/><br/>
• BoxArea = (x2 − x1) × (y2 − y1)<br/>
• AreaRatio = BoxArea / FrameArea<br/>
• Distance = BaseSize / √AreaRatio<br/>
• Distance = max(0.3, min(8.0, Distance))"]

C["OUTPUT<br/><b>Khoảng cách (m)</b><br/><br/>
• Gần: 0.3 − 2.0m<br/>
• Trung bình: 2.0 − 5.0m<br/>
• Xa: 5.0 − 8.0m"]

A --> B
B --> C

end

classDef input fill:#2348A5,color:#ffffff,stroke:#1B3D91,stroke-width:2px;
classDef process fill:#A65A17,color:#ffffff,stroke:#7A3F0F,stroke-width:2px;
classDef output fill:#5B2BB5,color:#ffffff,stroke:#47208F,stroke-width:2px;

class A input
class B process
class C output

style MAIN fill:#F7F7F7,stroke:#666666,stroke-width:2px
