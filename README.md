# 概要
webサーバーの環境構築に必要な作業をパッケージ化しました。<br>
現時点では、localhostに対して実行することを想定している。<br>
また、証明書取得後にnginxのdefaut.confに追記する部分については、<br>
コメントアウトしてtemplateファイルに記述してある。

## centos7 ansible 導入手順
### インストール
localhostで実行する時はgitをインストール

`yum install git`

`yum install epel-release`

`yum install ansible`

### 確認
`ansible --version`

# ansible 使い方

```
# リポジトリをクローン
git clone ssh://git@165.76.148.171:8890/InfrastructureAsCode/ansible-project.git
# 下記コマンドを実行すると、ジョブが開始される。
cd ansible-project
ansible-playbook main.yml
```
## 実行内容
laravelのHello Worldまで行います。<br>
`git(latest)` インストール<br>
`php(7.3)` のセットアップ<br>
`php-fpm` のセットアップ<br>
`composer` のインストール<br>
`laravel(5.6)` の新規プロジェクト作成<br>
`nginx` セットアップ<br>

# 各環境で書き換えが必要なところ
下記のファイルの環境変数のみansible-playbookコマンドを叩く前に修正が必要<br>
`./roles/vars/variables.yml`<br>
バーチャルホストは、 `./roles/vars/variables.yml` に登録されているhostの数に応じて自動で設定される。

```
# nginxのdefault.confの各設定に適用される
# nginx
hosts:
  - { domain: example.com, server_name: example.com, root_path: "/var/www/html/dev01/web/public", directory: dev01}
  - { domain: example.com, server_name: example.com, root_path: "/var/www/html/dev02/web/public", directory: dev02}
  - { domain: example.com, server_name: example.com, root_path: "/var/www/html/dev03/web/public", directory: dev03}
  - { domain: example.com, server_name: example.com, root_path: "/var/www/html/dev04/web/public", directory: dev04}
  - { domain: example.com, server_name: example.com, root_path: "/var/www/html/dev05/web/public", directory: dev05}

```