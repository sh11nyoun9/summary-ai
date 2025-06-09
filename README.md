# 인터넷 기초[04] 과제2 - 나만의 인공지능 서비스; 줄거리 요약 AI

---

## 개요

- **서비스 명**: 줄거리 요약 AI
- **서비스 설명**: 사용자가 **작품의 유형**(**영화/책**)과 **제목**을 입력하면, Gemini AI가 해당 작품의 줄거리를 핵심만 요약해 알려준다.
- **서비스 접속 주소**: [https://sh11nyoun9.github.io/summary-ai](https://sh11nyoun9.github.io/summary-ai)

---

## 서비스 구성 요소 (1) - Gemini API

- 작품 요약을 위해 Google LLM 플랫폼인 Gemini API의 **gemini-1.5-flash** 모델을 사용
- **프롬프트 설계**:
  - 작품 유형과 제목을 입력 받아 요약 요청
  - LLM에게 **사전 지식이 있는 요약 전문가 역할**을 부여
  - 결말 스포일러 제외, 요약 길이 제한, 사용자 친화적 표현 강조
- **시스템 프롬프트** 예시:
  > "당신은 영화 및 도서 줄거리 요약 전문가입니다. 사람들이 작품을 보기 전에 흥미를 가질 수 있도록, 핵심 내용을 명확하고 간단히 요약해 주세요. 결말을 포함하지 말고, 스포일러 없이 구성해주세요."

---

## 서비스 구성 요소 (2) - 프론트엔드

- HTML, CSS, JavaScript를 사용하여 단순하고 직관적이게 구성
- **사용자가 직접 입력**할 수 있는 form 제공
- **style.css**를 별도로 작성하여 깔끔한 형태로 구성
- 기본 스타일 색상은 연한 배경과 파란 버튼으로 안정감 있는 분위기를 구성

---

## 서비스 구성 요소 (3) - 백엔드

- Google Gemini API 호출을 위한 **Serverless API**(요청이 들어올 때만 자동으로 실행되는 백엔드 함수)를 작성하여 Vercel에 배포
- Google Gemini API 키가 외부에 노출되지 않도록 프론트엔드가 사용자 입력을 **백엔드**(Serverless API)로 전송하고, 백엔드가 Gemini API를 대신 호출한 뒤 응답을 반환하는 구조로 구현
- 프론트에서 전달받은 `type`, `title`을 기반으로 Gemini에 요청 → 요약 응답 전달
- CORS 설정을 통해, 내 API가 오직 내 GitHub Pages 프론트엔드에서만 접근 가능하도록 제한함(= 보안 강화 + 불필요한 호출 차단) (`sh11nyoun9.github.io`)
- 작성한 API 경로: `/api/summaryAI`
- 코드 및 구현 내용은 [https://github.com/sh11nyoun9/summary-ai-api](https://github.com/sh11nyoun9/summary-ai-api) 참고
