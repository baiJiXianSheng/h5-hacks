
# Yarn 安装使用-问题

### 1. 执行 通过 `yarn global add umi` 安装的全局模块命令，如 `umi -v` 时，提示 umi 命令不存在等：
>查看该模块安装目录：
>>$ `npm -g bin` &emsp;&emsp;查看 `npm` 模块应用安装目录 
C:\Users\username\AppData\Roaming\npm

>>$ `yarn global bin` &emsp;&emsp;查看 `yarn` 模块应用安装目录 
C:\Users\username\AppData\Local\Yarn\bin

>><font face="黑体" color=red size=5>*注意：*</font>若使用 `yarn -g bin` 
C:\Users\username\node_modules\.bin

>><font face="黑体" color=red size=5>*注意：*</font>yarn 全局安装命令为 `yarn global add xxx`，而非 `yarn -g add xxx`

>解决方案：
>>通过 npm 和 yarn 安装目录可知，通过 `npm install yarn -g` 安装的yarn，需要将 其路径添加到 环境变量中，（以win10为例）步骤如下：
>>`控制面板`-->`系统和安全`-->`高级系统保护`-->`系统属性-高级`-->`环境变量`-->`用户变量 和 系统变量` 的 `Path` 双击或单击选中后编辑-->`新建` 将刚才查看的yarn全局路径`C:\Users\username\AppData\Local\Yarn\bin`复制粘贴-->一路`保存退出`即可-->`重新打开 cmd`，再次输入 umi 即可正常使用该模块命令。

