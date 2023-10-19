有三种类型的 GitHub Pages 站点：项目、用户和组织。 项目站点连接到 GitHub 上托管的特定项目。 用户和组织站点连接到特定的 GitHub 帐户。

要发布用户站点，必须创建名为 `<user>.github.io` 的用户帐户所拥有的仓库。 要发布组织站点，必须创建名为 `<organization>.github.io` 的组织所拥有的仓库。 除非您使用自定义域，否则用户和组织站点位于 `http(s)://<username>.github.io` 或 `http(s)://<organization>.github.io`。

项目站点的源文件与其项目存储在同一个仓库中。 除非您使用自定义域，否则项目站点位于 `http(s)://<user>.github.io/<repository>` 或 `http(s)://<organization>.github.io/<repository>`。



## **创建项目**

1. 新建一个仓库，名称随意。

2. 进入仓库主页，点击右面的`Settings`，找到**GitHub Pages**部分，选择`source`和 `branch`

   **（注意这里需要选择一个主题，之后可以再改，不选择的话页面可能会无法加载，显示`“There isn't a GitHub Pages site here.”`）**

   **好像是点这个地方，点开随便看看，关闭就行。**

   ![](https://gcore.jsdelivr.net/gh/lzcgeorge/imagebed@main/20231019150849.png)

   

3. 建议勾选 `Enforce HTTPS`，否则访问时会出现安全警告。

4. 没有出错的话，一个项目主页就建立完成了，可以通过`<username>.github.io/<projectname>`访问到了