# GreenAI Pre-task

## ✅ 요구사항 충족 내역
- **GET /** 요청 시 HTML 반환  
  ```html
  Hello GreenAI
  ```
- **정적 페이지 서빙**  
  `/static/index.html` 접근 시 정상 표시
- **단일 컨테이너 구동**  
  포트 매핑 `-p 80:8000`  
  (Nginx, HTTPS 미사용)

***

## 1) 로컬 실행 (Python 직접 실행)
```bash
# 1. 가상환경 생성 및 활성화
python -m venv .venv
source .venv/bin/activate       # Mac/Linux
.venv\Scripts\activate          # Windows

# 2. 의존성 설치
pip install -r requirements.txt

# 3. 서버 실행
uvicorn app:app --host 0.0.0.0 --port 8000

# 4. 브라우저 접속
# http://localhost:8000
# http://localhost:8000/static/index.html
```

***

## 2) 로컬 실행 (Docker)
```bash
# 1. Docker 이미지 빌드
docker build -t greenai-app .

# 2. 컨테이너 실행 (포트 매핑 8000 → 80)
docker run -d -p 80:8000 greenai-app

# 3. 확인
curl -i http://localhost/
curl -i http://localhost/static/index.html
```

***

## 3) 배포 환경 (AWS Lightsail)
- **인스턴스**: Ubuntu 22.04  
- **도메인**: `http://greenai.p-e.kr`
- **방화벽 규칙**: 포트 80 허용  
- **도메인 설정**: A 레코드 → Static IP

***

## 4) 검증 방법
```bash
# DNS 확인: 도메인 → Lightsail Static IP 매핑 확인
dig +short A greenai.p-e.kr

# HTTP 확인: "Hello GreenAI" 응답
curl -i http://greenai.p-e.kr

# 정적 페이지 확인
curl -I http://greenai.p-e.kr/static/index.html
```
