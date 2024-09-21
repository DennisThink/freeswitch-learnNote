sofia相关指令：

 

1、status —— 显示当前状态

2、sofia status —— 显示sofia 的运行状态（查看freeswitch监听的IP和本电脑ip）/查看配置网关状态

　  sofia/sofia help —— 显示sofia命令的帮助信息

3、sofia status profile —— 查看trunk配置（网关gateway配置）

4、sofia status profile internal/external  —— 列出某个Profile的状态

5、sofia status profile internal reg —— 查看所有已经在其上注册的用户/列出某个Profile上所有已注册的用户

　  sofia status profile internal reg 1000 —— 过滤某些符合条件的用户（查询用户1000的详细信息，如该用户实际的IP地址（Contract字段表示））

　  sofia status profile internal user 1000 —— 列出某个特定的用户 ?????

　  sofia status gateway gwl —— 列出网关的状态

     （以上的命令都可以将 status 用 xmlstatus 来替代，已列出XML格式的状态，这样比较容易用其他程序解析）

6、sofia global siptrace on —— 可以看到更多sip通信的细节（如SIP软电话的用户注册的细节）

7、打开SIP消息 —— sofia profile internal siptrace on
                                  sofia profile external siptrace on

      关闭sip消息 —— sofia profile internal siptrace off
                                  sofia profile external siptrace off
8、sofia profile external/internal rescan/restart —— 网关配置重启生效

      sofia profile external restart —— 重启 external 生效

9、

10、Profile相关命令-汇总：（9.3.2）

　

常用的启动、停止、重启某个Profile额命令分别如下：

     　　　　　　　　　　　　　　　　　　　　　　   sofia profile internal start —— 启动

　　　　　　　　　　　　　　　　　　　　　　　　 sofia profile internal stop —— 停止

　　　　　　　　　　　　　　　　　　　　　　　　 sofia profile internal restart —— 重启



  　　　　　　　　　　　　　　　　　　　　  　　　　sofia profile internal rescan 

添加了一个新的gateway以后，也可以使用上述rescan指令读取。

如果是修改了一个网关，则可以先将该网关删除，再rescan，如：

　　                                                                                               sofia profile external killgw gw1 —— 删除一个网关

　　                                                                                               sofia profile external rescan —— 重读参数

下列命令可以指定某个网关立即向外注册或者注销：

　                                                                         　sofia profile external register gw1 —— 注册

　                                                                      　   sofia profile external unregister gw2 —— 注销

开启该Profile的SIP跟踪功能抓SIP包：

　　                                                  　sofia profile internal siptrace on /off

　　　　　　　　　　　　　　　　　 sofia profile external siptrace on /off

有时候，希望将已经注册的用户清理掉。可以使用如下方法实现，如：

　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　sofia profile internal flush_inbound_reg 1000@192.168.1.7

也可以通过找到该用户的call_id来清理，如下面的例子，再重新查看状态时，发现已经被清除了（Total items变成了0）：

　　　　　　　　　　　　　　　　　　sofia profile internal flush_inbound_reg  ZWIyNDVmMTU1ODIyMDA1ZD1（可以通过指令sofia status profile internal reg 1000查看其对应的Call_ID）

    

  11、SIP Capture



   

  　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　     sofia profile internal capture on

　 　                      　　　　　　　　　　　　　　　　　　　　　　     sofia profile internal capture off

12、global相关



 打开和关闭全局的SIP消息跟踪：

　　                                            　　sofia global siptrace on

　　　　　　　　　　　　　　　　  sofia global siptrace off

以下两条命令分别可以打开和关闭全局的SIP捕获（Homer方式抓包）：

　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　sofia global capture on 　　

　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　sofia global capture off

13、debug相关（参考10.1.2）



  　　　　　　　　　　　　　　　　　　sofia loglevel all  9



  　　　　　　　　　　　　                   sofia loglevel nua 9



  　　　　　　　　                              sofia tracelevel debug

　　　　　　　　                                sofia traceclevel notice

最后，可以使用如下命令关闭这些调试：

　　　　　　　　　　　　　　　　　　sofia loglevel all  0

14、其他命令



  　　1）sofia_username_of —— 返回用户的username

　　

  　　2) sofia_contract ——返回注册用户的联系地址

 　　

  　　3）sofia_count_reg —— 在允许多点注册的情况下（开启multiple-registrations时），计算有多少客户注册了

　　

  　　4）sofia _dig —— 类似于DNS的dig，返回其他服务器的服务地址和端口号，如下命令显示了指定IP上都有哪些SIP服务：

　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　  

　　

  　　5）sofia_presence_data —— 显示Presence数据，下面的命令显示1000处于Busy状态：

　　                                                                                                                                                 sofia_presence_data status 1000@192.168.1.123

　　

  　　下面的命令列出指定用户的Presence信息：

　　　　　　　　　　　　　　　　　　　　　sofia_presence_data list 1000@192.168.1.123

　　

  　　下面的命令列出指定用户的user_agent信息：

　　　　　　　　　　　　　　　　　　　　　sofia_presence_data  user_agent  1000@192.168.1.123

　　

　　



 15、show channels —— 找到当前通话的Channel的UUID

（只呈现了部分关键信息） 

 

 然后使用： uuid_debug_media 调制媒体的相关信息：



 指令： uuid_debug_media a8c54a3f-2ae7-4a4b-a801-478d98b11613  both  on 

