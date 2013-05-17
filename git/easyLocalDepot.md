若只是要在自已的電腦上，擁有一個簡單易使用的原始碼管理系統(Version Control System:VCS)，我認為 git 是一個不錯的選擇。在此提供一個很簡單的示範和說明；看完這篇你可以得到：
1. 看完示範和說明，你就可以馬上在你的電腦上使用 git 。
2. 瞭解git中的 working directory - staging area - repository 之間的關係。
3. 如何修改 git容器的名稱。

第一個範例如下：

    $ mkdir demo
    $ cd demo
    $ git init
    Initialized empty Git repository in /root/demo/.git/
    $ touch foo
    $ git add foo
    $ git commit 0m 'a demo'

在這個範例中，有三個 git 的指令，分別是 init / add / commit；

***init :***
* 這指令會在目前的目錄下 (即為工作目錄working directory的根目錄)，產生一個 ".git" 的子目錄，這個名為 ".git" 的子目錄，即為git 的容器(repository)。

* 而技術上 ".git"的名稱是可以改的，只要在執行 init 前，宣告一個 GIT_DIR＝"你希望的名稱" 的環境變數即可。例如 "export GIT_DIR=.test" 。再執行 init ，便會產生一個名為 ".test"的子目錄為 git容器！

* 另外，git 和 svn 不同的是 git容器只會存在工作目錄的根目錄；而 svn系統下，名為 ".svn"的子目錄，會存在於根目錄和其所有的子目錄。

***add：***
* 在工作目錄下，任何新增或修改過的檔案。要送交(commit)至容器前，一定要先註記為已完成階段性(staging)工作。故透過 add 指令，將註記新增或修改過的檔案，並加入已完成階段性檔案區域 (staging area)。(staging area僅是個邏輯的區域，並不會真的有個目錄作為staging area)

* 已放入 staging area的檔案，若有新的修改，即會被強迫脫離staging area，取消註記。需再透過 add 指令重新註記檔案。

***commit :***
* 最後，透過 commit 指令，將目前的版本送交至容器。

整個狀態，可以用下圖來描述：

![狀態圖](http://3.bp.blogspot.com/-wjCcvNlqIiQ/UNLIv6pYeAI/AAAAAAAAABw/SgtJ75GcLvU/s1600/Git_Local_Operations.png)

而在第一次送交時，可能會有下列錯誤訊息。

![錯誤訊息」](http://2.bp.blogspot.com/-7EaTclI_cbk/UNHsjODS1iI/AAAAAAAAABc/CAmoCcz9l-I/s320/%E8%9E%A2%E5%B9%95%E5%BF%A%E7%85%A7+2012-12-20+%E4%B8%8A%E5%8D%8812.33.44.png)

那是因為 git 要求要有記錄是誰送出這次送交的。可就訊息中的指令範例去設定使用者名稱和使用者 Email。這只要設定一次即可。設定後，會在使用者家目錄下，產生一個 ".gitconfig" 檔案，記錄著你的設定。


