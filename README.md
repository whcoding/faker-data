# faker-data
该包用于生成假数据,模拟生产环境真实数据量. 该项目集成了 [Faker](https://github.com/fzaninotto/Faker) 和 [phinx](https://github.com/cakephp/phinx)
, Faker 方便我们快速生成假数据, phinx 方便我们快速创建表和运行seed. 

进过测试 本地虚拟机 2h CPU 2G内存 单表插入10w数据 用时6.5秒左右

安装:
```
# 下载该项目
git clone https://github.com/whcoding/faker-data.git

# 进入目录
cd /path/to/faker-data

# 安装依赖
composer install 
```

使用:
```
# 初始化 phinx 
vendor/bin/phinx init

# 初始化完成后会自动创建数据库配置文件 phinx.php
```


创建迁移脚本: 
```
php vendor/bin/phinx create MyNewMigration
```


创建Seed类: 
```
php vendor/bin/phinx seed:create UserSeeder
```

其他命令具体参考 [phinx中文文档](https://tsy12321.gitbooks.io/phinx-doc)


---

Faker 生成中文数据 

```
$faker = Factory::create('zh_CN');
```

生成 [其他语言](https://github.com/fzaninotto/Faker/tree/master/src/Faker/Provider) 数据

Faker 方法总结 [原地址](https://blog.csdn.net/u010496966/article/details/94172566)

基础方法: 
```
随机数：randomDigit             // 7
不为空随机数：randomDigitNotNull      // 5
随机数：randomNumber($nbDigits = NULL, $strict = false) //
随机浮点数：randomFloat($nbMaxDecimals = NULL, $min = 0, $max = NULL) // 48.8932
区间内的随机数：numberBetween($min = 1000, $max = 9000) // 8567
随机字母：randomLetter            // 'b'
// returns randomly ordered subsequence of a provided array
随机选取数组中的几个，返回也为数组：randomElements($array = array ('a','b','c'), $count = 1) // array('c')
随机选取数组中的一个：randomElement($array = array ('a','b','c')) // 'b'
打乱字符串：shuffle('hello, world') // 'rlo,h eoldlw'
打乱数组:shuffle(array(1, 2, 3)) // array(2, 1, 3)
随机插入数字：numerify('Hello ###') // 'Hello 609'
随机字母替换：lexify('Hello ???') // 'Hello wgt'
随机字母或者数字替换：bothify('Hello ##??') // 'Hello 42jz'
asci码随机替换：asciify('Hello ***') // 'Hello R6+'
正则匹配后生成：regexify('[A-Z0-9._%+-]+@[A-Z0-9.-]+\.[A-Z]{2,4}'); // sm0@y8k96a.ej
```
文本: 
```
单词：word                                             // 'aut'
单词组：words($nb = 3, $asText = false)                  // array('porro', 'sed', 'magni')
句子：sentence($nbWords = 6, $variableNbWords = true)  // 'Sit vitae voluptas sint non voluptates.'
句子数组：sentences($nb = 3, $asText = false)              // array('Optio quos qui illo error.', 'Laborum vero a officia id corporis.', 'Saepe provident esse hic eligendi.')
段落：paragraph($nbSentences = 3, $variableNbSentences = true) // 'Ut ab voluptas sed a nam. Sint autem inventore aut officia aut aut blanditiis. Ducimus eos odit amet et est ut eum.'
段落数组：paragraphs($nb = 3, $asText = false)             // array('Quidem ut sunt et quidem est accusamus aut. Fuga est placeat rerum ut. Enim ex eveniet facere sunt.', 'Aut nam et eum architecto fugit repellendus illo. Qui ex esse veritatis.', 'Possimus omnis aut incidunt sunt. Asperiores incidunt iure sequi cum culpa rem. Rerum exercitationem est rem.')
文本内容：text($maxNbChars = 200)                          // 'Fuga totam reiciendis qui architecto fugiat nemo. Consequatur recusandae qui cupiditate eos quod.'
```

姓名:
```
称谓： title($gender = null|'male'|'female')     // 'Ms.'
男士称谓：titleMale                                 // 'Mr.'
女士称谓：titleFemale                               // 'Ms.'
前缀：suffix                                    // 'Jr.'
名字：name($gender = null|'male'|'female')      // 'Dr. Zane Stroman'
名：firstName($gender = null|'male'|'female') // 'Maynard'
男士名：firstNameMale                             // 'Maynard'
女士名：firstNameFemale                           // 'Rachel'
字：lastName                                  // 'Zulauf'
```

城市:
```
城市前缀：cityPrefix                          // 'Lake'
详细地址：secondaryAddress                    // 'Suite 961'
州：state                               // 'NewMexico'
州的缩写：stateAbbr                           // 'OH'
城市后缀：citySuffix                          // 'borough'
接到前缀：streetSuffix                        // 'Keys'
建筑物的号码：buildingNumber                      // '484'
城市：city                                // 'West Judge'
街道名称：streetName                          // 'Keegan Trail'
街道地址：streetAddress                       // '439 Karley Loaf Suite 897'
邮政编号：postcode                            // '17916'
详细地址：address                             // '8888 Cummings Vista Apt. 101, Susanbury, NY 95473'
国家：country                             // 'Falkland Islands (Malvinas)'
纬度：latitude($min = -90, $max = 90)     // 77.147489
经度：longitude($min = -180, $max = 180)  // 86.211205
```

电话号码:
```
电话号码：phoneNumber             // '201-886-0269 x3767'
免费电话号码：tollFreePhoneNumber     // '(888) 937-7238'
E164电话号码：e164PhoneNumber     // '+27113456789'
```

文本内容:
```
文本内容：realText($maxNbChars = 200, $indexSize = 2)
```

时间:
```
unixTime($max = 'now')                // 58781813
dateTime($max = 'now', $timezone = null) // DateTime('2008-04-25 08:37:17', 'UTC')
dateTimeAD($max = 'now', $timezone = null) // DateTime('1800-04-29 20:38:49', 'Europe/Paris')
iso8601($max = 'now')                 // '1978-12-09T10:10:29+0000'
date($format = 'Y-m-d', $max = 'now') // '1979-06-09'
time($format = 'H:i:s', $max = 'now') // '20:49:42'
dateTimeBetween($startDate = '-30 years', $endDate = 'now', $timezone = null) // DateTime('2003-03-15 02:00:49', 'Africa/Lagos')
dateTimeInInterval($startDate = '-30 years', $interval = '+ 5 days', $timezone = null) // DateTime('2003-03-15 02:00:49', 'Antartica/Vostok')
dateTimeThisCentury($max = 'now', $timezone = null)     // DateTime('1915-05-30 19:28:21', 'UTC')
dateTimeThisDecade($max = 'now', $timezone = null)      // DateTime('2007-05-29 22:30:48', 'Europe/Paris')
dateTimeThisYear($max = 'now', $timezone = null)        // DateTime('2011-02-27 20:52:14', 'Africa/Lagos')
dateTimeThisMonth($max = 'now', $timezone = null)       // DateTime('2011-10-23 13:46:23', 'Antarctica/Vostok')
amPm($max = 'now')                    // 'pm'
dayOfMonth($max = 'now')              // '04'
dayOfWeek($max = 'now')               // 'Friday'
month($max = 'now')                   // '06'
monthName($max = 'now')               // 'January'
year($max = 'now')                    // '1993'
century                               // 'VI'
timezone                              // 'Europe/Paris'
```

互联网:
```
邮箱：email                   // 'tkshlerin@collins.com'
安全邮箱：safeEmail               // 'king.alford@example.org'
免费邮箱：freeEmail               // 'bradley72@gmail.com'
公司邮箱：companyEmail            // 'russel.durward@mcdermott.org'
免费邮箱域名：freeEmailDomain         // 'yahoo.com'
安全邮箱域名：safeEmailDomain         // 'example.org'
用户名：userName                // 'wade55'
密码：password                // 'k&|X+a45*2['
域名：domainName              // 'wolffdeckow.net'
域名名称：domainWord              // 'feeney'
tld                     // 'biz'
连接地址：url                     // 'http://www.skilesdonnelly.biz/aut-accusantium-ut-architecto-sit-et.html'
口号：slug                    // 'aut-repellat-commodi-vel-itaque-nihil-id-saepe-nostrum'
iPv4地址：ipv4                    // '109.133.32.252'
本地的ipv4地址：localIpv4               // '10.242.58.8'
ipv6地址：ipv6                    // '8e65:933d:22ee:a232:f1c1:2741:1f10:117c'
MAC地址：macAddress              // '43:85:B7:08:10:CA'
```

用户代理:
```
用户代理：userAgent              // 'Mozilla/5.0 (Windows CE) AppleWebKit/5350 (KHTML, like Gecko) Chrome/13.0.888.0 Safari/5350'
谷歌：chrome                 // 'Mozilla/5.0 (Macintosh; PPC Mac OS X 10_6_5) AppleWebKit/5312 (KHTML, like Gecko) Chrome/14.0.894.0 Safari/5312'
火狐：firefox                // 'Mozilla/5.0 (X11; Linuxi686; rv:7.0) Gecko/20101231 Firefox/3.6'
safari：safari                 // 'Mozilla/5.0 (Macintosh; U; PPC Mac OS X 10_7_1 rv:3.0; en-US) AppleWebKit/534.11.3 (KHTML, like Gecko) Version/4.0 Safari/534.11.3'
opera：opera                  // 'Opera/8.25
```