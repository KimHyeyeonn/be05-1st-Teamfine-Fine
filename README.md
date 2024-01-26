# be05-1st-Teamfine-Fine

## Team 소개

<div align="center">
  <img src= "https://github.com/KimHyeyeonn/be05-1st-Teamfine-Fine/blob/main/img/header.png"/>
</div>

### 팀명
**`TEAMFINE`**

</br>

### 팀원 소개

|[팀장 장명훈](https://github.com/indoor98)|[팀원 김혜연](https://github.com/KimHyeyeonn)|[팀원 박혜경](https://github.com/BakHyegyeong)|[팀원 전찬우](https://github.com/chanwoo1999)|[팀원 정광수](https://github.com/Jrhkdtn)|


</br>

## 프로젝트 개요

### 프로젝트 시나리오

**[설정 상황]**

소방 정보 종합 제공 사이트는 여러 군데에 흩어져 있는 정보들 중에 실생활에서 알아두면 좋은 정보들을 한 곳에 모아서 Fine이라는 프로젝트 명으로 서비스를 제공하려고 한다. 
</br>

**[요구 사항]**

고객(소방 업계 종사자 혹은 희망자)은 소방 정보 종합 제공 사이트에서 소방 사건 사례, 소방 장비, 제설함, 소방 용수 시설 등 취업 혹은 날씨와 같은 고객들이 필요한 정보를 한 곳에서 제공하고자 한다.

</br>
# 요구 사항 정의

**[메인 페이지]**

1. 사용자는 서울시 내에서 25개의 지역구 중 하나를 선택할 수 있다.
2. 사용자는 사건, 기관, 장비, 제설함, 제설 도구, 용수 시설 중에서 조회할 정보를 선택할 수 다.

**[사건]**

1. 사용자는 사건의 사건 분류, 출동 일자 정보를 조회할 수 있다.
2. 옵션으로 사건 종류, 날짜, 날씨, 위치, 관련 소방 기관을 사용할 수 있다.

**[주소]**

1. 사용자는 특정 구에서 발생한 사건, 기관, 제설함, 제설 도구, 장비 및 용수 시설 정보를 조회할 수 있다.
2. 사용자는 모든 지역 구별로 사건, 소방 기관, 장비, 용수 시설을 조회할 수 있다.

**[기관]**

1. 사용자는 해당 구의 소방 기관의 주소와 전화번호 정보를 조회할 수 있다.
2. 사용자는 주소와 위치 별로 해당 소방 기관의 전화번호를 조회할 수 있다.

**[장비]**

1. 사용자는 소방 장비의 장비 분류, 구매 일자, 상태 정보를 조회할 수 있다.
2. 사용자는 소방 기관을 기준으로 소방 기관이 소유하고 있는 소방 장비를 조회할 수 있다.

**[제설함]**

1. 사용자는 주소를 통해 제설함의 정보를 조회할 수 있다.

**[제설 도구]**

1. 사용자는 제설 도구의 도구 유형, 구매 일자를 조회할 수 있다.
2. 사용자는 제설함 번호로 제설 도구를 조회할 수 있다.

**[용수 시설]**

1. 사용자는 소방 용수 시설의 사용 기한을 조회할 수 있다.
2. 사용자는 주소를 통해 용수 시설의 정보를 조회할 수 있다.

</br>
# **시스템 기능 명세**

1. **사용자 정보 관리**
    - 시스템은 사용자의 이름, 이메일, 비밀번호를 관리한다.
2. **사건 정보 제공**
    - 시스템은 사건의 사건 분류, 사건 일자, 날씨를 관리해 사용자에게 정보를 제공한다.
3. **소방 기관 정보 제공**
    - 시스템은 소방 기관의 주소, 전화번호 정보를 사용자에게 제공한다.
4. **소방 장비 정보 제공**
    - 시스템은 소방 장비의 장비 유형, 구매 일자, 상태, 소방 기관 정보를 사용자에게 제공한다.
5. **제설함 정보 제공**
    - 시스템은 제설함의 주소 정보를 사용자에게 제공한다.
6. **제설 도구 정보 제공**
    - 시스템은 제설 도구의 도구 종류, 구매 일자, 주소 정보를 사용자에게 제공한다.
7. **소방 용수 시설 정보 제공**
    - 시스템은 소방 용수 시설의 주소와 용량 정보를 사용자에게 제공한다.

</br>
# E-R Diagram

</br>
# ERD
</br>
# TEST CASE 명세서

### TEST CASE
## 정보조회
## 지역

- 사용자는 모든 지역구 별로 사건, 소방 기관, 장비, 용수 시설 조회할 수 있다.
    
    ```sql
    -- 성북구에서 발생한 사건, 기관, 제설함, 제설도구, 장비 및 용수시설 정보 조회
    SELECT
        e.id AS 'Event ID',
        e.event_case AS 'Event Case',
        a.district AS 'District',
        fa.id AS 'Fire Agency ID',
        fa.phone_number AS 'Phone Number',
        srb.id AS 'Snow Removal Box ID',
        srt.id AS 'Snow Removal Tool ID',
        srt.TYPE AS 'Tool Type',
        fe.id AS 'Equipment ID',
        fe.type AS 'Equipment Type',
        fw.id AS 'Firefighting Water ID',
        fw.last_inspection AS 'Last Inspection Date'
    FROM
        EVENT e
    INNER JOIN address a ON e.address_id = a.id
    LEFT JOIN fire_agency fa ON a.id = fa.address_id
    LEFT JOIN snow_removal_box srb ON a.id = srb.address_id
    LEFT JOIN snow_removal_tool srt ON srb.id = srt.snow_removal_box_id
    LEFT JOIN firefighting_equipment fe ON fa.id = fe.fire_agency_id
    LEFT JOIN firefighting_water fw ON a.id = fw.address_id
    WHERE
        a.district = '성북구'
    ```
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e6bb4003-6569-4926-984d-f00d6dbe2dea/a0c5d741-0de3-44f7-a0b9-80c629f6b2b3/Untitled.png)
    
