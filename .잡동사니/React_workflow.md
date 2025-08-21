# React 프로젝트 워크플로우

## React 프로젝트 폴더가 필요한 이유

1. **코드 관리**:
   - 애플리케이션의 컴포넌트, 스타일, 로직 등을 체계적으로 관리하기 위해 폴더 구조가 필요합니다.

2. **빌드 및 실행**:
   - React는 브라우저에서 실행 가능한 정적 파일로 변환(빌드)해야 합니다. 프로젝트 폴더는 이 과정을 지원합니다.

3. **종속성 관리**:
   - `package.json` 파일을 통해 필요한 라이브러리와 종속성을 관리합니다.

4. **개발 환경 제공**:
   - React 프로젝트는 개발 서버를 제공하여 실시간으로 변경 사항을 확인할 수 있습니다.

---

## React 프로젝트 생성 후 일반적으로 수행하는 작업

1. **개발 서버 실행**:
   - 프로젝트 폴더로 이동한 후 개발 서버를 실행합니다:
     ```bash
     npm start
     ```
   - 브라우저에서 `http://localhost:3000`을 열어 기본 React 앱을 확인합니다.

2. **폴더 구조 이해**:
   - 기본 폴더 구조:
     - `src/`: 애플리케이션의 주요 코드가 위치.
     - `public/`: 정적 파일(예: HTML, 이미지 등)이 위치.
     - `node_modules/`: 설치된 종속성 라이브러리.
     - `package.json`: 프로젝트 설정 및 종속성 관리.

3. **컴포넌트 작성**:
   - `src/` 폴더에서 새로운 컴포넌트를 작성하여 애플리케이션의 UI를 구성합니다.

4. **스타일 추가**:
   - CSS 파일을 작성하거나 `styled-components`와 같은 라이브러리를 설치하여 스타일을 추가합니다.

5. **라이브러리 설치**:
   - 필요한 라이브러리를 설치합니다. 예:
     ```bash
     npm install react-router-dom
     ```

6. **코드 작성 및 테스트**:
   - 애플리케이션의 로직을 작성하고 테스트를 실행합니다.

---

## Git 워크플로우

1. **Git 초기화**:
   - 프로젝트 폴더에서 Git을 초기화합니다:
     ```bash
     git init
     ```

2. **`.gitignore` 설정**:
   - React 프로젝트에서 무시해야 할 파일 및 폴더를 `.gitignore`에 추가합니다:
     ```plaintext
     node_modules/
     build/
     .env
     ```

3. **첫 커밋**:
   - 프로젝트 초기 상태를 커밋합니다:
     ```bash
     git add .
     git commit -m "Initial commit"
     ```

4. **원격 저장소 연결**:
   - GitHub에 저장소를 생성한 후, 원격 저장소를 연결합니다:
     ```bash
     git remote add origin https://github.com/<GitHub-Username>/<Repository-Name>.git
     git branch -M main
     git push -u origin main
     ```

5. **작업 후 커밋**:
   - 코드를 수정한 후 변경 사항을 커밋합니다:
     ```bash
     git add .
     git commit -m "Update feature X"
     ```

6. **배포**:
   - 작업이 완료되면 `npm run deploy` 명령어를 실행하여 `gh-pages` 브랜치에 정적 파일을 배포합니다:
     ```bash
     npm run deploy
     ```

7. **GitHub Pages 설정**:
   - GitHub 저장소의 **Settings > Pages**에서 `gh-pages` 브랜치를 활성화합니다.

---

## 추가 참고 사항

- **`gh-pages` 브랜치로 스위칭할 필요 없음**:
  - `npm run deploy` 명령어를 실행하면 `gh-pages` 브랜치가 자동으로 업데이트됩니다.
  - 따라서 `gh-pages` 브랜치로 직접 전환하거나 수동으로 작업할 필요가 없습니다.
  - 모든 작업은 `main` 브랜치에서만 진행하면 됩니다.

---

## 다음 단계
React 프로젝트 폴더가 생성되었으니, 개발 서버를 실행하고 기본 구조를 확인해보세요. 이후 컴포넌트 작성, 스타일 추가, 라이브러리 설치 등을 진행할 수 있습니다.