# centos7 ansible 導入手順
### インストール
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

## 実行内容
`php` セットアップル<br>
`composer` のセットアップ<br>
`git` インストール<br>
`nginx` セットアップ<br>

### 各環境で書き換えが必要なところ
下記のファイルの環境変数のみansible-playbookコマンドを叩く前に修正が必要
`./roles/vars/variables.yml`
```
# nginxのdefault.confの各設定に適用される
directory: dev
server_name: example.com
root_path: "/var/www/html/{{ directory }}/web/public"
domain: example.com
```