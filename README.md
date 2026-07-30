# thigiacmaytinhAnh

```mermaid
%%{init:{
'theme':'base',
'themeVariables':{
'background':'#FFFFFF',
'primaryTextColor':'#333333',
'fontFamily':'Times New Roman',
'fontSize':'14px',
'lineColor':'#4A5568'
},
'flowchart':{
'nodeSpacing': 35,
'rankSpacing': 35
}
}}%%

flowchart TB

subgraph FRAME["<b>KẾT QUẢ NHẬN DIỆN KHUÔN MẶT</b>"]
direction TB

    BOX1["<b>Person_A</b><br/>Conf: 0.75"]
    BOX2["<b>Unknown</b><br/>Conf: 0.95"]
    
    %% Tạo khoảng cách vô hình giữa 2 ô
    BOX1 ~~~ BOX2

end

classDef bbox fill:#2D3748,color:#48BB78,stroke:#48BB78,stroke-width:2px;

class BOX1,BOX2 bbox

style FRAME fill:#EDF2F7,color:#1A202C,stroke:#CBD5E0,stroke-width:2px
