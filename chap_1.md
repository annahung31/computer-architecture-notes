
# Chap.1: Introduction

### ISA\(Instruction set architecture\)

定義好的 HW/SW interface\[1\]。

根據 stack overflow\[2\] 上的回答，ISA 是電腦的 native language，最接近電腦能懂的語言。你可以用很多種的語言來寫出一部電腦，但是最後他們都必須要被轉譯成電腦能懂的語言，那就是 ISA。

如今最普遍的 ISA 是 x86 跟 ARM，但其實還是有其他 ISA 存在。

#### Reference

\[1\] [https://www.cis.upenn.edu/~milom/cis501-Fall05/lectures/02\_isa.pdf](https://www.cis.upenn.edu/~milom/cis501-Fall05/lectures/02_isa.pdf)

\[2\] [https://stackoverflow.com/questions/21248862/what-is-an-instruction-set-architecture-isa](https://stackoverflow.com/questions/21248862/what-is-an-instruction-set-architecture-isa)

### ABI\(Application binary interface\)

可以跟 API 比較：

當你想用某個 library 的時候，你會需要看 API 來知道如何使用。 API 會紀錄 data types, structures, 常數, functions 等等，告訴你怎麼用。

而 ABI 也是類似的概念，只是它是編譯過的 API，也就是比較接近機器看得懂的語言。

當你在寫 source code 的時候，你會用 API 來 access library。當 code 被編譯過後，你的 application 就會經由 ABI 來 access library 裡面的 binary data。

ABI 會定義這些 arguments\(例如 registers暫存器, stack...\)如何被 passed，定義你的 code 是怎麼被存放在 library file 裡面的。

Linux 跟 Windows 用不同的 ABI，所以一個 Windows program 會不知道怎麼 access 一個 為了Linux 編譯的 library。

有時候，無可避免地需要修改 ABI，那任何會用到這個 ABI 的 program 都必須要重新編譯才能 access。假設 ABI 有改，但 API 沒改，那就會變成source compatible，也就是說，這個 program 只有在這個 library版本上才能用，假如你要用別的版本，就要重新編譯。

所以說，開發者通常會盡量避免去更改 ABI。

ABI 並不是 language-specific 的，用 C 寫的跟用 Pascal 寫的，都可以用相同的 ABI，只要 ABI 經過編譯。

#### Reference

[https://stackoverflow.com/questions/2171177/what-is-an-application-binary-interface-abi](https://stackoverflow.com/questions/2171177/what-is-an-application-binary-interface-abi)

### Memory

* volatile: 把電腦關機，data就會不見。
* Non-volatile: 固態硬碟，關機後不會不見。缺點：寫入比較慢。

### Network

* Local area \(LAN\): 地區性的，讓同一個地方的人用。
* Wide area \(WAN\): 家裡租用的那種，讓外面的光纖進到你家，固網，或者是 4G/5G

### 晶片

![chap1_img/Screen\_Shot\_2020-09-22\_at\_10.24.28\_AM.png](.gitbook/assets/Screen_Shot_2020-09-22_at_10.24.28_AM.png)

#### 名詞解釋

`die`: 把晶圓切割為若干個小的單位

`wafer`: 晶圓，一個完整的晶圓由純矽組成，12吋=直徑300mm，可以切很多很多小晶片。

`Defects per area`: 每單位面積會有 defact 的機率。（經驗法則）

`Yield`: 產值

#### Reference

[https://kknews.cc/zh-tw/digital/ejnyav4.html](https://kknews.cc/zh-tw/digital/ejnyav4.html)

#### 晶片不用切，直接拿晶圓來用: 晶圓級引擎（Wafer-Scale Engine，WSE）

![chap1_img/Screen\_Shot\_2020-09-22\_at\_10.29.54\_AM.png](.gitbook/assets/Screen_Shot_2020-09-22_at_10.29.54_AM.png)

> 電腦系統公司Cerebras Systems發表了一款有史以來最大的半導體運算晶片Cerebras Wafer Scale Engine（WSE），其尺寸超過一個iPad Air大小，上面擁有超過1.2兆個電晶體，以及40萬個人工智慧最佳化的核心，要為深度學習應用提供更強大的運算能力。 可能問題：耗電量，散熱。
>
> #### Reference
>
> [https://www.ithome.com.tw/news/132516](https://www.ithome.com.tw/news/132516)

## Performance evaluation

### 評估 performance 的指標

* Response time：多久會做完一個工作。
* Throughput:   工作量/單位時間。ex: 要增加同時間內服務的客戶量  

兩者是相關的。  
接下來的討論會 focus 在 Response time。  
performance = $1/time$  
同一件事， A 花 10 秒執行， B 花 15 秒執行  
則 A 的 performance = 1/10 ， B 的 performance = 1/15  
則 A 比 B 快 $\(1/10\)/\(1/15\)=1.5$ 倍

#### Reference

[https://www.ibm.com/support/knowledgecenter/SSGU8G\_14.1.0/com.ibm.perf.doc/ids\_prf\_046.htm](https://www.ibm.com/support/knowledgecenter/SSGU8G_14.1.0/com.ibm.perf.doc/ids_prf_046.htm)

### 計算時間

* Elapsed time： overall 的執行時間
* CPU time：CPU, IO 執行時間

### Linux 計時的工具們

![chap1_img/Screen\_Shot\_2020-09-22\_at\_11.14.06\_AM.png](.gitbook/assets/Screen_Shot_2020-09-22_at_11.14.06_AM.png)

### Intel 提供的工具： Vtune

[https://software.intel.com/content/www/us/en/develop/videos/hpc-applications-need-high-performance-analysis.html](https://software.intel.com/content/www/us/en/develop/videos/hpc-applications-need-high-performance-analysis.html)

### CPU clocking

電路會有 clock, 可以告訴元件什麼時候要做什麼事，一個方波週期就是一個 clock period。 ![chap1_img/Screen\_Shot\_2020-09-22\_at\_11.18.41\_AM.png](.gitbook/assets/Screen_Shot_2020-09-22_at_11.18.41_AM.png)

某個元件開始做 data transfer，出現在某個公開的地方，在 clock cycle 結束的時候，確定當前狀態，並改變狀態\(update state\)。  
假設一個 clock period 執行一個指令，則當 clock period 越短，就可以執行越多事情。機器頻率越高，速度越快。  
CPU time = 執行該程式需要的 clock cycle 數量 \* clock cycle time  
= 執行該程式需要的 clock cycle 數量/ clock rate

### 如何改進 CPU time?

1. 如何降低執行該程式需要的 clock cycle 數量 → 設計好的 algorithm
2. 如何降低 clock cycle time → 買好一點的 CPU

可是兩者可能會互相影響，有時候降低 clock cycle time 可能會增加 執行該程式需要的 clock cycle 數量，需要有妥協。

例如： ![chap1_img/Screen\_Shot\_2020-09-22\_at\_11.28.11\_AM.png](.gitbook/assets/Screen_Shot_2020-09-22_at_11.28.11_AM.png)

![chap1_img/Screen\_Shot\_2020-09-22\_at\_11.31.22\_AM.png](.gitbook/assets/Screen_Shot_2020-09-22_at_11.31.22_AM.png)

`Instruction count` ：寫完程式就決定了，也跟 compiler 有關  
`CPI`：每個 instruction 需要多少個 cycle。  
針對一個 program，可以算出平均 CPI。  
compiler 的目標是聰明選擇 `Instruction count` 跟 `CPI` 來降低 CPU time。

#### Example

假定 ISA 相同的情況下，同一個 program 在兩台電腦上跑的速度差異？

#### Example 2

sequence: 編譯方式  
sequence 1 使用了 2 個 A class, 1 個 B class, 2 個 C class

![chap1_img/Screen\_Shot\_2020-09-22\_at\_11.41.54\_AM.png](.gitbook/assets/Screen_Shot_2020-09-22_at_11.41.54_AM.png)

雖然 seq 2 使用到比較多個 class ，但是 avg. CPI 比較低，所以應該要選擇 seq 2 的方式。

### Summary

![chap1_img/Screen\_Shot\_2020-09-22\_at\_11.42.38\_AM.png](.gitbook/assets/Screen_Shot_2020-09-22_at_11.42.38_AM.png)

彼此間會互相影響。

### Clock rate 的成長

![chap1_img/Screen\_Shot\_2020-09-22\_at\_11.48.08\_AM.png](.gitbook/assets/Screen_Shot_2020-09-22_at_11.48.08_AM.png)

我的 MB air: 1.2 GHz Quad-Core Intel Core i7  
速度很高 → 變很熱 → 降速以繼續正常運行  
沒辦法提高 clock rate，因為會燙  
後來比較強調電源效率，耗電較低，就比較不需要降速

### 耗電跟哪些因素有關？

1. Frequency（clock rate\) 
2. voltage 電壓\( 一般 USB 5V，電壓越高，充電速度越快，底線大約 1V\)  

    為了要區辨 0 和 1 ，只好把震動幅度（電壓）調高  

3. capacitive load：跟設計有關，負載，晶片越多就越大  

![chap1_img/Screen\_Shot\_2020-09-22\_at\_12.01.14\_PM.png](.gitbook/assets/Screen_Shot_2020-09-22_at_12.01.14_PM.png)

Power wall: 從十多年前就已經觸礁了  
雖然降低了功耗，但是很難真的把 voltage 降低 15%，因爲目前大多已經接近最低的 1V。  
想別的辦法： 平行計算\(multi-core\)  
上面跑的 program 必須要能夠平行運算，才能得到好處。

![chap1_img/Screen\_Shot\_2020-09-22\_at\_12.05.34\_PM.png](.gitbook/assets/Screen_Shot_2020-09-22_at_12.05.34_PM.png)

### CPU 的 Benchmark \(由 SPEC 制訂的\)

![chap1_img/Screen\_Shot\_2020-09-22\_at\_12.08.52\_PM.png](.gitbook/assets/Screen_Shot_2020-09-22_at_12.08.52_PM.png)

最新版是 SPEC CPU 2017\[1\]。做法是把你的電腦跟 baseline 比，再算出幾何平均。（幾何平均：全部相乘再開根號）

![chap1_img/Screen\_Shot\_2020-09-29\_at\_9.29.45\_AM.png](.gitbook/assets/Screen_Shot_2020-09-29_at_9.29.45_AM.png)

zip: 無損壓縮  
CPI值 和程式碼用了哪些指令有關，不同的 func 會使用的 CPI 不同；也跟指令的順序有關，拿資料會不會卡住等等。CPI 高，指令執行起來比較慢，或指令比較困難。  
SPECratio高，代表 performance 較差

### 量 power

機器在不同的工作情況之下不同，所以不能直接看電源功率。 看實際例子： ![chap1_img/Screen\_Shot\_2020-09-29\_at\_9.36.33\_AM.png](.gitbook/assets/Screen_Shot_2020-09-29_at_9.36.33_AM.png)

可以看到當滿載\(target load=100%\)，average power = 258，則他的效能\(performance\)可以達到 865618。  
當 load 降到 0% 時，因為完全不工作， performance 是 0，但是仍會耗電：80。  
所以假設電腦不用不關機，還是會耗電。  
把在各種 load 下的 performance 跟 average power 各自加起來，再相除。

![chap1_img/Screen\_Shot\_2020-09-29\_at\_9.37.29\_AM.png](.gitbook/assets/Screen_Shot_2020-09-29_at_9.37.29_AM.png)

**意義：單位 watts 可以完成多少工作。**

消耗的電費是一筆很大的開銷，所以買 server時要考慮。

### 有效使用機器，降低耗能

另外，我們可以發現在 50% load 時，耗電是 100%時的 66% ，只完成了一半的工作，耗電卻多於一半。  
因此，我們知道，與其讓兩台電腦各做一半的事，不如集中到一台，另一台關掉，還比較省電。  
讓電腦一直在小於 50 % load ，是沒有效率的。

### 估算升級 CPU 有沒有增進效能的方法： Amdahl's law

`T_affected`: 升級會提升哪些方面的時間  
`improvement factor`: 提升了幾倍

例如：有一份 code，花了 100s，花了 80s作乘法。  
有沒有可能把這份 code 的 performance 快 5 倍？  
代入 Amdahl's law 就可以知道不可能。  
快 5 倍 → 時間變 20 s → $20 = \frac{80}{n} + 20$ → n 是無限大

### 不要用MIPS當作 performance metric

`MIPS` : Millions of Instructions Per Second

![chap1_img/Screen\_Shot\_2020-09-29\_at\_10.09.34\_AM.png](.gitbook/assets/Screen_Shot_2020-09-29_at_10.09.34_AM.png)

這樣的比較是很片面的，沒有考慮到 ISA 的不同，也沒有考慮到不同 instruction 之間的差異。

### Other discussion

國網現在可以有 8 PB 的運算力  
但是要有 200多台電腦 \* 8 顆 GPU  
Deep learning 的training 就要耗掉大量的能量，使用時也是，所以未必是最有效率的。  
如今針對 DL 的加速器越來越多，也促成了 DL 的大放異彩。

`Reconfigurable computing`: 讓晶片或電腦像軟體一樣，可以下載更新。  
`Neuromorphic computing` ：就像 DL 從人體神經學得到靈感，借用這個概念做事，但其實其精密程度還遠不及大腦；當我們可以複製人類大腦，  
昆蟲可以閃躲攻擊，但其耗能很低。無人機還不能做這麼精密的動作，耗電量卻遠高於昆蟲，因此我們還有很多事情可以向大自然學習。  
`Quantum computing` ：我們知道他很有潛力，在他能解決的問題上，效率高出一般電腦很多，但目前他能解決的問題還沒有很多。  
Improve core technologies to enable new applications. 先找出程式最慢的部分，改進它，就能做到最快的加速

#### Reference

\[1\] [https://www.spec.org/benchmarks.html](https://www.spec.org/benchmarks.html)

