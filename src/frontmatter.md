# CMDB：降本增效的利器

借用物理上的熵增概念，封闭系统总是朝着无序的方向发展的。IT 环境也是如此，越来越多的设备，越来越多的业务，越来越多的人员，总是会像越来越混乱的方向发展。当规模扩张到一定程度时，凭人力维护 Wiki 或者 Excel 就会越来越力不从心。混乱的 IT 环境一般会导致资源空跑，变更易出错，琐事占用大量时间等问题。因此，IT 运维的一大价值就是要用技术手段去对抗熵增，抑制熵增，而最基础的技术手段就是 CMDB。一个设计良好的 CMDB，一个能将资源管理的井井有条的 CMDB，是降本增效的利器。

而在众多的 CMDB 软件中，iTop 以其易于理解的概念，直观的模型设计逻辑和方法，可扩展的插件及 API 能力，强大的查询及导入导出功能，开源并且相对活跃的社区，无疑是一个很好的选择。

# 自序

入行运维的第一份工作是某知名互联网公司的基础运维岗，主要的工作是处理涉及 IDC 的各种工单，比如服务器安装重装，机器故障处理等等。日常用的系统主要就是工单系统和 CMDB。经常要在两个系统之间复制粘贴数据，比如有一类改 IP 的工单，流程复杂，做完之后还要手动去 CMDB 更新 IP 和上联交换机信息。还有一类现场外包操作的，需要在外包工单系统里手写有一定格式要求的外包工单，包括服务器 SN，IP，管理员姓名电话等，同样是繁琐的复制粘贴。第二份工作，在一个互联网公司的业务部门做运维，没有了 IDC 相关工作的烦恼。但是有记录机器归属的业务和开发人员的需求，还需要在 Zabbix 里配置报警发送的开发人员。没有 CMDB 时，同事们习惯记录在 WIKI 里，Zabbix 的报警联系人也是手工维护。当业务数量越来越多，机器，数据库资源也越来越多时，WIKI 和 Zabbix 的信息维护就越来越困难，迫切需要一个 CMDB 工具去解决这个问题。不像第一份工作已经有一个现成的不太好用的 CMDB，我需要自己决定如何实现 CMDB。就这样，我接触到了 iTop。

iTop 是一个 PHP 开发的开源运维管理工具，CMDB 是其核心功能，另外还自带了一套工单系统，支持请求管理，事件管理，变更管理等兼容 ITIL 的流程。iTop 使用面向对象的方式来对现实世界建模，非常直观，易于理解。比如服务器和网络设备都有 SN，主机名，机柜等属性，将共同属性提取出来，定义一个父类。iTop 不仅自带了常用的模型，包含服务器，网络设备，办公设备，业务，软件等，还能够根据自身业务场景需求，灵活的增删或修改模型。通过 iTop 完善的插件体系，只需用 XML 来描述数据模型，iTop 负责将其编译为 PHP 代码，即使没有太多编程能力，也能快速设计和定制自己的 CMDB，非常适合运维人员。如果有更多 PHP 编码的能力，还可以进行更深入的定制，比如增加自定义的属性类型，给某一类 CI 增加操作，写入前检查 CI 的合规性等等。

iTop 的工单系统也可以通过定制简化很多运维工作，比如通过请求管理来做新业务申请，工单完成后，自动将新业务录入 iTop，并且建立和申请人的关联关系。再比如，可以将报警事件写入 iTop 的事件管理，自动分配给报警业务对应的联系人，来进行故障处理的跟踪。还有，通过变更管理，添加相关配置项，通过影响分析功能，图形化分析变更涉及的业务和人员。

iTop 足够灵活，只要想得到，你能用它完成很大一部分运维需求。比如将业务和联系人的关联关系做成一个开放接口，用于发报警时取联系人。比如基于 iTop 对 URL 进行建模，做一个 URL 监控系统的前端。比如用 iTop 对 Kubernetes 的 Deployment，Service，Ingress 进行建模，低成本的实现一个 Kubernetes 管理平台。

iTop 在数据管理方面也提供了很多好用的工具，比如强大的导入导出功能，全字段的筛选功能，OQL 查询功能，基于 OQL 查询的数据审计功能等等。

本文档将记录 iTop 使用过程中的一些问题，定制方法，场景建模，以及文档翻译等等内容。也希望国内 iTop 用户能够参与进来，共同完善。