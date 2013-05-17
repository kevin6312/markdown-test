Markdown  是一個非常方便用來寫部落格的語法。可以透過一些定義好的符號或格式，便可輕易的編排你的文章，先不需要使用大量的HTML，雖然最後仍是需要轉換成HTML。先讓我們先下面的範例：

    > ### This is a header
    > 
    > 1. This is the first list item.
    > 2. This is the secord list item.

如此所產生的結果如下：

> ### This is a header
> 
> 1. This is the first list item.
> 2. This is the secord list item.

就以上所產生的結果，我們可以看到

1. Blockquotes: Email形式的區塊引言，也在左側上一條灰色的直線，它是利用一個<code>&gt;</code>的符號所產生的。
2. 標題：Markdown 所支援的標題從 H1 到 H6。H1 字型最大，而 H6 字型最小；它是以<code>#</code>符號來表示，一個＃為 H1；而六個＃為 H6；
3. 有序清單：以一個數字開頭接著一個小數點，後面至少要接著一個空格，來表示。另外，還有無序清單，可用符號<code>*</code><code>+</code><code>-</code>一個加一個空格來表示。

_____

除了這些，還有

* 程式碼區塊：以一個tab或四個空格開始，結果會產生如下圖，一個區域。
<pre><code>我是程式碼區塊<code></pre>

* 分格線：用三個或以上的星號、減號、底線來建立分隔線。


* 連結：在字串中，有個關𨧞字會連到指定的網址。以\[方括號\]標記，接著以括號填入綱址如下：
<pre><code> 如同我在[之前](http://cypress-soho.blogspot.tw/)所提到的... </code></pre>

* 強調：在要__強調__的文字，在前後加入一或二個的星號或底線。
<pre><code>*singleasterisks*
_single underscores_
**double asterisks**
__double underscores__
</code></pre>
	結果為
    *singleasterisks*
    _single underscores_
    **double asterisks**
    __double underscores__

* 坎入圖片：和連結有像，但差別在多了一個驚嘆號。
<pre><code>![圖片的替代文字](http://localhost/cat.png)</code></pre>


