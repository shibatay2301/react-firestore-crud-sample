This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app).

### "firebaseプロジェクトの作成"
- https://console.firebase.google.comにアクセスして新しいプロジェクトを作成する。  
  →「Authentication」を有効化する<br />
  →「Sign-in method」のタブをクリックして「メール/パスワード」と「Google」の認証を有効する。  
  →
- Webアプリのコンソール画面の歯車マークを押して、プロジェクトの設定からアプリのconfigをメモしておく。  
  // Your web app's Firebase configuration  
  const firebaseConfig = {  
    apiKey: "XXXXXXXXX",  
    authDomain: "XXXXXXXXX",  
    projectId: "XXXXXXXXX",  
    storageBucket: "XXXXXXXXX",  
    messagingSenderId: "XXXXXXXXX",  
    appId: "XXXXXXXXX"  
  };

### "React環境におけるdeploy"
- 自身の開発環境にfirebase SDKをインストールする
  `npm install firebase`
- 事前準備：アプリを作成してワークするか確認する
  `npm create vite@latest <react-firestore-crud-sample
> -- --template react-ts　　
    cd <sample-app>  　
    npm install　　
    npm run dev`
  ➜  Local:   http://127.0.0.1:5174/　　
  ➜  Network: use --host to expose  
  にアクセスして初期画面の確認をして、Ctrl+Cで停止する  
  ディレクトリは消去して構わない  
- githubの現在のファイルをダウンロードして、ルートディレクトリ内に移動する  
- アプリのページ構成のために以下のコマンドを実行する  
  `cd react-firestore-crud-sample`  
  `npm install react-router-dom firebase `  
- firebaseで作成したアプリのconfig情報を.env内に記載しておく。<>内は各アプリの情報に書き換える  
  `touch .env`  
  `   // .env  
  REACT_APP_FIREBASE_KEY=<apiKey>  
  REACT_APP_FIREBASE_DOMAIN=<authDomain>  
  REACT_APP_FIREBASE_DATABASE=<databaseURL>  
  REACT_APP_FIREBASE_PROJECT_ID=<projectId>  
  REACT_APP_FIREBASE_STORAGE_BUCKET=<storageBucket>  
  REACT_APP_FIREBASE_SENDER_ID=<messagingSenderId>`
  
    
  

### `yarn test`

Launches the test runner in the interactive watch mode.<br />
See the section about [running tests](https://facebook.github.io/create-react-app/docs/running-tests) for more information.

### `yarn build`

Builds the app for production to the `build` folder.<br />
It correctly bundles React in production mode and optimizes the build for the best performance.

The build is minified and the filenames include the hashes.<br />
Your app is ready to be deployed!

See the section about [deployment](https://facebook.github.io/create-react-app/docs/deployment) for more information.

### `yarn eject`

**Note: this is a one-way operation. Once you `eject`, you can’t go back!**

If you aren’t satisfied with the build tool and configuration choices, you can `eject` at any time. This command will remove the single build dependency from your project.

Instead, it will copy all the configuration files and the transitive dependencies (webpack, Babel, ESLint, etc) right into your project so you have full control over them. All of the commands except `eject` will still work, but they will point to the copied scripts so you can tweak them. At this point you’re on your own.

You don’t have to ever use `eject`. The curated feature set is suitable for small and middle deployments, and you shouldn’t feel obligated to use this feature. However we understand that this tool wouldn’t be useful if you couldn’t customize it when you are ready for it.

## Learn More

You can learn more in the [Create React App documentation](https://facebook.github.io/create-react-app/docs/getting-started).

To learn React, check out the [React documentation](https://reactjs.org/).
