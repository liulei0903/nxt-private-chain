# nxt-private-chain
NXT未来币私有链版本

# 背景和目标：
本人是JAVA工程师，对区块链技术非常有兴趣，看过《精通比特币》等书籍，所以对比特币底层原理是点了解的，但没有到代码级别，比特币使用的C++语言又看不懂，
后来找到有个JAVA语言编写的数字货币[NXT未来币](https://github.com/Blackcomb/nxt),二话不说把代码下载部署起来，看看P2P网络，共识算法，挖矿，交易的广播，区块的广播到底是怎么实现的。  
但问题来了，NXT可以运行起来，但默认连接的外网公有链，发起交易就需要去交易所购买NXT币，这样怎么方便测试Debug呢？  
当然不行，我就想着把它改成私有链，因为我之前使用过以太坊的私有链Geth客户端，只用改下创世区块genesis.json文件即可。但NXT使用私有链没这么简单，看NXT白皮书也没找到改成私有链的方法，后面凭着对区块链的基础知识
(基础很关键)+NXT白皮书成功改成了私有链

# 行动：
为了让NXT部署私有链，主要修改点：  
1.将项目修改为在Eclipse下开发的Maven项目  
2.nxt-default.properties文件的nxt.defaultPeers参数，该参数指定了P2P网络的对等节点IP地址，可以是局域网  
3.修改创世区块信息，由于NXT的发布模式与比特币不同，比特币是不断减慢的速率逐步发出，NXT是IPO发行模式，将所有的币一次性释出， 而且只分给73个人（NXT团队开发人员或利益相关方）,
分币的逻辑写到java代码中，如果我要一个有币的账户测试，必须在创世区块的分币逻辑中分给我创建的账户。所以我把分币给73个账户的逻辑改成了分两个我自己控制的账户。  
4.NXT为了停止向下兼容，在一些逻辑处理中判断区块链的高度小于某个数就不做处理，由于我们私有链高度是0开始，导致很多逻辑执行不了，所以我把涉及高度判断的地方，把高度降低到0  
总结：修改的地方并不多，可以用 "update by liulei"关键字去搜索，我把修改的地方都加了这个注释  

# 结果：
由于NXT使用IPO发行方式，在以太坊推出智能合约后，NXT在市场上没有了技术亮点，也就慢慢没人关注了，但这不影响我们学习它的技术，看看NXT的POS共识算法，P2P传播网络，交易的广播，区块的打包、广播等，还是很有收获的
为此我也写了一份学习笔记[NXT未来币区块链学习笔记.docx](https://github.com/liulei0903/nxt-private-chain/blob/master/private-chain-nxt-master/docs/NXT%E6%9C%AA%E6%9D%A5%E5%B8%81%E5%8C%BA%E5%9D%97%E9%93%BE%E5%AD%A6%E4%B9%A0%E7%AC%94%E8%AE%B0.docx)，里面标记的NXT与比特币的差异、关键功能的简易流程图及JAVA入口类，方便有兴趣的同学学习。  
ps：学习过程中我们要带着问题去思考，学区块链之前我领导问我“大家一直诟病比特币，以太坊的TPS太低，那到底是什么决定了区块链平台的TPS?如何提升TPS呢？”  
关于这个问题我在 [NXT未来币区块链学习笔记.docx](https://github.com/liulei0903/nxt-private-chain/blob/master/private-chain-nxt-master/docs/NXT%E6%9C%AA%E6%9D%A5%E5%B8%81%E5%8C%BA%E5%9D%97%E9%93%BE%E5%AD%A6%E4%B9%A0%E7%AC%94%E8%AE%B0.docx) 中有自己的解答，可能有不对的地方，欢迎感兴趣的同学一起讨论，谢谢。  

# 创世区块中分配了币的两个账户：  
用户1：  
账户地址：NXT-JTQV-3YYD-RLFY-7FB58   
私钥：end apart laid tough handle spirit tease random fought adore truck stress  
公钥字符串：e115049da84efb677d48caf10628bbe4e732fe53715c14aaccf70c8499e30d03  
  
用户2：  
账户地址：NXT-7JHU-CNU9-PXZC-7ZF4D  
私钥: spell nation scratch satisfy watch closet normal color heat due recall movie  
公钥字符串：befe07305a13e1ab3c2018266e7dadae7cfd147f76c051e8e588b160d850a218  
