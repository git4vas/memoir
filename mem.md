# Security challenges in a cloud environment

##### *keywords*
_IoT, edge computing, virtualization and cloud infrastructures are gaining potential nowadays and industrial processes. 
Security challenges in a cloud environment_


## Contents
Intro
Cloud security layer
infrastructure usage by cloud
virtualization/docker/kubernetes
connectivity options (LoRa, WiFi, 5g)
edge computing
examples
Netw. infrastructure application: 2proc. @containers with netw. access via separate if
IoT application: separation from home network
ipcam + mobile provider + datacenter
conclusion
ref

## Intro
IoT, edge computing, virtualization and cloud infrastructures are gaining potential nowadays and industrial processes.

## cloud
### deployment
If we look at the cloud from a deployment perspective, there are three models. Public cloud, Private cloud, Hybrid cloud.
#### Hybrid cloud
This model of cloud combines the features of both private and public cloud, or you can say it integrates the public cloud and the on-premise hosted cloud. For example, suppose we have an internally deployed OpenStack cloud platform and now we want it to integrate with any of the public clouds. For this, there are multiple tools available that enable you to integrate both clouds and also facilitate you to lift and shift the workload to and fro. Recently, Cisco came up with a product called Cisco CloudCenter (formerly known as CliQr) providing the same facility.

On the basis of service, we categorize clouds into three parts, which we call the SPI model.
In the SPI model, S represents Software as a Service, P represents Platform as a Service, and I represents
#### Infrastructure as a Service.
IaaS stands for Infrastructure as a Service. In this model of cloud, you can subscribe to the complete infrastructure (networking, computing, and storage) that is required to run your application. Here, you will get the building blocks that you need to assemble to run your application as per your requirement. Suppose you want to run one web application that is developed in PHP and MySQL. To run this on the IaaS platform you need to subscribe to computing, networking, and storage. Now, you will configure each of them to run your application.

### layers
Before the hypervisor, we have the Orchestration Layer, which communicates with
the Virtualization Layer and makes available resource chunks (computing, storage, and network) to be shared among the multiple tenants on demand. The user logs in to the cloud dashboard to subscribe the resource and starts running their service or application on it. One thing we can see here is that the Security layer starts from base and goes up until the top. This means that we need to focus on the security aspect at each layer (from the physical layer to the user layer).

### security
Organizations started shifting their workload from on-premise physical infrastructures to the public cloud, or started to deploy their own private clouds to get all the benefits of the cloud. But security is a major concern, mostly in the case of the public cloud where we do not have control of the physical infrastructure. Also, there are compliance requirements that organizations need to match, for example, ISO/IEC, NIST, FedRAMP, PCI DSS, HIPAA, and so on.

In any environment for security, we always start with the following models: CIA, AAA. The CIA model focuses on Confidentiality, Integrity, and Availability (CIA triad).

### Auditing
Auditing does the accounting of user activity on data. Here, we log all the activity of users
One thing we need to understand is that implementing security in the cloud is a bit different from what we have been practising with on-premise or traditional infrastructures.
The cloud runs on top of physical boxes, such as storage, servers, and networking equipment. All these resources are controlled by a layer of abstraction that we call a hypervisor or virtualization layer. Further, all the aggregated resources are being controlled and managed by an orchestration. Internally, all these layers communicate with each other through an application program interface (API).

