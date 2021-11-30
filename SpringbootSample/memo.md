#Spingの全体像

<dl>
  <dt>SpringBoot</dt>
  <dt>セキュリティ</dt>
  <dd>Springセキュリティ</dd>
  <dt>Data Access</dt>
  <dd>Spring Data JDBC</dd>
  <dt>Web</dt>
  <dd>Spring MVC</dd>
  <dt>バッチ</dt>
  <dd>Spring バッチ</dd>
  <dt>Springコア</dt>
  <dd>Sprng DI</dd>
  <dd>Spring AOP</dd>
</dl>

***
#DI
- Dependency Injection(依存性の注入)の略。
- 端的に言うとインスタンス管理をしてくれるSpringにおいてのコアとなる部分の事。

#AOP
- Aspect Oriented Programingの略で、アスペクト指向プログラミングと言われている。共通処理をまとめておくことができ、本質的なプログラミングだけに専念することが可能。

#Spring MVC
- Web開発における設計の考え方として、MVCモデルというものがある。MVCモデルを使って、Webアプリケーション開発をできるようになるのがSpringMVCである。

#SpringBoot
- Spring MVCを使ってWebアプリケーションを開発しようとすると、事前に多くの設定が必要となる。開発をスムーズにできるよう問題点などを解消したのがSpringBootである。

#Spring Security
- Webアプリケーションにおけるセキュリティ設定を簡単に実装することができます。内容は、認証と認可。認証とはログイン機能であり、認可とはユーザ権限による機能制限のこと。

#Spring Data JDBC
- Spring Dataとは、データベース製品米に異なる操作を簡単に使えるようにしていくためのプロジェクト。JDBCとは、Javaを使ってデータベースにアクセスするための標準APIです。JDBCを使う場合、Select文１つ実行するだけでもかなりのコード量が必要となるが、Spring Data JDBCを使えば、SQLの実行が容易となる。（その他にもJPAやMongoDB用などのライブラリがある。）

以上がSpringの代表的なライブラリとなります。

***

#MVCモデルについて



以下の役割がある。

<dl>
  <dt>Model</dt>
  <dd>ロジックの処理を担当。例えばDBからのデータ取得や様々な計算など。Javaのクラスがこの役割を担う。</dd>
  <dt>View</dt>
  <dd>画面表示の役割を行う。htmlがこの役割を担う。</dd>
  <dt>Controller</dt>
  <dd>ユーザからのリクエストに対して、Modelクラスに処理を依頼し、処理結果に応じてどのViewをユーザに表示するのかを決定する。自分では処理はせず、指示を出す司令塔のような役割。Javaのクラスがこの役割を担う。</dd>
</dl>

クライアントがControllerへ「リクエスト」し、
ControllerがModelへ「依頼」し、
ModelがControllerへ「結果」を返し、
ControllerがViewへ「画面」を返す。

#アノテーション
「注釈」という意味。

<dl>
  <dt>@Controller</dt>
  <dd>Springでは、コントローラクラスに@Controllerアノテーションをつける。DI(依存性注入)で利用できるようになる。</dd>
  <dt>@GetMapping</dt>
  <dd>@GetMappingアノテーションをメソッドにつけると、HTTPリクエストのGETメソッドを処理できるようになる。なお、GETリクエストの場合、メソッド名の最初に get をつけるのが慣習となっている。そして、メソッドの戻り値には拡張子なしの html ファイル名を指定する。</dd>
  <dt>th:value</dt>
  <dd>th:value属性を使うことで、画面からコントローラクラスに値を渡すことができる。（th: と付く属性はタイムリーフの属性。inputタグにはvalue属性がもともと存在し、その属性に th: をつけると、タイムリーフの属性であると宣言している）</dd>
  <dt>@PostMapping</dt>
  <dd>@GetMappingと同様に、メソッドに@PostMappingアノテーションをつけるとPOSTメソッドで送られてきた場合の処理ができるようになる。</dd>
  <dt>@RequestParam</dt>
  <dd>メソッドの引数に@RequestParamアノテーションをつけることで、画面からの入力内容を受け取ることができます。アノテーションの引数には、htmlのname属性の値を指定します。(例)好きな文字を入力：  <input type="text" name="text1" th:value="${text1_value}"/></dd>
  <dt>model.addAttribute</dt>
  <dd>model.addAttribute にキーと値をセットすると、画面(html)から指定したキーの値を受け取ることができる。</dd>
  <dt>Modelからの値を受け取る</dt>
  <dd>th:text 属性に、model.addAttribute で登録したキーを指定することで、コントローラクラスからの値を受け取ることができる。なお、キーを指定する場合は、 ${ <キー名> }と入力する。</dd>
  <dt></dt>
  <dd></dd>
  <dt></dt>
  <dd></dd>
  <dt></dt>
  <dd></dd>  
