This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app).

### Filetree

### File tree

<pre>
.<root directory>
├── README.md //[create react appのREADMEを含む](https://github.com/facebook/create-react-app)
├── build //実質的なアプリのページ構成や機能をまとめたもの、本アプリではfirebaseのコンパイル先として使用
├── firebase.json //firebaseにおけるHostingの規約を記載
├── node_modules //npmライブラリ
├── package-lock.json
├── package.json
├── public //一般的にはこのディレクトリをコンパイルする
├── src //作業ディレクトリであり、実質的なアプリのページ構成や機能をまとめたもの
├── tsconfig.json
└── yarn.lock
</pre>


## 手順書

### "firebaseプロジェクトの作成"
- https://console.firebase.google.comにアクセスして新しいプロジェクトを作成する。  
  →「Authentication」を有効化する<br />
  →「Sign-in method」のタブをクリックして「メール/パスワード」と「Google」の認証を有効する。  
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

      npm install firebase
- 事前準備：アプリを作成してワークするか確認する
      
      npm create vite@latest <sample-app> -- --template react-ts
  
      cd <sample-app>
  
      npm install
  
      npm run dev  
  ➜  Local:   http://127.0.0.1:5174/  
  ➜  Network: use --host to expose  
  にアクセスして初期画面の確認をして、Ctrl+Cで停止する  
  ディレクトリは消去して構わない  
- githubの現在のファイルをダウンロードして、ルートディレクトリ内に移動する  
- アプリのページ構成のために以下のコマンドを実行する
  
       cd react-firestore-crud-sample
  
      npm install react-router-dom firebase   
- firebaseで作成したアプリのconfig情報を.env内に記載しておく。<>内は各アプリの情報に書き換える

      touch .env  
     // .env  
  REACT_APP_FIREBASE_KEY=<apiKey>  
  REACT_APP_FIREBASE_DOMAIN=<authDomain>  
  REACT_APP_FIREBASE_DATABASE=<databaseURL>  
  REACT_APP_FIREBASE_PROJECT_ID=<projectId>  
  REACT_APP_FIREBASE_STORAGE_BUCKET=<storageBucket>  
  REACT_APP_FIREBASE_SENDER_ID=<messagingSenderId>  
-  連携するアプリをbuildファイルにまとめる

        npm run build  
-  firebaseとReactのwebアプリの連携を行う
    
        firebase init  
   →featureの選択は、spaceキーでHostingを選択  
    ? Which Firebase features do you want to set up for this directory? Press Space to select features, then Enter to confirm your choices.  
     (Press <space> to select, <a> to toggle all, <i> to invert selection, and <enter> to proceed)  
    ❯◯ Hosting: Configure files for Firebase Hosting and (optionally) set up GitHub Action deploys
  
   →build、singleページではない、github連携なしで進める  
    ? What do you want to use as your public directory? build  
    ? Configure as a single-page app (rewrite all urls to /index.html)? No  
    ? Set up automatic builds and deploys with GitHub? No  
- deployしてwebアプリにする  
  
      firebase deploy  
  
  ✔  Deploy complete!  

    Project Console: https://console.firebase.google.com/project/<app0304.web.app>/overview  
    Hosting URL: https://<app0304.web.app>  

### "reference"
You can learn more in the [Create React App documentation](https://facebook.github.io/create-react-app/docs/getting-started).
To learn React, check out the [React documentation](https://reactjs.org/).
