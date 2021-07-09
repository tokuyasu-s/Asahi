FROM centos:7

# set timezone
RUN ln -sf /usr/share/zoneinfo/Asia/Tokyo /etc/localtime

# compile and install vim
RUN rpm --rebuilddb && yum update -y && \
    yum -y install git gcc ncurses-devel make && \
    yum -y install httpd which && \
    yum -y install vim && \
    rm -rf /var/cache/yum/* && \
    yum clean all

FROM golang:latest

# コンテナ作業ディレクトリの変更
WORKDIR ./src

# ホストOSの ./go の中身を作業ディレクトリに追加
ADD ./src .

# Dockerfileファイル中に以下のような記述を追加し、8080番ポートを公開する

# モジュール管理のファイルをコピー
COPY ./src .


# 外部パッケージのダウンロード
RUN go mod download
EXPOSE 9000