# Inventory Manager

즐거운 자재 관리 세상 우리 함께 만들어보아요.

# Pre-install
ApacheV2
TomcatV9(v7~)

# Website


# Database

## 컬럼 정의 관련 

_no 	int(7)   (100만) 	: order_no만 10자리 
_id 	varchar(15)
기타 	varchar(45)
note 	varchar(500)
cnt 	int(11) : 100억 
amt 	DEC(15,0) : 100조  	: 나중에 화폐코드 등 추가 

## table lists

### item
	item_no
	sku
	sku_id	

### order
	order_no
	order_item
	order_no
	seq
### user
	user_no
	user_auth
	user_no
	wh_no
### wh
	wh_no
	wh_item
	wh_no
	item_no

## facts... 

purchase order : 서비스센터가 MR 자재 주문서 작성        transfer order 
sales order : 서비스센터가 고객한테. 출력필요  		견적서 

일부 선불/차후 후불 가능 

## 주문 상태 관련
order_status_cd						<- 사용자 버튼 
01 : 주문      (주문서작성완료) 			<- 주문 
02 : 물품준비중 (접수완료. 재고 확보 전.)	<- 접수
03 : 배송준비중 (재고 확보 완료. 배송요청 전)<- 물품준비완료 
04 : 배송중    (발송완료)				<- 배송요청완료 
05 : 배송완료 							<- 배송완료 

## 권한 관련
- WH_NO
WH_NO 0번 : 전체 
WH_NO 1번 : MR IN IKSAN
WH_NO 2번 : SOMEWHERE
WH_NO 3번 : SOMEWHERE
...

- auth_lvl
S : SUPER ADMINISTRATOR (등록자 무관 CUD 가능)
A : ADMINISTRATOR (등록자 무관 CUD 가능)
C : 등록/수정/삭제 권한 (본인 등록에 한하여 CUD 가능)
R : 조회 권한 

로그인시 권한 테이블을 보고 권한 세션 SETTING 
AM, AC, AR : 전체창고 관리자/본인건CUD/조회 
WM, WC, WR : 해당창고 관리자/본인건CUD/조회

## 기타

- order 

고객에게 자재 제공시 : dest_wh_no = null 

실제 총 수령액 
	주문 직후 0
	선금만 입금한 경우 = deposit_amt
	후불 완납한 경우 = deposit_amt + credit_amt
