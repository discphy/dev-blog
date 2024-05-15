# 파이썬 FastAPI를 이용한 API 프로젝트 만들기 (0) - 소개 및 예제

## FastAPI란?

`Python`의 웹 프레임워크하면, 보통 `Django`와 `Flask`가 떠오를 것이다. 

**2023**년부터 **성능**과 **개발편의성**에 최적화된 `FastAPI`가 등장하면서 급 부상 중이다.

### FastAPI 특징

---

- **빠름**: (`Starlette`과 `Pydantic` 덕분에) **`NodeJS`** 및 **`Go`**와 대등할 정도로 매우 높은 성능. [사용 가능한 가장 빠른 파이썬 프레임워크 중 하나](https://fastapi.tiangolo.com/ko/#performance).
- **빠른 코드 작성**: 약 200%에서 300%까지 기능 개발 속도 증가.
- **적은 버그**: 사람(개발자)에 의한 에러 약 40% 감소.
- **직관적**: 훌륭한 편집기 지원. 모든 곳에서 자동완성. 적은 디버깅 시간.
- **쉬움**: 쉽게 사용하고 배우도록 설계. 적은 문서 읽기 시간.
- **짧음**: 코드 중복 최소화. 각 매개변수 선언의 여러 기능. 적은 버그.
- **견고함**: 준비된 프로덕션 용 코드를 얻으십시오. 자동 대화형 문서와 함께.
- **표준 기반**: `API`에 대한 (완전히 호환되는) 개방형 표준 기반: [`OpenAPI`](https://github.com/OAI/OpenAPI-Specification) (이전에 `Swagger`로 알려졌던) 및 [JSON 스키마](http://json-schema.org/).

### FastAPI 구글 트렌드 조사

---

> `Django`가 압도적이긴 하나, `Flask`와 비교해보면 2023년부터 많은 관심을 받았다고 볼 수 있을 것 같다.
>

![Untitled.png](/static/image/python-fastapi/Untitled.png)

## 파이썬 웹 프레임워크 성능과 장단점 비교 (GPT 답변 첨부)

|  | 성능 | 장점 | 단점 |
| --- | --- | --- | --- |
| FastAPI | 비동기 처리를 지원하여 빠른 속도와 높은 처리량을 제공합니다. 이는 https://docs.python.org/ko/3/library/asyncio.html 및 https://www.uvicorn.org/과 같은 비동기 웹 서버와의 통합으로 가능합니다. | - 빠른 개발과 테스트를 위한 기능을 제공합니다.
- Pydantic을 통한 자동 API 문서 생성과 타입 체크를 지원하여 API 문서화를 용이하게 합니다.
- Swagger UI와 OpenAPI를 지원하여 API 문서를 자동으로 생성합니다. | - 비동기 처리에 대한 학습 곡선이 있을 수 있습니다.
- Flask나 Django에 비해 아직까지 생태계가 상대적으로 작습니다. |
| Flask | 가볍고 간결한 프레임워크이므로 속도 면에서 빠르게 실행될 수 있습니다. 하지만 비동기 처리를 지원하지 않으므로 FastAPI보다는 성능이 낮을 수 있습니다. | - 미니멀한 디자인을 가지고 있어 필요한 기능을 필요할 때마다 확장하여 사용할 수 있습니다.
- 다양한 확장 라이브러리를 통해 유연성을 제공하며, 개발자들이 익숙한 인터페이스를 제공합니다. | - 비동기 처리를 지원하지 않아 대규모 및 실시간 데이터 처리에 적합하지 않을 수 있습니다.
- Flask 애플리케이션의 구조가 복잡해질 경우 유지보수가 어려울 수 있습니다. |
| Django | Django는 전체적으로 안정적이고 빠른 프레임워크입니다. 그러나 비동기 처리를 지원하지 않기 때문에 FastAPI보다는 성능이 떨어질 수 있습니다. | - ORM, 관리자 패널, 인증 시스템 등 다양한 기능을 기본으로 제공하여 개발 생산성을 향상시킵니다.
- 안정성과 보안성이 높으며, 커뮤니티 및 생태계가 활성화되어 있어 다양한 문제에 대한 지원이 용이합니다. | - 무거운 프레임워크이기 때문에 작은 프로젝트나 빠른 프로토타이핑에는 적합하지 않을 수 있습니다.
- Django의 강력한 기능과 기본 제공되는 기능 때문에 프로젝트의 요구 사항에 따라 필요하지 않은 기능을 갖게 될 수도 있습니다. |

한 마디로 정리하자면, `FastAPI`는 개발과 테스트가 간단하면서 `API` 문서를 제공하고 비동기 처리를 지원하는 프레임워크라고 생각하면 된다! 

## FastAPI로 웹 프로젝트 만들기

> 예제소스 : [https://wikidocs.net/book/8531](https://wikidocs.net/book/8531)
> 

노마드 코더에서 제공하는 “[Python으로 웹 스크래퍼 만들기](https://nomadcoders.co/python-for-beginners)”에서 제공하는 예제를 응용하여 간단한 `API` 서비스를 만들어보도록 하자. 

### 1. 프로젝트 생성 및 Hello World

---

1. 프로젝트 생성 : `PyCharm IDE`를 실행하고 프로젝트 이름과 가상환경 세팅 후 생성
    
    ![Untitled.png](/static/image/python-fastapi/Untitled 1.png)
    

1. 가상환경 적용 확인
    
    `.venv` 가상 환경 폴더가 생성된 것 확인 후 좌측 하단에 있는 **터미널** 아이콘을 클릭 하면 다음과 같은 터미널이 등장하는데 **`(.venv)`** 가 반드시 확인 되어야 한다.
    
    ![Untitled.png](/static/image/python-fastapi/Untitled 2.png)
    
    ```bash
    # 확인이 안된다면, 다음 명령어를 차례대로 실행
    cd .venv 
    source activate
    
    ```
    

1. 패키지 설치
    
    ```bash
    # FastAPI 설치
    pip install fastapi
    
    # FastAPI 프로그램을 구동하기 위한 웹 서버 Uvicon(비동기 호출을 지원하는 파이썬 웹 서버) 설치
    pip install "uvicorn[standard]"
    ```
    

1. `main.py` 작성 및 구동 
    
    ```python
    # main.py 생성 
    
    from fastapi import FastAPI
    
    app = FastAPI()
    
    @app.get("/hello")
    def hello():
        return {"message": "hello world"}
    ```
    
    ```python
    # 터미널에서 다음 명령어 실행 
    uvicorn main:app --reload
    
    # main:app : main.py의 app을 의미 
    # --reload : 서버 재시작 없이 반영 
    ```
    

1. 접속 및 자동으로 생성 된 `API` 문서확인 
    - [http://127.0.0.1:8000/hello](http://127.0.0.1:8000/hello) 접속 시 `main.py` 에 작성한 응답 결과가 나온다.
    
    ![Untitled.png](/static/image/python-fastapi/Untitled 3.png)
    
    - [http://127.0.0.1:8000/docs](http://127.0.0.1:8000/docs) 에 접속하면 실행 가능한 `Swagger UI` 가 제공 되고, [http://127.0.0.1:8000/redoc](http://127.0.0.1:8000/redoc) 에 접속하면 읽기 전용인 `Redoc`문서가 자동으로 제공된다.
        
        > `Spring`에서는 `API` 문서를 작성하려면 까다로운데…(`Spring rest docs` 테스트 코드 구성, `Swagger`로 인한 `Controller` 소스 침투로 인한 직관성 떨어짐) `FastAPI`는.. 와.. 대단한 것 같다..
        > 
        
        ![스크린샷 2024-04-09 16.23.31.png](/static/image/python-fastapi/2024-04-09_16.23.31.png)
        
        ![스크린샷 2024-04-09 16.23.45.png](/static/image/python-fastapi/2024-04-09_16.23.45.png)
        

### 2. DB & ORM 설정

---

1. `ORM` 패키지 설치 - 가장 많이 사용하는 `SQLAlchemy` 설치
    
    ```bash
    pip install sqlalchemy
    ```
    

1. `database.py` 생성
    
    ```python
    from sqlalchemy import create_engine
    from sqlalchemy.ext.declarative import declarative_base
    from sqlalchemy.orm import sessionmaker
    
    # Python 기본 패키지에 포함 되어있는 sqlite 사용
    SQLALCHEMY_DATABASE_URL = "sqlite:///./fastapi-scrap.db"
    
    engine = create_engine(
        SQLALCHEMY_DATABASE_URL, connect_args={"check_same_thread": False}
    )
    
    SessionLocal = sessionmaker(autocommit=False, autoflush=False, bind=engine)
    
    Base = declarative_base()
    
    # DB 세션 객체 함수
    def get_db():
        db = SessionLocal()
        try:
            yield db
        finally:
            db.close()
    ```
    

1. 모델 생성 - 채용정보 도메인
    
    1) 채용정보 모델 설계 
    
    ```mermaid
    erDiagram
    	employ{
    		Integer id
    		String platform
    		String keyword
    		String company_name
    		String position
    		DateTime create_date
    	}
    ```
    
    2) [models.py](http://models.py) 생성 
    
    ```python
    # models.py
    from sqlalchemy import Column, Integer, String, DateTime
    
    from database import Base
    
    class Employ(Base):
    	__tablename__ = "employ"
    
    	id = Column(Integer, primary_key=True)
    	platform = Column(String, nullable=False)
    	keyword = Column(String, nullable=False)
    	company_name = Column(String, nullable=False)
    	position = Column(String, nullable=False)
    	create_date = Column(DateTime, nullable=False)
    ```
    

1. `alembic` 설정
    
    `alembic`이란? `SQLAlchemy`에서 제공하는 데이터베이스 마이그레이션 도구이다. 
    
    1) 터미널에서 `alembic` 패키지 설치 및 초기화
    
    ```bash
    # alembic 패키지 설치 
    pip install alembic
    
    # alembic 초기화
    alembic init migrations
    ```
    
    2) 초기화 시, 생긴 마이그레이션 설정 파일 수정 `alembic.ini`, `migrations/env.py`
    
    ![Untitled](/static/image/python-fastapi/Untitled 4.png)
    
    ```python
    # alembic.ini 수정
    ...
    sqlalchemy.url = sqlite:///./fastapi-study.db # 수정 
    ...
    ```
    
    ```python
    # migrations/env.py 수정
    ...
    import models
    
    ...
    target_metadata = models.Base.metadata
    ...
    ```
    
    3) 리비전 파일 생성
    
    ```bash
    # 리비전 파일 생성 - 테이블 스크립트 문 생성 
    alembic revision --autogenerate
    
    # 리비전 파일 실행 - 테이블 스크립트 적용
    alembic upgrade head
    ```
    
    4) `fastapi-scrap.db` 생성 확인
    
    ![Untitled](/static/image/python-fastapi/Untitled 5.png)
    

### 3. API 작성

---

1. 도메인 디렉토리 생성 - `domain/employ`
    
    ![Untitled](/static/image/python-fastapi/Untitled 6.png)
    

1. `Pydantic`을 활용한 `employ_schema.py` 작성 
    
    `Pydantic`이란, 입출력 스펙을 정의하고 값을 검증하는 라이브러리이다. 
    
    ```python
    from datetime import datetime
    from pydantic import BaseModel, field_validator
    
    # 조회시, 응답 스펙 정의
    class Employ(BaseModel):
        id: int
        platform: str
        keyword: str
        company_name: str
        position: str
        create_date: datetime
    
    # 등록시, 요청 스펙 정의
    class EmployCreate(BaseModel):
        keyword: str
        company_name: str
        position: str
    
        # 빈 문자열 검증
        @field_validator('keyword', 'company_name', 'position')
        def not_empty(cls, v):
            if not v or not v.strip():
                raise ValueError("Required value")
            return v
    
    ```
    

1. `employ_crud.py` 작성 - 실제 쿼리 적용 구현 부 
    
    ```python
    from datetime import datetime
    from models import Employ
    from sqlalchemy.orm import Session
    from domain.employ.employ_schema import EmployCreate
    
    # 채용 정보 전체 조회
    def employ_list(db: Session):
        return db.query(Employ) \
            .order_by(Employ.create_date.desc()) \
            .all()
    
    # 채용 정보 등록
    def employ_create(db: Session, create_request: EmployCreate, platform):
        db.add(Employ(platform=platform,
                      keyword=create_request.keyword,
                      company_name=create_request.company_name,
                      position=create_request.position,
                      create_date=datetime.now()))
        db.commit()
    
    ```
    

1. `APIRouter`을 활용한 `employ_router.py` 작성
    
    `router` 객체를 생성하여 `FastAPI` 앱에 등록해야만 라우팅 기능 정상 동작
    
    ```python
    from fastapi import APIRouter, Depends
    from sqlalchemy.orm import Session
    from database import get_db
    
    # 위에서 정의한 employ_schema, employ_crud 참조
    from domain.employ import employ_schema, employ_crud
    
    # prefix 설정
    router = APIRouter(
        prefix="/api/employ"
    )
    
    # 채용 정보 전체 조회 API
    @router.get("/list", response_model=list[employ_schema.Employ])  # employ_schema.py 에서 정의한 응답 스펙 기재
    def employ_list(db: Session = Depends(get_db)):
        return employ_crud.employ_list(db)
    
    # 채용 정보 수동 등록 API
    @router.post("/manual/create")
    def employ_manual_create(create_request: employ_schema.EmployCreate,  # employ_schema.py 에서 정의한 요청 스펙 파라미터
                             db: Session = Depends(get_db)):
        employ_crud.employ_create(db, create_request, "MANUAL")
    
    ```
    

1. `router`를 `main.py`에 등록
    
    ```python
    from fastapi import FastAPI
    from domain.employ import employ_router
    
    app = FastAPI()
    
    # 라우터 등록
    app.include_router(employ_router.router)
    
    ```
    

1. 실행 후 `Swagger UI`를 이용한 `API` 테스트 
    
    1) `uvicorn` 명령어로 서버 재실행 
    
    ```bash
    uvicorn main:app --reload
    ```
    

