# 杂项

## 发布版本配置

### uglify mini scopes配置

配置pattern

```
file:*.js&&!file:*.min.js&&!file:*.pack.js
```

### sass去除sourcemap调试

配置arguments

```
--sourcemap=none --no-cache --update --style compressed $FileName$:$FileNameWithoutExtension$.css
```

### js 统一配置成.min.js后缀

## 编辑器配置

### phpstorm sass配置

首先安装ruby

preference-&gt;file watcher下应该会自动配置好，若没配置好，请参照[这里](https://stackoverflow.com/questions/15760140/phpstorm-scss-file-watcher-settings)

安装compass

```
sudo gem install -n /usr/local/bin compass
```

然后在file watchers 下添加scss，配置arguments

```
--no-cache --update --style compressed $FileName$:$FileNameWithoutExtension$.css
```

output paths 配置

```
$FileNameWithoutExtension$.css:$FileNameWithoutExtension$.css.map
```

### phpstorm js压缩配置

安装uglify-js，一般放在/usr/local/bin/路径下，[参考](https://github.com/mishoo/UglifyJS2)

```
npm install uglify-js -g
```

然后配置file watchers

```
$FileName$ -o $FileNameWithoutExtension$.min.js --mangle-props keep_quoted,reserved=[$,jQuery,attach],regex=/^_/ -c -m
```

output paths 配置

```
$FileNameWithoutExtension$.min.js
```

### svn忽略文件

首先添加css文件，其他文件 scss css.map 不要放入SVN控制

svn status \| grep "^\?" \| awk "{print $2}" &gt; ignoring.txt  
svn propset svn:ignore -F ignoring.txt .  
rm ignoring.txt  
svn ci --message "ignoring some files"  
svn proplist -v

### sublime3插件

1.安装node包

jscs npm install jscs -g  
jshint npm install jshint -g  
csscomb npm install csscomb -g  
csslint npm install csslint -g

2.安装gem包

scss-lint gem install scss\_lint

3.安装sublime3 [Package Control](https://packagecontrol.io/installation#st3)

按下 ctrl+\`  
复制粘贴以下代码 import urllib.request,os,hashlib; h = 'eb2297e1a458f27d836c04bb0cbaf282' + 'd0e7a3098092775ccb37ca9d6b2e4b7d'; pf = 'Package Control.sublime-package'; ipp = sublime.installed\_packages\_path\(\); urllib.request.install\_opener\( urllib.request.build\_opener\( urllib.request.ProxyHandler\(\)\) \); by = urllib.request.urlopen\( '[http://packagecontrol.io/](http://packagecontrol.io/)' + pf.replace\(' ', '%20'\)\).read\(\); dh = hashlib.sha256\(by\).hexdigest\(\); print\('Error validating download \(got %s instead of %s\), please try manual install' % \(dh, h\)\) if dh != h else open\(os.path.join\( ipp, pf\), 'wb' \).write\(by\)

4.安装sublime3插件

按下 ctrl+shift+p，输入'ip'（Install Package）  
输入以下插件的名字，按顺序逐个进行安装：

EditorConfig  
Sass  
SublimeLinter  
SublimeLinter-jscs  
SublimeLinter-jshint  
SublimeLinter-csslint  
SublimeLinter-contrib-scss-lint  
JSFormat  
CSScomb

5.插件的配置文件

将以下配置文件分别下载后放入项目根目录下：

EditorConfig [配置文件](http://alloyteam.github.io/CodeGuide/.editorconfig)  
JSCS [配置文件](http://alloyteam.github.io/CodeGuide/.jscsrc)  
JSHint [配置文件](http://alloyteam.github.io/CodeGuide/.jshintrc)  
注意：全局变量需要手动加到配置文件的globals属性里，例：

{  
    "globals": {  
        "ImageHandle": true  
    }  
}  
CSSLint [配置文件](http://alloyteam.github.io/CodeGuide/.csslintrc)  
SCSS-Lint [配置文件](http://alloyteam.github.io/CodeGuide/.scss-lint.yml)

6.编辑器及插件设置

* sublime3 自身

  Preferences-&gt;Setting-User，增加下面两个配置：

  {  
        "translate\_tabs\_to\_spaces": true,  
        "word\_wrap": true  
    }  
    点击右下角的Spaces-&gt;Convert Indentation to Spaces可以将文件中的所有tab转换成空格

* JSFormat

  Preferences-&gt;Package Settings-&gt;JSFormat-&gt;Setting-User，下载[配置文件](http://alloyteam.github.io/CodeGuide/jsformat_setting_user.json)覆盖

  配置好后格式化的默认快捷键是 ctrl+alt+f

* SublimeLinter

  右键-&gt;SublimeLinter-&gt;Lint Mode，有4种检查模式，建议选择 Load/save

  右键-&gt;SublimeLinter-&gt;Mark Style，建议选择 Outline

  右键-&gt;SublimeLinter-&gt;Choose Gutter Theme，建议选择 Blueberry-round

  右键-&gt;SublimeLinter-&gt;Open User Settings，将linter里面jscs的args改成 \["--verbose"\]，将linter里面csslint的ignore改成 "box-model,adjoining-classes,box-sizing,compatible-vendor-prefixes,gradients,text-indent,fallback-colors,star-property-hack,underscore-property-hack,bulletproof-font-face,font-faces,import,regex-selectors,universal-selector,unqualified-attributes,overqualified-elements,duplicate-background-images,floats,font-sizes,ids,important,outline-none,qualified-headings,unique-headings"

  当光标处于有错误的代码行时，详细的错误信息会显示在下面的状态栏中

  右键-&gt;SublimeLinter可以看到所有的快捷键，其中 ctrl+k, a 可以列出所有错误

* CSScomb

  Preferences-&gt;Package Settings-&gt;CSScomb-&gt;Setting-User，下载[配置文件](http://alloyteam.github.io/CodeGuide/csscomb_setting_user.json)覆盖

  配置好后格式化的默认快捷键是 ctrl+shift+c



