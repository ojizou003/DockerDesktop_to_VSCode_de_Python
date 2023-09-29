# 「Docker Desktop for Win/Mac と VSCode でつくるクリーンな開発環境構築入門(Python 版)」 太田和樹 著

2023/9/27~9/29  

## 環境構築

仮想環境の作成  
```python -m venv 仮想環境名```

仮想環境の有効化  
```仮想環境名\Scripts\activate```

仮想マシン  

コンテナー技術  
WSL2 ..Windows Subsystem for Linux  
コンテナーは、アプリケーションの依存関係を解消するための技術  

WSL2のインストール  
カーネル ..Linuxの基本機能  
ディストリビューション ..カーネルとその上で動作するソフトウェアを組み合わせたもの  

Docker Desktop のインストール  

VS Code のインストール  

Git Hub アカウントの登録  

Git のインストールと環境設定  

## Docker 入門

Docker イメージ ..コンテナーのひな型となる  
Docker イメージには以下のような内容が含まれる  

- Linux ディストリビューション ..Debian、alpineなど
- アプリケーション ..Pythonなど
- プログラムや設定ファイル ..Pythonのソースコードなど
- コンテナー実行時に起動するプロセス ..DjangoのWebサーバーの起動など

Dockerfile ..Docker イメージの設計書(テキストファイル)  
Dockerfile には以下のような内容が含まれる  

- ベースとなるイメージ
- ビルドするときに実行するコマンド ..ライブラリのインストールなど
- コンテナーを外部公開する際のポート番号
- ファイルのコピーやドライブのマウント
- コンテナー起動時に実行するコマンド
Dockerfile から Docker イメージを作成することを「ビルドする」という  
ベースとなるイメージは DockerHub や GitHub で公開されている  

イメージレジストリ ..Docker イメージを共有する場所  

コンテナー ..イメージを実体化したもの  

Docker イメージに関するコマンド  
docker image

- docker image ls ..イメージの一覧を表示
- docker image rm [オプション] イメージID
- docker image prune [オプション] ..不要なイメージを一括削除
- docker image pull [オプション] イメージ名:タグ ..DockerHub からイメージを取得
- docker image push
- docker image build
- docker image inspect
- docker image history
- docker image tag

コンテナーに関するコマンド  

- docker container ls ..コンテナーの一覧を表示
- docker container run ..コンテナーの作成と起動
- docker container logs ..コンテナーのログを取得
- docker container inspect ..コンテナーの詳細情報を取得
- docker container stats ..コンテナーのリソースの使用状況を表示
- docker container stop  ..コンテナーの停止d
- docker container create ..コンテナーの作成
- docker container start ..コンテナーの起動
- docker container restart ..コンテナーの再起動
- docker container attach ..コンテナーに接続
- docker container exec ..コンテナーに接続
- docker container rm ..コンテナーを削除
- docker container prune ..停止中のコンテナーを一括削除  

volume に関するコマンド  

- docker volume create
- docker volume ls
- docker volume rm
- docker volume prune

Dockerfile  
Dockerfileには以下のような内容を記述する  

- FROM ..ベースイメージの指定
- LABEL ..情報(メタデータ)の付与
- RUN ..ビルド時に実行するコマンド
- EXPOSE ..コンテナーを外部公開する際のポート番号
- COPY ..ファイルやフォルダをコンテナーにコピー
- ADD .. 〃(zipの解凍や外部URLからのコピー)
- CMD ..コンテナーを起動するときに1回だけ実行するコマンド
- ENTRYPOINT ..runコマンドで実行するコマンド
- ARG ..一時変数
- ENV ..環境変数
- USER ..ユーザの切替
- WORKDIR ..作業フォルダの指定

VS Code の拡張機能「Docker」のインストール  

Dockerfile からイメージをビルド  
```docker image build [オプション] Dockerfileのパス```

Dockerfile の記述例(2)：RUN コマンドの使用  

Dockerfile の記述例(3)：CMD コマンドの使用  

CMDとENTRYPOINTの違い  
ENTRYPOINT は、コンテナー起動時に実行するプロセスを指定する  
CMD は、コンテナー起動時に実行するコマンドを指定する  

USER ..ユーザーの切替を行うコマンド  

DockerHub へのイメージの登録  
> docker login  
> docker push アカウント名/イメージ名:タグ  

コンテナーのネットワーク  
同じホスト上で2つのコンテナーが起動している場合は、コンテナー同士はコンテナー名でアクセスできる  
ブリッジ ..コンテナーが属するネットワークとホスト側のネットワークを中継する  

Docker Compose  
Docker Compose は、コマンドを入力する代わりに「compose.yml」という設定ファイルを用いて、コンテナのビルドや実行、停止をおこなうためのツール  
コンテナーは1アプリケーション1コンテナーが基本 -> 複数のコンテナーを利用する場面が多い  
Docker Compose を使うことでコマンドの入力ミスを防ぎ、複数のコンテナの管理が容易になる  
コマンドには以下のようなものがある  

- docker compose up ..サービスの起動/再起動  
- docker compose exec ..コマンドの実行  
- docker compose logs ..ログの表示
- docker compose ps ..コンテナーの一覧を表示
- docker compose stop ..サービスの停止
- docker compose start ..サービスの開始
- docker compose down ..サービスの停止とコンテナーの削除
- docker compose build ..イメージのビルド
- docker compose create ..コンテナーの作成
- docker compose rum ..サービスのコンテナーを起動

compose.ymlには以下のような内容を記述する  

- image: ..ベースイメージ/ビルドイメージ名
- container_name: ..コンテナー名
- expose: ..公開するポート番号
- ports: ..ホストに公開するポートの番号
- environment: ..環境変数
- build: ..Dockerfileの格納先
- working_dir: ..作業ディレクトリ
- volumes: ..ボリュームのマウント/名前付きボリューム
- depends_on: ..サービスの依存関係
- stdin_open: ..標準入力の受付
- tty: ..疑似TTY端末の割当
- command: ..デフォルトのコマンドを上書き

Docker Dashboard  
Docker Dashboard は、Dockerの GUI ツール  

Docker Explorer  
VS Code の Docker Explorer でも GUI による操作ができる  

## VS Code と Docker による開発環境の構築

必要となる VS Code の拡張機能  
Remote Development ..コンテナーに接続し、ローカル環境と同等に開発を行うための拡張機能  

Git 管理  

別のフォルダを開き、Ctrl＋Shift＋Pのコマンドパレットでgitclone  
リモートリポジトリのURLを貼り付け  
クローン先のフォルダの指定  
コンテナーで再度開くをクリック  

機械学習(Scikit-learn)SVMによる分類モデル  
Scikit-learnで機械学習のプログラミングを行うための環境のポイント  

- logging の導入
- git 管理の除外設定  
- タイムゾーンを日本に設定
- 一般権限のユーザーの追加

機械学習(TensorFlow) 転移学習とモデルの保存(IntelCPU/TensorFlow イメージ版)  

機械学習(TensorFlow) 転移学習とモデルの保存(IntelCPU/Python イメージ版)  

機械学習(TensorFlow) 転移学習とモデルの保存(GPU 対応版)  

スクレイピング(BeautifulSoup)  

Django  

Flask  

Jupyter Notebook  

Jupyter Lab  
