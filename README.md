tomcat启动顺序：
bootstrap的静态块初始化和加载环境 然后bootstrap的一切操作其实都是对catalinadd dcaozuo
bootstrap:start --> catalina:start-->server:start(其实调用接口Lifecycle的抽象实现LifecycleBase的start方法而LifecycleBase的start的方法里其实调用了抽象
方法startInternal,server的StandarServer实现了抽象LifecycleBase的startInternal方法，所以即使调用StandardServer的startInternal方法）service:start(StandarService:startinternal)-->Connector:start(Connector: startInternal) --> ProtocolHandler:start --> AbstractEndpoint:start(AbstractEndpoint:startInternal )AbstractEndpoint的startInternal方法是抽象方法 AbstractEndpoint的子类就是一个endpoint，用于接收请求的

组件关系：
server包含多个service包含一个Container和多个Connector
server.xml看tomcat架构：
<Server>                                                //顶层类元素，可以包括多个Service 
    <Service>                                           //顶层类元素，可包含一个Engine，多个Connecter
        <Connector>                                     //连接器类元素，代表通信接口
                <Engine>                                //容器类元素，为特定的Service组件处理客户请求，要包含多个Host
                        <Host>                          //容器类元素，为特定的虚拟主机组件处理客户请求，可包含多个Context
                                <Context>               //容器类元素，为特定的Web应用处理所有的客户请求
                                </Context>
                        </Host>
                </Engine>
        </Connector>
    </Service>
</Server>

tomcat体系图：

![image](https://github.com/Mitnick5194/tomcat-src/blob/master/images/tomcat_struct.jpg)
![image](https://github.com/Mitnick5194/tomcat-src/blob/master/images/tomcat_struct.jpg)

container组件图：

![image](https://github.com/Mitnick5194/tomcat-src/blob/master/images/container_components.jpg)