</dl>

***
<dl>
  <dt>リポジトリークラス</dt>
  <dd>DBへのCRUD操作を行い、その結果を返す。MVCモデルでいうとModelに該当する。</dd>
  <dt>サービスクラス</dt>
  <dd>リポジトリークラスなどを使ったいろいろなサービスを提供する。MVCモデルでいうとModelに該当する。</dd>
  <dt>コントローラークラス</dt>
  <dd>どのサービスを使うか指定して、サービスの結果を画面に返す。MVCモデルでいうとControllerに該当する。</dd>  
</dl>

***
<dl>
  <dt>@Repository</dt>
  <dd>コントローラークラスに@Controllerアノテーションをつけたように、リポジトリークラスにも@Repositoryクラスをつける。こうすることで、DIに登録されるからです。</dd>
  <dt>JdbcTemplate</dt>
  <dd>上記のサンプルではSpringが用意しているJDBC接続用のクラス(JdbcTemplate)を使って、SELECT文を実行している。JdbcTemplateを使う場合は、@Autowiredアノテーションをつける。</dd>
  <dt>@Data</dt>
  <dd>@Dataアノテーションをつけると、getterやsetterなどを自動で作成してくれる。これはlombokの機能で、開発時のちょっとした仕様変更にすぐに対応できるので便利。</dd>  
  <dt>domainクラス(ドメインクラス)</dt>
  <dd>リポジトリークラスやサービスクラスなどの間で渡すクラスのことを、Springではdomain(ドメイン)クラスと呼びます。別の呼び方はモデルクラス、DTO(Data Transfer Object)などの呼び方がある。</dd>  
  <dt>@Service</dt>
  <dd>コントローラークラスなどと同様に、サービスクラスには@Serviceアノテーションをつける。HelloRepositoryクラスを使うために、@Autowiredアノテーションをつけている。(イメージ：private HelloRepository helloRepository = new HelloRepository();)</dd>  
  <dt></dt>
  <dd></dd>  
  <dt></dt>
  <dd></dd>  
</dl>

***
#DIの概要
- DIが何をやっているかを一言で説明するなら、インスタンス管理。@Autowiredアノテーションをフィールドなどにつけると、DIコンテナからインスタンスを取得してくる。
#インスタンス管理とは？
- インスタンスの生成及びインスタンスのライフサイクル管理の２つをやっている。

<dl>
  <dt>インスタンスの生成</dt>
  <dd>DIコンテナの中で、インスタンスを生成する。クラスをnewするイメージ。そして、アプリケーションではそれらのインスタンスを取得して利用する。DIの中で、毎回newしたインスタンスをアプリケーションに渡すのか、それとも一度newしたインスタンスをアプリケーションに渡すのかを管理している。</dd>  
  <dt>インスタンスのライフサイクル管理</dt>
  <dd>インスタンスのライフサイクル管理を簡単に実装できるようになる。これは、Webアプリケーション開発をとても楽にしてくれます。サーブレットのリクエストスコープや、セッションスコープにインスタンスを簡単に登録できるということ。</dd>  
</dl>

- インスタンスの生成とライフサイクル管理(インスタンスの破棄)をDIがやってくれているため、クラスをnewしたり、使い終わった変数にnullを入れる必要がなくなる。こうすることで、nullの入れ忘れ防止でき、コードの可読性が上がる。

#補足
- Javaでクラスをnewするということは、インスタンスがメモリーに載るということですので、たくさんnewすればするほどメモリーをたくさん使う。大量のリクエストを処理するのであれば、おなじくらすをいくつもnewする必要があります。基本的にnewした後は、nullを入れる。nullを入れることで、ガベージコレクションがメモリ上のインスタンスをきれいに掃除してメモリを解放してくれるからです。しかし、DIを使う場合は、基本的にnullを入れる必要はない。(入れるケースもある。)

#DIの説明の前に（「依存性」と「注入」）

