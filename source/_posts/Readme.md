# 作者信息
[覃雨翔（Eric Qin）Blog](http://code4cocoa.com)，热爱编程，爱学习，爱折腾，关注敏捷研发及项目管理。
# 开发编译环境
- Windows 10
- Visual Studio 2017
- .Net Framework 4.6.2

# 工程目录结构
```
ThoughtWorksHomeWork
    Extension
    ThoughtWorksHomeWork
    Trains
        Exceptions
        Models
        Resources
            Cities.json
            CitiesDistance.json
            InputData.json
        Utilities
        TrainsProcess.cs
    TrainsUnitTest
```
## Extension
该类库放置公共的扩展方法。
## ThoughtWorksHomeWork
控制台应用程序
## Trains
该类库放置解决Trains问题需要使用的相关类及资源。
### Exception
该文件夹放置Trains业务中使用的异常类。
### Models
该文件夹放置Trains业务中使用的模型。
### Resources
该文件夹放置Trains业务中使用的资源、数据模板。
#### Cities.json（预置数据）
城市列表预置数据。
#### CitiesDistance.json（预置数据）
城市间距离预置数据。
#### InputData.json（预置数据）
业务参数。
### Utilities
该文件夹放置Trains业务中使用的工具类。
### TrainsProcess.cs
该静态类包含实现Trains业务的主要方法。
## TrainsUnitTest
Trains业务的单元测试。