#### Confidentiality
Here, we use Identity and Access Management (IAM) to define the resource accessibility permissions. In IAM, we can define users, groups, roles, and policies. IAM also helps to manage the API access using access keys and secret keys. Similarly, we have a keystone in OpenStack to define users, groups, roles, and policies. You can define policies to access the other OpenStack services and APIs.
#### Integrity
For integrity, we have multiple types of encryption for the storage where data is stored and for data in transit we can use SSL. If we want to implement an additional layer of security, we can use the AWS CloudHSM module as well. In OpenStack, we have the following process to manage integrity. It starts from the bootstrap level and goes up until the file level. (We've studied this process in detail in the Private cloud section.)
#### Availability
For availability, AWS offers you many services that ensure the service availability at different layers. We have Route 53 as DNS, Elastic Load Balancing (ELB), and autoscaling. All three services ensure that you have the service available in case of DDoS attacks as well. Availability of the application or solution also depends on how it is designed and deployed. Let's take an example of a web application; here in order to ensure maximum availability of the application, we should always design the solution in such a way that there is no single point of failure. For this, we must consider high availability (HA), autoscaling, and also try to decouple the resources (using message queuing) so that it can be fault tolerant as well. 
#### Authentication
In AWS, we have IAM for user identity. Here, we can define users and groups. IAM enables you to define the password-based authentication and key-based authentication for users. Apart from this, for the application, we can use the AWS Directory Service and Cognito (token-based authentication) for user authentication. For console users, we can also enable multi-factor authentication (MFA) as well. In OpenStack, we have a keystone, which provides user and service authentication. Here, we also create users and groups and define password-based and key-based authentication for users. Apart from this, we can use SAML-based authentication, OAuth, and OpenID-based authentication.
#### Authorization
For authorization, AWS uses IAM roles and policies. There are many predefined user roles for different services. Apart from this, we can define custom roles. For example, suppose we have an EC2 instance, that needs to access the Simple Storage Service (S3) resource and CloudWatch Logs. Here we can also define a custom role of an EC2 instance which grants access to the S3 bucket and CloudWatch Logs and binds that role with the EC2 instances. There is no need to store the access keys in text format on EC2 instances, but you will find that people are not practicing this. In the same way, if you need to manage multiple or linked accounts then you should define the role for cross-account access and use it instead of logging in using the root account. Similarly, in OpenStack, we have a keystone where we can define different roles and policies for users and groups. For each service, there is an associated access policy file defined in JSON format.
#### Auditing
AWS provides CloudTrail to log all the action or activity for AWS services. Apart from this, we have Virtual Private Cloud (VPC) logs and ELB logs, which can be stored in the S3 bucket or can be transferred to CloudWatch Logs. For analysis, we can use the Elasticsearch service or query it using Athena. For solution auditing, you can use AWS Config and Trusted Advisor. Now we are moving toward machine learning and Internet of Things (IoT). For this, AWS started a new service called Macie, which uses machine learning to identify the accessibility of data and services. In OpenStack, we have a telemetry service called Ceilometer to store and manage logs. Apart from this, you can use custom monitoring solutions called New Relic.
### Shared responsibility model
### Key concern areas of cloud security
#### Infrastructure level
#### User access level
#### Storage and data level
##### Volume storage:
A block storage, which can be mapped with VM as a partition.
To ensure security, we can use OS-based encryption or HSM to ensure the security of data.
For data protection, we can define RAID as well. For example, in AWS we have Elastic Block Store (EBS), which provides an encryption facility and also provides the feature to create RAID.
##### Object storage:
static content, such as images and documents.
Here, we can define encryption and ACLs to ensure the security of data. There are many cloud providers who already keep multiple copies of object storage data to ensure safety. For example, in AWS we have S3, which keeps six copies of data for redundancy.
##### Database storage:
This is the type of storage that we use to store our database. In AWS, we have RDS. To ensure data security, we must ensure that encryption is enabled and also that only authorized users have access.
#### Application access level
We must secure this transferring data using a secure channel, such as SSL.
<s>Apart from this, if our application is a web application, we must ensure availability. We have heard about cases of DDoS attacks, SQL injections, and so on. There are always bad guys who work in the dark to steal your important data. To disable this, we must ensure that we have defined preventive parameters such as the use of the web application firewall (WAF), and that our infrastructure should be deployed in such a way that it can handle the DDoS attack. Security groups should allow the traffic on specific ports and from specific sources only. For example, we have a web application that runs with SSL on port 443, so make sure that only port 443 is open for public access.</s>
We can also use WAF to stop malicious traffic and prevent DDoS attacks. WAF also helps to apply rules on your websites for accessibility. You can also manage the traffic on the basis of geographical locations.
There is also a chance that your VM gets compromised and starts broadcasting the packet. To eliminate this situation, we must do security hardening of the virtual machine and enable monitoring so that, if any such adverse situation comes about, you will get an alert to take appropriate action.
what about the internal users?—Check the load balancer logs, application server logs, and user access, or you can use any monitoring tool that can display real-time logs in a meaningful way.
Elasticsearch, Logstash, and Kibana (ELK) stack gives very interactive dashboards and graphs.

Network ACLs should also be configured to allow only legitimate traffic.

#### Network level
For private subnet VMs, we can use the NAT service to enable internet access.
If you need to meet a specific compliance, you can use IPS and IDS to make the environment more secure.
To access resources from a management perspective, we should use a VPN connection. There are different types of VPN connections offered by AWS.
For a private and secure connection, we can use the Direct Connect connection between the customer site to AWS.

#### Logging and monitoring level








Каждая новая технология приходит на смену старой. Иногда, как и в случае с облаком, проводится ребрендинг старых технологий, чтобы сделать их более привлекательными для потребителей и, тем самым, создать иллюзию нового продукта. Облачные вычисления ранее существовали в той или иной форме. На одном из этапов они назывались «on demand computing» (компьютерные ресурсы по требованию), а затем преобразовались в «application service provider» (ASP).

Теперь существует edge computing которому отраслевые обозреватели и эксперты пророчат способность заменить облако.
Конечно, есть некоторые технологии, которые действительно осуществляют переворот в том, что меняют привычки людей и их образ мышления.

Пророчество Левина
Так почему же люди думают, что edge computing победит облако? Это утверждение было заявлено во многих статьях. Например, Клинт Бултон в марте этого года пишет об этом в статье «edge computing заменит облако». Он ссылается на венчурного капиталиста Эндрю Левина, генерального партнера Andreessen Horowitz, который считает, что больше вычислительных ресурсов будут двигаться в направлении оконечных устройств — таких, как беспилотный автомобиль и дроны, — которые составляют, по меньшей мере, часть Интернета вещей. Левин прогнозирует, что это будет означать то, что облаку пришел конец, т.к. процесс обработки данных будет двигаться назад по направлению к edge computing.

Другими словами, сейчас идет тенденция централизации вычислений в ЦОДах, в то время, как в прошлом они часто были децентрализованы или находились ближе к месту использования.
Левин видит беспилотный автомобиль, как центр обработки данных: они имеют более чем 200 процессоров, способных обеспечить полную отказоустойчивость, чтобы не привести к несчастному случаю на дороге. Характер автономных транспортных средств означает, что их вычислительные мощности должны быть независимыми и для того, чтобы обеспечить безопасность нужно свести к минимуму любую связь, которую они имеют с облаком. Тем не менее, они не смогут полностью обойтись без него.



Взаимодополняющие модели

увеличивается количество данных на одну транзакцию, «тяжелые» видео и много данных разных датчиков. решить проблемы задержки представляется более сложной задачей, чем это было раньше.

Сейчас имеет смысл размещать данные ближе к устройствам типа беспилотного автомобиля для того, чтобы устранить задержку, но тем не менее большая часть данных всё-еще находится удаленно в облаке. Облако по-прежнему будет использоваться в качестве поставщика сервисов, таких как СМИ и развлечения. Оно также может быть использовано для резервного копирования данных и для обмена данными, исходящих от транспортного средства.

Немного отойдем от автономных транспортных средств и вернемся к более привычному бизнесу. Создание ряда небольших ЦОДов или площадок аварийного восстановления может уменьшить эффект масштаба, как следствие, увеличить затраты и сделать работу менее эффективной. Да, задержка может быть уменьшена, но в случае катастрофы последствия будут не менее плачевными; поэтому для обеспечения непрерывности бизнеса некоторые данные следует хранить и обрабатывать в другом месте – в облаке. В случае беспилотных машин, в частности, потому что они должны работать независимо от того, есть сетевое соединение или его нет, имеет смысл, чтобы определенные типы вычислений и анализа были совершены самим транспортным средством. Однако эти данные по-прежнему будут бэкапиться в облако, когда соединение доступно. Подход будет гибридным: edge и cloud computing будут взаимодополнять друг друга, а не использоваться по одиночке.

От периферии до облака
Сейджу Скария, старший директор консалтинговой фирмы TCS, предлагает несколько примеров, где edge computing может оказаться полезным. В своей статье на LinkedIn Pulse, «Edge computing vs. Облачные вычисления: за кем будущее?». Он не считает, что с облаком будет покончено.

«Edge computing не заменит облачные вычисления… на самом деле, аналитическая модель или правила могут быть созданы в облаке и затем применяться оконечными устройствами… и некоторые [из них] способны делать анализ». Затем он продолжает говорить о fog computing (туманные вычисления), которая включает в себя обработку данных от периферии до облака. Он считает, что люди не должны забывать о хранилищах данных, так как они используется для «медленных аналитических запросов и массивного хранения данных».

Edge победит облако
Несмотря на этот аргумент, аналитик компании Gartner Томас Битман считает, что «Edge computing «съест» облако». «Сегодня облачные вычисления пожирают центры обработки данных предприятий, все больше и больше нагрузок приходится на облако, а некоторые преобразовываются и перемещаются в облако… но есть еще одна тенденция, которая переместит рабочие нагрузки, данные и стоимость бизнеса далеко от облака… И тенденция перехода к edge computing еще более важная и сильная, чем когда-то была тенденция облачных вычислений.

Позже в своем блоге Битман пишет: «Не хватает одной только быстроты облачных решений. Массивная централизация, экономия от масштаба, самообслуживание и полная автоматизации преодолевает только полпути — но все это не преодолеет физику — вес данных, скорость света. Как люди должны взаимодействовать с цифровой реальностью в режиме реального времени, если происходит задержка от центра обработки данных, расположенного за тысячи километров. Задержка имеет большое значение. Я существую здесь и прямо сейчас. Воспроизвести правильную рекламу, прежде чем я не отвернулся, указать на магазин, который я ищу, когда я за рулём, помочь моему беспилотному автомобилю выбрать верный путь через оживленный перекресток. И все это мне нужно получить СЕЙЧАС».

Ускорение данных
Битман делает некоторые справедливые замечания, но он употребляет аргумент, который часто используется в отношении задержек и ЦОДов: они должны быть расположены близко друг к другу. Истина заключается в том, что глобальные сети всегда будут фундаментом edge computing и облачных вычислений. Во-вторых, Битману явно не попадались инструменты ускорения данных, такие, как PORTrockIT и WANrockIT. В то время как физика, безусловно, является ограничивающим и сложным фактором, который всегда будет иметь место в сетях всех видов – включая WANs, сегодня можно разместить свои центры обработки данных на расстоянии друг от друга. Задержка может быть уменьшена, и его воздействие может быть нивелировано, независимо от того, где происходит обработка данных, и независимо от того, где хранятся данные.

Поэтому, edge computing это не новое прорывное решение. Это лишь одно из решений, как и облако. Вместе эти две технологии могут поддержать друг друга. Различие между edge computing и облачными вычислениями, в том, что «edge являются методом ускорения и повышения производительности облачных вычислений для мобильных пользователей». Таким образом, аргумент, что edge computing заменит облачные вычисления является очень неубедительным. По маркетинговым соображениям, облачные вычисления могут быть переименованы, но суть останется та же.







you do not have to worry about the purchase of physical boxes (CapEx) to run your application. You pay the cost of the resource based on the usage (OpEx). CapEx stands for capital expenditures and denotes one-time cost investment to purchase any resource, for example, the purchase of a physical server. OpEx stands for operating expenditures and denotes expenses to make the resource operational, for example, the purchase of manpower, power, OS, and so on to make the server operation
In the SPI model, S represents Software as a Service, P represents Platform as a Service, and I represents Infrastructure as a Service
Security layer starts from base and goes up until the top. This means that we need to focus on the security aspect at each layer (from the physical layer to the user layer).

AAA:
auth
Now we are moving toward machine learning and Internet of Things (IoT). For this, AWS started a new service called Macie, which uses machine learning to identify the accessibility of data and services. In OpenStack, we have a telemetry service called Ceilometer to store and manage logs. Apart from this, you can use custom monitoring solutions called New Relic.
=======
In cloud security, compliance is defined on the shared responsibility model. Here, the cloud provider is responsible for managing security and compliance at the physical infrastructure level, hypervisor level, physical network level, storage level, and orchestration layer.  
The cloud consumer assumes responsibility for managing security and compliance from the virtual machine level to the application level.
In AWS it's a bit more clarified, and here the security responsibility model is defined in three different categories:
A shared responsibility model for infrastructure 
A shared responsibility model for container service 
A shared responsibility model for abstract service

=========





link
link
book
paper
paper
