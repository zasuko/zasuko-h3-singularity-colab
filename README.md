# Singularity Colab：V2 / v1.3＋新VAE

ざすこ（道草 雑草子）が用意した、MiniMax H3系 **Singularity V2** と **Singularity v1.3** 用のGoogle Colab Notebookです。

[FastH3 Colab](https://github.com/zasuko/zasuko-fasth3-colab) と並ぶ専用リポジトリです。本体・設定を取り違えず、モデルごとに別の新GPUランタイムで使用してください。

## Colabでひらく

| モデル | 保存方式 | 起動 |
|---|---|---|
| Singularity V2＋新INT8映像VAE | Driveレス・Colab一時ディスクへ取得 | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/zasuko/zasuko-h3-singularity-colab/blob/main/notebooks/Singularity_V2_NewVAE_Colab_Driveless.ipynb) |
| Singularity v1.3＋新INT8映像VAE | Driveレス・Colab一時ディスクへ取得 | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/zasuko/zasuko-h3-singularity-colab/blob/main/notebooks/Singularity_V1_3_NewVAE_Colab_Driveless.ipynb) |

**検証範囲：Notebook構文と同梱8ワークフローの設定・接続をローカル検査済み。Colabでのインストール・接続・実際の動画生成は未検証です。** ローカルの別環境での比較実績を、Colabでの動作・速度保証へ転用しません。

## 最初の使い方

1. モデルの利用地域・用途と、Colabの契約・計算単位残高を確認します。H3のCommunity Licenseは **EU・英国・韓国・米国を適用対象から除外**しています。日本からのアクセスだけでColabの実行先も日本になるとは判断できません。必要な条件や許諾が確認できる環境で使用してください。
2. 上のボタンでNotebookをひらき、新しいGPUランタイムを選びます。約24GB以上のGPUメモリを想定し、22GiB未満とT4は停止します。より大きなメモリを持つGPUでも成功を保証するものではありません。
3. Colab左の鍵マークで `PINGGY_TOKEN` を登録し、Notebookからのアクセスを許可します。接続は `pro.pinggy.io` を使用するので、対応するPinggyトークンと契約を確認してください。
4. 起動セルを実行し、ログに出るComfyUI接続ボタンへ進みます。
5. User workflows > `Singularity_V2_NewVAE` または `Singularity_V1_3_NewVAE` の `r2v_app` を選び、まず0.4MP・5秒・参照画像1枚から試します。
6. 動画をPCへ保存します。Driveレスの初期設定では、Colabのランタイム終了でモデルと出力が消えます。Driveへの出力保存・モデル再利用はNotebook内で任意設定できます。

[詳しい使い方](docs/USAGE.md) ／ [検査結果](docs/validation-report.json) ／ [利用条件の注意](MODEL_LICENSE_NOTICE.md)

## 同梱設定

| 項目 | V2 | v1.3 |
|---|---|---|
| 本体 | `Minimax-h3_Singularity_ref2va_v2_pruned_int8.safetensors` | `Minimax-h3_Singularity_ref2va_Pruned_v1.3_int8.safetensors` |
| 映像VAE | `minimax_h3_video_vae_int8_convrot.safetensors` | 同左 |
| 計算 | Euler・20ステップ | 同左 |
| shift | 動画12／音声3 | 同左 |
| VSA | 無効（BlockSparseAttentionノードをバイパス） | 同左 |
| Turbo LoRA | なし | なし |

20回は今回のローカル比較で用いた開始設定です。作者唯一の推奨値を意味しません。FastH3の8回/VSA用の値は流用していません。

- T2V（文章）、I2V（開始画像）、R2V（参照素材）、R2Vアプリ版の4画面を各Notebookに同梱。
- 元NotebookのPinggy、Colabシークレット、任意Drive保存、サンプル画像を継承。
- ComfyUI v0.36.0 / `ee71d5c4993f29086b27fde1629a945ae48425bf` を固定。
- モデル本体も固定revisionから取得。公開SHA256は検査結果に記録（Colabでの全ファイル自動ハッシュ照合は実装していません）。
- ワークフロー単体JSONは [workflows](workflows) から取得できます。

## 配布元・注意

- [Singularity作者配布](https://huggingface.co/WarmBloodAban/Minimax-h3_Singularity)
- [共通VAE・文章理解モデル](https://huggingface.co/Comfy-Org/MiniMax-H3)
- [元モデルのCommunity License](https://huggingface.co/MiniMaxAI/MiniMax-H3/blob/main/LICENSE)
- [Colabの制限](https://research.google.com/colaboratory/faq.html)
- [Pinggy](https://pinggy.io/)

SingularityページのApache-2.0表記だけで元モデルの条件が消えるとは判断しないでください。無料・残高なしのColabで外部Web画面を無制限に使える案内ではありません。クラウドGPU・接続サービス等の費用は別途発生する場合があります。

このリポジトリはモデルの巨大な重みを再配布せず、Notebookと操作設定を提供します。トークンをNotebook本文や公開した出力へ貼り付けないでください。

制作：[AIみちくさch](https://www.youtube.com/channel/UC84fyKjiilxssZVxhE_RiaA) ／ ざすこ（道草 雑草子）

最終確認：2026-10-26。追加の実機検証後に検証範囲を更新します。
