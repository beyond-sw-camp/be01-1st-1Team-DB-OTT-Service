
전승민, 박민성, 김정민, 이경민

 [PLAYDATA] 한화시스템 BEYOND SW캠프








 프로젝트 소개
 =============
OTT 서비스의 구성.
OTT 서비스에 가입한 회원들의 결제와 영화 정보 그리고 제일 중요한 컨텐츠에 대한 정보를 제공한다.
OTT 서비스를 사용하면서 높은 시청률을 보유한 컨텐츠들에 대한 정보를 추가한다.


프로젝트 배경
========
요즘은 TV를 시청하는 경우보다 OTT 서비스를 이용하여 컨텐츠를 시청하거나, 유튜브 등의 매체를 사용하여 여가시간을 보내는 경우가 많다. 최근 OTT 서비스들이 비약적으로 발전함에 따라, 우리가 잘쓰고 있는 서비스에서 우리가 서비스를 이용하면서 아쉬웠던 부분들을 추가하고 싶어졌다.

프로젝트 시나리오 (요구사항 분석)
======


>OTT 서비스 회원정보
1. 아이디
2. 비밀번호
3. 구독여부
     
>선택사항
1. 선호하는 컨텐츠 타입
2. 선호하는 장르
3. 성별
4. 나이
5. 국가
    
>시청정보
1. 영화 이름
2. 마지막 시청 지점
3. 시청 완료 여부
4. 컨텐츠 타입

>결제정보
1. 아이디
2. 이름
3. 카드번호
4. 카드사
5. 휴대폰 번호
    
>은행
1. 휴대폰 번호
2. 카드 번호
3. 결제 확인
4. 카드사
5. 이름

>영화
1. 영화 이름
2. 영화 장르
3. 영화 감독
4. 영화 제작 나라
5. 영화 평점
6. 영화 러닝타임
7. 영화 개봉일
     
>신규 컨텐츠
1. 컨텐츠 타입
2. 장르
3. 컨텐츠 업로드 날짜
4. 컨텐츠 이름

>시청률
1. 컨텐츠 타입
2. 드라마 이름
3. 제작 나라
4. 국내 시청률
5. 해외 시청률
6. 드라마 장르





System Architecture
======
```
CREATE TABLE `Payment_info` (
	`Phone_num`	int	NULL,
	`id`	varchar(10)	NULL,
	`name`	varchar(10)	NULL,
	`card_num`	int	NULL,
	`card_cmp`	Varchar(10)	NULL
);

CREATE TABLE `User_info` (
	`id`	varchar(10)	NULL,
	`pwd`	varchar(20)	NULL,
	`sub`	smallint(1)	NOT NULL
);

CREATE TABLE `selected_Options table` (
	`id`	varchar(10)	NULL,
	`preferred_category`	varchar(10)	NULL,
	`preferred_genre`	varchar(10)	NULL,
	`gender`	smallint	NULL,
	`age`	int	NULL,
	`nation`	varchar(5)	NOT NULL
);

CREATE TABLE `Bank` (
	`Phone_num`	int	NULL,
	`card_num`	int	NULL,
	`Field`	smallint	NULL,
	`card_cmp`	varchar(10)	NOT NULL,
	`name`	varchar(10)	NOT NULL
);

CREATE TABLE `Drama rating` (
	`d_name`	varchar(10)	NULL,
	`d_nation`	varchar(10)	NULL,
	`rating`	int	NULL,
	`f_rating`	int	NULL,
	`d_genre`	varchar(10)	NULL
);

CREATE TABLE `New` (
	`c_category`	varchar(10)	NULL,
	`c_genre`	varchar(10)	NULL,
	`c_uploaddate`	date	NULL,
	`c_name`	varchar(10)	NULL
);

CREATE TABLE `record` (
	`id`	varchar(10)	NULL,
	`category`	varchar(10)	NULL,
	`title`	varchar(10)	NULL,
	`latest_point`	int	NULL,
	`hitLastPoint`	smallint	NULL
);

CREATE TABLE `Movie` (
	`m_name`	varchar(10)	NOT NULL	COMMENT '영화이름',
	`m_genre`	varchar(10)	NOT NULL	COMMENT '영화 장르',
	`m_director`	varchar(10)	NOT NULL	COMMENT '영화감독',
	`m_nation`	varchar(20)	NOT NULL	COMMENT '영화 제작 국가',
	`m_rate`	int	NOT NULL	COMMENT '영화 평점',
	`m_run`	time	NOT NULL	COMMENT '영화 러닝 타임',
	`m_open`	date	NOT NULL	COMMENT '영화 개봉일'
);

CREATE TABLE `mov_accu` (
	`p_id`	VARCHAR(10)	NULL,
	`genre`	VARCHAR(10)	NULL
);

ALTER TABLE `Payment_info` ADD CONSTRAINT `PK_PAYMENT_INFO` PRIMARY KEY (
	`Phone_num`,
	`id`
);

ALTER TABLE `User_info` ADD CONSTRAINT `PK_USER_INFO` PRIMARY KEY (
	`id`
);

ALTER TABLE `selected_Options table` ADD CONSTRAINT `PK_SELECTED_OPTIONS TABLE` PRIMARY KEY (
	`id`
);

ALTER TABLE `Bank` ADD CONSTRAINT `PK_BANK` PRIMARY KEY (
	`Phone_num`
);

ALTER TABLE `New` ADD CONSTRAINT `PK_NEW` PRIMARY KEY (
	`c_category`
);

ALTER TABLE `record` ADD CONSTRAINT `PK_RECORD` PRIMARY KEY (
	`id`
);

ALTER TABLE `Payment_info` ADD CONSTRAINT `FK_User_info_TO_Payment_info_1` FOREIGN KEY (
	`id`
)
REFERENCES `User_info` (
	`id`
);

ALTER TABLE `selected_Options table` ADD CONSTRAINT `FK_User_info_TO_selected_Options table_1` FOREIGN KEY (
	`id`
)
REFERENCES `User_info` (
	`id`
);

ALTER TABLE `Bank` ADD CONSTRAINT `FK_Payment_info_TO_Bank_1` FOREIGN KEY (
	`Phone_num`
)
REFERENCES `Payment_info` (
	`Phone_num`
);

ALTER TABLE `record` ADD CONSTRAINT `FK_User_info_TO_record_1` FOREIGN KEY (
	`id`
)
REFERENCES `User_info` (
	`id`
);
```