- Javaにおける依存とは？
- 依存度が高い状態を「密結合」と言い、インターフェースを使って依存度合いを低くすることを「疎結合」と言う。

<dl>
  <dt>依存性</dt>
  <dd>他のクラスをローカル変数として持っている。</dd>  
  <dd>他のクラスがメソッドの引数、戻り値になっている</dd>
  <dt>注入</dt>
  <dd>インターフェース型の変数に、インスタンスを入れることを注入という。</dd>  
  <dt>Factoryクラス</dt>
  <dd>インスタンスを生成するクラス。</dd>  
</dl>

***
- Springを起動すると、コンポーネントスキャンという処理が走ります。これはDIで管理する対象のアノテーションがつけられているクラスを探します。コンポーネントスキャン対象のアノテーションは以下の通りです。

#コンポーネントスキャン対象のアノテーション


<dl>
  <dt>@Component</dt>
  <dt>@Controller</dt>
  <dt>@Service</dt>
  <dt>@Repository</dt>
  <dt>@Configuration</dt>
  <dt>@RestController</dt>
  <dt>@ControllAdvice</dt>
  <dt>@ManagedBean</dt>
  <dt>@Named</dt>
  <dt></dt>
  <dt></dt>  
</dl>

- 使用頻度が高いアノテーションは以下の４つです。
<dl>
  <dt>@Component</dt>
  <dt>@Controller</dt>
  <dt>@Service</dt>  
  <dt>@Repository</dt>
</dl>

#DIコンテナ上で管理するクラスのことを「Bean」と呼びます。（アノテーションがついているクラスのこと。）

***
- 補足：@Autowiredをつけられる箇所
<dl>
  <dt>フィールド変数</dt>
  <dt>コンストラクタの引数</dt>
  <dt>setterの引数</dt>
</dl>

#DIの実装方法について
- アノテーションベース
- JavaConfig
- xml
- JavaConfig + アノテーション
- xml + アノテーション

#DIのライフサイクル管理機能とは
- インスタンスの生成(new)と破棄を管理してくれる。
- @Autowiredをつけたフィールドに、nullを入れるのはSpringが自動でやってくれる。
- JavaでWebアプリケーションを作る場合、サーブレットを使いますが、インスタンスをSessionスコープやRequestスコープに登録するのもSpringがやってくれる。（ただしそのインスタンスがいつ破棄されるのかを把握しておく必要がある。）

- 補足：
<dl>
  <dt>スコープ</dt>
  <dd>SessionスコープやRequestスコープというのは、インスタンスの有効期限。Javaのローカル変数をイメージするとif文の中で宣言した変数は、if文の中がスコープなので、if文外では使用できないのと同じ</dd>
- 各スコープの有効期限
  <dt>Sessionスコープ</dt>
  <dd>ユーザがろぐいんしてからログアウトするまでが有効期限。例えば、ユーザ情報やそれに紐づく権限などの情報をSessionスコープとして持っておく。</dd>
  <dt>Requestスコープ</dt>
  <dd>HTTPの１リクエストが有効期限。例えば、ユーザ登録画面で入力を行い、登録ボタンを押すと、登録結果として入力値を出す画面が出るとしたら、その場合、ユーザ登録画面から登録結果画面までがRequestスコープの範囲になる。</dd>
</dl>

# ライフサイクル管理方法
- @Scopeアノテーションをつける。そのアノテーションに、どのスコープに登録するかを指定する。

#スコープ一覧
<dl>
  <dt>singleton</dt>
  <dd>Spring起動時にインスタンスを1つだけ生成する。生成後は、１つのインスタンスを共有して使う。デフォルト設定のため、@Scopeアノテーションをつけなかった場合は、すべてsingletonとなる。</dd>
  <dt>prototype</dt>
  <dd>Beanを取得する度に、毎回インスタンスが生成される。</dd>
  <dt>session</dt>
  <dd>HTTPのセッション単位でインスタンスが生成される。Webアプリケーションの場合のみ使用可</dd>
  <dt>request</dt>
  <dd>HTTPのリクエスト単位でインスタンスが生成される。Webアプリケーションの場合のみ使用可</dd>
  <dt>globalSession</dt>
  <dd>ポートレット環境におけるGrobalSession単位でインスタンスが生成される。ポートレットに対応したWebアプリケーションの場合のみ使用可</dd>
  <dt>application</dt>
  <dd>サーブレットのコンテキスト単位でインスタンスが生成される。Webアプリケーションの場合のみ使用可</dd>