- 사용자는 특정 구에서 발생한 사건, 기관, 제설함, 제설 도구, 장비 및 용수시설 정보를 조회할 수 있다
    
    ```sql
    SELECT
        a.district AS 'District',
        e.event_case AS 'Event Case',
        fa.phone_number AS 'Fire Agency Phone Number',
        fe.type AS 'Equipment Type',
        fw.last_inspection AS 'Last Inspection Date'
    FROM
        address a
    LEFT JOIN EVENT e ON a.id = e.address_id
    LEFT JOIN fire_agency fa ON a.id = fa.address_id
    LEFT JOIN firefighting_equipment fe ON fa.id = fe.fire_agency_id
    LEFT JOIN firefighting_water fw ON a.id = fw.address_id
    ORDER BY
        a.district; -- 지역구별로 정렬
    ```
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e6bb4003-6569-4926-984d-f00d6dbe2dea/5376b115-e549-4272-a8a3-1b013ffbaa55/Untitled.png)
    

## 사건

- 사용자는 사건의 사건 분류, 출동 일자 정보를 조회할 수 있다.
    
    ```sql
    SELECT event_case, dispatch_date
    FROM EVENT;
    ```
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e6bb4003-6569-4926-984d-f00d6dbe2dea/9589b4ea-4617-4b2a-93e2-d1765663873b/Untitled.png)
    
- 사용자는 사건 정보를 사건 분류, 출동 일자, 날씨, 소방 기관을 기준으로 조회할 수 있다.
    
    ```sql
    SELECT
        e.event_case AS 'Event Case',
        e.dispatch_date AS 'Dispatch Date',
        w.date AS 'Weather Date',
        w.temperature AS 'Temperature',
        w.humidity AS 'Humidity',
        w.wind_volume AS 'Wind Volume',
        w.wind_direction AS 'Wind Direction',
        fa.phone_number AS 'Fire Agency Phone Number'
    FROM
        EVENT e
    INNER JOIN weather w ON e.weather_id = w.id
    INNER JOIN address a ON e.address_id = a.id
    LEFT JOIN fire_agency fa ON a.id = fa.address_id;
    ```
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e6bb4003-6569-4926-984d-f00d6dbe2dea/d372eec4-0167-4015-b440-92d90aa8846e/Untitled.png)
    

## 소방 기관

- 사용자는 해당 구의 소방 기관의 주소와 전화번호 정보를 조회할 수 있다.
    
    ```sql
    SELECT fa.phone_number AS 'Fire Station Phone Number'
    FROM fire_agency fa
    JOIN address a ON fa.address_id = a.id
    WHERE a.district = '동작구';
    ```
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e6bb4003-6569-4926-984d-f00d6dbe2dea/60c36315-ed4e-4b5d-96fb-138ec0dc3331/Untitled.png)
    
