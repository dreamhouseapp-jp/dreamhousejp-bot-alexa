# Alexa 用 DreamHouse ボット

DreamHouse サンプルアプリケーションで使用する、Salesforce ベースの Alexa スキルです。

スキルのインスタンスを作成するには、以下の手順を実行します。


### ステップ 1：DreamHouse アプリをインストールする

DreamHouse サンプルアプリケーションをまだインストールしていない場合は、[この手順](http://dreamhouseappjp.io/installation/)を実行してインストールします。

### ステップ 2：接続アプリケーションを作成する

Salesforce 接続アプリケーションをまだ作成していない場合は、以下の手順を実行して作成します。

1. Salesforce の［設定］で、クイック検索ボックスに「**アプリ**」と入力して［**アプリケーション**］リンクをクリックします。

1. ［**接続アプリケーション**］セクションで、［**新規**］をクリックし、次のように接続アプリケーションを定義します。

    - 接続アプリケーション名：DreamhouseJpAlexaApp（または任意の名前）
    - API 参照名：DreamhouseJpAlexaApp
    - 取引先責任者メール：自分のメールアドレスを入力します。
    - OAuth 設定の有効化：チェックボックスをオンにします。
    - コールバック URL：http://localhost:8200/oauthcallback.html
    - 選択した OAuth 範囲：フルアクセス（full）
    - ［**保存**］をクリックします。

### ステップ 3：DreamHouse Alexa スキルをデプロイする

1. [Heroku ダッシュボード](https://dashboard.heroku.com/)にログインしていることを確認します。
1. 下のボタンをクリックして、Alexa スキルを Heroku にデプロイします。

    [![Deploy](https://www.herokucdn.com/deploy/button.png)](https://heroku.com/deploy)

1. 以下の通りに環境変数を設定します。

    - **SF_CLIENT_ID**：Salesforce 接続アプリケーションのコンシューマキーを入力します。
    - **SF_CLIENT_SECRET**：Salesforce 接続アプリケーションのコンシューマの秘密を入力します。
    - **SF_USER_NAME**：Salesforce 統合ユーザーのユーザー名を入力します。
    - **SF_PASSWORD**：Salesforce 統合ユーザーのパスワードを入力します。

### ステップ 4：Amazon AWS アカウントを作成する

まだ AWS アカウントを取得していない場合は、以下の手順を実行して作成します。

1. ブラウザを開き、AWS コンソール（http://aws.amazon.com/）にアクセスします。

1. ［**まずは無料で始める**］をクリックします。

### ステップ 5：スキルを構成する

1. Alexa コンソール（https://developer.amazon.com/edw/home.html）にログインします。

1. ［**Alexa Skills Kit**］の［**Get Started**］をクリックします。

1. ［**Add New Skill**］ボタンをクリックします。

1. ［**Skill Information**］画面で次のように入力します。

    - Skill Type：**Custom Interaction Model**
    - Name：**DreamHouse**
    - Invocation Name：**dreamhouse**

1. ［**Interaction Model**］画面で次のようにします。    
    - 次の JSON ドキュメントをコピーして［**Intent Schema**］ボックスに貼り付けます。

        ```
        {
        "intents": [
         {
           "intent": "SearchHouses"
         },
         {
           "intent": "AnswerCity",
           "slots": [
             {
               "name": "City",
               "type": "AMAZON.US_CITY"
             }
           ]
         },
         {
           "intent": "AnswerNumber",
           "slots": [
             {
               "name": "NumericAnswer",
               "type": "AMAZON.NUMBER"
             }
           ]
         },
         {
           "intent": "Changes",
           "slots": [
             {
               "name": "City",
               "type": "AMAZON.US_CITY"
             }
           ]
         },
         {
           "intent": "AMAZON.HelpIntent"
         }
        ]
        }
        ```
    - 次のテキストをコピーして［**Sample Utterances**］ボックスに貼り付けます。

        ```
        SearchHouses for listings
        SearchHouses to search for houses
        SearchHouses what's for sale
        SearchHouses what is for sale
        AnswerCity {City}
        AnswerNumber {NumericAnswer}
        Changes for changes
        Changes for price changes
        ```

1. ［**Configuration**］画面で、［**HTTPS**］を選択し、ステップ 3 でデプロイした Heroku アプリの URL を入力し、末尾に /dreamhouse パスを付加します。次に例を示します。

     ```
     https://myalexabot.herokuapp.com/dreamhouse
     ```

1. ［**SSL certificate**］画面で、［**My development endpoint is a subdomain of a domain that has a wildcard certificate from a certificate authority**］を選択します。

1. これで、DreamHouse スキルをテストする準備が整いました。  
