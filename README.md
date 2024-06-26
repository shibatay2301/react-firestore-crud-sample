This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app).
# cloud firestoreの操作を行うReactアプリ
## File tree

<pre>
.root directory
├── README.md         //facebook公式のcreate react appのREADMEを含む
├── build             //実質的なアプリのページ構成や機能をまとめたもの、本アプリではfirebaseのコンパイル先として使用。reate React Appを使用した場合はBuildが作られる
├── firebase.json     //firebaseにおけるHostingの規約を記載
├── node_modules      //npmライブラリの保管ディレクトリ。プロジェクトが依存する npmパッケージが格納される
├── package-lock.json //プロジェクトの依存関係を固定するためのファイルでパッケージのバージョンに制限をかける
├── package.json      //プロジェクトのパッケージのバージョンを記載したjsonファイル
├── public            //デフォルトのReactをダウンロードしたときに作られるファイル。一般的にはこのディレクトリをコンパイルする
├── src                 //作業ディレクトリであり、実質的なアプリのページ構成や機能をまとめたもの
│ ├── App.css           //メインコンポーネントのスタイルシート
│ ├── App.test.tsx      //App.tsxのコンポーネントのUIテストをするファイル。React testing liblaryを使用する
│ ├── App.tsx           //メインコンポーネントの記載ファイル。firebaseとの連携やページ機能について記載されている
│ ├── PrivateRoute.tsx  //ログインした時の認証ユーザーと非認証ユーザーを分けるコンポーネント
│ ├── components        //
│ │ ├── CreateMemo.tsx  //
│ │ ├── LoginWithEmail.tsx  //
│ │ ├── LoginWithGoogle.tsx  //
│ │ ├── MemoList.tsx  //
│ │ ├── SignupWithEmail.tsx  //
│ │ └── UpdateDeleteMemo.tsx  //
│ ├── consts.ts         //アプリケーション全体で使用する定数を定義するファイル。APIのエンドポイントや固定の文字列、色などの定数を指定。
│ ├── contexts.ts       //ReactのコンテキストAPIを使用してグローバルな状態を管理するファイル。例えば、ユーザー情報やテーマ設定などのコンテキストが定義
│ ├── firebase.tsx      //firebaseアプリの初期化とfirestoreへの接続を設定。.envからAPI接続の設定ファイルを呼び出す
│ ├── index.css         //グローバルスタイルシート
│ ├── index.tsx         //アプリケーションのエントリーポイント。ReactDOM を使用して App コンポーネントを HTML のルート要素にマウント
│ ├── logo.svg          //アプリケーションで使用するロゴ画像
│ ├── models.ts         //アプリケーションで使用する TypeScript 型定義を含むファイル
│ ├── pages             //アプリケーションのページコンポーネントを格納するディレクトリ
│ ├── paths.ts          //アプリケーションのルーティングパスを定義するファイル
│ ├── react-app-env.d.ts //TypeScript 用の環境変数定義ファイル。Create React App によって生成される設定ファイル
│ ├── reportWebVitals.ts //ウェブバイタルのパフォーマンス計測を行うファイル。
│ ├── serviceWorker.ts   //サービスワーカーの登録と設定を行うファイル
│ └── setupTests.ts      //テスト環境のセットアップを行うファイル
├── tsconfig.json        //Typescriptの設定ファイル
└── yarn.lock            //yarnを使用した時のプロジェクトの依存関係を固定するためのファイル。npmを使用している場合は必須ではない
</pre>


## 手順書

### "firebaseプロジェクトの作成"
- https://console.firebase.google.comにアクセスして新しいプロジェクトを作成する。  
  →「Authentication」を有効化する<br />
  →「Sign-in method」のタブをクリックして「メール/パスワード」と「Google」の認証を有効する。  
- Webアプリのコンソール画面の歯車マークを押して、プロジェクトの設定からアプリのconfigをメモしておく。
  <pre>
  // Your web app's Firebase configuration  
  const firebaseConfig = {  
    apiKey: "XXXXXXXXX",  
    authDomain: "XXXXXXXXX",  
    projectId: "XXXXXXXXX",  
    storageBucket: "XXXXXXXXX",  
    messagingSenderId: "XXXXXXXXX",  
    appId: "XXXXXXXXX"  
  };
  </pre>
  
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
You can learn more in the [Create React App documentation](https://facebook.github.io/create-react-app/docs/getting-started).<br>
To learn React, check out the [React documentation](https://reactjs.org/).<br>
[参考サイト:React/TypeScriptでFirestoreのCRUD処理を実装する
](https://btj0.com/blog/react/firestore-crud/)

