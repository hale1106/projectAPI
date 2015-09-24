# projectAPI
指尖灵动 项目构建说明

1.	目前的构建工具为yeoman+grunt
	*	利用yeoman生成的新项目
		*	全局安装<font style="color:#999;background:#eee;border:1px solid #999;padding:2px;border-radius:5px;margin:0 3px">nodejs</font>， 运行<font style="color:#999;background:#eee;border:1px solid #999;padding:2px;border-radius:5px;margin:0 3px">npm install -g yo generator-pitaya</font>安装项目生成依赖的相关脚本
		*	在项目存放路径下运行<font style="color:#999;background:#eee;border:1px solid #999;padding:2px;border-radius:5px;margin:0 3px">yo pitaya</font>生成主项目，生成过程中会有以下选项供选择和填写
			*	选择项目类型：如果为纯静态项目，选择h5，如果为需后端java参与的项目，选择java
			*	填入主项目的名称，一般为客户名
			*	填入子项目的名称，一般为项目名
			*	生成完成！
		*	如需在主项目下新建子项目，即同一个客户的多个项目时，
			*	如本身为h5项目，则在主项目的根目录下运行<font style="color:#999;background:#eee;border:1px solid #999;padding:2px;border-radius:5px;margin:0 3px">yo pitaya --sub</font>，后面步骤同上按提示填入
			*	如本身为java项目，则在fe-source运行<font style="color:#999;background:#eee;border:1px solid #999;padding:2px;border-radius:5px;margin:0 3px">yo pitaya --sub</font>，后面步骤同上按提示填入
		*	安装服务依赖包
			*	h5项目：进入<font color="#f00">子</font>项目根目录，运行<font style="color:#999;background:#eee;border:1px solid #999;padding:2px;border-radius:5px;margin:0 3px">npm install</font>安装
			*	java项目，进入<font color="#f00">主</font>项目根目录，运行<font style="color:#999;background:#eee;border:1px solid #999;padding:2px;border-radius:5px;margin:0 3px">npm install</font>安装
	*	开发环境
		*	安装：全局安装<font style="color:#999;background:#eee;border:1px solid #999;padding:2px;border-radius:5px;margin:0 3px"> npm install -g grunt-cli fis jello fis-postpackager-simple fis-parser-less</font>
		*	概括：
			*	h5项目：
				*	核心脚本为fis，在fis的基础上进行封装，fis相关<a href="http://fis.baidu.com/docs/beginning/getting-started.html" target="_blank">查看官网</a>
			*	java项目：
				*	核心脚本为jello，在jello的基础上进行封装，前端模版引驚为velocity，jello相关<a href="https://github.com/fex-team/jello" target="_blank">查看git</a>
		*	目录结构和重要文件说明
			*	h5项目：src为前端主开发目录，build目录为发布目录(grunt build后生成)
			*	java项目：
				*	fe-source为前端主开发目录，webApp为发布目录
				*	page下为vm文件，loyout.vm为公共模版文件，包括头，尾，分享等公共代码
			*	fis-conf.js为主配置文件，一般无需改动
			*	abc.json为项目相关信息，如出现端口，可改变其中的part字段后重启服务
		*	相关命令（windows系统在命令后加_win）：
			*	<font style="color:#999;background:#eee;border:1px solid #999;padding:2px;border-radius:5px;margin:0 3px">grunt demo</font>
				*	启动调试服务，不做压缩，去缓存处理，默认启动9000端口，如需改端口，可在abc.json里修改port
				*	自动监听文件变动，调试时修改文件直接刷新浏览
			*	<font style="color:#999;background:#eee;border:1px solid #999;padding:2px;border-radius:5px;margin:0 3px">grunt debug</font>
				*	启动调试服务，会做压缩，去缓存处理，完全模拟线上环境，默认启动9000端口，如需改端口，可在abc.json里修改port
				*	自动监听文件变动，调试时修改文件直接刷新浏览
			*	<font style="color:#999;background:#eee;border:1px solid #999;padding:2px;border-radius:5px;margin:0 3px">grunt build</font>
				*	构建并在项目根目录下生成压缩、加md5去缓存后完整项目
				*	然后就可以用该目录发布上线啦
			*	<font style="color:#999;background:#eee;border:1px solid #999;padding:2px;border-radius:5px;margin:0 3px">grunt newbranch</font>
				*	用于新建并切换git分支
				*	功能相当于git checkout -b branch_name，但自动会规则分支名形如daily/0.0.1自加
			*	<font style="color:#999;background:#eee;border:1px solid #999;padding:2px;border-radius:5px;margin:0 3px">grunt prepub</font>
				*	用于提交该分支到git仓库
				*	可在命令后加参数做为提交的日志，如grunt prepub:'up date'
				*	功能相当于git add . ; git commit -m 'up date' ; git push origin branch_name;
			*	grunt publish
				*	用于提交分支、加tag、切换到master、更新并提交master
				*	可在命令后加参数做成提交的日志，如grunt publish:'up date'
				*	功能相当于git tag tag_name;git push origin tag_name:tag_name; git checkout master; git pull orign branch_name; git push origin master
			*	开发流程一般为，<font style="color:#999;background:#eee;border:1px solid #999;padding:2px;border-radius:5px;margin:0 3px">grunt newbranch</font>新建分支，<font style="color:#999;background:#eee;border:1px solid #999;padding:2px;border-radius:5px;margin:0 3px">grunt demo</font>启服务，<font style="color:#999;background:#eee;border:1px solid #999;padding:2px;border-radius:5px;margin:0 3px">grunt build</font>进行构建，<font style="color:#999;background:#eee;border:1px solid #999;padding:2px;border-radius:5px;margin:0 3px">grunt prepub</font>提交到当前分支，<font style="color:#999;background:#eee;border:1px solid #999;padding:2px;border-radius:5px;margin:0 3px">grunt publish</font>提交合并到master
			*	注意：
				*	提交前务必grunt build到发布目录
				*	grunt publish后会新建对应的git tag，下次不可以在该分支上开发
				*	如直接在master上进行开发，则不可用grunt prepub，grunt publish进行上传，可用git原始命令提交
		*	前后端分离
			*	路由管理	
				*	h5项目在用grunt demo启服务成功后，自动会在浏览器中打开调试链接，如127.0.0.1:9000，该链接对应index.html首页，如有新加的页面，如test.html,可直接访问127.0.0.1:9000/test.html。
				*	java项目grunt demo启服务成功后，自动会在浏览器中打开调试链接，如127.0.0.1:9000，该链接对应index.vm，路由的配置文件在server.conf里已配置好，如新加vm页面，可在server.conf中按示例配置
			*	数据模拟
				*	页面数据模拟：模拟的数据都在/fe-source/test/page/下，默认有json文件做为对应的数据，如/fe-source/page/index.vm在数据文件为/fe-source/test/page/index.json，无需配置，即自动对应解析相关的变量和数据
				*	ajax数据模拟：在/fe-source/test/page/下新建接口同名的json文件，然后在server.conf文件里配置对应的路由。如接口为/fe-source/aa/bb/submitInfo，则对应的文件为/fe-source/page/bb/submitInfo，然后在server.conf中按示例配置<font style="color:#999;background:#eee;border:1px solid #999;padding:2px;border-radius:5px;margin:0 3px">rewrite ^\/aa\/bb\/submitInfo$ /page/bb/submitInfo.json</font>
	*	注意事项
		*	如遇到权限不足，启服务失败，不要用sodu提权，可以<font style="color:#999;background:#eee;border:1px solid #999;padding:2px;border-radius:5px;margin:0 3px">chmod 777 -R 对应的路径	</font>来提权
