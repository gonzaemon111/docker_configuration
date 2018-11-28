# docker_configuration

Dockerでの環境構築用の覚書

## 1. アプリケーション用のディレクトリを作成

```
$ mkdir <アプリケーション名>_docker
$ vi docker-compose.yml # docker-compose.ymlの内容をコピペ
```

## 2. Railsアプリのdocker環境構築

```
$ pwd # <アプリケーション名>_dockerがカレントディレクトリになっていることを確認
$ rails new <アプリケーション名> -d mysql -T
$ cd <アプリケーション名>
$ vi Gemfile # コピペ
$ vi Dockerfile # コピペ
$ vi config/database.yml # 以下をコピペ
```


config/database.yml
```
default: &default
  adapter: mysql2
  encoding: utf8
  pool: <%= ENV.fetch("RAILS_MAX_THREADS") { 5 } %>
  username: root
  password: <%= ENV["MYSQL_PASSWORD"] %>
  host: db
```

Railsでの注意事項

新しいgemを入れた際の`bundle install`にまだ成功していないため、基本新しいgemを入れちゃダメ
もし入れた場合は、初めから`docker-compose build`からやりなおす必要がある。

## 3. Nuxt.jsアプリケーションの環境構築

```
$ pwd # <アプリケーション名>_dockerがカレントディレクトリになっていることを確認
$ yarn create nuxt-app <アプリケーション名>
$ cd <アプリケーション名>
$ yarn
$ vi Dockerfile # コピペ
$ vi nuxt.config.js # 以下を書き換える -> エラー出る
```

```
module.exports = {
  ~
  省略
  build: {
    /*
    ** You can extend webpack config here
    */
   extend (config, { isDev }) {
    if (isDev && process.isClient) {
        config.module.rules.push({
          enforce: 'pre',
          test: /\.(js|vue)$/,
          loader: 'eslint-loader',
          exclude: /(node_modules)/
        })
      }
    }
  }
  省略
  ~
}
```

