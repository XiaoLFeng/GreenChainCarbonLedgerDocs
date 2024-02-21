# 本项目开发方式

> 敏捷开发

本项目采纳敏捷开发方法，致力于提高开发效率，加强团队之间的协作与沟通，以及快速响应市场和客户需求的变化。敏捷开发强调短周期交付可工作的软件版本，以便于及时获得用户反馈，确保项目方向与用户需求保持一致。



## 仓库规定

为确保开发过程有序、高效，本项目设定详细的仓库规定和流程指南。

### 流程规定

> **开发流程**设计旨在确保每个功能点都能够得到充分理解和有效实施，同时保证项目整体进度符合预期。

1. **工单管理**：项目管理者将根据功能需求创建工单，并分配给相应的开发者。每个工单都详细描述了功能点的需求，开发者应仔细阅读并理解工单内容。如有疑问，应及时在工单中提问或请求帮助。
2. **开发与代码审查**：开发者在完成对工单的理解后，开始在`feature`分支进行代码编写。编码完成后，通过创建Pull Request来请求将代码合并到`master`分支。项目管理者或指定的代码审查员将对代码进行审查，确保代码质量和功能实现符合要求。
3. **自动化部署**：`master`分支的更新将触发自动化部署流程，通过Jenkins等CI/CD工具自动部署到测试环境，以便进行集成测试和性能测试。这一流程确保了代码的稳定性和可部署性。
4. **漏洞修补与补丁更新**：在项目开发过程中发现的任何漏洞都将通过创建新的`fix/patch`分支来进行修补。修补工作完成后，同样需要经过Pull Request和代码审查流程，确保补丁的正确性和稳定性。

### 分支规定

> 该部分内容前端与后端规定一致

项目定义了三条主要分支：`master`, `feature`, `fix/patch`。

- **主分支(`master`)** ：代表项目的当前稳定版本，用于生产部署。
- **功能开发分支(`feature`)** ：用于新功能的开发。每个新功能应在单独的`feature`分支上进行开发，待功能完成并通过审查后，再合并回`master`分支。
- **修补分支(`fix/patch`)** ：用于修复发现的漏洞或进行必要的补丁更新。分支命名需遵循`fix-工单ID`或`patch-工单ID`的规则，以便追踪和管理。

其中 `master` 分支禁止开发者直接推送至仓库。对于所有的新业务代码请在 `feature` 分支编写，业务逻辑完成后，使用仓库功能 **Pull Request(合并请求)** 将代码往 `master` 分支合并；若在 `master` 分支下出现漏洞情况，按需创建 `fix/patch` 分支（该部分分支有命名要求），修补完成后提交 **Pull Request(合并请求)**  至 `master` 分支。

另外，对于 `fix/patch` 分支命名要求：由于开发按照流程进行，对应开发内容带有工单ID，请在对应分支加上横杠“-”后加上工单ID作为分支操作，例如下图所示工单ID **#3**

![](https://i-cdn.akass.cn/2024/02/65d4deae81462.png!wp60)

故命名为 `fix-3` 或 `patch-3`。

除此之外，请注意，`feature` 分支和 `fix/patch` 分支不可随意合并，避免后期造成代码混淆难进行业务状态跟踪。

### 问题处理

对于开发过程中遇到的问题，鼓励开发者首先尝试在工单内解决。如果问题超出了单一工单的范围，或者是跨功能点的，开发者可以创建新的工单来描述这些问题。新工单应明确问题的性质、影响范围，并指定负责人或相关协作者。

问题请各位开发者务必描述清楚！！！



-----

> 以下部分只有测试用例和单元测试需要开发者完成编写并测试。其余测试将有我来完成或配置自动化处理。但请各位开发者了解测试流程操作，学习如何进行自动化操作以及其余方面测试工作。

## 自动化测试与测试部署规定

本项目重视自动化测试和测试环境的部署，以确保软件质量和加快开发周期。自动化测试能够帮助我们及时发现错误和性能问题，而合理的测试部署流程则确保测试环境的稳定性和可靠性。以下是本项目自动化测试与测试部署的具体规定：

### 自动化测试规定

- **单元测试**：覆盖所有核心代码模块，确保单独的函数或方法按预期工作。`「在本次开发中尽量完成，需要各位开发者进行学习」`
- **集成测试**：检查不同模块或服务之间的交互是否正确，确保系统各部分能够协同工作。
- **性能测试**：评估系统在高负载或极限条件下的表现，包括响应时间、吞吐量等关键指标。
- **安全测试**：检测软件的安全漏洞，确保系统的数据安全和防御能力。

### 测试实施

1. **测试用例编写**：开发者在编码阶段同时编写测试用例，测试用例需覆盖功能的正常流程和异常流程。
2. **持续集成（CI）**：将自动化测试集成到持续集成流程中，每次代码提交后自动运行测试，确保及时发现并修复问题。
3. **代码审查**：除了自动化测试外，还应结合人工代码审查，以发现测试覆盖不到的潜在问题。
4. **测试报告**：自动化测试完成后，生成测试报告，包括测试覆盖率、发现的错误等信息，供团队评估软件质量。



## 测试部署规定

### 测试环境

项目应设立独立的测试环境，模拟生产环境的配置，确保测试结果的准确性。测试环境应包括但不限于数据库、服务器、网络配置等。

### 部署流程

1. **自动化部署**：测试环境的部署应自动化，通过脚本或使用CI/CD工具如Jenkins、GitLab CI进行。
2. **环境隔离**：确保测试环境与开发、生产环境完全隔离，避免相互影响。
3. **数据管理**：测试环境应使用模拟数据或脱敏数据，确保数据安全，同时满足测试需求。
4. **访问控制**：对测试环境的访问进行严格控制，只允许授权的测试人员和开发者访问。

### 环境监控与维护

1. **监控**：对测试环境进行实时监控，包括系统性能、日志等，以便及时发现和解决问题。
2. **定期更新**：测试环境的软件和硬件配置应定期更新，以保持与生产环境的一致性。
3. **问题响应**：设立快速响应机制，当测试环境出现问题时，能够迅速定位并解决。