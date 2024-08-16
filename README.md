[개발 환경 설정]
<br>[버전정보]

- react : 18.3.1
- node : 20.16.0

<br>[에러현상]

1. bash: /c/Program Files/nodejs/yarn: No such file or directory

- npm install -g yarn 명령어 실행

1. Prettier, ESLint 설치

- .prettierrc.json 파일 추가
- yarn add prettier --dev 설치
- yarn add eslint --dev 설치
- yarn add eslint-plugin-prettier --dev 설치
- yarn add eslint-plugin-react --dev설치
- yarn add eslint-plugin-react-hooks --dev설치
- yarn add eslint-plugin-jsx-a11y --dev설치

[Setting]

1. vscode 상단에 >settings.json 입력
2. 코드 저장시 포맷 코드

{
...
"editor.formatOnSave": true
}

3. 안쓰는 import 제거

   "editor.codeActionsOnSave": {
   "source.organizeImports": "explicit"
   }