Trigger 응용
=======


```
CREATE or replace TABLE mov_accu
(	
	p_id VARCHAR(10) PRIMARY key,
	genre VARCHAR(10) NOT null
);

DROP TABLE if EXISTS selected_Options;
CREATE TABLE selected_Options (
	id	varchar(10)	NULL,
	preferred_category	varchar(10)	NULL,
	preferred_genre	varchar(10)	NULL,
	gender	varchar(10)	NULL,
	age	int	NULL,
	nation	varchar(5)	NOT NULL
);

INSERT INTO selected_Options VALUES('TDS', '영화',  '액션', '남자', 26, '한국');
DROP TRIGGER if EXISTS TRIGGER_in;

SELECT * FROM selected_Options;
SELECT * FROM mov_accu;

-- -------------------------------------------------insert

delimiter $$
CREATE TRIGGER TRIGGER_in
AFTER INSERT
ON selected_Options
FOR EACH ROW -- 각 행에서 모두 실행
BEGIN
	INSERT INTO mov_accu
		VALUES( new.id, new.preferred_genre );
--	SELECT 영화장르, COUNT(*) 'CG' FROM  mov_accu
--		GROUP BY 영화장르
--		HAVING CG DESC ; 
END $$
delimiter ;

-- ---------------------------------------------- delete

delimiter $$
CREATE TRIGGER TRIGGER_del
AFTER DELETE 
ON selected_Options
FOR EACH ROW -- 각 행에서 모두 실행
BEGIN
   DELETE FROM mov_accu WHERE p_id = OLD.id;
END $$
delimiter ;

SELECT * FROM selected_Options;
SELECT * FROM mov_accu;
INSERT INTO selected_Options VALUES('TDS', '영화',  '액션', '남자', 26, '한국');
DELETE FROM selected_Options WHERE id = 'TWC';

-- ----------------------------------------------------- update

DROP TRIGGER if EXISTS trigger_upd;
delimiter $$

CREATE TRIGGER trigger_upd
AFTER UPDATE
ON selected_Options
FOR EACH ROW
BEGIN
    -- 실행 구문
    UPDATE mov_accu
    SET genre = NEW.preferred_genre
    WHERE p_id = NEW.id;
END $$

delimiter ;



SELECT * FROM selected_Options;
SELECT * FROM mov_accu;
UPDATE selected_Options SET preferred_genre = '로맨스' WHERE id = 'TDS'; 
```

Entity-Relationship Diagram
============



![OTTERD](https://github.com/beyond-sw-camp/be01-1st-1Team-DB-OTT-Service/assets/125641153/6ac56896-4833-42c9-b499-831d942f119d)





Entity-Relationship model
===========



![ER fixfix](https://github.com/beyond-sw-camp/be01-1st-1Team-DB-OTT-Service/assets/125641153/afe832e1-01be-4ca8-b9ab-0ed9333a801f)





old
==========
<img src="https://user-images.githubusercontent.com/51365114/119627750-716f3100-be47-11eb-8e83-686b23c2c161.png  width="200" height="400"/>

![IMG_6115](https://github.com/beyond-sw-camp/be01-1st-1Team-DB-OTT-Service/assets/125641153/646ba48c-387c-478d-960a-b4ccd8a57a6e ){: width="30%" height="30%"}

![IMG_6114](https://github.com/beyond-sw-camp/be01-1st-1Team-DB-OTT-Service/assets/125641153/ab0e5d24-449a-4df2-bc24-84375c48c035){: width="30%" height="30%"}

![IMG_6113](https://github.com/beyond-sw-camp/be01-1st-1Team-DB-OTT-Service/assets/125641153/e3f34367-d528-4255-b2c4-7e2f12ee988a){: width="30%" height="30%"}

