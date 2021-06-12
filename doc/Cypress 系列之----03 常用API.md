# Cypress 系列之----03 常用API

### Cypress 的所有command都是异步的

## 元素选择和操作

| 方法                 | 功能                                                         | 范例                                                         | 参考 |
| -------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ---- |
| contains(content)    | 获取单元素 - 通过文本                                        | cy.get('.nav').contains('About') cy.contains('Hello') cy.contains(/^b\w+/) |      |
| get(selector\|alias) | 获取多元素 通过CSS选择器 \| 别名 CSS选择器支持jquery语法     | cy.get('.list > li’) cy.get('ul li:first') cy.get('[data-test-id="test-example"]') |      |
| within(fn)           | 连缀处理元素 - 函数                                          | cy.get('.list').within(() =>{...})                           |      |
| find(selector)       | 连缀处理元素 - 选择器                                        | cy.get('.list').find('>li')                                  |      |
| children             | 获取子元素                                                   | cy.get('nav').children()                                     |      |
| parent()             | 获取父元素                                                   | cy.get('header').parent()                                    |      |
| parents()            | 获取所有的父节点                                             | cy.get('aside').parents()                                    |      |
| closest              | 获取第一个匹配的元素                                         | cy.get('td').closest('.filled')                              |      |
| eq(index)            | 序号 \| 序列中的元素                                         |                                                              |      |
| filter(selector)     | 过滤元素                                                     | cy.get('td').filter('.users')                                |      |
| not()                | 过滤元素 和filter相反                                        |                                                              |      |
| first()              | 返回第一个元素                                               | cy.get('nav a').first()                                      |      |
| last()               | 返回最后一个元素                                             | cy.get('nav a').last()                                       |      |
| next()               | 下一个元素                                                   | cy.get('nav a:first').next()                                 |      |
| nextAll()            | 接下来所有                                                   |                                                              |      |
| nextUntil()          | 接下来直到                                                   |                                                              |      |
| prev()               | 前一个元素                                                   | cy.get('li').prev('.active')                                 |      |
| prevAll()            |                                                              |                                                              |      |
| prevUntil()          |                                                              |                                                              |      |
| url                  | 获取当前页面 url                                             |                                                              |      |
| title                | 获取当前页面标题                                             |                                                              |      |
| window元素           |                                                              |                                                              |      |
| document             | 获取window.document                                          |                                                              |      |
| location             | 获取window.location查询                                      | cy.location('host')                                          |      |
|                      | params&query                                                 | cy.location('port')                                          |      |
|                      | 可用参数： hash \| host \| hostname \| href \| origin \| pathname \| port \| protocol \| search \| toString |                                                              |      |
| Cypress.browser      | window.browser                                               |                                                              |      |

## 元素内容处理

| 方法                                 | 功能         | 范例                                                         | 参考 |
| ------------------------------------ | ------------ | ------------------------------------------------------------ | ---- |
| each(callbackFn)                     | 遍历         | cy.get('ul>li').each(function () {...})                      |      |
| clear                                | 清除元素内容 | cy.get('[type="text"]').clear() //清除内容 赋予新值 cy.get('input[name="name"]').clear().type('Jane Lane') |      |
| type( txt[,options]) }               | 模拟输入内容 | cy.get('input').type(' 233 ') cy.get('input').type('{shift}{alt}Q')---组合键盘操作 cy.get('input').type('{alt}这里是按了一下alt后输入的内容') |      |
| fixture(filePath, encoding, options) | 读取文件     | cy.fixture('users.json').as('usersData') cy.fixture('users') .then((json) => { cy.route('GET', '/users/**', json) }) |      |

## 元素操作事件

