# コントリビューション

コントリビューションを歓迎します。

このリポジトリでは、インポートして試しやすく、他の環境にも移植しやすいn8n workflowサンプルを扱います。

## 歓迎する変更

- 新しいn8n workflowサンプル
- 既存workflowのノード設定や式の修正
- セットアップ手順の改善
- 外部サービス連携時の注意点の追加
- ドキュメントの改善

## workflowの方針

workflowを追加・更新するときは、次の方針に合わせてください。

- `YOUR_SLACK_CHANNEL_ID` や `YOUR_GOOGLE_SHEET_ID` のようなプレースホルダーを使う
- n8n credentials、credential ID、webhook ID、個人メール、個人ドメイン、プライベートな接続情報を含めない
- 他のユーザーが自分の環境に合わせて変更しやすい構成にする
- ノード名は処理内容が分かる名前にする
- 外部APIを呼ぶノードでは、必要に応じてリトライやエラーハンドリングを設定する

## n8n export時の注意

n8nからエクスポートしたJSONには、環境固有の情報が含まれることがあります。

workflowを追加する前に、以下のようなフィールドが残っていないか確認してください。

- `credentials`
- `webhookId`
- `shared`
- `projectId`
- `creatorId`
- `versionId`
- `activeVersionId`
- `createdAt`
- `updatedAt`

## ローカルチェック

変更後は、workflow JSONが壊れていないか確認してください。

```bash
node -e "const fs=require('fs'); for (const p of fs.readdirSync('workflows').filter(f=>f.endsWith('.json'))) JSON.parse(fs.readFileSync('workflows/'+p,'utf8')); console.log('workflow json ok')"
```

```bash
docker compose -f docker-compose.example.yml config
```

## Pull Requestに含めるとよい情報

- workflowの目的
- 利用する外部サービス
- 置き換えが必要なプレースホルダー
- 必要なn8n credential
