**1. データ構造**

- **全体構造**: GeoJSON形式のFeatureCollection。
- **Feature**: 各路線を1つのFeatureとして表現。
    - **geometry**: LineString型。路線の経路を表す座標列。
        - 座標列の始点と終点は、それぞれ始発停留所と終着停留所の座標に一致する。
        - 座標列は、OpenStreetMapの道路ネットワークに沿っている必要がある。
    - **properties**: 路線と停留所の属性情報。
        - `route_id`: 路線ID（文字列）。
        - `route_name`: 路線名（文字列）。
        - `color`: 路線の色分け（16進数カラーコード）。
        - `metrics`: 路線全体の指標（オブジェクト）。
            - 年月（YYYYMM）をキーとしたネスト構造。
            - `emissions`: 路線全体のCO2排出量（数値）。
            - `od_distance`: OD距離（オブジェクト）。
                - `car`: 車移動距離（数値）。
                - `motorbike`: バイク移動距離（数値）。
                - `train`: 電車移動距離（数値）。
                - `non_emission`: 徒歩・自転車移動距離（数値）。
            - `environmental_value`: 環境価値（オブジェクト）。
                - `car`: 車の環境価値（数値）。
                - `motorbike`: バイクの環境価値（数値）。
                - `train`: 電車の環境価値（数値）。
                - `non_emission`: 徒歩・自転車の環境価値（数値）。
        - `stops`: 停留所の配列。
            - `stop_id`: 停留所ID（文字列）。
            - `stop_name`: 停留所名（文字列）。
            - `coordinates`: 停留所の座標（[経度, 緯度]）。
            - `metrics`: 停留所ごとの指標（オブジェクト）。
                - 年月（YYYYMM）をキーとしたネスト構造。
                - `passengers_on`: 乗車した人数（数値）。
                - `passengers_off`: 降車した人数（数値）。
                - `revenue`: 運賃収入（数値）。
                - `cost`: コスト（数値）。
                - `average_passenger_density`: 平均乗車密度（数値）。
                - `emissions`: CO2排出量（数値）。始発停留所は0、それ以外は前の停留所からの排出量。

**2. データ作成ルール**

- Linestringの座標列は、始発停留所から終着停留所まで、順番に停留所の座標を結ぶように作成する。
- Linestringの座標列は、OpenStreetMapの道路ネットワークに沿っている必要がある。
- 各停留所の`emissions`は、前の停留所からの距離に固定係数をかけた値とする。
- 路線全体の`emissions`は、各停留所の`emissions`の合計値とする。

**3. 属性情報**

- `color`: 路線ごとに異なる色を指定する。
- `emissions`: CO2排出量を表す。単位はkgとする。
- `od_distance`: 各交通手段のOD距離の合計値を表す。単位はkmとする。
- `environmental_value`: 各交通手段の環境価値を表す。単位は円とする。
- `revenue`: 運賃収入を表す。単位は円とする。
- `cost`: コストを表す。単位は円とする。
- `average_passenger_density`: 平均乗車密度を表す。単位は人/平方メートルとする。