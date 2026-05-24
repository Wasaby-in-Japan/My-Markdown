# 設計書サンプル

<font color="Red"> ※このファイルは設計書のサンプルとしてmermaidを紹介するために作成されたものです。このファイル内で作成した図・仕様などは実在するシステムとは一切関係ありません</font>

* アーキテクチャ図
システムアーキテクチャを説明するための図です。
基本的な3層アーキテクチャを採用した場合の図をサンプルとして掲示します。
  
```mermaid

graph TB
    subgraph "クライアント層"
        Web[Webブラウザ]
    end

    subgraph "アプリケーション層"
        LB[LoadBarancer]
        API1[API Servre 1]
        API2[API Servre 2]
        API3[API Servre 3]
     end

    subgraph "データ層"
        Primary[Primaly DB]
        Replica[Replica DB]
        Cache[Cahce DB]
    end

Web --> LB
LB --> API1
LB --> API2
LB --> API3
API1 --> Primary
API2 --> Primary
API3 --> Primary
Primary --> Replica
API1 --> Cache
API2 --> Cache
API3 --> Cache
```

* ER図
DBの論理設計に用いる図です。
スキーマごとの属性と、属性間のリレーションを説明します。

```mermaid
erDiagram

    users ||--o{ Order :"ユーザーは多数の注文を持つ"

    Order ||--o{ Statement : "注文には明細が紐づく"

    Statement ||--o{ items : "明細には商品が記載される"

    users{
    bigint id PK
    String name "ユーザー名"
    timestamp create
    timestamp delete
    }

    Order{
    bigint id PK
    bigint custmerid FK
    timestamp order_date
    timestamp deliverly_date
    }

    Statement{
    bigint Order_id FK
    bigint State_number
    bigint item_id FK
    }

    items{
    bigint id PK
    String name "商品名"
    bigint price "価格"
    }

```

* クラス図
オブジェクト指向プログラミングを行う際に各クラスの定義とそのポリモーフィズムを定義できます。(詳細設計での使用を想定)

```mermaid
classDiagram
    class human{
    -int age
    -String name
    -あいさつ()
    -あるく()
    }

    class student{
    -int 学年
    -int クラス
    -学ぶ()
    }

    class teacher{
    -int 担任クラス
    -String 担当教科
    -教える()
    }

    class 校長{
    -String 学校
    -給食の毒見()
    }

    human <|-- student
    human <|-- teacher
    teacher <|-- 校長
```

*シーケンス図
処理の流れを整理するシーケンス図です。

```mermaid
sequenceDiagram
 participant クライアント
 participant Webサーバー
 participant APサーバー

クライアント->>+Webサーバー: リクエスト 
Webサーバー->>-クライアント: レスポンス
クライアント->>+Webサーバー: 計算要求
Webサーバー->>-APサーバー:要求転送
loop 計算処理
APサーバー->>APサーバー:計算実行
end
APサーバー-->>+Webサーバー:結果送信
Webサーバー-->>-クライアント:結果送信

```

* 円グラフ
UMLの他、円グラフを書きこともできます。

```mermaid
pie showData
 title mermaidについてどう思うか
 "非常に便利だ" : 40
 "ぜひ採用したい" : 30
 "活用事例を知りたい" : 20
 "つかExcelで良くね?(笑)" :10
```
