# 프로젝트 기획서

## 서비스 개요
- 어드민이 여러 상품을 등록/관리하고, 유저는 상품 리스트에서 선택해 구매
- 결제 수단: 카드 리다이렉트 / USDT(Kaia Wallet)
- USDT 결제는 항상 N% 할인(상품별 설정)
- 결제 완료 기준: 온체인 1컨펌 확인
- 결제 후 휴대폰 번호 입력 → SMS로 상품 전달(일괄 처리, 1일 뒤 배송 안내)
- 인터뷰 참여 시 3만원 쿠폰 지급 안내

## 결제 정책
- 카드 결제: 상품 등록 시 입력한 URL로 리다이렉트
- USDT 결제:
  - 컨트랙트: 0xd077a400968890eacc75cdc901f0356c943e4fdb
  - 금액 계산: USDT결제금액 = 상품가격 × (1 - N%)
  - Kaia Wallet 연결 → 송금 트랜잭션 생성/서명/전송
  - 결제 완료: 트랜잭션 1컨펌 확인 시 완료 처리

## 화면 구성
- 유저
  - 상품 리스트
  - 상품 상세
  - 결제수단 선택(카드/USDT)
  - USDT 결제 화면(지갑 연결, 할인 적용 금액 표시)
  - 구매 완료 + 휴대폰 번호 입력
- 어드민
  - 로그인(이메일/비번)
  - 상품 등록/수정
  - 상품 리스트 관리

## 상품 등록 필수 입력
- 상품명, 설명, 가격(USDT)
- 카드 결제 리다이렉트 URL(프로모션별 변경 가능)
- USDT 수신 지갑 주소
- USDT 할인율 N%

## 필수 안내 카피
- “USDT 결제 시 N% 즉시 할인”
- “상품은 일괄 처리되며, 구매 후 1일 뒤 배송됩니다.”
- “인터뷰 참여 시 3만원 쿠폰 지급”

## 데이터 모델(요약)
- Product: id, name, description, price_usdt, card_redirect_url, usdt_wallet_address, usdt_discount_percent, is_active, created_at
- Order: id, product_id, pay_method, paid_amount, tx_hash, confirmations, phone_number, status, created_at
- AdminUser: id, email, password_hash, created_at
