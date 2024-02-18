# 开发文档

> 为了构建一个全国碳市场一体化管理平台，我们需要准备一个详细的开发文档，以便于开发团队理解项目的整体架构、功能需求、技术选型以及各个模块的实现细节。以下是为开发者准备的开发说明：



## 开发前的准备事项

1. **环境搭建**：确保开发团队具备必要的软件安装和环境配置，包括但不限于 `Node.js`, `Vue CLI`, `JDK-17`, `Kotlin`, `MySQL`, `Redis`, `Elasticsearch`, `Docker`, 以及 `Hyperledger Fabric` 的环境设置。
2. **需求理解**：进行需求分析，确保每位开发人员都能完全理解项目需求和业务逻辑。
3. **设计评审**：进行系统设计评审，确保架构设计能够满足项目需求，同时保持良好的扩展性和维护性。
4. **代码规范**：制定统一的代码编写规范和提交规范，确保代码质量和团队协作的高效性。
5. **安全考虑**：加强对数据安全和隐私保护的重视，确保所有模块都采取合适的安全措施。
6. **项目管理**：使用敏捷开发方法进行项目管理，定期进行迭代计划和回顾会议，保证项目按时进展。



## 项目开发

我们协作开发采用 git 进行，使用 gitea 平台（锋楪仓库）进行项目管理与敏捷开发管理。

- 后端项目：https://git-fy.cn/FrontLeaves/GreenChainCarbonLedger

- 前端项目：https://git-fy.cn/FrontLeaves/green-chain-carbon-ledger-web



## 人员配置

- 曾昶雯【项目负责人|全栈工程】
- 杨娜【前端工程|前端设计】
- 戴闯【后端工程|后端设计】
- 张林浦【后端工程】
- 郑文琰【文档处理|后勤】



## 环境搭建

后端开发者前期需要准备 `JDK-17`, `Kotlin-1.9.22`, `Maven`, `Mysql8`, `Redis` 相应开发环境，统一使用 Jetbrains Intellij IDEA Ultimate 2023.3.X，`Docker` 环境选择配置，建议使用 `Docker` 部署 Mysql、Redis 等服务。

前端开发者前期需要准备 `Node.js`, `Vue CLI` 相应开发环境，统一使用 Jetbrains WebStorm 2023.3.X，无需额外配置 Docker 环境。

### 框架配置

#### 后端

- 使用主体框架 `Springboot3.2.2`
  - SDK配置：
    - [org.springframework.boot] spring-boot-starter-data-redis
    - [org.springframework.boot] spring-boot-starter-thymeleaf
    - [org.springframework.boot] spring-boot-starter-validation
    - [org.springframework.boot] spring-boot-starter-web
    - [com.fasterxml.jackson.module] jackson-module-kotlin
    - [org.jetbrains.kotlin] kotlin-reflect
    - [org.jetbrains.kotlin] kotlin-stdlib
    - [com.mysql] mysql-connector-j
    - [org.projectlombok] lombok
  - 架构打包
    - [dev] 开发测试使用
    - [test] 对接测试使用
    - [prod] 部署使用
- 数据库采用 `Mysql8.2` 具体数据库设计逻辑见后
- 缓存数据库采用 `Redis7.2` 具体数据库样式逻辑见后

### 前端

- 使用框架 `Vue3`
- 使用设计框架，主要为 [AntDesign](https://antdv.com/docs/vue/introduce-cn) ，辅助设计为 [Flowbite](https://flowbite.com/)
- 原型图设计工具 [Pixso](https://pixso.cn/)
- 
