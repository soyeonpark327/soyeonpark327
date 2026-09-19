<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:6EE7F9,100:F0C987&height=220&section=header&text=Soyeon%20Park&fontSize=42&fontColor=ffffff&animation=fadeIn&fontAlignY=35&desc=Backend%20Developer&descAlignY=58&descSize=18" width="100%"/>

<a href="https://www.gitanimals.org/en_US?utm_medium=image&utm_source=soyeonpark327&utm_content=farm">
<img
  src="https://render.gitanimals.org/farms/soyeonpark327"
  width="600"
  height="300"
/>
</a>

</div>

## Projects

### [Glocalizer](https://github.com/Linkshimcat/Glocalizer)
한국어 이모티콘을 다국어로 현지화하는 SaaS (NAVER OGQ마켓 AI 공모전 출품작). Node.js/TypeScript 백엔드, React 프론트엔드, PaddleOCR·LLM 기반 OCR/번역 파이프라인.

**담당 작업**
- OCR 줄바꿈 병합 로직 개선 — 여러 줄로 나뉜 한글 캡션을 하나의 영역으로 정확히 병합하도록 수정 ([#24](https://github.com/Linkshimcat/Glocalizer/pull/24))
- 이모티콘 변환 완주(다운로드) 횟수 카운팅 기능 설계·구현 — DB 스키마부터 API, 프론트 연동, 관리자 키 기반 접근 제어까지 ([#25](https://github.com/Linkshimcat/Glocalizer/pull/25), [#26](https://github.com/Linkshimcat/Glocalizer/pull/26))
- 폐기된 번역 모델(Groq) 대응 — 공식 문서 기반 사실 확인 후 대체 모델로 교체 ([#27](https://github.com/Linkshimcat/Glocalizer/pull/27))
- OCR 엔진 벤치마크 및 아키텍처 전환 — PIL 기반 ground truth 측정과 IoU 지표로 PaddleOCR·Gemini·GPT 3개 provider를 직접 비교 평가하고, 정확도·안정성·비용을 종합해 주력 OCR 엔진 교체 (PaddleOCR IoU 0.637 → GPT-5.6 Luna 0.914) ([#29](https://github.com/Linkshimcat/Glocalizer/pull/29))
- 이미지 배경 정리(cleanup) 안전 임계값 버그 진단·수정 — 단색/투명 배경에서 정상적인 지우기 비율(71~87%)을 위험으로 오판해 수동 처리로 빠지던 문제를 실제 파이프라인 재현·측정으로 근본 원인 규명 후 수정, manual cleanup 비율 3/8 → 0/8로 개선 ([#46](https://github.com/Linkshimcat/Glocalizer/pull/46))
- 실사용 이미지 재현으로 Luna OCR의 캡션 분절 비결정성 발견·수정 — 같은 캡션이 호출마다 다르게 쪼개져 클린업이 부분적으로만 성공하던 문제를, 기존 PaddleOCR용 같은 줄 병합 로직을 재사용해 provider 무관하게 해결 ([#47](https://github.com/Linkshimcat/Glocalizer/pull/47))
- Vision LLM(Luna) OCR 오독 안전망 설계·구현 — 반복 호출해도 신뢰도 점수로 정답/오답을 구분 못 하는 사례를 실측으로 확인하고, PaddleOCR와 결과를 대조해 불일치 시 자동승인 대신 검수로 전환하도록 처리, 크기가 다른 박스 간 대조를 위해 IoU 대신 겹침 비율 지표 직접 설계 ([#48](https://github.com/Linkshimcat/Glocalizer/pull/48))
- 반복 패턴 배경 인페인팅 스머지 문제 해결 — 색 분산 기반 가설을 실측으로 반증한 뒤, 자기상관(autocorrelation)의 트로프+리바운드 패턴으로 배경의 주기성을 직접 감지하는 알고리즘을 설계해 그라디언트 오탐 없이 반복 패턴만 정확히 걸러내도록 구현 ([#49](https://github.com/Linkshimcat/Glocalizer/pull/49))
- 클린업 잔상 버그 근본 원인 규명·수정 — mask 자체는 완전한데 옅은 글자 잔상이 남는 현상을 mask만 따로 렌더링해 직접 검증하며 원인을 배경색 추정 로직으로 좁히고, 참조 픽셀이 mask상 글자로 표시된 경우를 걸러내도록 수정 ([#50](https://github.com/Linkshimcat/Glocalizer/pull/50))
- 사용자 제보("배경 단순한데 복잡하다고 뜸") 실시간 진단·수정 — 배경 분류 자체는 정상임을 먼저 검증해 원인을 OCR 대조 단계로 좁히고, PaddleOCR가 놓치기 쉬운 문장 끝 구두점 차이를 실제 오독과 구분하도록 대조 로직 보정 ([#55](https://github.com/Linkshimcat/Glocalizer/pull/55))
- 위 수정의 후속으로 에디터 UX 오류까지 추적·수정 — 원인이 배경이 아니라 OCR 검수 필요일 때도 "복잡한 배경" 문구가 뜨던 3곳(안내 문구·지우기 탭·토스트)을 실제 원인 기준으로 분기, 4개 언어 문구 신규 작성 ([#57](https://github.com/Linkshimcat/Glocalizer/pull/57))
- 원문 지우기(수동 클린업)에 브러시 도구 신규 설계·구현 — 사각형 도구를 대체하지 않고 새 모드로 추가, 실시간 미리보기용 캔버스와 실제 내보내기용 오프스크린 마스크를 분리 설계. Playwright로 실제 흐름 전체 검증 중 텍스트 오버레이가 브러시 캔버스의 포인터 입력을 가로채는 문제를 발견해 함께 수정, 다운로드한 PNG를 픽셀 단위로 검사해 투명/단색 두 모드 모두 정확히 동작함을 확인 ([#61](https://github.com/Linkshimcat/Glocalizer/pull/61))
- 대회 사무국 제공 OGQ 마켓 API 연동 설계·구현 — 키를 서버에만 두는 백엔드 프록시로 감싸고, 랜딩페이지 예시 갤러리와 업로드 페이지 샘플 체험 기능에 연결. 검증 과정에서 OGQ 검색 API의 `imageUrl` 필드가 리사이즈 파라미터 누락으로 CDN에서 400이 나는 것과, CDN이 이미지에 잘못된 Content-Type을 내려줘 업로드 파이프라인의 MIME 필터에 걸리는 것을 실측으로 발견해 수정. 그 과정에서 Express 5의 `req.query`가 getter 전용이라 검증 미들웨어의 직접 대입이 strict mode에서 실패하는 프레임워크 레벨 버그도 함께 찾아 수정 ([#66](https://github.com/Linkshimcat/Glocalizer/pull/66))
