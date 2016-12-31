# Preparation
In order to create repository, you must have macOS or Linux. We don't support other platforms.  
Sample repository is [here](https://github.com/BlitzModder/BMRepository). When you trouble creating repository, please refer to this sample.  
First, you have to create your own [GitHub](https://github.com) account. After that, create a repository named `BMRepository`.
# Create plist file
## Input necessary information
The mod list shown in BlitzModder is generated from plist file on GitHub repository.  
Refer to [Sample plist file](https://github.com/BlitzModder/BMRepository/blob/master/en.plist).    
![correspond-1](http://subdiox.com/blitzmodder/ja/img/correspond-1.png)
First key corresponds to the category name of the mod, and second to the type name of the mod.  
![correspond-2](http://subdiox.com/blitzmodder/ja/img/correspond-2.png)
Second key also corresponds to the title of the screen shown after tapping on a mod item, and third to the concrete name.
DictionaryのKeyは`表示名:ID`のように設定してください。このとき、次のルールを守るようにしてください。
- それぞれのkeyについて、コロン`:`が1個だけ含まれている必要があります。0個または2個以上の`:`があると、`error`と表示されます。
- `en.plist`には英語のMod名、`ja.plist`には日本語のMod名を書きましょう。
- IDは小文字のアルファベット、数字、アンダーバーで構成しましょう。ピリオドを含んではいけません。

plistファイルの作成が終わったら、以下のコマンドを実行してください。

    git add .
    git commit -m "add plist"
    git remote add origin https://github.com/ユーザ名/BMRepository.git
    git push origin master

この時点でModリストだけならBlitzModder上で表示できるようになります。BlitzModderであなたのユーザ名のリポジトリを追加してみましょう。
ここでerrorが起きる場合や、何も表示されない場合は何かが間違っています。どうしてもわからない場合は、[@subdiox](https://twitter.com/subdiox)に質問しましょう。

## 動作するBlitzのバージョンやOSの種類の指定(オプション)
これは必ずしも必要ではありませんが、これによってiOS版のBlitzModderとAndroid版のBlitzModderで表示する内容を変えることができます。
また、動作するBlitzのバージョンを指定すれば、そのバージョン以外のBlitzをインストールしている場合、リストに表示されなくなります。
指定する文字列は、指定したいModのKeyに対応するString欄に次のように入力します。  
`動作するBlitzのバージョン:動作するOSの種類`  
ここで、  
- `動作するBlitzのバージョン`には、`3.4.2`のように、マイナーバージョンまでが必要です。
- `動作するOSの種類`には、iOS版で表示する場合は`i`、Android版で表示する場合は`a`、Windows版で表示する場合は`w`、macOS版で表示する場合は`m`を繋げて入力します。

3.4.2のBlitzで動作し、iOS、Windows、macOSの環境で動作するModの場合は、`3.4.2:iwm`とします。

# InstallフォルダとRemoveフォルダの作成
`en.plist`と`ja.plist`の作成が終わったら、`BMRepository`フォルダを作りそれらを入れます。  
`BMRepository`フォルダの中に、`Install`フォルダを作ります。`Install`フォルダ内にModデータの入ったフォルダを作成します。
フォルダ名は`Data`にして、Blitzの`Data`フォルダ内のファイル構造と全く同じ構造になるように配置する必要があります。  
つまり、そのフォルダをBlitzのアプリ内にあるDataフォルダとマージすることでModを適用できるような状態にする必要があるということです。  
次に、その`Data`フォルダをzip圧縮します。zip圧縮する方法はいろいろありますが、zipコマンドを使って圧縮してください。
ターミナルを起動し、`Install`フォルダ内で以下のコマンドを実行することでzip圧縮できます。

    zip -r 一番目のID.二番目のID.三番目のID.zip Data

たとえば、`Gfx Mods/Reticle/HUD Type`のModを作った場合、ファイル名は`gfx.reticle.hud.zip`となります。  
`Install`フォルダの中にすべてのModデータを入れ終わったら、`BMRepository`フォルダの中で以下のコマンドを実行します。
  
    git add .
    git commit -m "add mods"
    git push origin master

次に削除用データを作る必要があります。`Install`フォルダから`Remove`フォルダを自動生成するスクリプトを作りました。  
`BMRepository`フォルダ内で以下のコマンドを実行して`Remove`フォルダを自動生成してください。  

    git submodule add https://github.com/BlitzModder/BMData Data
    curl -O https://github.com/BlitzModder/BMRepository/raw/master/autogen.sh
    bash autogen.sh
    git add .
    git commit -m "add remove"
    git push origin master

# Modの詳細ページの作成 (オプション)
オプションとして、Modをタップしたときに表示される詳細ページを作ることができます。  
まず、Detailフォルダを作成してください。その中に`en`, `ja`, `img`フォルダを作成してください。  
Modの詳細ページのhtmlファイルを`en`, `ja`フォルダの中にそれぞれ入れます。画像を使用する場合は`img`フォルダの中に入れてください。
htmlファイルはModファイルの場合と同様に、`一番目のID.二番目のID.三番目のID.html`とする必要があります。たとえば、`HUD Type`の場合は、`gfx.reticle.hud.html`とする必要があります。
すべてのhtmlファイルを置き終わったら、以下のコマンドを実行してください。

    git add .
    git commit -m "add html"
    git push origin master

BlitzModderでhtmlを表示できるようにするには、GitHubリポジトリの設定からGitHub Pagesを有効にする必要があります。
GitHub Pagesについての詳しい情報は各自で調べてください。