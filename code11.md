```mermaid
%%{init:{
'theme':'base',
'themeVariables':{
'background':'#FFFFFF',
'primaryTextColor':'#222222',
'fontFamily':'Times New Roman',
'fontSize':'14px',
'lineColor':'#555555'
},
'flowchart':{
'nodeSpacing': 10,
'rankSpacing': 10
}
}}%%

flowchart TB

subgraph FRAME["<b>HÌNH 3.1. KẾT QUẢ PHÁT HIỆN VẬT THỂ TỪ YOLOv8</b>"]
direction TB

    subgraph ROW1[" "]
    direction LR
        BOX1["<b>Người</b><br/>Conf: 0.92 | Dist: 2.5m"]
        BOX2["<b>Xe máy</b><br/>Conf: 0.85 | Dist: 5.0m"]
    end

    subgraph ROW2[" "]
    direction LR
        BOX3["<b>Ghế</b><br/>Conf: 0.78 | Dist: 1.5m"]
    end

    ROW1 ~~~ ROW2
end

classDef bbox fill:#102A12,color:#00FF66,stroke:#00FF66,stroke-width:2px;

class BOX1,BOX2,BOX3 bbox

style FRAME fill:#1A1A1A,color:#FFFFFF,stroke:#333333,stroke-width:2px
style ROW1 fill:transparent,stroke:none
style ROW2 fill:transparent,stroke:none
