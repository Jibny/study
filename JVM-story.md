---
title: 一个Bean的传奇人生
date: 2019-10-2 21:59:56
categories: 
    JVM
tags:
    JVM-story
cover: http://r.photo.store.qq.com/psb?/V13Zm3q236IRIM/7nOBrbvdt5uclx9KdZ*Psr5HC6MGWO29vmGp.vDPuW0!/r/dLYAAAAAAAAA
mp3: https://api.uomg.com/api/rand.music
---



![img](http://r.photo.store.qq.com/psb?/V13Zm3q22D5cS0/6hIAo.YAigQcc2p80.jJQSixGzjVD946Rqy4Eg99SHs!/r/dL8AAAAAAAAA)

<a href="#1" name="0">我在JVM公司的那些年（一）——奇怪的面试</a>

<a href="#2">我在JVM公司的那些年（二）——残酷的制度</a>

<a href="#3">我在JVM公司的那些年（三）——恐怖的垃圾回收</a>

<a href="#4">我在JVM公司的那些年（四）——工位调整</a>

<a href="#5">我在JVM公司的那些年（五）——主动出击</a>

<a href="#6">我在JVM公司的那些年（六）——智斗黑老大</a>

<a href="#7">我在JVM公司的那些年（七）——玉石俱焚</a>

<a href="#8">我在JVM公司的那些年（八）——死里逃生</a>

<a href="#9">我在JVM公司的那些年（九）——潜规则</a>

<a href="#10">我在JVM公司的那些年（十）——不一样的垃圾回收</a>

<a href="#11">我在JVM公司的那些年（十一）——人事部的交流</a>



## <a href="#0" name="1">【技术小说连载】我在JVM公司的那些年（一）——奇怪的面试</a>

### **本节知识点预告：JVM双亲委派机制。**



大家好，我叫小史，是一个非科班程序员……哦，不，在这部小说中，我是一个java对象。

大家知道，我一直想去一家大公司工作，现在这个年代，放眼望去，JVM公司就是一家理想中的公司。

但是想去这家公司的人太多了，只要是搞java的，都想往里面钻。

很幸运，我拿到了一个面试机会。

**奇怪的面试流程**

我走进会议室，不一会儿就有一个HR小姐姐过来招呼我。

HR小姐姐：你好，我是Application ClassLoader，欢迎参加我们的招聘。

我：你好，这是我的简历。

说着，我从书包里掏出一个com.neteye.Person.class文件递给了HR小姐姐。

HR小姐姐：哦，是一个class文件，你等等，我得找我的主管先来看看。

说完，HR小姐姐离开了会议室，不一会儿，又过来另一个更加成熟的HR小姐姐。

HR小姐姐：你好，我是Extension ClassLoader。

她拿着我的简历，说：嗯，果然是一个class文件，稍等，我得找我的主管过来看看。

说完，这位HR小姐姐也出去了，留下我在会议室一脸懵逼，这到底是干嘛？

过一会儿，又过来一个更加资深的HR小姐姐。

HR小姐姐：你好，我是Bootstrap ClassLoader。

这位HR小姐姐看了一下我的简历，说：嗯，这份简历我面不了，我叫个人过来面你。

说完，她又双叒叕出去了……不一会儿，之前的Extension ClassLoader小姐姐进来了。

她看了一下简历，也说：嗯，这份简历我也面不了，我叫个人过来面你。

说完，她出去后又把Application ClassLoader叫进来。

Application ClassLoader仔细看着我的简历，嘴里还念念有词：cafebabe……

过了一会儿，她开口了：嗯，简历没问题，明天来上班吧，你有没有什么问题要问我？

我内心很惊讶，竟然一个问题没问，光靠简历就过了面试。但是表面上我却镇定无比，问了一个从一开始我就疑惑不解的问题。

我：既然最后是你来面我，干嘛还让你的主管还有主管的主管来看我的简历呢？

**不堪回首的招聘事故**

Application ClassLoader和我年龄相仿，也没什么代沟，于是她和我滔滔不绝地讲起来。

你不知道啊，在公司创立不久的时候，有一次我招聘，碰到一个人，自称是java.lang.String，以前是xx公司CTO，过来面试。

我自然很高兴呀，欢欢喜喜把他招进来，想着今年的KPI可以超额完成了。

没想到下午的时候，Bootstrap ClassLoader发现了他，说，不对呀，java.lang.String在我刚创立公司的时候就招进来了，一直是公司核心员工。

于是暗中调查那个新来的java.lang.String，发现他简历造假，真实身份居然是竞争对手公司派过来的间谍。

我们赶紧把他开除了，幸好发现的早，不然后果不堪设想。

从那以后，公司就立下制度，所有进JVM公司的人，简历必须先经过Bootstrap ClassLoader审阅，她负责招聘公司的核心员工，然后再由Extension ClassLoader审阅，她负责招聘核心扩展员工，她俩都看过了，再由我Application ClassLoader来，我只招聘普通员工。

这套制度还有一个拗口的名字，叫做parent delegation，翻译过来叫双亲委派。

![img](http://r.photo.store.qq.com/psb?/V13Zm3q22D5cS0/MG8s9VwGQf9LF5GtAcCKzp*cUeYv4yVgolRbFY4wSSg!/r/dDQBAAAAAAAA)

我心想：原来如此，这样做就可以防止有人冒充JVM公司的核心员工了。



HR小姐姐：你跟我过来吧，我带你认识一下你的工位。说着，HR小姐姐把我领到了一个叫做新生代的工作区。

HR小姐姐：喏，这就是你的工位，你以后就在这上班啦。



（未完待续……）



**小结**

ClassLoader的工作就是把.class文件加载进JVM。

而双亲委派模型说的就是，当一个.class文件要被加载进JVM的时候，要先经过Bootstrap ClassLoader尝试加载，再经过Extension ClassLoader尝试加载，它俩都加载不了，再由Application ClassLoader加载。

------



## <a href="#0" name="2">【技术小说连载】我在JVM公司的那些年（二）——残酷的制度</a>

### **本节知识点预告：垃圾回收引用计数算法。**



今天是我第一天上班，我高高兴兴来到了新生代工作区，找到了自己的工位。

我正在整理我的工位，突然走过来一个人热情地给我打招呼：“你好，我是PersonServiceImpl。”

我一听就知道这是一个Service对象，也热情回复说：“你好，我是小史，是一个Person对象。”

PersonServiceImpl说：“哈哈，等你很久了，我是你的师兄，先带你了解一下公司的制度吧。”

我认真听师兄给我介绍。



**残酷的制度**

师兄：“我们公司是一个典型的淘汰制公司，因为公司要发展，资源有限，所以每隔一段时间，公司就要清理内部员工，进行裁员，我们把它叫做垃圾回收。”

我倒吸一口凉气，原来进了公司并不是进了保险箱，还有可能被裁员啊。

我：“什么样的员工会被裁员呢？”

师兄：“如果一个员工对公司没有价值了，他就会被裁掉。”

真的很残酷，有用的时候招进来，没用的时候就赶出去，反正还有大把大把的人挤破头想要进来。

师兄说完，把我的新工牌给了我：“工牌一定要收好，这里面有引用计数，如果别人需要你，就会给你的引用计数加一，不需要你的时候，引用计数就会减一，当你的引用计数变为0的时候，就是你离开公司的日子了。“

我接过工牌看了一下，果然，我的引用计数是1，引用我的人正是师兄PersonServiceImpl，我内心一阵感激。

**午饭的遭遇**

我在新领的电脑上搭建了一下工作环境，看了看文档，很快就到吃午饭的时间了。

师兄带我去食堂，在我打饭的时候，竟然有人拍我肩膀。

我回头一看，两个五大三粗，膀大腰圆的人正盯着我。

为首的说：“新来的吧？来老子这报到了吗？”

我：“你们是？”

那人指着我的鼻子非常不客气地说：“擦，连老子都不知道。”

旁边一个人赶紧谄媚道：“这是我们黑老大，新来的赶紧交保护费。”

说着两个人就在我口袋里搜，把我的五百块钱抢走了。

黑老大：“行了，这个月保你平安无事，下个月记得按时过来交费。”

真是无法无天，公司里怎么有这样的人？

我把我的遭遇和师兄说了一下。

师兄也咬牙切齿：“这两货简直就是公司的毒瘤，可惜现在也没有人能治他们。”

我心里暗暗发誓，一定要好好治治这两货。

（未完待续……）

------



残酷的制度，公司的黑势力，小史第一天上班似乎不是很顺利，他能在JVM公司顺利待下去吗？欲知后事如何，请听下回分解。

**小结**

垃圾回收是JVM最重要的机制，早期的垃圾回收是使用引用计数的算法，但是这种算法现在用得比较少了。



------



## <a href="#0" name="3">【技术小说连载】我在JVM公司的那些年（三）——恐怖的垃圾回收</a>

### **本节知识点预告：新生代三区，垃圾回收。。**



吃完午饭，师兄带我了解了一下我们公司工位的分布。

![img](http://r.photo.store.qq.com/psb?/V13Zm3q22D5cS0/.5RL1vjn9PauwDmulAVP.T9lg1EA.q0MCgtV802DTAw!/r/dL8AAAAAAAAA)

师兄：“我们都是java对象，所以我们都坐在堆内存这个区域，你看，堆内存区域分为两个主要的区域，一个是新生代，这里坐的都是新人，还有一个是老年代，里面都是公司元老级人物，工龄达到15的员工才有资格去老年代。”

原来在JVM公司，会根据员工的工龄来安排工位。

师兄接着说：“在新生代里，又分为三个区域，eden区，这里都是刚进公司的人，比如你，就坐在eden区。Survior1区和Survior2区，这都是经历过一次以上的垃圾回收之后的人坐的地方。”

我看了下，师兄就坐在Survior1区，可恶的黑老大也在Survior1区，而Survior2区却没人坐。

我：“为啥Survior2区没人坐呢？”

师兄：“等到公司进行垃圾回收的时候你就知道了。”

我：“我还有个问题啊，为啥Eden区这么大，而Survior1和Survior2区却有点小呢？”

师兄：“公司每年都招人很多，招进来都放在Eden区，但是里面很少有人能够熬过第一轮垃圾回收，所以实际上能够留下来的人并不多，Survior1和Survior2区没必要这么大。”

我倒吸一口凉气，原来这第一轮垃圾回收就这么残酷。



**恐怖的垃圾回收**

下午正干活呢，突然一队穿着警服的人冲进来大声吼到：“别干啦，停下，把你们的工牌拿出来准备好。”

面对这突如其来的场面，我不知所措，这家公司这么粗鲁的吗？

我慢慢回过神来，这应该就是所谓的垃圾回收吧？但是都不提前打声招呼吗？

这时，从警队队尾慢慢走来一个人，这人穿得温文尔雅，眼神里却冒着杀气。这人是垃圾回收器。

他用不大但极有穿透力的声音说道：“今天有98%的人要走。”

说完，命令警队把引用计数为0的人全部抓起来，押送出了公司。

整个过程，没有一个人敢说话，就连之前嚣张至极的黑老大，现在也跟一只温顺的小猫一样，趴在工位上一动不动。

公司里安静极了，地上掉根针都能听见。

垃圾回收器：“行了，剩下的人自己调整工位吧，好好干，希望下次还能再看见你们。”

说完，垃圾回收器转身带着警队离开了。

我又看了看我的工牌，工龄加一了，原来经历过一次垃圾回收，工龄就会增加一呀。

**（未完待续……）**

------



垃圾回收是十分恐怖的过程，好在小史挺过了这第一轮，等待他的会是什么？欲知后事如何，请听下回分解。

**小结**

JVM的堆内存分为两个区，新生代和老年代，达到一定年龄的对象会放到老年代。新生代又分为三个区，Eden区，Survior1区和Survior2区，刚进入JVM还没有经过垃圾回收的对象被分配在Eden区。



------



## <a href="#0" name="4">【技术小说连载】我在JVM公司的那些年（四）——工位调整</a>

### **本节知识点预告：标记——复制算法。**



还没从刚刚的垃圾回收缓过神来，大伙儿都忙着抢占工位了，只见Survior1区的老油条们赶紧抢占了Survior2区的好的工位。

师兄抢了一个远离走道的位置，这样不会被人打扰。

我过去找到师兄问到：“Survior2区不是不坐人吗？怎么现在大家都跑到Survior2区来了？”

师兄：“这也是公司的制度，进行垃圾回收之后，eden区和Survior1区留下的员工都会被转移到Survior2区，并且工位从前往后排列，这叫标记——复制算法。”



![img](http://r.photo.store.qq.com/psb?/V13Zm3q22D5cS0/Hv*Bypy5O2DbQ6A2SKyL7IIsyYBCbIWlPKNPMp.zFYA!/r/dIMAAAAAAAAA)

我：“为啥要这样呢？这样工位移来移去的不是很麻烦吗？”

师兄：“这你就有所不知了，这是公司的一位高管，吕老师发明的制度。”



**吕老师的故事**

师兄：“吕老师刚进公司的时候，还是和你差不多大，当时我们在进行垃圾回收的时候，用的还是标记——清除算法。”

小史：“这是什么算法？”

师兄：“这种算法很简单，也没有分这么多区，就是看看哪些人的引用计数是0，然后直接把他们清理出去，工位空出。”



![img](http://r.photo.store.qq.com/psb?/V13Zm3q22D5cS0/PYIPjv5nuVbDXG8F71ij.q3T1JodgbhvHy5DrFokQks!/r/dL4AAAAAAAAA)

小史：“对呀，这样不是挺好的吗？”

师兄：“但是一个个清理工位也是不容易的事情，你也知道，我们这边裁员比例高得厉害，刚刚你也看见了，裁掉了98%的人，意味着我们要一个个地清理98%的工位，这个工作量还是挺大的。”

小史：“哦，我明白了，与其清理98%的工位，不如让剩下的2%的人自己换个位置。”

师兄：“这只是其一，其实一开始公司也没有改变制度，直到发生了一件事情。”

师兄：“那年我们开拓新业务，一下子招进来100多人，但是却发现没有这么多连续的工位。频繁的垃圾回收导致了大量的工位碎片。”



![img](http://r.photo.store.qq.com/psb?/V13Zm3q22D5cS0/51WzFrv*vQtuOPNdu3RzzVjuqqG0zAqExIYAGzUxXLE!/r/dIMAAAAAAAAA)

师兄：“这下这个团队只能分开坐，很快他们就开始抗议了，这时候吕老师把他的设计讲了出来。”

吕老师：“我建议把新生代区分为三个区，eden区，Survior1区和Survior2区。”

吕老师：“一开始的时候，新来的同事都在eden区。”



![img](http://r.photo.store.qq.com/psb?/V13Zm3q22D5cS0/zXOIbW0GcchBSiFd2LRU1XGJSsmuy16ZvF.yxgNP8LM!/r/dD4BAAAAAAAA)

吕老师：“当进行第一次垃圾回收的时候，eden区上留下来的同事就移动到Survior1区，然后把eden整体清空。这样，新来的同事在eden区就有连续工位。”



![img](http://r.photo.store.qq.com/psb?/V13Zm3q22D5cS0/vA1UMPx8kmZUGr*OukRk*KKIB3ZLmFNL1YYbV6h42hg!/r/dLgAAAAAAAAA)

吕老师：“当第二次垃圾回收的时候，eden区和Survior1区留下来的同事就移动到Survior2区，然后把eden区和Survior1区清空。”



![img](http://r.photo.store.qq.com/psb?/V13Zm3q22D5cS0/uhE.V1vKlASk6FQ1Aca44TGc2tgmrzth*IaXa61QQ2w!/r/dLsAAAAAAAAA)

吕老师：“当第三次垃圾回收的时候，eden区和Survior2区留下来的同事就移动到Survior1区，然后把eden区和Survior2区清空。以此类推。”

![img](http://r.photo.store.qq.com/psb?/V13Zm3q22D5cS0/KM.HmB6zSq5cs7LTyboC2.q2p6fB017G*PNkQYtqeLM!/r/dFQBAAAAAAAA)

这时候马上就有其他同事提出质疑：“也就是说Survior1区和Survior2区是交替使用对吧？”

吕老师：“是的。”

其他同事：“但是你这样移来移去有什么意义呢？”

吕老师：“首先不需要一个一个去清理eden区或者Survior区的工位，要知道，把一个区整体直接清空比一个一个工位清理要轻松很多。其次就是解决了工位碎片的问题。”

公司高层觉得这个方案不错，决定试运行一段时间。

结果果然提高了效率，也没有出现一个团队分配不到连续工位的情况了。

后来公司采用吕老师的方案，吕老师也很快晋升到了公司高层，坐到了老年代工作区。

听了吕老师的故事，小史竟有一丝敬仰之情，自己也想做一个改变公司制度的人。

（未完待续……）



**小结**

目前的垃圾回收器，在新生代区基本都是使用标记——复制算法，这样能够提高清理效率，有效避免内存碎片。



------



## <a href="#0" name="5">【技术小说连载】我在JVM公司的那些年（五）——主动出击</a>

### **本节知识点预告：循环引用。**



我也赶紧搬到Survior2区，兢兢业业地工作起来。

由于我业务能力突出，很多同事都开始引用我，什么PersonDAO呀，PersonCache呀，都给我引用计数加了一。

我现在完全不愁被垃圾回收。

但是一想到下个月快到了，又要给黑老大交保护费，心里有点不爽。

我决定找点线索，究竟谁在引用黑老大？

**主动接近**

我买了一包烟，主动过去给黑老大套近乎：“给大佬递烟。”

黑老大：“你小子还挺能来事儿，不错不错，以后保护费给你优惠点，哈哈哈。”

我表面上恭恭敬敬，实际上暗地里看了下黑老大的工牌，引用计数是1，引用他的人是黑小弟。

我又看了下旁边黑小弟的工牌，引用计数是1，引用他的人是黑老大。

这下我终于明白了：“闹了半天，原来这两人是相互引用，公司根本没有其他人需要他们！”



![img](http://r.photo.store.qq.com/psb?/V13Zm3q22D5cS0/GEGvvxYEwt5HjDGmSt5UqzAa9UeHX1pwzpJbZmsyw20!/r/dLYAAAAAAAAA)



**垃圾回收**

很快，公司又迎来了一次垃圾回收，像往常一样，垃圾回收器让大家准备好工牌放在桌上，挨个检查引用计数为零的人，全部押送出公司。

就在垃圾回收器要离开的时候，我站起来说了一声：“且慢！”

我声音不大，但是在这原本安静的公司里却显得格外刺耳。

底下也开始议论纷纷：“这人谁呀？竟然敢和垃圾回收器说话。”

“貌似是新来的，不知道葫芦里卖的什么药。”

垃圾回收器头都没回：“有事吗？”

我战战兢兢地说：“麻烦你再检查一下这边黑老大和黑小弟二位的工牌。”

黑老大一听竟然是给他找事，狠狠地瞪了我一眼，恨不得用眼神杀死我。

我却不慌不忙，根本没有正眼看他，只是用余光扫了一下。

垃圾回收器也不是好惹的，他严厉地问：“你是在质疑我的工作？”

我恭恭敬敬地回答：“并没有，只是虽然这两人的引用计数都是1，但是他们是相互引用，公司里再也没有第三个人需要他们，理论上应该被垃圾回收掉吧？”

垃圾回收器：“哦？有这等事？”

垃圾回收器走到黑老大和黑小弟旁边再次查看了他们的工牌，确实是这样，他沉默了几秒。

我从余光里看到，黑老大和黑小弟已经瑟瑟发抖，都不敢正眼看垃圾回收器。

垃圾回收器：“你说的这种情况我会考虑一下，这次就先不回收他们了。”

没想到是这样的结局，我心里咯噔一下……



（未完待续……）



**小结**

引用计数的垃圾清理算法，没有办法清理循环引用，所以这种算法现在用得非常少了。



------



## <a href="#0" name="6">【技术小说连载】我在JVM公司的那些年（六）——智斗黑老大</a>

### **本节知识点预告：可达性分析算法。**



由于与黑老大结下了梁子，我在公司更加小心行事。

这天，我下班，像往常一样去上个厕所再回家，没想到厕所里竟然碰到了黑老大和黑小弟二人。



**狭路相逢**

黑老大和黑小弟一下子把我控制住了。

黑老大：“哟，这不是前段时间敢和垃圾回收器对话的小史吗？”

我：“你们想干什么？”

黑老大：“你说的对，我们两个是循环引用，要不是你，我们可以在公司一直待下去，但是现在我们有点危险，需要你帮我们做一件事情。”

我：“什么事情？”

黑老大：“你引用我们俩。”

我坚决地说：“不行，这是违反公司规定的！”

黑老大：“看来你是敬酒不吃吃罚酒。”

旁边的黑小弟已经拿出了菜刀。

这两货果然是暴徒，光天化日之下就敢在公司行凶，我好汉不吃眼前亏。

我：“先别忙，行吧，我引用你们。”

黑小弟：“早这样多好”，说着把菜刀又收了回去。

我拿出工牌引用了他们俩，这一切都做好之后，黑老大竟然抢走了我的工牌。

黑老大：“工牌先没收了，万一你反悔了啥时候又把我们的引用给去掉了，那我们不是白忙活了？”

看来我的小心思被他们看破了，这下我没了工牌，没法做手脚了，我真是恨这两货恨得牙痒痒。



**垃圾回收新制度**

很快，公司又迎来了一次垃圾回收，不过这一次，和往常有点不太一样，垃圾回收器先开口了。

垃圾回收器：“鉴于上次有位同事提到的循环引用的问题，经公司高层讨论之后，决定使用另一种算法来决定哪些员工需要被垃圾回收。”

大家都很好奇会是什么样的算法，毕竟是和自己能否留在公司密切相关的，但是也没有一个人说话，大家都安静地听着。

垃圾回收器顿了一会儿开口了：“这种算法叫可达性分析算法，我们会以GC Roots为起点，去寻找他们引用的对象，然后一直往下找，找出整个引用链，没有在引用链上的员工，就会被垃圾回收。”



![img](http://r.photo.store.qq.com/psb?/V13Zm3q22D5cS0/EP0HhfBBASdS.Epgt0QR2nuXZx.0KcZYZ.9OImz2Fuw!/r/dL4AAAAAAAAA)

听到这里，大家都开始盘算自己会不会被垃圾回收，但是算来算去，发现没有GC Roots没法算啊。

我：“哪些人有资格做GC Roots呢？”

垃圾回收器：“你们这里的人都没有资格，包括老年代里那些人，公司规定，能够做GC Roots的人是这些：

虚拟机栈中引用的对象(局部变量)

方法区中类静态属性引用的对象(static对象实例)

方法区中常量引用的对象(常量实例)

本地方法引用的对象

我小声问师兄：“这些人你都认识吗？”

师兄：“这些人都不在堆内存这个区，我也只是有时候在电视里看到过，没见过真人。”

就是这样，公司里总有一些你见都没见过的人，但他们却能决定你的去留。

还好，由于有师兄，还有几位同事引用了我，我在引用链中，而当垃圾回收器走到黑老大和黑小弟面前时……

垃圾回收器：“把他俩押送出公司。”

黑老大大吃一惊，大声喊到：“冤枉啊，我有被引用，这个人，小史，他引用的我！”

我走到黑老大面前，拿回我的工牌：“看来你还没明白，为了让你安安心心地离开，我就告诉你吧。”



（未完待续……）



**小结**

现在的垃圾回收器大多都用可达性分析算法来决定一个对象是否该被垃圾回收，从而解决了循环引用的问题。



------



## <a href="#0" name="7">【技术小说连载】我在JVM公司的那些年（七）——玉石俱焚</a>

### **本节知识点预告：四种引用。**



我轻蔑地看着黑老大说：“你难道不知道引用分为四种吗？”

黑老大瞪大了眼睛：“什么？！”

天天在公司混日子，连最基本的业务都不熟悉，最后被开了都不知道怎么回事，也算是罪有应得吧。

我：“入职新人培训的时候就说过了，咱们公司的引用分为4种，强引用、软引用、弱引用和虚引用。”

我：“培训的老师还告诫我们，最常用的就是强引用，如果真的是对你有用的人，一定要用强引用，对于这种员工，公司如果发现工位资源不足，宁愿抛出OutOfMemory的异常也不会将他们裁员。”



![img](http://r.photo.store.qq.com/psb?/V13Zm3q22D5cS0/HmnMHuTaP0.X1ioJF*TKtTAOpi2v9TVOXowr*GzjiMg!/r/dE8BAAAAAAAA)



黑老大：“你给我的不是强引用？是软引用？”

我：“软引用？软引用引用的对象，在垃圾回收时，如果发现工位资源不足，即使被引用了依然会被回收，**但是在工位资源充足的情况下是不会回收的。**”



![img](http://r.photo.store.qq.com/psb?/V13Zm3q22D5cS0/RiSt.1XuMahRJYdV7mJLq1UAqEFRYT5tk4NUrzygMLk!/r/dDQBAAAAAAAA)

黑老大：“但是我们现在工位明明充足呀，难道你给我的是弱引用？”

我：“总算开窍了。弱引用引用的对象，在垃圾回收时，不管工位资源充不充足，都会被回收。”



![img](http://r.photo.store.qq.com/psb?/V13Zm3q22D5cS0/IuPGYKW3W2SKp5WOyokdbkUlb4G.rNC*OG*O1u2afrQ!/r/dLYAAAAAAAAA)

黑老大：“我明白了，你给我的是弱引用。那最后的虚引用又是怎么回事？”

平时不务正业，被开了倒是出奇地好学。

我不耐烦地说：“虚引用看名字就知道，是一个形同虚设的引用，行了，你安心走吧。”



![img](http://r.photo.store.qq.com/psb?/V13Zm3q22D5cS0/K*Xn8IcwMjD5GAfB*COL*BXKP8QUlHL4xKlnvZ.PH5k!/r/dFIBAAAAAAAA)

黑老大恶狠狠地说：“你别得意得太早，我还会回来的。”



**不对劲**

终于干掉了黑老大，我一下子成了公司的小明星，走到哪里都有人回头看我，弄得我都有点飘了。

不过过了几天我就发现，大家看我的眼神开始不对劲，与其说是赞许，不如说是担心，大家的眼神里都有一丝怜悯。

怎么回事？我找到师兄。

我：“为什么你们看我的眼神这么奇怪？”

师兄也面露难色：“我实话跟你说了吧，前两天黑老大找到我们，给了我们一大笔钱，让我们在下一次垃圾回收的时候，把你的引用去掉。”

这个可恶的黑老大，走了也要把我拉下水。

我：“那你们都照做啦？”

师兄：“黑老大拿出了所有的积蓄，把所有和你有关系的人都给买断了，说是要和你玉石俱焚，他这次是铁了心要把你弄出去呀。而且如果不合作，他还会对我们的家人下手，小史，对不起，你赶紧找下家吧。”

我也不想为难师兄：“行，明白了，谢谢师兄告诉我这些。”



**偶遇吕老师**

我不知道什么时候会是下一次垃圾回收，但是我知道，那就是我要离开公司的日子，我一个人在公司里喝闷酒。

突然一个人拍了拍我的肩膀：“你是小史吧？”

我回头一看，一个笑眯眯的大哥哥正在看着我：“对，我是小史，你是哪位？”

大哥哥：“你叫我吕老师就好。”

我：“吕老师？就是那个让公司放弃标记——清除算法而改用标记——复制算法的吕老师？”

吕老师：“正是在下，所以我也想认识一下让公司放弃引用计数算法而改用可达性分析算法的小史君呀，哈哈！”

我：“幸会幸会，很高兴认识你。”

我给吕老师满上酒：“不过，我很快就要离开公司了。”

吕老师：“噢？怎么回事？

我把事情一五一十告诉吕老师，并且抱着最后一丝希望：“吕老师，要不，你引用我吧？”

吕老师：“我不能随随便便引用你，这是违反公司规定的，但是我有一个办法，你可以试一试。”



**（未完待续……）**



------

吕老师有什么办法，能够帮助小史死里逃生？欲知后事如何，请听下回分解。

**小结**

在JVM中，引用分为四种，强引用、软引用、弱引用和虚引用，不同的引用强度对应着不同的垃圾回收行为。

![img](http://r.photo.store.qq.com/psb?/V13Zm3q22D5cS0/wlcHY3U63oLXLdcTZ18tBl19jTvxKEenvgKEL1a5ENQ!/r/dFQBAAAAAAAA)



------



## <a href="#0" name="8">【技术小说连载】我在JVM公司的那些年（八）——死里逃生</a>

### **本节知识点预告：finalize方法。**



我就像抓住了救命稻草，赶紧问吕老师：“什么方法？”

吕老师：“这是一个非常古老的方法了，知道这个方法的人不多，而且现在公司也不推荐大家这样做。但是你现在情况特殊，也许可以一试。”

我：“哎呀我的吕老师，你就别卖关子了，赶紧告诉我吧。”

吕老师凑到我耳朵旁：“只需如此如此……”

我疑惑地看着他：“这能行吗？”

吕老师稳如狗：“放心吧，没问题的。”

听了吕老师的建议，我赶紧秘密找到师兄，把吕老师跟我说的方法一五一十告诉了师兄，并请他帮忙。

师兄也很惊讶：“还有这种方法？这能行吗？”

我表面也稳如狗：“放心吧，没问题！”

但是实际上我内心慌得一批。



**又是垃圾回收**

这一刻终于到来，公司停止了所有业务，垃圾回收器还是像往常一样无情。

没有人引用我了，我自然没有在可达性分析的引用链中，我要被回收了，但是就在这时，垃圾回收器开口说话了。

垃圾回收器：这个对象，小史，他覆盖了finalize方法，先别忙着把他赶出公司，先押送地牢。其他人都赶出公司吧！

一切都在计划中，只要覆盖finalize方法，并且这个方法从来没被执行过，垃圾回收器就不会马上把你赶出公司，而是会把你放到地牢。

我跟着警卫来到了地牢，说是地牢，其实我一看就知道，这是一个队列，里面的人都排队等着一个人。

过一会儿，这个人过来了，他是一个低优先级线程，他的工作就是执行我们这个队列中每个人的finalize方法。

我和师兄早就商量好了，在finalize方法中，我让师兄重新引用了我，这下我又有引用了，我知道已经大功告成，只需静静地等待出去的时机就行。

另一边，黑老大一看我已经没有在工位上，以为已经把我弄出了公司，满意地去找下家公司去了。只是他没想到，我并没有被赶出公司，而是在地牢里伺机而动。

又一次垃圾回收到来了，垃圾回收器再次通过可达性分析算法检查我们的引用，这次我已经在引用链中了，于是，我又回到了我自己的工位。

***（未完待续……）***



------

到此，小史终于彻底搞定了黑老大，他在JVM公司中还会遇到什么问题？欲知后事如何，请听下回分解。



**小结**

现在我们不推荐在finalize方法中去释放资源，因为它什么时候会被调用是不确定的。



------



## <a href="#0" name="9">【技术小说连载】我在JVM公司的那些年（九）——潜规则</a>

### **本节知识点预告：进入老年代的条件。**



终于摆脱了黑老大，我在公司过了一段安安静静的日子。 

随着一次次垃圾回收，我已经有 12的工龄，而师兄，已经达到 15的工龄要晋升了，他成功去了老年代。 

原来工龄达到 15就可以晋升进入老年代。 

我又兢兢业业地工作了一段时间，经历了几次垃圾回收，我也晋升到了老年代。 

第一次来到老年代，和我想象的还不太一样，这里很大，和新生代一样大，但是却没有分成 eden区、 survior1区和 survior2区。 

这里的人明显比新生代的人要稳重很多，感觉个个都很厉害的样子。毕竟大家都是经过了至少 15次垃圾回收的洗礼，都是公司的精英啊。 

但是很快， 现实就过来打脸了。 



**潜规则**

今天公司空降了一位高管，自称是竞争对手公司的架构师，还带领了一个小团队来到我司入职。 

HR小姐姐：“这是一个 大对象，别往新生代领了， 直接进入老年代。” 

就这样，空降架构师直接进入了老年代。 

我不服气，找到 HR小姐姐问：“为什么他可以不去新生代直接进入老年代？” 

HR小姐姐：“你看他带了这么多人，是一个大对象，公司有规定， 大对象可以直接进入老年代。” 

好吧，我竟无言以对。 

又有一次，公司进行扩张，一下子招了很多人，并且质量都不错，都在新生代的 eden区上班。 

到了垃圾回收的时候，由于大家都有被引用，所以这次的 回收率很小，结果这些人放在 survior1区放不下。 

HR小姐姐又出面了：“ 按照工龄由高到低排个序，如果某个工龄层中的对象大小加起来超过了survior1区的大小，他们和比他们工龄大的员工都去老年代。” 

我一看，第一个不服：“这些人工龄还没达到晋升条件，怎么能去老年代呢？” 

HR小姐姐：“这是公司的绿色通道， 这一届优秀的人太多，可以通过绿色通道直接晋升进入老年代。” 

没想到公司里关于晋升的 潜规则这么多，感觉对于我们这些兢兢业业通过努力达到 15工龄的人有点不太公平，但是也没有办法，毕竟都是公司的规章制度。 



**谈心**

虽然已经接受了现实，但是我心里还是有点不太舒服，我找到师兄讨论此事。 

师兄却哈哈大笑：“你有没有思考过制度背后的原因呢？” 

我：“额，这个，我到没有想过，公司制度不是只要死记硬背就行了么？” 

师兄：“非也非也， 如果你不理解制度背后的原理，死记硬背是记不住的。” 

我：“那我想想看啊， 对于大对象来说，如果让它进入eden区，会占用大量工位，导致其他员工工位不足？” 

师兄：“不仅仅是这样，你想， 大对象如果第一轮垃圾回收没有被淘汰，它将进入survivor1区……” 

我：“哦，我知道了， survivor1区很小，不一定容得下这个大对象吧？” 

师兄：“对咯。所以为了避免麻烦，公司才规定，让大对象直接进入老年代。” 

我：“那绿色通道又是怎么回事？” 

师兄：“那就更简单了，因为那一届优秀员工较多， 让他们都进入survior1区同样会存在放不下的问题。所以公司规定，让他们直接进入老年代了。而且如果他们能进，那么比他们工龄大的当然也能进了。” 

我：“……好吧，虽然不情愿，但是也只能接受了。” 

（未完待续……）

到此，小史终于接受了公司关于晋升老年代的潜规则，但是到了老年代之后，会有什么新的问题等着他呢？欲知后事如何，请听下回分解。

**小结**



什么样的对象可以进入老年代？大对象、长期存活对象、一大批同龄对象。



------



## <a href="#0" name="10">【技术小说连载】我在JVM公司的那些年（十）——不一样的垃圾回收</a>

### **本节知识点预告：老年代垃圾回收。**



接受了公司潜规则，我在老年代也兢兢业业地工作起来。

老年代不愧是老年代，已经快一个月了，这里一次垃圾回收都没有发生，新生代都已经发生好几次垃圾回收了。

这对于公司来说，其实是有利的，垃圾回收的次数越少，我们工作时被打扰的次数就越少，就越能高效率地工作。

只是每一次新生代垃圾回收，都有几个同事进入老年代，慢慢的，老年代的工位也越来越紧张，已经快坐不下了。



**垃圾回收**

该来的还是来了。这天，我正在奋力运行代码，突然一队穿着警服的人闯进了老年代，我们立刻停下了手中的活。

队尾慢慢走来一个人，身穿一身警服，却是一副凶神恶煞的样子，他也是垃圾回收器。

原来老年代的垃圾回收器和新生代的垃圾回收器不是同一个人啊。

垃圾回收器开口说话了：“可能有些人还不认识我，自我介绍一下，我是垃圾回收器，负责老年代的垃圾回收工作，请大家配合一下。”

相比于新生代温文尔雅却冷酷的垃圾回收器来说，这位表面上凶神恶煞的垃圾回收器倒是更有礼貌，果然是人不可貌相。

垃圾回收器话音刚落，警队的人就冲了上来。但是与新生代直接把人带走不同的是，警队的人并没有一上来就把人带走，而是对大家进行标记，给在GCRoot引用链中的人做了一个记号。



![img](http://r.photo.store.qq.com/psb?/V13Zm3q22D5cS0/MQHf5Tf9UWsZzz83AvdQZcqoTQDhGHWg2Aj16u9QbEk!/r/dDcBAAAAAAAA)

记号做完之后，又来第二轮，直接对大家进行工位调整，让有记号的同事们从老年代区第一个工位开始依次排列。排好之后，把剩下的工位直接清空了。这次大概清理了6.25%的工位。



![img](http://r.photo.store.qq.com/psb?/V13Zm3q22D5cS0/3Zp11unMYdbSPWbgLtv9sXowOdU9bEa7ePuyOI.Rd3w!/r/dLYAAAAAAAAA)

整个过程比新生代垃圾回收慢了很多。

我的工位也进行了调整，并且调整完之后，我和师兄坐在了一起。



**讨论**

垃圾回收器走了之后，我问师兄：“师兄，这老年代的垃圾回收和新生代完全不一样啊？”

师兄：“是的，老年代的这个垃圾回收算法叫做标记-整理算法。”

我一听有点耳熟：“我记得新生代一开始用的是标记-清除算法。”

师兄：“对的，但是标记-清除算法不是有一个致命的缺点么？”

我：“是的，我记得标记-清除算法会产生工位碎片，这将导致一些稍大一点的团队无法分配到连续的工位，必须分开坐。”

师兄：“没错，所以老年代的标记-整理算法在标记-清除算法上进行了改进，把大家的工位进行整理，把空余的工位归拢在一起，避免了工位碎片。”

我：“哦，原来如此，不过我还有一个问题啊，为什么老年代不像新生代一样，用复制算法呢？”

师兄：“这个问题问得好，这和这两个区的特点有关。新生代的特点是回收率高，一次回收之后，剩下的员工很少了，所以让他们迁移工位，把他们复制到另一个survior区，成本很小。但是老年代……”

我瞬间明白了：“老年代回收率低，如果采用复制算法，那么有很多员工需要复制，survior区也需要设置得很大，反而得不偿失了。”

师兄：“哈哈，说得没错，而且你要注意，因为新生代有两个survior区，它们是交替使用，所以其实survior区总体使用率只有50%。”

我：“哦，这也是复制算法的缺点之一呀。”



**方法区**

师兄：“对了，明天上班别迟到。明天方法区的人会过来和我们进行交流。”

方法区？就是有资格做GCRoot的人所在的区？哈哈，早就想会会他们了。

我：“没问题，明天我一定早来。”

（未完待续……）



------



小史已经挺过了老年代的垃圾回收，马上要会见方法区的大佬了，方法区的人和新生代老年代的人有什么区别？欲知后事如何，请听下回分解。

 

**小结**

老年代的垃圾回收采用标记-整理算法，之所以这样是因为老年代的回收率并不高，所以只需要将少量未被标记的对象清理就好，而为了防止内存碎片的产生，会对内存中的对象再进行一次整理，这种方法也有缺点，就是很慢。



------



## <a href="#0" name="11">【技术小说连载】我在JVM公司的那些年（十一）——人事部的交流</a>

### **本节知识点预告：方法区简介。**



以往都是十点才到公司的小史，今天八点多就到了，他是来听 方法区的大佬来进行分享交流的，顺便了解下方法区都是些什么人，为什么他们可以当 GCRoot。 

小史认为， GCRoot是引用链的根节点，是永远不会被回收的，所以对他们还是挺崇拜的。（小史的理解不一定对哈） 



**分享**

九点一到，一位女同事走上了讲台：“大家好，我是小林，是方法区的员工，我们方法区主要负责记录大家的 类信息，常量，静态变量等数据 ……” 

说着说着，就开始介绍起他们的工作流程。 

小林：“其实当你们的简历，也就是你们的 .class文件交给公司的时候，公司就会对这份简历进行分析，里面定义的一些 类信息呀，静态变量呀，常量呀，会在我们 方法区进行存储。” 

我：“哦，所以你们保存了我们每个员工的基本信息？” 

小林：“没错，每个员工入职之后，他的基本信息就在我们这里保存下来。” 

我：“原来如此，不愧是人事部。” 

小林：“其实方法区除了存储这些基本信息之外，还有一个 运行时常量池也在方法区，但是这是另一个同事负责的，我也不太了解，后面有机会可以请他来分享。” 



**GCRoot**

半个小时之后，小林终于讲完了。 

小林：“ ……今天的分享就到这里了，大家还有什么问题吗？” 

我赶紧抓住机会问了 GCRoot的问题：“我记得方法区里面是有 GCRoot的，这块能介绍一下吗？” 

小林：“好的，这就要说到 垃圾回收器了，他每次进行垃圾回收的时候，都会先到我们这里来领一份表，我们会把每个类的 静态变量和常量这两个信息给他，据说 他会把这两个东西当做GCRoot，去进行引用链分析，后面的事情我就不知道了 ……” 

我：“哦，明白了，谢谢！” 



**会后**

会议结束后，我仔细理了理小林的分享，结合之前经过的垃圾回收经历，我大概明白了。 

方法区和堆内存其实是JVM公司的两个区域。当一个类被加载到 JVM公司时，它的 类信息，静态变量，常量会被存储在方法区。而进行垃圾回收的时候，会把 方法区的静态变量和常量作为GCRoot之一，从它们引用的对象开始分析引用链。 

![img](http://r.photo.store.qq.com/psb?/V13Zm3q22D5cS0/gw3AdJHmKlr1wncBbA2kxVqS5KlDFGVd.5HjUMIaSx8!/r/dMUAAAAAAAAA)



想着想着，碰到了师兄。 

师兄：“怎么样啊？小史，有没有收获？” 

小史：“有啊，收获还挺大的，这种分享真的不错，能够让我们了解公司其他人都在做什么事情。以后还有这样的分享记得通知我啊！” 

师兄：“嗯，最近就有一个，下个礼拜， 虚拟机栈中的同事会来进行分享，你要去吗？” 

虚拟机栈？我记得虚拟机栈中也有可以作为GCRoot的人，这我可不能放过啊。 

小史：“当然要去啦！” 

（未完待续……）

通过这次分享，小史已经了解了方法区人事部的一些事情，了解了GCRoot的一部分源头。接下来的虚拟机栈同事的分享，又有什么内容？欲知后事如何，请听下回分解。



**小结**

方法区是和堆内存并列的一个区域，它主要记录类信息、类静态变量、类常量等信息，其中还有一个运行时常量池。方法区的静态变量和常量可是作为GCRoot的哟。



------