</dl>
- @Component以外にも、@Beanや@Controllerなどにも@Scopeアノテーションは利用可能。@Scopeアノテーションを使用することで、簡単にインスタンスの生成と破棄ができるようになる。




#第5章　Webアプリケーションの最終イメージ
【画面一覧】（画面は合計６）
<dl>
  <dt>ログイン画面</dt>
  <dt>ユーザ登録画面</dt>
  <dt>ホーム画面</dt>
  <dt>ユーザ一覧画面</dt>
  <dt>ユーザ詳細画面</dt>
  <dt>アドミン権限専用画面</dt>
</dl>

#第6章　データバインド＆バリデーション
- 学ぶこと
<dl>
  <dt>データバインド</dt>
  <dd>画面で入力されたユーザIDやパスワードなどを、オブジェクトとして受け取る方法</dd>
  <dt>バリデーション（入力チェック）</dt>
  <dd>ユーザ登録時のバリデーション方法</dd>
  <dt></dt>
  <dd></dd>
</dl>

***
- アノテーション一覧(分類：BeanValidation)
<dl>
  <dt>@NotNull</dt>
  <dd>(説明) nullでないことをチェックします。</dd>
  <dd>(例) @NotNull String userName;</dd>
  <dt>@NotEmpry</dt>
  <dd>(説明) 文字列やCollectionがnull、または空でないことをチェックします。</dd>
  <dd>(例) @NotEmpry List< User > userList;</dd>
  <dt>@NotBlank</dt>
  <dd>(説明) 文字列がnull、空文字、空白スペースのみでないことをチェックします。</dd>
  <dd>(例) @NotBlank String password;</dd>
  <dt>@Max</dt>
  <dd>(説明) 指定した値以下であるかをチェックします。</dd>
  <dd>(例) @Max(100) int age;</dd>
  <dt>@Min</dt>
  <dd>(説明) 指定した値以上であるかをチェックします。</dd>
  <dd>(例) @Min(20) int age;</dd>
  <dt>@Size</dt>
  <dd>(説明) 文字列の長さやCollectionのsizeが指定した範囲内にあるかどうかをチェックします。</dd>
  <dd>(例) @Size(min = 0, max = 20) List< User > userList;</dd>
  <dt>@AssertTrue</dt>
  <dd>(説明) trueかどうかをチェックします。</dd>
  <dd>(例) @AssertTrue boolean marriage;</dd>
  <dt>@AssertFalse</dt>
  <dd>(説明) falseかどうかをチェックします。</dd>
  <dd>(例) @AssertFalse boolean marriage;</dd>
  <dt>@Pattern</dt>
  <dd>(説明) 指定した正規表現に一致するかどうかをチェックします</dd>
  <dd>(例) @Pattern() String password;</dd>
  <dt>@Email</dt>
  <dd>(説明) 文字列がメールアドレス形式かどうかをチェックします。</dd>
  <dd>(例) @Email String userId;</dd>
  <dt>@Range</dt>
  <dd>(説明) 数値が指定した範囲内にあるかをチェックします。</dd>
  <dd>(例) @Range(min = 20, max = 100) int age;</dd>
  <dt>@Length</dt>
  <dd>(説明) 文字列の長さが指定した範囲内であるかをチェックします。</dd>
  <dd>(例) @Length(min = 8, max = 100) String password;</dd>
  <dt>@CreditCardNumber</dt>
  <dd>(説明) 文字列がクレジットカード番号形式かどうかをチェックします。</dd>
  <dd>(例) @CreditCardNumber String cardNumber;</dd>
  <dt>@URL</dt>
  <dd>(説明) 文字列がURL形式かどうかをチェックします。</dd>
  <dd>(例) @URL String url;</dd>
</dl>

***
- NotNullとNotEmpryとNotBlankの違い（null→空文字→空白）
<dl>
  <dt>@NotNull</dt>
  <dd>NG→OK→OK</dd>
  <dt>@NotEmpty</dt>
  <dd>NG→NG→OK</dd>
  <dt>@NotBlank</dt>
  <dd>NG→NG→NG</dd>
</dl>

