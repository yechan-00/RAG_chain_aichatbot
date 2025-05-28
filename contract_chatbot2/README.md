<p align="center">
  <img src="https://raw.githubusercontent.com/yourusername/contract-chatbot/main/docs/logo.png" alt="전세계약서 분석 챗봇" width="200"/>
</p>

# 🏠 전세계약서 분석 챗봇

[![Streamlit](https://static.streamlit.io/badges/streamlit_badge_black_white.svg)](https://streamlit.io)  
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)  
[![Python](https://img.shields.io/badge/Python-3.9%2B-blue.svg)](https://www.python.org/)  
[![OpenAI](https://img.shields.io/badge/OpenAI-GPT%20API-brightgreen.svg)](https://platform.openai.com/)

---

## 📖 목차

1. [프로젝트 소개](#프로젝트-소개)  
2. [주요 기능](#주요-기능)  
3. [시스템 아키텍처](#시스템-아키텍처)  
4. [설치 및 실행](#설치-및-실행)  
5. [데모 화면](#데모-화면)  
6. [폴더 구조](#폴더-구조)  
7. [환경 변수](#환경-변수)  
8. [기술 스택](#기술-스택)  
9. [향후 계획](#향후-계획)  
10. [라이선스](#라이선스)  

---

## 📌 프로젝트 소개

**전세계약서 분석 챗봇**은  
FAISS 기반 벡터 검색과 OpenAI GPT-3.5/4를 결합한 RAG(Retrieval-Augmented Generation) 아키텍처를 통해,  
전세 계약서의 복잡한 법률 용어와 사기 위험을 **즉시 분석**, **위험 요소 하이라이트**, **자연어 해설**해 드리는 대화형 웹 애플리케이션입니다.  

- 🏘️ **대상**: 청년·사회 초년생, 부동산 중개사, 법률 비전문가  
- 🔒 **목표**: 전세 사기 리스크 사전 예방 및 계약 이해도 향상  

---

## 🎯 주요 기능

| 기능                        | 설명                                                         |
|---------------------------|------------------------------------------------------------|
| 📎 계약서 업로드             | PDF 또는 이미지(PNG/JPG/JPEG) 지원                               |
| 🔍 텍스트 추출 & 전처리       | PDF 파싱, OCR(이미지) → 하이픈/특수문자 정제                         |
| 📚 벡터 인덱싱              | 청크(500자/50자 오버랩) → OpenAI 임베딩 → FAISS 로컬 DB            |
| 🤖 RAG 기반 QA             | GPT-3.5/4와 벡터 검색 조합으로 계약서 근거 질문 응답 및 해설 제공         |
| ⚠️ 위험 탐지 & 점수화        | 키워드·패턴 기반 0~100% 위험도 계산 → 하이라이트 및 추천 수정안 출력     |
| 📊 계약서 비교              | 최대 2개 문서 나란히 비교                                         |
| 📥 PDF 리포트 다운로드      | 요약·위험 요소 포함한 맞춤형 분석 리포트 생성                           |
| 📂 업로드 이력 관리          | 업로드 일자별 필터링 및 미리보기 기능                                 |

---

## 🏗️ 시스템 아키텍처

```text
+-------------+      +--------------+      +-------------+      +---------+
|  Streamlit  | <--> |   FAISS DB   | <--> |   OpenAI     |      |  User   |
|   Frontend  |      | (벡터 검색)   |      |  GPT-3.5/4   |      |         |
+-------------+      +--------------+      +-------------+      +---------+
        |                    |                    ↑
        |                    |                    |
        ↓                    ↓                    |
    파일 업로드 → OCR/PDF → 텍스트 분할 → 인덱싱 → 검색 → 답변 생성 → 화면 출력