- 사용자는 주소와 위치 별로 해당 소방 기관의 전화번호를 조회할 수 있다.
    
    ```sql
    SELECT
        a.district AS 'District',
        a.street_name AS 'Street Name',
        a.detail AS 'Detail',
        a.zip_code AS 'Zip Code',
        fa.phone_number AS 'Phone Number'
    FROM
        address a
    LEFT JOIN
        fire_agency fa ON a.id = fa.address_id;
    ```
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e6bb4003-6569-4926-984d-f00d6dbe2dea/fb5634ad-5acf-4b0a-83f3-2b79d0691c4f/Untitled.png)
    

## 소방 장비

- 사용자는 소방 장비의 장비 분류, 구매 일자, 상태 정보를 조회할 수 있다.
    
    ```sql
    SELECT type, purchase_date, status
    FROM firefighting_equipment ;
    ```
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e6bb4003-6569-4926-984d-f00d6dbe2dea/e2a65d67-30fd-4fae-8a16-2455fdd3a4e1/Untitled.png)
    
- 사용자는 특정 구의 소방 기관이 소유하고 있는 장비랑 소방 기관 번호를 알 수 있다.
    
    ```sql
    SELECT fe.type, fe.purchase_date, fe.status, fa.phone_number
    FROM firefighting_equipment fe
    JOIN fire_agency fa ON fe.fire_agency_id = fa.id
    JOIN address a ON fa.address_id = a.id
    WHERE a.district = '관악구';
    ```
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e6bb4003-6569-4926-984d-f00d6dbe2dea/579f447a-7bd2-4fa5-b8ef-6e7a25c69ab8/Untitled.png)
    

## 제설함

- 사용자는 주소를 통해 제설함의 정보를 조회할 수 있다.
    
    ```sql
    SELECT sr.address_id, a.district, a.street_name, a.detail, sr.id AS snow_removal_box_id
    FROM snow_removal_box sr
    JOIN address a ON sr.address_id = a.id;
    ```
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e6bb4003-6569-4926-984d-f00d6dbe2dea/99a39c1c-a9ed-4e8d-abc4-385bedca28e6/Untitled.png)
    

## 제설 도구

- 사용자는 제설 도구의 도구 유형, 구매 일자를 조회할 수 있다
    
    ```sql
    SELECT TYPE, purchase_date
    FROM snow_removal_tool;
    ```
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e6bb4003-6569-4926-984d-f00d6dbe2dea/75288d56-9191-44a8-b850-3a40445dc3ad/Untitled.png)
    
- 사용자는 제설함 번호로 제설 도구의 정보를 조회할 수 있다.
    
    ```sql
    SELECT srt.*
    FROM snow_removal_box srb
    JOIN snow_removal_tool srt ON srb.id = srt.snow_removal_box_id
    WHERE srb.id = '3';
    ```
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e6bb4003-6569-4926-984d-f00d6dbe2dea/71b005a7-5068-45bb-9637-0d4b279e840a/Untitled.png)
    

## 용수 시설

- 사용자는 소방용수시설의 사용 기한을 조회할 수 있다.
    
    ```sql
    SELECT last_inspection
    FROM firefighting_water;
    ```
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e6bb4003-6569-4926-984d-f00d6dbe2dea/89544a90-292d-445b-8901-5d65f5605794/Untitled.png)
    
- 사용자는 특정 주소의 소방용수시설 사용 기한을 조회할 수 있다.
    
    ```sql
    SELECT fw.address_id, a.district, a.street_name, a.detail, fw.last_inspection
    FROM firefighting_water fw
    JOIN address a ON fw.address_id = a.id
    WHERE a.district = '강남구' AND a.street_name = '테헤란로'
    ORDER BY fw.last_inspection DESC;
    ```
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e6bb4003-6569-4926-984d-f00d6dbe2dea/ed504e7d-3044-40dc-a5a7-a6bf39a5d326/Untitled.png)

- 사용자는 최근에 사용한 소방용수시설의 사용 기한을 조회할 수 있다.
    
    ```sql
    SELECT fw.address_id, a.district, a.street_name, a.detail, fw.last_inspection
    FROM firefighting_water fw
    JOIN address a ON fw.address_id = a.id
    ORDER BY fw.last_inspection DESC
    LIMIT 1;
    ```
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/e6bb4003-6569-4926-984d-f00d6dbe2dea/367c8831-8e82-44ac-b47d-17ce1390b779/Untitled.png)