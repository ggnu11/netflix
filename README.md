[개발 환경 설정]
<br>[버전정보]

- react : 18.3.1
- node : 20.16.0

<br>[에러현상]

1. bash: /c/Program Files/nodejs/yarn: No such file or directory

- npm install -g yarn 명령어 실행

2.  (node:2472) [DEP_WEBPACK_DEV_SERVER_ON_AFTER_SETUP_MIDDLEWARE] DeprecationWarning: 'onAfterSetupMiddleware' option is deprecated. Please use the 'setupMiddlewares' option.
    (Use `node --trace-deprecation ...` to show where the warning was created)
    (node:2472) [DEP_WEBPACK_DEV_SERVER_ON_BEFORE_SETUP_MIDDLEWARE] DeprecationWarning: 'onBeforeSetupMiddleware' option is deprecated. Please use the 'setupMiddlewares' option.

- node_modules -> 📁react-scripts -> 📁config -> webpackDevServer.config.js 의 파일을 연다
  onBeforeSetupMiddleware(devServer) {
  // Keep `evalSourceMapMiddleware`
  // middlewares before `redirectServedPath` otherwise will not have any effect
  // This lets us fetch source contents from webpack for the error overlay
  devServer.app.use(evalSourceMapMiddleware(devServer));

  if (fs.existsSync(paths.proxySetup)) {
  // This registers user provided middleware for proxy reasons
  require(paths.proxySetup)(devServer.app);
  }
  },
  onAfterSetupMiddleware(devServer) {
  // Redirect to `PUBLIC_URL` or `homepage` from `package.json` if url not match
  devServer.app.use(redirectServedPath(paths.publicUrlOrPath));

  // This service worker file is effectively a 'no-op' that will reset any
  // previous service worker registered for the same host:port combination.
  // We do this in development to avoid hitting the production cache if
  // it used the same host and port.
  // https://github.com/facebook/create-react-app/issues/2272#issuecomment-302832432
  devServer.app.use(noopServiceWorkerMiddleware(paths.publicUrlOrPath));
  },

해당 코드를

setupMiddlewares: (middlewares, devServer) => {
if (!devServer) {
throw new Error('webpack-dev-server is not defined')
}

    if (fs.existsSync(paths.proxySetup)) {
        require(paths.proxySetup)(devServer.app)
    }

    middlewares.push(
        evalSourceMapMiddleware(devServer),
        redirectServedPath(paths.publicUrlOrPath),
        noopServiceWorkerMiddleware(paths.publicUrlOrPath)
    )
    return middlewares;

},

으로 수정(참고 사이트 : https://velog.io/@sjmh0507/DeprecationWarning-onAfterSetupMiddleware-option-is-deprecated.-Please-use-the-setupMiddlewares-option.-%ED%95%B4%EA%B2%B0%ED%95%98%EB%8A%94-%EB%B0%A9%EB%B2%95)

1. Prettier, ESLint 설치(참고 사이트 : https://tyoon9781.tistory.com/entry/vscode-React-Prettier-ESLint-setting)

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
