# phpMyAdmin网页MySQL客户端安装

## 实现方案——工具/原料
实现方案：Apache+PHP+MySQL+phpMyAdmin，Windows7 64位操作系统

[Apache官网](https://www.apachehaus.com/cgi-bin/download.plx)下载最新版本，如Apache2.4.29

[PHP官网](http://windows.php.net/download#php-7.0)下载最新版本，如php-7.0.27

[MySQL官网](https://dev.mysql.com/downloads/mysql/5.7.html)下载最新版本

[phpMyAdmin官网](https://www.phpmyadmin.net/downloads/)下载最新版本，如phpMyAdmin-4.7.7
## 一，Apache的下载，安装

 1. 下载并解压apache安装包，如【[httpd-2.4.29-o102n-x64-vc14-r2.zip](https://www.apachehaus.com/cgi-bin/download.plx?dli=OBDe24UeNRTTUp1KUxmSEBlVOpkVFVFdTtmSTR2Z)】![enter image description here](https://gitee.com/lidechenyan/images/raw/master/Apache.PNG)
 2. 解压至自定义目录下，如C:\Program Files\Apache24
 3. 找到“apache存放目录\conf\httpd.conf”文件，用编译器打开，找到Define SRVROOT，修改为apache存放目录，如下。

	    Define SRVROOT "C:\Program Files\Apache24"

 4. 进入apache存放目录\bin，打开cmd窗口，执行以下语句。

	    httpd.ext -k install -n apache24
    
 5. 在apache存放目录\bin，找到ApacheMonitor.exe，点击后弹出设置框，选择Apache24，点击start启动服务。
 6. 打开浏览器，访问http://localhost，若如下图显示，Apache安装成功。
 ![enter image description here](https://gitee.com/lidechenyan/images/raw/master/apache-success.PNG)
 ## 二、php的下载，与Apache整合
 

 1. 下载PHP，如【[php-7.0.27-Win32-VC14-x64.zip](http://120.198.248.35/cache/windows.php.net/downloads/releases/php-7.0.27-Win32-VC14-x64.zip?ich_args2=883-19103700016945_d32b64561aed4a0605dc2fae024fd7e9_10001002_9c89652ad4c1f8d5913d518939a83798_5d92b3637e149382a4da400d148d5e6d)】
![enter image description here](https://gitee.com/lidechenyan/images/raw/master/php.PNG)

 2. 解压至自定义目录下，如C:\Program Files\php-7.0.27
 3. 找到C:\Program Files\php-7.0.27\php.ini-development文件，重命名为php.ini，打开后，找到extension_dir="ext"，去掉分号，修改为如下语句。

	     extension_dir = "C:/Program Files/php-7.0.27/ext"
 4. 找到apache存放目录\conf\httpd.conf文件，打开如下代码位置，加入注释中的代码（从180行开始）。

        #LoadModule watchdog_module modules/mod_watchdog.so
	    #LoadModule xml2enc_module modules/mod_xml2enc.so
	    
	    #***********php与Apache整合*****************************
	    #让apache载入php处理模块
	    LoadModule php7_module "C:/Program Files/php-7.0.27/php7apache2_4.dll"
	    #指定php的ini文件，该文件是对php的一些配置
	    PHPIniDir "C:/Program Files/php-7.0.27"
	    AddType application/x-httpd-php .php .phtml
	    #*******************************************************
	    
	    <IfModule unixd_module>
 5. 在apache存放目录\htdocs目录下，新建test.hph文件，内容如下：

	    <?php
	    	phpinfo();
	    ?>
 6. 在浏览器访问http://localhost/test.php，有PHP version等信息显示，说明整合成功。
## 三、MySQL的下载，与PHP整合

  1. 下载MySQL，如【[mysql-5.7.21-winx64.zip](https://cdn.mysql.com//Downloads/MySQL-5.7/mysql-5.7.21-winx64.zip)】
  2. 解压，存放到自定义目录下，如C:\Program Files (x86)\mysql-5.7.21-winx64
  3. 在MySQL存放目录下，新建data文件夹；配置环境变量，将MySQL存放目录\bin添加到path中；打开cmd窗口，输入mysqld -install；启动mysql服务，输入net start mysql；输入mysql -uroot -p；设置MySQL密码，输入SET PASSWORD FOR 'root'@'localhost'=PASSWORD('新密码')。
  4. 与PHP整合，打开PHP存放目录下php.ini文件，找到887行开始，修改如下。去除php_mbstring.dll和php_mysqli.dll之前的注释。

	;extension=php_ldap.dll
	extension=php_mbstring.dll
	;extension=php_exif.dll      ; Must be after mbstring as it depends on it
	extension=php_mysqli.dll
	;extension=php_oci8_12c.dll  ; Use with Oracle Database 12c Instant Client
	;extension=php_openssl.dll`

 5. 在apache存放目录\htdocs目录下，新建testsql.php，内容如下。

	    <?php
			 $coun=mysqli_connect("localhost","root","数据库密码");
			 if ($coun) {
				 echo"OK";
		  }else{
				 echo "error";
		  }
		?>
 6. 在浏览器访问http://localhost/testsql.php，显示OK，MySQL整合成功。
## 四，phpMyAdmin的安装
 1. 下载phpMyAdmin，如【[phpMyAdmin-4.7.7-all-languages.zip](https://files.phpmyadmin.net/phpMyAdmin/4.7.7/phpMyAdmin-4.7.7-all-languages.zip)】![enter image description here](https://gitee.com/lidechenyan/images/raw/master/phpMyAdmin.PNG)
 2. 解压到apache存放目录\htdocs目录下
 3. 进入phpMyAdmin目录，如C:\Program Files\Apache24\htdocs\phpMyAdmin-4.7.7-all-languages，复制config.sample.inc.php重命名为config.inc.php，修改config.inc.php文件。在20行开始，加入以下代码，设置多个数据源的数据库连接。

	    /**
	     * Servers configuration
	     */
	    $i = 0;
	    
	    /**
	     * First server
	     */
	    $hosts = array(
	    '1'=>array('host'=>'主机1的IP','user'=>'你的数据库用户名','password'=>'你的密码'),
	    '2'=>array('host'=>'主机2的IP','user'=>'你的数据库用户名','password'=>'你的密码'),
	    '3'=>array('host'=>'主机3的IP','user'=>'你的数据库用户名','password'=>'你的密码')
	    );
	    for($i=1;$i<=count($hosts);$i++){
	    
	    /* Authentication type */
	    $cfg['Servers'][$i]['auth_type'] = 'cookie';
	    /* Server parameters */
	    $cfg['Servers'][$i]['host'] = $hosts[$i]['host'];   //修改host
	    $cfg['Servers'][$i]['connect_type'] = 'tcp';
	    $cfg['Servers'][$i]['compress'] = false;
	    /* Select mysqli if your server has it */
	    $cfg['Servers'][$i]['extension'] = 'mysql';
	    $cfg['Servers'][$i]['AllowNoPassword'] = true;
	    $cfg['Servers'][$i]['user'] = $hosts[$i]['user'];  //修改用户名
	    $cfg['Servers'][$i]['password'] = $hosts[$i]['password']; //密码
	    /* rajk – for blobstreaming */
	    $cfg['Servers'][$i]['bs_garbage_threshold'] = 50;
	    $cfg['Servers'][$i]['bs_repository_threshold'] = '32M';
	    $cfg['Servers'][$i]['bs_temp_blob_timeout'] = 600;
	    $cfg['Servers'][$i]['bs_temp_log_threshold'] = '32M';
	    }
 4. 在浏览器访问http://localhost/phpMyAdmin-4.7.7-all-languages/index.php，出现选择服务器选择框，并且有三个主机选项，说明phpMyAdmin安装成功。
