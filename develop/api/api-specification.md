# 接口开发规范

> 本文档旨在规定使用SpringBoot 3作为框架的后端接口设计标准，以确保开发的高效性、一致性及可维护性。



## 1. 接口设计基本原则

- **明确性**：接口和参数命名应直观明确，能够准确描述其功能和用途。
- **简洁性**：接口应尽量做到简洁，避免不必要的复杂性。
- **一致性**：接口设计应保持一致性，如命名规则、参数格式、返回信息等。
- **安全性**：设计接口时必须考虑到安全因素，采取相应措施保护数据安全。



## 2. 接口命名规则

- **使用RESTful风格**：接口设计遵循RESTful架构风格，使用HTTP方法表示操作，如GET（获取资源）、POST（创建资源）、PUT（更新资源）和DELETE（删除资源）。
- **路径命名**：路径应使用小写字母，单词之间以连字符（-）分隔，如`/user-info`。
- **资源命名**：资源命名应使用名词，避免动词，表明操作的对象，如`/users`、`/orders`。



## 3. 请求与响应格式

- **请求格式**：采用JSON格式作为主要的请求体格式，保证数据的轻量和易于处理。

- **响应结构**：所有API响应应遵循统一的格式，包括状态码、消息和数据三部分，如下示例所示：

  ```json
  {
      "output": "Success",
      "code": 200,
      "message": "操作成功",
      "data": {
          // 具体数据(data为非必需)
      }
  }
  ```

- **状态码使用**：应正确使用HTTP状态码，如`200 OK`表示请求成功，`404 Not Found`表示资源不存在，`500 Internal Server Error`表示服务器错误等。



## 4. 错误处理

- **错误响应**：当请求失败时，返回明确的错误码和错误信息，帮助前端定位问题，例如：

  ```json
  {
      "output": "UserNotFounded",
      "code": 40301,
      "message": "用户未找到",
      "data": {
          // 具体数据(data为非必需)
      }
  }
  ```



## 5. 安全性设计

- **身份验证**：接口调用需通过JWT、OAuth2等机制进行身份验证，确保接口调用的安全性。
- **数据加密**：敏感信息传输时应使用HTTPS加密，避免数据在传输过程中被截获。
- **权限控制**：对于需要权限控制的接口，应实现细粒度的权限验证，确保只有授权用户才能访问。
- **输入验证**：对所有输入数据进行验证，防止SQL注入、XSS等安全漏洞。



## 6. 版本管理

- **接口版本控制**：在URL中包含版本号，如`/api/v1/users`，以支持接口的平滑升级。



## 7. 控制器命名规则

> 其余例如 Service / DAO 等同理

- **类命名**：控制器类名应以`Controller`结尾，明确表示其作用，如`UserController`。
- **包结构**：控制器应放在`controller`包下，根据业务模块进一步分包。
- **资源命名**：控制器的@RequestMapping应反映出资源路径，使用复数形式，如`/users`。



## 8. HTTP请求方法使用规范

- **GET**：用于请求资源，不应产生副作用。不使用请求体。
- **POST**：用于创建新资源。可接受请求体携带数据。
- **PUT**：用于更新资源的全部信息。接受请求体携带完整资源信息。
- **DELETE**：用于删除资源。通常不使用请求体。
- **PATCH**：用于对资源进行部分更新。接受请求体携带部分资源信息。

## 9. 请求与响应要求

- **禁止GET请求使用请求体**：遵循HTTP规范，GET请求不应包含请求体。所有查询参数应通过URL的查询字符串传递。
- **统一响应结构**：无论请求成功还是失败，都应返回统一格式的响应体，包括状态码、消息和数据。



## 10. 示例代码

````java
@RestController
@RequestMapping("/api/v1/users")
public class UserController {

    @GetMapping
    public ResponseEntity<List<User>> getAllUsers() {
        List<User> users = userService.findAll();
        return ResponseEntity.ok(users);
    }

    @PostMapping
    public ResponseEntity<User> createUser(@RequestBody User user) {
        User newUser = userService.save(user);
        return ResponseEntity.status(HttpStatus.CREATED).body(newUser);
    }

    @PutMapping("/{id}")
    public ResponseEntity<User> updateUser(@PathVariable Long id, @RequestBody User user) {
        User updatedUser = userService.update(id, user);
        return ResponseEntity.ok(updatedUser);
    }

    @DeleteMapping("/{id}")
    public ResponseEntity<Void> deleteUser(@PathVariable Long id) {
        userService.delete(id);
        return ResponseEntity.noContent().build();
    }
}
````