# 안녕하세요, 박소연입니다 👋

한국어 콘텐츠를 다국어로 현지화하는 OCR·번역 파이프라인에 관심이 많은 개발자입니다.

📫 s2608@e-mirim.hs.kr

<a href="https://www.gitanimals.org/en_US?utm_medium=image&utm_source=soyeonpark327&utm_content=farm">
<img
  src="https://render.gitanimals.org/farms/soyeonpark327"
  width="600"
  height="300"
/>
</a>

## Projects

### [Glocalizer](https://github.com/Linkshimcat/Glocalizer)
한국어 이모티콘을 다국어로 현지화하는 SaaS (NAVER OGQ마켓 AI 공모전 출품작). Node.js/TypeScript 백엔드, React 프론트엔드, PaddleOCR·LLM 기반 OCR/번역 파이프라인.

**담당 작업**
- OCR 줄바꿈 병합 로직 개선 — 여러 줄로 나뉜 한글 캡션을 하나의 영역으로 정확히 병합하도록 수정 ([#24](https://github.com/Linkshimcat/Glocalizer/pull/24))
- 이모티콘 변환 완주(다운로드) 횟수 카운팅 기능 설계·구현 — DB 스키마부터 API, 프론트 연동, 관리자 키 기반 접근 제어까지 ([#25](https://github.com/Linkshimcat/Glocalizer/pull/25), [#26](https://github.com/Linkshimcat/Glocalizer/pull/26))
- 폐기된 번역 모델(Groq) 대응 — 공식 문서 기반 사실 확인 후 대체 모델로 교체 ([#27](https://github.com/Linkshimcat/Glocalizer/pull/27))
- OCR 엔진 벤치마크 및 아키텍처 전환 — PIL 기반 ground truth 측정과 IoU 지표로 PaddleOCR·Gemini·GPT 3개 provider를 직접 비교 평가하고, 정확도·안정성·비용을 종합해 주력 OCR 엔진 교체 (PaddleOCR IoU 0.637 → GPT-5.6 Luna 0.914) ([#29](https://github.com/Linkshimcat/Glocalizer/pull/29))
