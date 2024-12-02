```
提示:16
标题:账户多签名
作者：马库斯赵（@赵红）<zhaohong229@gmail.com>
讨论到 https://github.com/tronprotocol/TIPs/issues/16
状态:最终
类型:标准跟踪
类别：真相与和解委员会
创建时间:2018-12-27
```



##动机

1.不支持帐户访问控制；

函数抽象平衡（）公共公开
uint balance = this.balance；
要求（余额>0）；所有者。转账（余额）；
提款（余额）；

杂合物固化度^0.5.8；
合同 MyContract {
地址私人所有者；
构造函数（） 公共 {
所有者=发件人；
}
函数抽象平衡（）公共public {
ler = 所有者，“只有所有者才能使用
// 获取合约的余额
uint256余额=地址（此）。
// 确保余额大于0
要求（余额 > 0， "无余额"
// 转移余额给合约所有者
转账（余额）；0, "No balance to withdraw");msg.sender.transfer(balance);

  

    
 
  

    响应码代码 = 1；
    字符串消息=1；


#### 添加签名
*TJGFPbyb7cabepNoZW7g9CbMY4t1DWXb2J


