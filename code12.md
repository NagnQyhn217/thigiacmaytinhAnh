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

flowchart LR

subgraph MAIN["<b>HÌNH 3.2. KẾT QUẢ THEO DÕI ĐỐI TƯỢNG VỚI DeepSORT</b>"]
direction LR

    %% FRAME 1
    subgraph F1["<b>FRAME 1</b>"]
    direction TB
        F1_OBJ1["<b>[ID: 1] Người</b><br/>Dist: 2.5m"]
        F1_OBJ2["<b>[ID: 2] Xe máy</b><br/>Dist: 5.0m"]
        F1_OBJ1 ~~~ F1_OBJ2
    end

    %% FRAME 2
    subgraph F2["<b>FRAME 2</b>"]
    direction TB
        F2_OBJ1["<b>[ID: 1] Người</b><br/>Dist: 2.8m"]
        F2_OBJ2["<b>[ID: 2] Xe máy</b><br/>Dist: 4.8m"]
        F2_OBJ1 ~~~ F2_OBJ2
    end

    %% Duy trì ID qua các Frame
    F1_OBJ1 -- "Duy trì ID: 1" --> F2_OBJ1
    F1_OBJ2 -- "Duy trì ID: 2" --> F2_OBJ2

end

classDef bbox fill:#102A12,color:#00FF66,stroke:#00FF66,stroke-width:2px;

class F1_OBJ1,F1_OBJ2,F2_OBJ1,F2_OBJ2 bbox

style MAIN fill:#F7F7F7,stroke:#666666,stroke-width:2px
style F1 fill:#1A1A1A,color:#FFFFFF,stroke:#333333,stroke-width:2px
style F2 fill:#1A1A1A,color:#FFFFFF,stroke:#333333,stroke-width:2px
