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
`git` インストール<br>
`php` のセットアップ<br>
`php-fpm` のセットアップ<br>
`composer` のインストール<br>
`laravel` の新規プロジェクト作成<br>
`nginx` セットアップ<br>

# 各環境で書き換えが必要なところ
下記のファイルの環境変数のみansible-playbookコマンドを叩く前に修正が必要<br>
`./roles/vars/variables.yml`<br>
バーチャルホストを５つまで設定できるようにしてある。

```
# nginxのdefault.confの各設定に適用される
domain: 
  1: example.com
  2: example.com
  3: example.com
  4: example.com
  5: example.com
server_name: 
  1: example.com
  2: example.com
  3: example.com
  4: example.com
  5: example.com
root_path: 
  1: "/var/www/html/{{ list_of_directory[1] }}/web/public"
  2: "/var/www/html/{{ list_of_directory[2] }}/web/public"
  3: "/var/www/html/{{ list_of_directory[3] }}/web/public"
  4: "/var/www/html/{{ list_of_directory[4] }}/web/public"
  5: "/var/www/html/{{ list_of_directory[5] }}/web/public"
list_of_directory: 
  1: dev01
  2: dev02
  3: dev03
  4: dev04
  5: dev05
```