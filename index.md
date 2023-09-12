造成ORA-12560: TNS: 协议适配器错误的问题的原因有三个：

　　1.监听服务没有起起来。windows平台个一如下操作：开始---程序---管理工具---服务，打开服务面板，启动oraclehome92TNSlistener服务。

　　2.服务oracleserviceXXXX没有开启,XXXX就是你的database SID.database instance没有起起来。windows平台如下操作：开始---程序---管理工具---服务，打开服务面板，启动oracleserviceXXXX,XXXX就是你的database SID.

注释：当服务oracleserviceXXXX开启后，database instance有没有起来，都不会提示ORA-12560的。

　　3.如果在注册表、cmd窗口和Windows“系统属性”界面上，都没有设置过oracle_sid的话，则会提示ORA-12560的。

注释：

regedit，然后进入HKEY_LOCAL_MACHINE\SOFTWARE\ORACLE\HOME0将该环境变量ORACLE_SID设置为XXXX,XXXX就是你的database SID.

或者右几我的电脑，属性--高级--环境变量---系统变量--新建，变量名=oracle_sid,变量值=XXXX,XXXX就是你的database SID.

或者进入sqlplus前，在command line下输set oracle_sid=XXXX,XXXX就是你的database SID.

　　经过以上步骤，就可以解决问题。



oracle服务丢失的处理方法之OracleOraDb11g_home1TNSListener与OracleServiceORCL
问题：服务器长时间没访问，忽然发现OracleOraDb11g_home1TNSListener与OracleServiceORCL服务都消失不见了
一、OracleOraDb11g_home1TNSListener解决

用Net Manager查看，如果之前创建的listener是存在的，因此只需要启动该监听服务就OK了，cmd窗口下用lsnrctl start命令就可以启动了

二、OracleServiceORCL服务解决
cmd中执行如下命令

oradim -NEW -SID orcl -STARTMODE manual -PFILE “D:\app\Administrator\product\11.2.0\dbhome_1\dbs\init.ora”

执行完毕后，会提示orcl实例创建成功，但稍后会提示启动该服务失败，可以不用理他。

然后执行如下命令，启动服务

oradim -STARTUP -SID orcl -STARTTYPE inst

到此，数据库实例服务已经创建并启动。