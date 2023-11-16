
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
{
OTT 서비스 회원정보
  1. 아이디
  2. 비밀번호
  3. 구독여부
     
     선택사항
       1. 선호하는 컨텐츠 타입
       2. 선호하는 장르
       3. 성별
       4. 나이
       5. 국가
    
     시청정보
       1. 영화 이름
       2. 마지막 시청 지점
       3. 시청 완료 여부
       4. 컨텐츠 타입
}

}
  결제정보
    1. 아이디
    2. 이름
    3. 카드번호
    4. 카드사
    5. 휴대폰 번호
  은행
    1. 휴대폰 번호
    2. 카드 번호
    3. 결제 확인
    4. 카드사
    5. 이름
}

{
영화
  1. 영화 이름
  2. 영화 장르
  3. 영화 감독
  4. 영화 제작 나라
  5. 영화 평점
  6. 영화 러닝타임
  7. 영화 개봉일
     
신규 컨텐츠
  1. 컨텐츠 타입
  2. 장르
  3. 컨텐츠 업로드 날짜
  4. 컨텐츠 이름

시청률
  1. 컨텐츠 타입
  2. 드라마 이름
  3. 제작 나라
  4. 국내 시청률
  5. 해외 시청률
  6. 드라마 장르
}




System Architecture
======

 CREATE TABLE `Payment_info` (
	`Phone_num`	int	NULL,
	`id`	varchar(10)	NULL,
	`name`	varchar(10)	NULL,
	`card_num`	int	NULL,
	`card_cmp`	Varchar(10)	NULL
);

CREATE TABLE `Movie` (
	`c_category`	varchar(10)	NULL,
	`m_name`	varchar(10)	NOT NULL	COMMENT '영화이름',
	`m_genre`	varchar(10)	NOT NULL	COMMENT '영화 장르',
	`m_director`	varchar(10)	NOT NULL	COMMENT '영화감독',
	`m_nation`	varchar(20)	NOT NULL	COMMENT '영화 제작 국가',
	`m_rate`	int	NOT NULL	COMMENT '영화 평점',
	`m_run`	time	NOT NULL	COMMENT '영화 러닝 타임',
	`m_open`	date	NOT NULL	COMMENT '영화 개봉일'
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
	`c_category`	varchar(10)	NULL,
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

ALTER TABLE `Payment_info` ADD CONSTRAINT `PK_PAYMENT_INFO` PRIMARY KEY (
	`Phone_num`,
	`id`
);

ALTER TABLE `Movie` ADD CONSTRAINT `PK_MOVIE` PRIMARY KEY (
	`c_category`
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

ALTER TABLE `Drama rating` ADD CONSTRAINT `PK_DRAMA RATING` PRIMARY KEY (
	`c_category`
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

ALTER TABLE `Movie` ADD CONSTRAINT `FK_New_TO_Movie_1` FOREIGN KEY (
	`c_category`
)
REFERENCES `New` (
	`c_category`
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

ALTER TABLE `Drama rating` ADD CONSTRAINT `FK_New_TO_Drama rating_1` FOREIGN KEY (
	`c_category`
)
REFERENCES `New` (
	`c_category`
);

ALTER TABLE `record` ADD CONSTRAINT `FK_User_info_TO_record_1` FOREIGN KEY (
	`id`
)
REFERENCES `User_info` (
	`id`
);
