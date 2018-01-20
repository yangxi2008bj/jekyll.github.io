---
layout:     post
title:      "SonarLint代码审查"
date:       2017-09-20
author:     "Xi Yang"
tags: 
	- sonar
	- eclipse
---

##### SonarLint简介
SonarLint是Eclipsede的一个插件，在编码过程中实时提示你的代码是否符合规范，是否存在bug，代码复杂度是否过高等的插件。目前支持Java, JavaScript, PHP, Python等。它能够帮助程序员更好的养成规范的代码习惯。同时也为SonarQube进行代码质量检查提供了基础，避免开发过程中的多次返工。

##### Eclipse如何安装SonarLint
- 打开Eclipse后，help -> Eclipse Marketplace 查找sonarLint, 进行插件安装。

- 也可打开Eclipse后，help -> Eclipse Marketplace后，在网页https://marketplace.eclipse.org/content/sonarlint，将install拖拽至已打开的marketplace中进行下载

##### 如何使用SonarLint
- 在Window -> Show view -> Other 中去查找，并添加SonarLint On-The-Fly控制台或SonarLint Report。   
![](/blogImages/eclipsesonarlint1.jpg)

- 添加SonarQube server。

	* Window -> Show view -> Other 中去查找SonarQube server view。
	
	* 在SonarQuebe server view中右件选择 New -> Server connection (也可直接通过File -> New -> Other... -> SonarLint -> New Server 进行添加)

	* 选择SonarQube，下一步  
	![](/blogImages/eclipsesonarlint2.jpg)
	* 配置SonarQube服务器信息，如图  
	![](/blogImages/eclipsesonarlint3.jpg)
	* 可选择关联服务器上已建立的项目和本地项目，在需要绑定的项目右键，SonarLint -> Bind to a SonarQube project...，并按照下图步骤车进行绑定  
	![](/blogImages/eclipsesonarlint4.jpg)
	![](/blogImages/eclipsesonarlint5.jpg)

- 分析代码，在需要分析的项目右键，SonarLint -> Analyze，即可在SonarLint Report控制台或者SonarLint On-The-Fly控制台中查看代码分析结果  
	![](/blogImages/issuelocationsview.gif)

更多问题可以参考SonarLint官网，http://www.sonarlint.org/eclipse/index.html