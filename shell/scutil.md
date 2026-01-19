# scutil

macOSのネットワーク設定を管理するコマンド。

## VPNの設定に関するオプション

`scutil --nc help`でVPN関連のコマンドを確認することができる。

### list

`scutil --nc list`で現在利用可能なVPNの設定(サービス)一覧を表示する。

### status

`scutil --nc status <service>`で指定されたサービスのステータスを表示する。

### show

`scutil --nc show <service>`で指定されたサービスの詳細設定を表示する。

### statistics

`scutil --nc statistics <service>`で指定されたサービスのバイト数、パケット数、エラーに関する統計情報を表示する。

### select

`scutil --nc select <service>`で指定されたサービスをアクティブにし、サービスを起動できるようにする。

### start

`scutil --nc <service> [--user user] [--password password] [--secret secret]`で指定されたサービスを起動する。

### stop

`scutil --nc stop <service>`で指定されたサービスを停止する。

### suspend

`scutil --nc suspend <service>`で指定されたサービス(PPP、モデム保留)を一時停止する。

### resume

`scutil --nc resume <service>`で指定されたサービス(PPP、モデム保留)を再開する。

### ondemand

`scutil --nc ondemand [-W] [hostname]`、`scutil --nc ondemand -- --refresh`でVPNオンデマンド情報を表示する。

### trigger

`scutil --nc trigger <hostname> [background] [port]`で指定したホスト名およびオプションのポートとバックグラウンド(?)でVPNオンデマンドを起動する。

### enablevpn

`scutil --nc enablevpn <service or vpn type> [path]`で指定したVPNアプリケーションタイプを有効にする。
サービスまたはVPNタイプのいずれかを指定する。
アプリケーションURLを設定するためのパスを渡す。

### disablevpn

`scutil --nc disablevpn <service or vpn type>`で指定したVPNアプリケーションタイプを無効にする。
サービスまたはVPNタイプのいずれかを指定する。

### help

`scutil --nc`で`--nc`で使用できるコマンドを表示する。

