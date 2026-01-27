---
layout: bootstrap
title: Privacy Policy
permalink: /apps/overlaytimer/privacy/
hide: true
---

# プライバシーポリシー（OverlayTimer）

施行日：2026-01-28

本アプリ「OverlayTimer（オーバーレイタイマー）」における利用者情報の取扱いについて定めます。

## 1. 収集する情報
本アプリは、氏名・メールアドレス・電話番号等の個人情報を収集しません。
本アプリは、以下の設定情報を端末内（ローカル）に保存する場合があります。

- 設定した時刻（例：12:34:56:789）
- タイムゾーン（JST/UTC）
- 音・通知の ON/OFF

これらは端末内にのみ保存され、開発者が外部で取得することはありません。

## 2. 通信について
本アプリは、時刻同期（NTP等）により現在時刻の精度を高める目的でインターネット通信を行うことがあります。
ただし、利用者の個人情報を送信する設計にはしていません。

## 3. 使用する権限と目的
- SYSTEM_ALERT_WINDOW：他アプリ上にオーバーレイ表示を行うため
- FOREGROUND_SERVICE：オーバーレイ機能を安定動作させるため
- POST_NOTIFICATIONS（Android 13+）：通知ONの場合に通知を表示するため
- INTERNET：時刻同期（NTP等）のため

## 4. 第三者提供
本アプリは、利用者情報を第三者へ提供しません。

## 5. 第三者サービス
本アプリは、広告SDK・解析SDK等の第三者サービスを利用しません（利用する場合は本ポリシーを更新します）。

## 6. 改定
必要に応じて改定されることがあります。改定後は本ページにて告知します。

## 7. お問い合わせ
- GitHub Issues： https://github.com/tunagohan/tunagohan.github.io/issues
