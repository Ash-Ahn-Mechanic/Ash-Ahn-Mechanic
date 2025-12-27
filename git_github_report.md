# Git & GitHub 기초 학습 보고서

## 1. 서론
최근 소프트웨어 개발 환경에서는 여러 사람이 동시에 하나의 프로젝트를 개발하는 협업 방식이 일반적이다. 이러한 환경에서는 코드와 문서의 변경 이력을 체계적으로 관리하고, 작업 충돌을 최소화하는 도구가 필수적이다.
본 보고서는 Git과 GitHub의 기본 개념을 학습하고, 실제 사용 흐름과 실습 과정을 정리함으로써 초심자 관점에서 버전 관리와 협업 도구의 활용 방법을 이해하는 것을 목표로 한다.

## 2. Git과 GitHub의 개념
### 2.1 Git의 개념
Git은 파일의 변경 이력을 관리하는 분산 버전 관리 시스템(DVCS)이다. 개발자는 Git을 통해 파일의 수정 사항을 기록하고, 이전 상태로 되돌리거나 변경 내역을 비교할 수 있다.

### 2.2 GitHub의 개념
GitHub는 Git을 기반으로 한 원격 저장소 서비스로, 프로젝트를 온라인에 저장하고 여러 사용자와 협업할 수 있도록 지원한다.

## 3. Git 기본 사용 흐름
작업 디렉토리 → 스테이징 영역 → 로컬 저장소 → 원격 저장소(GitHub)

## 4. Git 기본 명령어
```bash
git init
git status
git add .
git commit -m "first commit"
git push
```

## 5. 파일 상태 관리
Untracked, Modified, Staged, Committed 상태를 통해 변경 이력을 관리한다.

## 6. .gitignore
버전 관리가 필요 없는 파일을 제외하여 협업 시 불필요한 충돌을 방지한다.

## 7. GitHub 협업 기능
Collaborators 기능을 통해 팀원을 저장소에 초대할 수 있다.

## 8. Git 로그 관리
```bash
git log
git log --graph --pretty=oneline
```

## 9. GitHub Pages
Repository를 웹 페이지 형태로 배포할 수 있는 기능이다.

## 10. Mermaid 문서화
Markdown 문서 내에서 텍스트 기반 다이어그램 작성을 지원한다.

## 11. 결론
Git은 버전 관리 도구이며, GitHub는 협업과 공유를 위한 플랫폼이다.
