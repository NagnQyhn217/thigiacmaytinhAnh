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

subgraph FRAME["<b>HÌNH 3.1. KẾT QUẢ PHÁT HIỆN VẬT THỂ TỪ YOLOv8</b>"]
direction TB

    subgraph ROW1[" "]
    direction LR
        BOX1["<b>Người</b><br/>Conf: 0.92<br/>Dist: 2.5m"]
        SPACE1[" "]
        BOX2["<b>Xe máy</b><br/>Conf: 0.85<br/>Dist: 5.0m"]
    end

    subgraph ROW2[" "]
    direction LR
        BOX3["<b>Ghế</b><br/>Conf: 0.78<br/>Dist: 1.5m"]
    end

    ROW1 ~~~ ROW2
end

classDef bbox fill:#102A12,color:#00FF66,stroke:#00FF66,stroke-width:2px;
classDef invisible fill:transparent,stroke:none;

class BOX1,BOX2,BOX3 bbox
class SPACE1 invisible

style FRAME fill:#1A1A1A,color:#FFFFFF,stroke:#333333,stroke-width:3px
style ROW1 fill:transparent,stroke:none
style ROW2 fill:transparent,stroke:none
