# セットアップガイド

このガイドでは、ローカル環境でn8nを起動し、`workflows/` 配下のサンプルworkflowをインポートする手順を説明します。

## 必要なもの

- Docker Desktop または Docker Engine
- n8nで使う各サービスのアカウント
- Slack workspace
- Googleアカウント
- Ollamaを使う場合はOllama本体

## 1. リポジトリを取得

```bash
git clone https://github.com/yun434/n8n-ai-workflow-starter-ja.git
cd n8n-ai-workflow-starter-ja
```

## 2. 環境変数を作成

```bash
cp .env.example .env
```

`.env` を開き、必要に応じて値を変更します。

最低限、ローカルで試すだけなら `POSTGRES_PASSWORD` を任意の値に変えてください。

Slack slash command の署名検証を使う場合は、Slack app の signing secret を設定します。

```text
SLACK_SIGNING_SECRET=replace-with-your-slack-signing-secret
```

## 3. n8nを起動

```bash
docker compose -f docker-compose.example.yml up -d
```

起動後、ブラウザで次のURLを開きます。

```text
http://localhost:5678
```

## 4. n8n credentialsを設定

使うworkflowに応じて、n8nのCredentials画面から認証情報を作成します。

| Workflow | Required credentials |
| --- | --- |
| `gmail-ai-summary-to-slack-sheets.n8n.json` | Gmail, Slack, Google Sheets, Ollama |
| `slack-task-to-google-tasks-calendar.n8n.json` | Slack, Google Tasks, Google Calendar |
| `morning-slack-secretary.n8n.json` | Google Calendar, Google Tasks, Slack |
| `slack-monitor-ai-to-sheets.n8n.json` | Slack, Google Sheets, Ollama |
| `slack-daily-digest-starter.n8n.json` | Slack |

## 5. workflowをインポート

n8nの画面で次の順に操作します。

1. Workflowsを開く
2. Import from Fileを選ぶ
3. `workflows/` 配下の `.n8n.json` ファイルを選ぶ
4. ノードごとにcredentialを割り当てる
5. プレースホルダー値を自分の環境に合わせて置き換える

代表的なプレースホルダー:

```text
YOUR_SLACK_CHANNEL_ID
YOUR_SLACK_ALERT_CHANNEL_ID
YOUR_GOOGLE_SHEET_ID
YOUR_GOOGLE_CALENDAR_ID
replace-with-your-channel-name
replace-with-your-sheet-name
replace-with-your-calendar-name
```

## 6. Ollamaを使うworkflow

Ollamaノードを使うworkflowでは、n8nからOllamaへ接続できる必要があります。

Docker上のn8nからホスト側のOllamaへ接続する場合は、一般的に次のURLを使います。

```text
http://host.docker.internal:11434
```

モデル例:

```bash
ollama pull llama3.2
```

## 7. 動作確認

workflowを有効化する前に、Manual executionで各ノードを確認してください。

- SlackチャンネルIDが正しいか
- Google Sheet IDが正しいか
- Google Calendar IDが正しいか
- Ollama credentialが接続できるか
- Slack slash command のRequest URLがn8nのWebhook URLになっているか

## 8. 停止

```bash
docker compose -f docker-compose.example.yml down
```
