workflow
========

## ブランチモデルについて

GitはSVNより簡単にブランチが作成できるので、混乱をきたさないよう__ブランチモデル__という考え方を共有している必要がある。有名なブランチモデルとして__Git Flow__と__GitHub Flow__の2つがある。

### Git Flow

__Git Flow__は「A successful Git branching model」というタイトルで2010年にVincent Driessen氏によって提唱されたブランチモデル。

__Git Flow__では下記の5つのブランチを作成して開発していく。
* __develop__ブランチ
* __feature__ブランチ
* __release__ブランチ
* __master__ブランチ
* __hotfix__ブランチ

#### develop、featureブランチ

開発は__develop__、__feature__の各ブランチで行う。__develop__ブランチが、開発する際のメインブランチ。軽微な修正などは例外として、基本的には__develop__ブランチに直接コミットをpushすることはほとんどしない。かわりに、__feature__ブランチを作り、__feature__ブランチから__develop__ブランチへPull Requestを送るようにする。

利点としては、どういった機能・修正が施されたブランチがマージされたのかがわかりやすくなること。

普段の開発はこの繰り返しで進めるようにする。また、Pull Requestを送られたらほかの開発者はコードレビューを行う。

コードレビューの結果、修正などが必要になった場合は、同じ__feature__ブランチに修正をpushするだけで修正済みのコードが新しいPull Requestとして使用されるようになる。

#### master、releaseブランチ

いよいよリリースという段階になったら、いったん__develop__ブランチから__release__に分岐する。
__release__ブランチではリリースに向けての準備を行う。

ソースコードを修正していくというよりは、たとえばREADMEファイルの修正であったり、ちょっとしたバグフィックスなどを行い、コミットしていく。

リリースしたあとに、__release__ブランチから__master__ブランチへマージしてリリースのバージョンのタグをつける。また、__release__ブランチから__develop__ブランチにも同様にマージする（この時はタグをつけない）。

これでリリース後のバージョンの修正点を__develop__ブランチへ反映しえ開発を続けられるようになる。__master__ブランチは基本的にこのリリース作業のときにしか更新されない（__master__ブランチはリリース時のみ更新される）。

#### hotfixブランチ

リリース後に緊急度の高いバグ修正等があった場合には、この__hotfix__ブランチを使ってリリースする。それほど緊急性が高くない場合は、通常のフロー通りに__develop__ブランチと__feature__ブランチを使った開発で対応する。

__hotfix__ブランチは唯一__master__ブランチから分岐することになるブランチになるので、リリース後の流れは__release__ブランチと同様、新しいタグをつけて__master__ブランチにマージして、__develop__ブランチにもマージしていくこと。

#### リソース

* [A successful Git branching model](http://nvie.com/posts/a-successful-git-branching-model/)
* [A successful Git branching model(日本語訳)](http://keijinsonyaban.blogspot.jp/2010/10/successful-git-branching-model.html)

### GitHub Flow

__GitHub Flow__は「GitHub Flow」というタイトルで2011年にGitHubに勤めるSchott Chacon氏によって提唱されたブランチモデル。
GitHub社内でもこの開発フローが採用されている。__Git Flow__では5つの決まったブランチで開発を進めていくが、__GitHub Flow__はよりシンプルなブランチ構成になっている。

* masterブランチはすべての大元のブランチ、このブランチにマージされたらすべてリリースされる
* 通常、開発で使用するのは__トピックブランチ__と呼ばれるブランチ。どの機能の開発なのかをわかりやすくブランチ名としておき、ほかの開発者にレビューしてもらいたいタイミングや、masterブランチに取り込んでもらいたいタイミング（コードレビューを含む）でPull Requestを送る。
* 
#### リソース

* [GitHub Flow](http://scottchacon.com/2011/08/31/github-flow.html)
* [GitHub Flow(日本語訳)](http://gist.github.com/Gab-km/3705015)

