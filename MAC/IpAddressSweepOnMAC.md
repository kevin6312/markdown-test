# 在 MAC 上，去掃描網路上的 ip address。

想知道，網路上有那些 IP 位址己經被使用了嗎了，在 Windows 上，可以使用Angry IP Scanner。
但，在 MAC 上，並不用這麼麻煩，只要打開終端機(terminal), 在上面鍵入以下指令即可。

<pre><code>xCedar$ for x in {1..254}; do ping -c 1 -W 100 192.168.1.$x | grep 'time='; done</code></pre>

以上，簡單吧～！
指令中，以 __for ... done__ 為主的迥圈，設定 x 的值，從 1 到 254; 並變數 x 的值，<br>以 $x 代入 ping 的指令中。<br>
__-c 1__: ping 的次數為一次； __-W 100__: 等待回應時間為 100ms。<br>
最後以關鍵字 "time=" 來列出有回應的 IP 位址。<br>

[Ref:Ping Sweep for MAC OS X](http://www.markholloway.com/blog/?p=1952)
