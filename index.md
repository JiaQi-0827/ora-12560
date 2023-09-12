造成ORA-12560: TNS: 协议适配器错误的问题的原因有三个：

　　1.监听服务没有起起来。windows平台个一如下操作：开始---程序---管理工具---服务，打开服务面板，启动oraclehome92TNSlistener服务。

　　2.服务oracleserviceXXXX没有开启,XXXX就是你的database SID.database instance没有起起来。windows平台如下操作：开始---程序---管理工具---服务，打开服务面板，启动oracleserviceXXXX,XXXX就是你的database SID.

注释：当服务oracleserviceXXXX开启后，database instance有没有起来，都不会提示ORA-12560的。

　　3.如果在注册表、cmd窗口和Windows“系统属性”界面上，都没有设置过oracle_sid的话，则会提示ORA-12560的。




二、OracleServiceORCL服务解决
cmd中执行如下命令

oradim -NEW -SID orcl -STARTMODE manual -PFILE “D:\app\Administrator\product\11.2.0\dbhome_1\dbs\init.ora”

执行完毕后，会提示orcl实例创建成功，但稍后会提示启动该服务失败，可以不用理他。

然后执行如下命令，启动服务

oradim -STARTUP -SID orcl -STARTTYPE inst

到此，数据库实例服务已经创建并启动。