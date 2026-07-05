# ArchiQ - AWS 아키텍처 리뷰 도구 / AWS Architecture Review Tool

ArchiQ는 Amazon Q Developer와 통합되어 고객의 현재 AWS 아키텍처를 자동으로 분석하고 개선 방안을 제시하는 도구입니다. 서울 리전 최적화 및 간소화된 사용자 경험을 제공하며, **한국어와 영어를 모두 지원**합니다. AWS 프로파일을 선택하여 멀티 계정 환경에서도 편리하게 사용할 수 있습니다.

ArchiQ is a tool integrated with Amazon Q Developer that automatically analyzes customers' current AWS architecture and provides improvement recommendations. It offers Seoul region optimization and simplified user experience, **supporting both Korean and English languages**. AWS profile selection enables convenient use in multi-account environments.

## 🌐 언어 지원 / Language Support

- **한국어 (Korean)**: 기본 지원, 한국어 프롬프트 및 UI
- **English**: Full English support with localized prompts and interface
- **언어 전환**: 실행 시 언어 선택 가능, 메뉴에서 언어 변경 옵션 제공
- **Language Switching**: Language selection at startup, language change option in menu

## 🔑 AWS 프로파일 지원 / AWS Profile Support

- **멀티 프로파일**: `~/.aws/credentials` 및 `~/.aws/config`에 등록된 모든 프로파일 자동 감지
- **시작 시 선택**: 프로그램 실행 시 사용할 AWS 프로파일을 대화형으로 선택
- **메뉴에서 변경**: 실행 중 언제든지 메뉴에서 프로파일 변경 가능
- **CLI 옵션**: `run.sh` 실행 시 `-p` 옵션으로 프로파일 직접 지정 가능
- **Multi-profile**: Auto-detects all profiles in `~/.aws/credentials` and `~/.aws/config`
- **Startup selection**: Interactively select the AWS profile at startup
- **In-menu change**: Change profile anytime from the menu during execution
- **CLI option**: Specify profile directly with `-p` option when running `run.sh`

## 🚀 주요 기능 / Key Features

### 1. AWS 리소스 기반 현대화 경로 분석
- 현재 운영 중인 AWS 리소스 기반 현대화 기회 식별
- Well-Architected Framework 6개 기둥 적용한 포괄적 분석
- 단계별 현대화 로드맵 및 비용 효과 분석 제시
- 실제 리소스 ID와 설정값을 활용한 구체적 권장사항

### 2. AWS 리소스 기반 보안 점검
- 실제 AWS 리소스를 스캔하여 보안 위험 요소 식별
- 네트워크 보안, 접근 제어, 데이터 보호 등 종합 분석
- 구체적인 보안 강화 방안 제시

### 3. AWS 리소스 기반 Well-Architected 리뷰
- 현재 운영 중인 AWS 리소스 기반 아키텍처 분석
- 6개 기둥별 상세 평가 및 점수 산정
- Mermaid 다이어그램을 포함한 시각적 아키텍처 표현

### 4. AWS 리소스 기반 아키텍처 다이어그램 생성
- 현재 AWS 환경의 아키텍처를 자동으로 시각화
- Mermaid 및 draw.io 호환 형식 제공
- 다중 레벨 다이어그램 (High-Level, Network-Level, Service-Level)

### 5. Service Screener 결과 기반 Well-Architected Review
- 특정 디렉토리의 Service Screener 결과 파일을 분석
- Well-Architected Framework 6개 기둥 기반 종합 평가
- 우선순위별 개선 권장사항 제시

## 🔧 핵심 기술 특징

- **안정적인 프로세스 관리**: Interactive Session 기반 안정적인 qchat 연동
- **간단한 구조**: 복잡한 예외 처리 제거하고 핵심 기능에 집중
- **AWS 프로파일 전파**: 선택한 프로파일이 모든 AWS CLI 및 q chat 호출에 자동 적용

## 📁 프로젝트 구조

