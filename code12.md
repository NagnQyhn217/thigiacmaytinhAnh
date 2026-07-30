```mermaid
%%{init:{
'theme':'base',
'themeVariables':{
'background':'#FFFFFF',
'primaryTextColor':'#333333',
'fontFamily':'Times New Roman',
'fontSize':'14px',
'lineColor':'#4A5568',
'tertiaryColor':'#E2E8F0'
},
'flowchart':{
'nodeSpacing': 35,
'rankSpacing': 45
}
}}%%

flowchart LR

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

    %% Nối trực tiếp
    F1_OBJ1 -- "ID: 1" --> F2_OBJ1
    F1_OBJ2 -- "ID: 2" --> F2_OBJ2

classDef bbox fill:#2D3748,color:#48BB78,stroke:#48BB78,stroke-width:2px;

class F1_OBJ1,F1_OBJ2,F2_OBJ1,F2_OBJ2 bbox

style F1 fill:#EDF2F7,color:#1A202C,stroke:#CBD5E0,stroke-width:2px
style F2 fill:#EDF2F7,color:#1A202C,stroke:#CBD5E0,stroke-width:2px