2) [http://127.0.0.1:8000/docs](http://127.0.0.1:8000/docs) 접속 하면 다음과 같이 생성한 `API` 2개가 보인다.

![Untitled](/static/image/python-fastapi/Untitled 7.png)

3) 채용 정보 등록 `API` 테스트 

- `Try it out` 을 클릭하면 테스트를 진행 할 수 있다.

![Untitled](/static/image/python-fastapi/Untitled 8.png)

- `Request Body`를 작성 후 `Execute` 버튼을 누르면 API 호출이 된다.

![Untitled](/static/image/python-fastapi/Untitled 9.png)

4) 등록한 채용 정보를 채용 정보 조회 `API`를 통해 확인

- 위와 같이 채용 정보 조회 `API` 를 `Try it out` 버튼과 `Execute` 버튼을 차례대로 클릭 하면 다음 이미지와 같이 결과를 확인 할 수 있다.

![Untitled](/static/image/python-fastapi/Untitled 10.png)

## 마무리

위의 과정에서 자세한 라이브러리 사용은 언급하지 않았다. (저자도 파이썬 초보라… 😹)
자세한 내용은 아래 [참고] 링크를 통해 확인하길 바란다.

`FastAPI` 웹 프레임워크를 활용하니 `API`는 공장처럼 찍어 낼 수 있을 것 같다. 
너무 간단하기도 하고.. 문서도 자동화 해주니.. 너무 편리하지 않는가!!!??? 

![Untitled](/static/image/python-fastapi/Untitled.jpeg)

분량이 많아진 관계로 스크래핑한 채용 정보 등록을 `API`로 구성하는 예제는 다음 글에서 뵙도록 하겠다. 👋🏻

[https://github.com/discphy/fastapi-scrap](https://github.com/discphy/fastapi-scrap)

[참고]

[https://github.com/tiangolo/fastapi](https://github.com/tiangolo/fastapi)

[https://dasima.co.kr/125/fastapi는-무엇인가-fastapi-사용설명서-01/](https://dasima.co.kr/125/fastapi%EB%8A%94-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80-fastapi-%EC%82%AC%EC%9A%A9%EC%84%A4%EB%AA%85%EC%84%9C-01/)

[https://wikidocs.net/book/8531](https://wikidocs.net/book/8531)