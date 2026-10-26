# Singularity Colab Notebook 2種類

添付のFastH3 V2＋新VAE版を基に、Singularity V2用とv1.3用を別ファイルで作成しました。元のDownloadsファイルは変更していません。

| Notebook | 使用する本体 | 共通設定 |
|---|---|---|
| Singularity_V2_NewVAE_Colab_Driveless.ipynb | V2 pruned INT8 | 新映像VAE・20回・Euler・通常Attention |
| Singularity_V1_3_NewVAE_Colab_Driveless.ipynb | v1.3 pruned INT8 | 新映像VAE・20回・Euler・通常Attention |

Attentionは映像内の情報同士の関係を計算する処理です。VSAという計算を間引く機能は、両方とも無効です。Turbo LoRAという少ない回数向けの追加モデルも入れていません。動画shift12／音声shift3、計算の進み方の数列は、今回のローカル比較で使った20回設定を引き継いでいます。作者唯一の推奨値ではありません。

## 始め方

1. 使用したいipynbをPCへ保存し、[Google Colab](https://colab.research.google.com/)の「ファイル」→「ノートブックをアップロード」から読み込みます。
2. 古いFastH3版と実行環境を共用せず、新しいGPUランタイムを使います。GPUメモリ約24GB以上を想定します。T4は対象外です。メモリの多いA100級から小さく試してください。機種ごとの実機成功は未確認です。
3. Colab左の鍵マークで `PINGGY_TOKEN` を設定し、このNotebookからのアクセスを許可します。元の接続コードは `pro.pinggy.io` を使うため、利用できるトークン・契約をPinggy側で確認してください。トークンを本文へ貼る必要はありません。
4. 「起動」のコードセルを実行します。モデルを取得し、ComfyUIを起動します。初回は大きなファイルの取得と導入のため時間がかかります。
5. 実行ログに出るComfyUI接続ボタンから画面をひらき、User workflowsの `Singularity_V2_NewVAE` または `Singularity_V1_3_NewVAE` 内の `r2v_app` を選びます。
6. 最初は0.4MP・5秒で、参照画像1と文章を設定して生成します。予備画像・音声・動画は、ノード画面で接続したものだけが有効です。
7. Driveを使わない初期設定では、動画は `/content/ComfyUI/output` に一時保存されます。ランタイム終了前にPCへダウンロードしてください。Drive保存を使う場合は、元の `use_google_drive` と `enable_gdrive_output` を両方オンにします。モデルのDrive保存は別の `persist_models_to_drive` 設定です。

文章だけから生成するT2V、開始画像から生成するI2V、参照素材を使うR2V、入力欄を整理したR2Vアプリ版を両Notebookに同梱しています。元の入力画面とサンプル画像取得を維持しています。

## 検査済みの範囲

- 元Notebookのバイト単位の不変を確認。
- 両NotebookのJSON構造とPython構文を検査。Colab特有の `!pip` と `%cd` の行は、実行せず構文検査時だけ置き換え。
- 内部GPU確認用プログラムのPython構文も検査。
- 合計8グラフについて全接続の両端、モデル名、新VAE、Euler、動画12／音声3、20回を表す21個の数値を検査。
- VSAノードはmode4（入力をそのまま通すバイパス）に設定。元のVSA専用GPUテストを通常Attentionのテストへ変更。
- 配列の保存値と名前付きの保存値を両方更新し、アプリの6入力欄と1.0MPを含む解像度選択を維持。
- 作者の公開メタデータから、両モデルの固定版URL・サイズ・SHA256を確認。大容量モデルは今回再取得していません。Colab側では元のサイズ検査を維持しますが、ハッシュの全自動照合は行いません。

**Colab上でのインストール完了・トンネル接続・実際の動画生成は未検証です。** 起動時の小規模GPUテストだけで、大きなモデルの読み込みや長尺生成成功を保証するものではありません。まず短尺で試すための派生版です。

## 配布物と出所

- `notebooks/`: V2用とv1.3用のColab Notebook。
- `workflows/`: 各Notebookに埋め込んだ4種類のComfyUIワークフローを単体JSONでも配布。
- `docs/validation-report.json`: 構文・設定・接続の検査範囲。Colab実機は未検証。
- [元のFastH3 V2 Colab](https://github.com/zasuko/zasuko-fasth3-colab)
- [Singularity作者](https://huggingface.co/WarmBloodAban/Minimax-h3_Singularity)
- [共通VAE等](https://huggingface.co/Comfy-Org/MiniMax-H3)
- [元モデルの利用条件](https://huggingface.co/MiniMaxAI/MiniMax-H3/blob/main/LICENSE)

モデル本体は含めず、Notebookから配布元の固定版へアクセスします。
