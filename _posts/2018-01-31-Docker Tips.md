---
layout: post
title: Docker Tips
tags: [Docker, Tips]
---

# Dockerで使える小技集
Dockerを使っていて、「あーこれいいね」と思ったものを集めた
自分のメモを公開しました。

皆様のお役に立てたらいいねしていただけると嬉しいです。

## よく使うオプション一覧
- -a 全ての
- -q IDのみの取得
- --filter フィルターの利用
- -f 強制削除(--force)
- -v 関連付けボリューム(--volumes)

## Dockerの初期化
DockerにはFactory Reset(初期化)なるものがあり
これをすることで全てをまっさらにしてくれます。
全てを抹消しDockerそのものを再インストールします。

<img width="492" alt="スクリーンショット 2017-07-08 22.40.20.png" src="https://qiita-image-store.s3.amazonaws.com/0/177207/eea62762-7196-0254-e129-72aa46006355.png">


### 手順

`Dockerアイコンをクリック > Preferences > Reset > Reset to factory defaults`


## タグの付いてない<none>imageを削除する

タグのついていないDockerのimageの取得方法は以下の通り

{% highlight js %}
$ docker images --filter "dangling=true"
{% endhighlight %}

合わせて削除をするのであれば

{% highlight js %}
$ docker rmi -f $(docker images --filter "dangling=true" -q)
{% endhighlight %}

ちょっと長ったらしいですが…

{% highlight js %}
$ docker rm -f $(docker ps -aq) & docker rmi -f $(docker images -qf "dangling=true") & docker system prune
{% endhighlight %}

なんかしてみるといいかもですね。
.bashrcなんかにaliasとして追加しておくのもありかもしれません

ちなみにprocessでも下記の通りでできます

{% highlight js %}
$ docker rm -f $(docker ps -aq)
{% endhighlight %}

## あれこれ一括で削除をする

- 停止中のコンテナ全て
- 紐ついていないVOLUME全て
- 紐ついていないネットワーク全て
- 紐ついていないイメージ全て

を一括で削除できるコマンドが

{% highlight js %}
$ docker system prune
{% endhighlight %}

{% highlight js %}
WARNING! This will remove:
	- all stopped containers
	- all volumes not used by at least one container
	- all networks not used by at least one container
	- all dangling images
Are you sure you want to continue? [y/N]
{% endhighlight %}

これら消しちゃうけど本当に大丈夫？続けてもいい？
的な感じのメッセージが来るので`y`でokです

### GUIでもいける!!!!

`Dockerアイコンをクリック > Preferences > Reset > Remove all data`

<img width="492" alt="スクリーンショット 2017-07-08 22.40.20.png" src="https://qiita-image-store.s3.amazonaws.com/0/177207/e01ad41f-54a0-8156-366c-2d6e25962529.png">

## Railsコンテナを立ち上げてコンテナに入らずにコマンドを打つ！

{% highlight js %}
$ docker-compose run {service} rake routes
{% endhighlight %}

とか

{% highlight js %}
$ docker-compose run --rm app rake db:migrate
{% endhighlight %}

とか

{% highlight js %}
$ docker-compose run --rm app rails generate controller user
{% endhighlight %}

ちなみにrun系のオプション一覧はこちらです

http://docs.docker.jp/compose/reference/run.html

## コンテナ内のファイルをコピーする

{% highlight js %}
$ docker cp {コンテナID} or {プロセス名} :{パス} ローカルの保存したい場所
{% endhighlight %}

{% highlight js %}
$ docker cp b5e5bab3c242:/etc/httpd/conf/httpd.conf $HOME/Downloads/
{% endhighlight %}

もちろんコンテナ内へローカルからコピーも可能です

httpd.confの上書き

{% highlight js %}
$ docker cp $HOME/Downloads/httpd.conf b5e5bab3c242:/etc/httpd/conf/httpd.conf
{% endhighlight %}
