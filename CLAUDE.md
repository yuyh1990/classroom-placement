# 교실 배치 돌리기 — 배포 안내 (Claude Code용)

## 이 프로젝트는
- 초등학교 교실 배치 프로그램. `index.html` 파일 하나로 끝나는 정적 웹페이지다(빌드 과정 없음, 서버 없음).
- 데이터는 방문자 각자의 브라우저 `localStorage`(키: `classroom-shuffle-v6`)에만 저장한다. 서버나 데이터베이스를 붙이지 말 것.
- 외부에서 불러오는 것은 Google Fonts(Jua, Noto Sans KR)뿐이다.

## 목표
- 링크만 있으면 누구나 로그인 없이 볼 수 있게 **GitHub Pages**로 무료 배포한다.

## 배포 순서
1. `git`과 `gh`(GitHub CLI)가 설치돼 있는지 확인한다. `gh auth status`로 로그인 상태를 확인하고, 안 돼 있으면 사용자에게 `gh auth login`을 직접 실행해 달라고 안내한다(비밀번호·토큰을 대신 입력하지 말 것).
2. 이 폴더에서 git 저장소를 만들고 첫 커밋을 한다.
3. 공개(public) 저장소 `classroom-placement`를 만들고 푸시한다.
   - `gh repo create classroom-placement --public --source=. --push`
4. GitHub Pages를 켠다(main 브랜치, 루트 폴더).
   - `gh api -X POST repos/{owner}/classroom-placement/pages -f "source[branch]=main" -f "source[path]=/"`
5. 1~2분 뒤 `gh api repos/{owner}/classroom-placement/pages`로 주소를 확인하고 사용자에게 알려 준다.
   - 주소 형식: `https://<GitHub아이디>.github.io/classroom-placement/`

## 수정 후 다시 배포
- `index.html`을 고친 뒤 커밋하고 `git push`하면 1~2분 안에 같은 주소에 반영된다.

## 주의
- 저장소가 public이라 코드는 누구나 볼 수 있다. 학생 실명 같은 개인정보를 `index.html`에 넣지 말 것.
- `index.html` 안의 `INIT` 배열이 처음 접속한 사람에게 보이는 기본 학교 배치다.
- 저장 구조를 바꿀 때는 `KEY` 값(예: `classroom-shuffle-v7`)을 올려서, 예전 저장 데이터와 충돌하지 않게 한다.