***
#AOPの用語（Aspect Oriented Programming - アスペクト指向プログラミング）
- AOPで管理できる共通処理の代表的なものは以下の通りです。
<dl>
  <dt>ログ出力</dt>
  <dt>セキュリティ</dt>
  <dt>トランザクション</dt>
  <dt>例外処理</dt>
  <dt>キャッシュ</dt>
  <dt>リトライ</dt>
</dl>

***
- AOPの用語
<dl>
  <dt>Advice</dt>
  <dd>AOPで実行する処理のこと</dd>
  <dt>Pointcut</dt>
  <dd>処理を実行する場所(クラスやメソッド)のこと</dd>
  <dt>JoinPoint</dt>
  <dd>処理を実行するタイミングのこと</dd>
</dl>

- Adviceが実行されるタイミングによって、JoinPoint(タイミング)は以下の5種類に分かれる。
- 【JoinPoint(実行タイミング)】
<dl>
  <dt>Before</dt>
  <dd>メソッドが実行される前に、AOPの処理(Advice)を実行します。</dd>
  <dt>After</dt>
  <dd>メソッドが実行された後に、AOPの処理(Advice)を実行します。</dd>
  <dt>AfterReturning</dt>
  <dd>メソッドが正常終了した場合だけ、AOPの処理(Advice)を実行します。</dd>
  <dt>Around</dt>
  <dd>メソッド実行の前後に、AOPの処理(Advice)を実行します。</dd>
  <dt>AfterThrowing</dt>
  <dd>メソッドが異常終了した場合だけ、AOPの処理(Advice)を実行します。</dd>
</dl>

***
- Pointcut(実行場所)の指定方法
<dl>
  <dt>execution</dt>
  <dd>正規表現を使って任意のクラス、メソッドなどをAOPの対象に指定します。</dd>
  <dt>bean</dt>
  <dd>DIコンテナに登録されているBean名でAOPの対象に指定します。</dd>
  <dt>@annotation</dt>
  <dd>アノテーション名で指定します。指定したアノテーションがついているメソッドがAOPの対象となります。</dd>
  <dt>@within</dt>
  <dd>アノテーション名で指定します。指定したアノテーションがついているクラスのすべてのメソッドがAOPの対象となります。</dd>
  <dt></dt>
  <dd></dd>
</dl>

***
- AOPまとめ
- AOPとは、k表痛の処理をまとめて管理できる仕組みのこと。
<dl>
  <dt>AOPの用語</dt>
  - Advice:処理内容
  - Pointcut:実行場所
  - JoinPoint:実行タイミング
  <dt>AOPの作り方</dt>
  - AOPのクラスには@Aspectと@Componentをつける
  - AOPクラスのメソッドには、JoinPoint(実行タイミング)のアノテーションをつける
  - JoinPointのアノテーション内に、Pointcut(実行場所)を指定する
  
  <dt>JoinPoint(実行タイミング)の指定方法</dt>
  <dt>AOPクラスのメソッドには、以下のJoinPoint(実行タイミング)のアノテーションをつける</dt>
  - Before:実行の前
  - After:実行の後(正常終了・異常終了)
  - Around:実行の前後
  - AfterReturning:正常終了後
  - AfterThrowing:異常終了後

#Pointcut(実行場所)の指定方法
- JoinPoint(実行タイミング)のアノテーション内に、以下のPointcut(実行場所)を指定する
<dl>
  <dt>execution(< 戻り値 >< パッケージ名 >.<クラス名>.< メソッド名 >(< 引数 >))</dt>
  <dt>bean(< Bean名 >)</dt>
  <dt>@annotation(< パッケージ名 >.< アノテーション名 >)</dt>
  <dt>@within(< パッケージ名 >.< アノテーション名 >)</dt>
</dl>

***
#8章　Spring JDBC

 - SpringJDBCの概要

<dl>
  <dt>アプリケーション</dt>
  <dd>↓　↑</dd>
  <dt>SpringJDBC</dt>
  <dd>↓　↑</dd>
  <dt>JDBC</dt>
  <dd>↓　↑</dd>
  <dt>DB</dt>
</dl>

- SpringJDBCは、JDBCを使ってデータベースにアクセスしに行く。
- SpringJDBCを使えば、DBの接続やクローズなどの処理を書かなくて済む。ほかにも、DB製品固有のエラーコードを解釈して適切な例外を投げてくれる。


# スーバークラスのDataAccessExceptionという例外クラスを利用すれば、データベース関連のエラーをすべてキャッチすることが可能。

