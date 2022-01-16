# Install-tools-use-ansible

## 目錄

- [運行環境](#運行環境)
- [環境準備](#環境準備)
    - [應用安裝](#應用安裝)
    - [遠端連線設置](#遠端連線設置)
- [應用部署](#應用部署)

## 運行環境

主機運行在 GCP

#### Ubuntu 

- 系統版本：18.04
- CPU：2 核心
- 記憶體：4GB

## 環境準備

### 應用安裝

使用下面指令安裝 *ansible*：

```bash
$ sudo apt update
$ sudo apt install software-properties-common
$ sudo add-apt-repository --yes --update ppa:ansible/ansible
$ sudo apt install ansible
```

### 遠端連線設置

#### GCP 實例

為了能夠對 gcp 任意實例可以遠端操作，使用下面指令添加 `ssh-key` 在 *metadata*：

```bash
$ gcloud compute project-info add-metadata \
    --metadata=ssh-keys="yuki:$(cat /Users/yuki/.ssh/id_rsa.pub)"
```

> [!!!警告!!!] 該指令僅限個人測試環境，並且只使用一支公鑰。否則請手動添加，
> 或是參考下面文件：
> https://cloud.google.com/compute/docs/connect/add-ssh-keys#during-vm-creation

#### 自建主機

使用下面腳本指令，可以自動生成 `ssh-key` 以及替主機添加相關配置：

```bash
$ ./set-ssh [directory] [hoatname] [address] [user]
```

## 應用部署

使用下面腳本指令，即可以部署 *nomad* 和 *consul*：

```bash
$ ./deploy [host] [user]
```

查看部署的歷史紀錄：

```
$ cat deploy_history
```
