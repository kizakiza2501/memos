# 仮想環境インストール


# 日本語キーボード設定
```
sudo dpkg-reconfigure keyboard-configuration
```

# 日本語入力
 - 念のためまずapt-getのアップデートを行います
```
sudo apt-get update
sudo apt-get upgrade
```

 - 言語パックやibus-mozcのインストール、日本語ロケールの設定
```
sudo apt-get install language-pack-ja
sudo apt-get install ibus-mozc
sudo update-locale LANG=ja_JP.UTF-8
```

 - 言語サポートを起動し、IBusをIMシステムとして選択
```
ここで言語サポートが起動するようになりますが、「言語サポートが完全にはインストールされていません」のメッセージが出ます。
「インストール」を選択すると、「すべての言語サポートがインストールできません」のメッセージが続くので、Closeします。
「You are not allowed to perform this action」のメッセージもClose。
そして、画面下方にある「キーボード入力に使うIMシステム」を「IBus」にしてClose。
```

 - IBusデーモンを自動起動するように設定
```
ibus-daemon -rdx
```

 - 環境変数の設定
```
sudo mousepad /etc/profile
↓を追記
export GDM_LANG=ja
export GTK_IM_MODULE=ibus
export XMODIFIERS=@im=ibus
export QT_IM_MODULE=ibus
```

 - IBusの設定
```
アプリーションーIBusの設定ーInput Methodのタブを選択。
GeneralのタブでKeyboard Shortcutsを設定しますが、Control + Spaceにすると、切り替え時にスペースが連打されて切り替わらない現象が起こったので、自分はControl + Alt + Spaceにしました。
Input Methodのタブを選択し、Addボタンを押します。
ここで表示される選択肢の中で日本語-Mozcを見つけて選択し、Add、Closeします。
(ただの「日本語」を選択しても動作しないのでMozcがついたものを選択してください。最初はMozcの選択肢が表示されず、試行錯誤のうちようやく出てきたものを選択してうまく行ったので、これまでの手順を順調にこなしても表示されない可能性があります。何かのタイミングで表示されるように感じてしまいましたが、再起動等試してみてください)
設定完了後画面右上のユーザー名の隣にAまたはENになっているアイコンをクリックして日本語-mozcに切り替えます。
```

 - トラックパッドの無効化
```
# トラックパッドOFF
synclient TouchpadOff=1

# トラックパッド有効
synclient TouchpadOff=0
```

 # 参考サイト
 - 日本語入力
http://undecimber.com/wp/2017/12/21/%E7%B6%9Achromebook-flip-c101pa%E3%81%ABlinux%E5%B0%8E%E5%85%A5%E6%9B%B4%E6%96%B0%E4%B8%AD/

 - トラックパッドの無効
https://linux.just4fun.biz/?Ubuntu/%E3%82%BF%E3%83%83%E3%83%81%E3%83%91%E3%83%83%E3%83%89%E3%82%92%E3%82%AA%E3%83%B3%E3%83%BB%E3%82%AA%E3%83%95%E3%81%99%E3%82%8B%E3%82%B3%E3%83%9E%E3%83%B3%E3%83%89%E3%83%BBsynclient