| 方法     | 功能                          | 范例                                                         | 参考 |
| -------- | ----------------------------- | ------------------------------------------------------------ | ---- |
| trigger  | 触发DOM元素                   | cy.get('a').trigger('mousedown')                             |      |
| visit    | 访问链接                      | cy.visit('landing') 根据情况拼接 设置过baseUrl就是baseUrl+landing 没设置过就是直接访问 cy.visit('lesson_report/807212') 活动路由 |      |
| click    | 单击                          |                                                              |      |
| dblclick | 双击                          | cy.focused().dblclick()                                      |      |
| focus    | 聚焦                          | cy.get('input').first().focus()                              |      |
| blur     | 失焦                          |                                                              |      |
| check    | 选中选项 限定: checkbox/radio |                                                              |      |
| uncheck  | 取消选中                      | cy.uncheck()                                                 |      |
| select   | 选择选项 限定option           | cy.get('select').select('user-1')                            |      |
| end      | 清空返回值 用于继续连缀       | cy .get('#a').click().end() .get('#b').click() 等价于 cy.get('#a').click() cy.get('#b').click() |      |
| exec     | 执行原生事件                  | cy.exec('npm run build').then((result) => { ... }            |      |
| focused  |                               |                                                              |      |
| reload   | 刷新                          | cy.reload() // 普通刷新 cy.reload(forceReload) //强刷        |      |

## 数据请求 | 数据处理

| 方法                        | 功能                                                | 范例                                                         | 参考                                                      |
| --------------------------- | --------------------------------------------------- | ------------------------------------------------------------ | --------------------------------------------------------- |
| server()                    |                                                     |                                                              |                                                           |
| route(options)              | 参数                                                | cy.route(url) cy.route(url, response) cy.route(method, url) cy.route(method, url, response) cy.route(callbackFn) cy.route(options) |                                                           |
| clearCookie(name[,options]) | 清除选定cookie 默认会清除 一般用不到                | cy.clearCookie('authId')                                     |                                                           |
| clearCookies                | 清除所有cookie                                      |                                                              |                                                           |
| clearLocalStorage           | 清除localstorage                                    |                                                              |                                                           |
| request(method, url, body)  | 数据请求                                            |                                                              | [参考](https://docs.cypress.io/api/commands/request.html) |
|                             | 存在cypress.json的baseUrl baseUrl作为主机           | // cypress.json {"baseUrl": "[http://localhost:1234](http://localhost:1234/)"} // spec.js cy.request('seed/admin')http://localhost:1234/seed/ad |                                                           |
|                             | 没有cypress.json的baseUrl 上一个visit的网址作为主机 | cy.visit('http://localhost:8080/app') cy.request('users/1.json') http://localhost:8080/users/1.json |                                                           |
| wrap                        | 传值测试                                            | const getName = () => { return 'Jane Lane'} cy.wrap({ name: getName }).invoke('name').should('eq', 'Jane Lane') // true |                                                           |

## 其他

| 方法               | 功能                                                         | 范例                                                         | 参考 |
| ------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ---- |
| debugger           | 要在 then() 里调用                                           |                                                              |      |
| task()             | 通过插件事件在Node.js中执行代码task。                        |                                                              |      |
| exec()             | 执行Shell                                                    |                                                              |      |
| config()           | 在测试中获取和设置配置选项                                   | Cypress.config() Cypress.config(name) Cypress.config(name, value) Cypress.config(object) |      |
| as( str )          | 设置别名 不能单独使用                                        | cy.route('PUT', 'users', 'fx:user').as('putUser') cy.get('.main-nav').find('li').first().as('firstNav') |      |
| this.alias @alias  | 使用别名 简写符号@                                           | cy.get('.contain').as('c') cy.get('this.c').find('input') 等价于 cy.get('@c').find('input') |      |
| clock( )           | 时间有关的各种 * setTimeout * clearTimeout * setInterval * clearInterval * Date 对象 | cy.clock()                                                   |      |
|                    |                                                              | cy.clock(now)                                                |      |
|                    |                                                              | cy.clock(now, functionNames)                                 |      |
|                    |                                                              | cy.clock(options)                                            |      |
|                    |                                                              | cy.clock(now, options)                                       |      |
|                    |                                                              | cy.clock(now, functionNames, options)                        |      |
| clock.tick( time ) | 时间偏移量                                                   | cy.clock()                                                   |      |
|                    |                                                              | cy.visit('/index.html')                                      |      |
|                    |                                                              | cy.tick(1000)                                                |      |
|                    |                                                              | cy.get('#seconds-elapsed')                                   |      |
|                    |                                                              | .should('have.text', '1 seconds') cy.tick(1000) cy.get('#seconds-elapsed') |      |
|                    |                                                              | .should('have.text', '2 seconds')                            |      |
| clock.restore()    |                                                              |                                                              |      |
| go                 | 前进后退                                                     | cy.go('back') cy.go(1)                                       |      |
| hover              | 禁止使用(有BUG)                                              | cy.get('.menu-item').trigger('mouseover') cy.get('.popover').should('be.visible') |      |
|                    | 可以使用trigger模拟                                          |                                                              |      |
| invoke             | 调用函数的别名                                               | cy .wrap({ animate: fn }) .invoke('animate')                 |      |
|                    | 注意 别名必须先出现                                          |                                                              |      |
| its                | 调用元素别名                                                 | cy .wrap({ width: '50' }).its('width')                       |      |
|                    | 获取元素数量，元素属性，sessionStorage等 https://docs.cypress.io/api/commands/its.html#Command-Log | // Get the 'width' property cy .window().its('sessionStorage') |      |
|                    |                                                              | // Get the 'sessionStorage' property cy .wrap({ age: 52 })   |      |
|                    |                                                              | .its('age').should('eq', 52)                                 |      |
|                    |                                                              | // true                                                      |      |
|                    |                                                              | cy .get('ul li').its('length') .should('be.gt', 2)}) cy.request(...) .its('body.user') .then(user => ...) |      |
|                    |                                                              | cy .title().its('length').should('eq', 24)                   |      |
| log                | 打印log                                                      | cy.log('created new user’) cy.log( str, args ) cy.log('events triggered', events) |      |
| pause              | 暂停 - 暂停运行 可以手动操作                                 |                                                              |      |
| resume             | 恢复 - 继续运行                                              |                                                              |      |
| then               | 处理前缀yield的内容                                          | cy.get('button') .then(($btn) => { const cls = $btn.class() cy.wrap($btn).click() .should('not.have.class', cls) }) |      |

## 补充 - 断言相关的语法

| 方法   | 功能                       | 范例                                                         | 参考 |
| ------ | -------------------------- | ------------------------------------------------------------ | ---- |
| should | 断言                       | cy.get('.btn').should('be.empty') cy.get('.greeting').should('not.be.visible') |      |
|        |                            | cy.get('.btn') .should((text2) => { expect(text1).not.to.eq(text2) }) |      |
|        |                            | cy.get('option:first') .should('be.selected') .then(($option) => { ... }) |      |
|        |                            | cy.request('/users/1').its('body').should('deep.eq', { name: 'Jane' }) |      |
|        | value id \| class \| value | cy.get('input') .should('have.class', 'btn')                 |      |
|        |                            | cy.get('input') .should('not.have.value', 'Jane')            |      |
|        |                            | cy.get('button') .should('have.id', 'a') .then(($button) => { // $button is yielded }) |      |
|        | Method and Value           | cy.get('#header a') .should('have.attr', 'href', '/users')   |      |
|        | Focus                      | cy.get('#ipt') .should('have.focus')                         |      |
|        | Function                   | 看官网                                                       |      |
|        | 断言样式                   | cy.get('div').should('have.css','color','blue')              |      |
|        | 断言文本 完全匹配          | cy.get('div').should('have.text', 'foobarbaz')               |      |
|        | 断言文本 部分匹配\|包含    | cy.get('div').should('contain', 'foobarbaz')                 |      |
|        | 断言之前使用文本           | cy.get('div').should(($div) => {                             |      |
|        |                            | const text = $div.text()                                     |      |
|        |                            | expect(text).to.match(/foo/)                                 |      |
|        |                            | expect(text).to.include('foo')                               |      |
|        |                            | expect(text).not.to.include('bar') })                        |      |
|        | 保留引用 or 比较文本值     | cy.get('div').invoke('text') .then((text1) => { cy.get('button').click() //text change cy.get('div').invoke('text') .should((text2) => { expect(text1).not.to.eq(text2) }) }) |      |
|        |                            | cy.get('#header a') .should('have.class', 'active') .and('have.attr', 'href', '/users') |      |
|        | 获取innerText              | cy.get('div').should(($div) => { // access the native DOM element expect($div.get(0).innerText).to.eq('foobarbaz') }) |      |

======end======