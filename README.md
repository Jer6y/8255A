# 8255A
# 描述:
1.8255A in logiSim<br />
2.实现功能 A 和B端口的方式0 外设可以对A和B端口进行输入和输出<br />
3.实现手段 每个端口采用两个Reg进行实现 <br />
对于CPU而言:<br />
  &nbsp;&nbsp;写入是往第一个Reg进行写入<br />
  &nbsp;&nbsp;读取时则根据当前端口的模式进行选择<br />
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;若工作模式为输出模式 则从第一个Reg进行读入<br />
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;若工作模式为输入模式 则抢占外设对第二个Reg的权限 锁存同时读入<br />
  &nbsp;&nbsp;对于外设而言:<br />
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;在输入模式下: <br />
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;可以使用PAIN 对A端口的第二个Reg进行写入<br />
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;此时不应该使用PAOUT<br />
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;在输出模式下：<br />
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;可以使用PAOUT得到A端口的第二个Reg的值<br />
    &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;此时PAIN被禁止<br />
4. 特别说明 由于Logisim并不允许一个引脚即是输入引脚 又是输出引脚 所以存在PAIN 和PAOUT的说法 <br />
5. 更细节的 <br />
     &nbsp;&nbsp;&nbsp; 若A或者B端口在输入模式 也可以利用PAOUT或者PBOUT对该端口的第二个Reg获取值<br />
      &nbsp;&nbsp;&nbsp;若A或者B端口在输出模式 也可以利用PAIN或者PBIN对该端口的第二个Reg进行写入<br />
7. 特别说明 文件格式为Logisim的circ 模式 同时使用的仿真软件为Logisim-evolution (非logisim)<br />