```
/home/ec2-user/archiQ
├── src/
│   ├── cli.py                    # 🎯 ArchiQ 메인 CLI 인터페이스 (다국어 지원)
│   ├── middleware/               # Amazon Q Developer 통합 레이어
│   │   └── amazon_q_hook.py     # 🔧 간소화된 Interactive Session 핸들러
│   └── prompt/                   # 🎨 기능별 프롬프트 템플릿
│       ├── modernization_path.md
│       ├── service_screener_review.md
│       ├── security_check.md
│       ├── well_architected_review.md
│       ├── architecture_diagram.md
│       └── en/                   # 🌐 영어 프롬프트 템플릿
│           ├── modernization_path.md

│           ├── service_screener_review.md
│           ├── security_check.md
│           ├── well_architected_review.md
│           └── architecture_diagram.md
├── output/                       # 📊 생성된 HTML 보고서 저장소
│   ├── modernization/            # 현대화 경로 분석 결과
│   ├── service-screener/         # Service Screener 분석 결과
│   ├── security/                 # 보안 점검 결과
│   ├── well-architected/         # Well-Architected 리뷰 결과
│   ├── architecture/             # 아키텍처 다이어그램 결과
│   └── en/                       # 🌐 영어 보고서 저장소
│       ├── modernization/
│       ├── service-screener/
│       ├── security/
│       ├── well-architected/
│       └── architecture/
├── requirements.txt              # Python 의존성
├── run_archiq.sh                # 🚀 메인 실행 스크립트
├── run_modernization_path.sh    # 현대화 경로 분석 실행 스크립트
├── run_service_screener.sh      # Service Screener 실행 스크립트
├── run_security_check.sh        # 보안 점검 실행 스크립트
├── run_well_architected.sh      # Well-Architected 리뷰 실행 스크립트
├── run_architecture_diagram.sh  # 아키텍처 다이어그램 실행 스크립트
└── LICENSE                      # MIT 라이선스
```

## 🛠️ 설치 및 설정

### 1. 저장소 복제
```bash
git clone <repository-url>
cd archiQ
```

### 2. 의존성 설치
```bash
pip install -r requirements.txt
```

**주요 의존성:**
- `pytest==7.0.1` - 테스트 프레임워크
- `pytest-mock==3.10.0` - 모킹 라이브러리
- `websockets==10.1` - WebSocket 통신
- `inquirer==3.1.3` - 대화형 CLI 인터페이스
- `boto3>=1.26.0` - AWS SDK
- `botocore>=1.29.0` - AWS 핵심 라이브러리

### 3. AWS 자격 증명 및 프로파일 설정
```bash
# 기본 프로파일 설정
aws configure

# 특정 프로파일 추가
aws configure --profile my-profile

# 여러 계정을 사용하는 경우 ~/.aws/credentials 직접 편집
# [default]
# aws_access_key_id = ...
# aws_secret_access_key = ...
#
# [prod]
# aws_access_key_id = ...
# aws_secret_access_key = ...
```

### 4. 실행 권한 설정
```bash
chmod +x *.sh
```

## 🚀 사용 방법

### 기본 실행
```bash
# 메인 ArchiQ 실행
./run.sh

# 또는 Python으로 직접 실행
python src/cli.py
```

### 시작 순서 / Startup Sequence
프로그램 시작 시 아래 순서로 설정합니다:
1. **언어 선택**: 한국어 / English
2. **AWS 프로파일 선택**: `~/.aws/credentials`에서 감지된 프로파일 목록 표시

### AWS 프로파일 선택 (대화형)
```
사용 가능한 AWS 프로파일:
  1. default (현재)
  2. dev
  3. prod
  4. staging

프로파일 번호를 선택하세요 (기본값: default):
```

### CLI 메뉴 옵션 (한국어)
```
Language: 한국어  |  AWS Profile: prod
  1. 사용중인 AWS 리소스 기반 현대화 경로 분석
  2. 사용중인 AWS 리소스 기반 보안 점검
  3. 사용중인 AWS 리소스 기반 Well-Architected 리뷰
  4. 사용중인 AWS 리소스 기반 아키텍처 다이어그램 생성
  5. Service Screener 결과 기반 Well-Architected Review
  6. 종료
  7. 언어 변경 (Change Language)
  8. AWS 프로파일 변경
```

