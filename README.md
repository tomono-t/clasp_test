# GAS開発環境

## docker環境構築

```
cd docker

docker-compose build --no-cache
```

## docker起動

```
docker-compose up -d
```

## Google Apps Script API有効化

https://script.google.com/u/0/home/usersettings


## clasp 操作

```
docker-compose exec clasp_test bash
```

### ログイン

```
clasp login --no-localhost
```

### ログアウト

```
clasp logout
```

### 新規プロジェクト create

ローカルでプロジェクトを作成し、Google Driveにpush

```
mkdir /usr/src/app/projects/{PROJECT_NAME}

cd /usr/src/app/projects/{PROJECT_NAME}

# typescriptを使いたい場合
npm init
npm install @types/google-apps-script

clasp create --title {PROJECT_NAME} --parentId {DRIVE_FOLDER_ID} --rootDir ./
```

DRIVE_FOLDER_IDはGoogleDriveのリソースIDを記述する
ex. https://drive.google.com/drive/folders/{DRIVE_FOLDER_ID}


スプレッドシートを作りたい場合、
create時に`--type sheets` で作れるが、parentIdが効かなくなるので
後述のcloneをする方法で取り込むか、
シート作成後スクリプトだけ作成してparentIdにシートのidを入れて作成する

### 既存プロジェクト clone

Google Driveのプロジェクトをローカルに配置

```
cd /usr/src/app/projects/
mkdir {PROJECT_NAME}
cd {PROJECT_NAME}
clasp clone {PROJECT_ID}
```

PROJECT_IDはGASの以下リソースIDを記述する

ex. https://script.google.com/u/0/home/projects/{PROJECT_ID}/edit



### GAS push

ローカルの変更をGoogle Driveにpush

```
cd /usr/src/app/projects/{PROJECT_NAME}

clasp push
```

### webエディタ表示

```
clasp open
```


### ローカルで実行

GCPのプロジェクトと紐付ける必要性あり

https://t-cr.jp/memo/3ad17a27aa48af71

また、ディレクトリ構造をネストさせているとログイン情報(.clasp.json)の参照先がおかしくなる

https://github.com/google/clasp/issues/92

必要性が出てきたら検討


## 参考
https://zenn.dev/marusho/scraps/3579309aabf5eb
