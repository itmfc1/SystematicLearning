05Kafka章节1-(顺序写入&ZeroCopy)05



![image-20201220140616840](../image/image-20201220140616840.png)



kafka高性能之道——顺序写&mmap



![image-20201220141335858](../image/image-20201220141335858.png)

顺序写

MMF（Memoery Map File）

![image-20201220141940554](../image/image-20201220141940554.png)

zero copy(零拷贝)



![image-20201220142322348](../image/image-20201220142322348.png)

IO常规

![image-20201220142729213](../image/image-20201220142729213.png)

引入DMA，减轻CPU的负担



![image-20201220142837492](../image/image-20201220142837492.png)

常规IO

![image-20201220142923569](../image/image-20201220142923569.png)

zero拷贝



![image-20201220143124979](../image/image-20201220143124979.png)

DMA读取

![image-20201220143145270](../image/image-20201220143145270.png)

网络IO

* 一般方案
* zero拷贝



![image-20201220143442851](../image/image-20201220143442851.png)

小结