### CLI Menu Options (English)
```
Language: English  |  AWS Profile: prod
  1. AWS Resource-based Modernization Path Analysis
  2. AWS Resource-based Security Assessment
  3. AWS Resource-based Well-Architected Review
  4. AWS Resource-based Architecture Diagram Generation
  5. Service Screener Results-based Well-Architected Review
  6. Exit
  7. 언어 변경 (Change Language)
  8. Change AWS Profile
```

## 📊 생성되는 보고서

모든 분석 결과는 `output/` 디렉토리에 HTML 형식으로 저장됩니다:

### 보고서 특징
- **종합 요약 대시보드**: 핵심 지표 및 개선 기회
- **시각적 다이어그램**: Mermaid를 사용한 아키텍처 표현
- **상세 분석**: 각 AWS 서비스별 현재 상태 및 권장사항
- **실행 계획**: 구체적인 AWS CLI 명령어 및 구현 방법
- **우선순위별 권장사항**: High/Medium/Low 분류된 개선 방안

### 디자인 특징
- **푸른색 테마**: 전문적이고 신뢰감 있는 디자인
- **반응형 레이아웃**: 다양한 화면 크기 지원
- **일관된 브랜딩**: 모든 보고서에서 동일한 디자인 언어 사용

## 🔧 고급 사용법

### 프롬프트 커스터마이징
`src/prompt/` 디렉토리의 Markdown 파일을 수정하여 분석 기준을 조정할 수 있습니다:

- `modernization_path.md`: 현대화 경로 분석 프롬프트
- `service_screener_review.md`: Service Screener 분석 프롬프트
- `security_check.md`: 보안 점검 프롬프트  
- `well_architected_review.md`: Well-Architected 리뷰 프롬프트
- `architecture_diagram.md`: 아키텍처 다이어그램 생성 프롬프트

### 리전 및 프로파일 설정
기본 리전은 서울(ap-northeast-2)로 설정되어 있으며, 각 기능 실행 시 다른 리전을 선택할 수 있습니다.

`run.sh` 사용 시 옵션으로 직접 지정할 수도 있습니다:
```bash
# 프로파일과 리전 함께 지정
./run.sh 2 -p prod -r us-east-1

# 프로파일만 지정 (리전은 기본값 ap-northeast-2)
./run.sh 3 -p dev

# 옵션 없이 실행 시 대화형으로 프로파일 선택
./run.sh
```

## 🤝 기여하기

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📝 라이선스

이 프로젝트는 MIT 라이선스 하에 배포됩니다. 자세한 내용은 `LICENSE` 파일을 참조하세요.

## 🆘 지원

문제가 발생하거나 질문이 있으시면:
- GitHub Issues에 문제를 등록해주세요
- 프로젝트 Wiki를 확인해주세요
- 커뮤니티 토론에 참여해주세요

## 🔄 버전 히스토리

### v2.2.0 (Latest)
- ✅ AWS 프로파일 선택 기능 추가 (멀티 계정 지원)
- ✅ `run.sh`에 `-p/--profile` 옵션 추가
- ✅ 시작 시 대화형 프로파일 선택 및 메뉴 내 프로파일 변경 지원
- ✅ 불필요한 자동 응답(pexpect) 코드 제거

### v2.1.0
- ✅ 코드 간소화 및 안정성 개선
- ✅ 복잡한 예외 처리 제거
- ✅ Hanging 문제 완전 해결

### v2.0.0
- ✅ Interactive Session 기반 안정성 개선
- ✅ HTML 보고서 디자인 표준화

### v1.0.0
- ✅ 기본 AWS 아키텍처 분석 기능
- ✅ Service Screener 통합
- ✅ Well-Architected Framework 지원

---

**ArchiQ**로 AWS 아키텍처를 더 안전하고 효율적으로 만들어보세요! 🚀
