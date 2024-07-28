# PalWorld 専用サーバ構築手順

## 前準備

### ネットワーク
- VPCが作成されている
- Subnetが作成されている
- SubnetからIGWに対してRouteTableが設定されている

### インスタンス
- KeyPairが作成されている
- SecurityGroupが作成されている
- IAMRoleが作成されている

## OS設定

1. rootユーザーでsteamユーザーを作成
```bash
sudo useradd -m steam
sudo passwd steam
```

2. steamユーザーをsudoグループに追加
```bash
sudo gpasswd -a steam sudo
```

## SteamCMDのインストール
1. マルチバースリポジトリとx86パッケージを有効化
```bash
sudo add-apt-repository multiverse
sudo dpkg --add-architecture i386
sudo apt update
```
2. SteamCMDをインストール
```bash
sudo apt install steamcmd
```

3. 依存関係をインストール
```bash
sudo apt-get install lib32gcc-s1
```

4. SteamCMD用のディレクトリを作成し、移動
```bash
mkdir ~/Steam && cd ~/Steam
```

5. SteamCMDをダウンロードして展開
```bash
curl -sqL "https://steamcdn-a.akamaihd.net/client/installer/steamcmd_linux.tar.gz" | tar zxvf -
```

## SteamCMDの起動と設定
1. SteamCMDを起動
```bash
./steamcmd.sh
```

2. 以下のコマンドをSteamCMD内で実行
```bash
login anonymous
force_install_dir /home/steam/Steam/palworld/
app_update 2394010 validate
```
3. 必要なディレクトリとシンボリックリンクを作成
```bash
mkdir .steam
cd .steam
mkdir sdk64
ln -s /home/steam/Steam/palworld/linux64/steamclient.so /home/steam/Steam/.steam/sdk64/
ln -s /home/steam/Steam/palworld/linux64/steamclient.so /home/steam/.steam/sdk64/
```

参考:
Valve Developer Community-SteamCMD(https://developer.valvesoftware.com/wiki/SteamCMD)