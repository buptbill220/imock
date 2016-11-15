# д��ǰ�� #
���ڲ��Ե�mock����

����Ҫ�κεĴ��뿪����ֻ�Ǽ����򵥵������ļ�������ʵ��mock�����Ĵ�Ͳ������ݵ�׼����

����Э����棺֧��http/https��֧����չ���Զ��崫��Э��(����arpc��)

���ݸ�ʽ���棺֧���Զ�������ݸ�ʽ������json/protobuf/kv/�����Զ����ʽ��

������棺֧��client/server

# ���� #

```bash
$ git clone https://github.com/hqin6/imock.git
$ cd imock/rpm
$ ./imock-build.sh
$ rpm -Uvh imock-*.rpm
```

# ����˵�� #
imock�Ľṹ�ܼ򵥣��κ�һ��imock��ɫ��������server����client�������Ĳ�����ɣ�

* ��ִ�г���
* config�������ļ�
* fmt.xmlӦ�����ݸ�ʽ�����ļ�
* dat.xmlӦ����������

���У���ʹ��ʱ���û�ֻ��Ҫ��ע���������ļ����ɡ���һ�����ã�����xml��

## ��ִ���ļ� ##

��ִ���ļ�����������һ����imock-client��һ����imock-server����Ϊc++����������Ӷ��ɵĶ������ļ���

### imock-server ###
```bash
$ imock-server -h 
Usage: imock-server [OPTION] 

  -c <config file>  default: /home/a/imock/conf/server/imock-server.conf
  -s <start|stop>   default: start

Examples:
  imock-server -s start
  imock-server -c imock-server.conf -s start
```
imock-server�Ѿ����������ӵ�`/usr/local/bin`Ŀ¼�¡�����Ҫ�����ִ�г����ȫ·����

�����в���˵����

* `-c <config file>` : ָ��ʹ�õ��������ļ���Ĭ��ֵ��`/home/a/imock/conf/server/imock-server.conf`
* `-s <start | stop>`: ָ���������ͣ����� | ֹͣ��Ĭ��ֵ��`start`

Ϊ�˷����ڲ���ʱ��������ķ����࣬�Ƽ�ʹ��Ĭ�ϲ��������磬�������ֻ��Ҫ`sudo imock-server`��ֹͣ���ֻ��Ҫ`sudo imock-server -s stop`

### imock-client ###
```bash
$ imock-client -h
imock-client: invalid option -- h

Usage: imock-client [OPTION]
Send query to server and get answer from server

  -a <area name>      the area will be used in config file.
  -c <config file>    default:/home/a/imock/conf/client/imock-client.conf
  -n <send num>       the number of sending all query for a worker.
  -s <send seconds>   the seconds for client workers run.
  -w <workers>        the number of client workers.
  -l <log level>      crit, error, warn, notice, info, debug. default:info
  -p <msec>           pause milliseconds intervals
  -I <qa id>          the qa id which need send
  -i <q id>           the q id which need send in qa

Examples:
  imock-client -c imock-client.conf -a xxx 
  imock-client -c imock-client.conf -a xxx -w 8
```
imock-client�Ѿ����������ӵ�/usr/local/binĿ¼�¡�����Ҫ�����ִ�г����ȫ·����

�����в���˵����

* `-a <area name>` : ָ����Ҫ������ģ���ɫ������������
* `-c <config file>` : ָ��ʹ�õ������ļ���Ĭ��ֵ��`/home/a/imock/conf/client/imock-client.conf`
* `-n <send num>` : ��ÿ��worker���̣���Ҫ�ظ����͵Ĵ�����Ĭ��ֵ��1��
__ע��__����ָ��������(dat.xml)��ͷ��β��һ����һ�Ρ����ָ��`-n 4`����dat.xml��ͷ��β�ظ�����4��
* `-s <send second>` : ָ�����͵���������`-s`ָ��ʱ��`-n`����Ч��ע�⣺ÿ��ָ��������(dat.xml)��ͷ��β��һ�����ж�ʱ�䣬���Բ���`-s`ָ�����٣����͵ı����϶�������
* `-w <workers>` :	����worker�Ľ�������Ĭ��ֵ��1��ע�⣺��ָ����ֵ����Ḳ�������ļ��е�workers����ֵ��������/ѹ������ʱ��ͨ����ѡ���ܷܺ���ĵĵ���������
* `-l <log level>` :	ָ����־���𡣿���ֵ��crit, error, warn, notice, info, debug��Ĭ��ֵ��info
* `-p <msec>` :	ָ��ÿ���������͵�ʱ��������λ�����롣Ĭ��ֵ��0
* `-I <qa ID>` :	ָ��Ҫ���͵�qa����Ӧ��debugID�ţ�����`<qa>`�ڵ��id����ֵ��������ж��qa�ڵ������ͬ��debugIDֵ���򶼻���з��͡������ָ������ᰴ˳�������qa�ڵ㷢�͡�
* `-i <q ID>` :	ָ��Ҫ���͵�q����Ӧ��debugID�ţ�����`<q>`�ڵ��id����ֵ��������ж��q�ڵ������ͬ��debugIDֵ���򶼻���з��͡������ָ������ᰴ�ո��ʷ��͡�

�������������`sudo imock-client -a mock1`

ֹͣ���`ctrl+c`����Ϊimock-client������Daemon�ķ�ʽ���У������Ǽ���ͣ�ķ�ʽ��

## config�����ļ� ##
���ļ���Ҫ����imock�ķ�����ص���Ϣ��client��server���ֽ�ɫ�����÷�ʽ�����ݻ���һ�¡�Ϊ�������������Ծɷֿ�˵����

### ��������һ��/��� mock server
```bash
#��ѡ��������Ҫ������mockģ�飬���mockģ��ʹ�ö��ŷָ�
#�����mockģ��ÿһ�����������ҵ���Ӧ�������򣬼���������������ã�
#����Ҫ���������ж�ȡ��[mock1] [mock2]����������
#������κ�һ����ȡ������������imock-serverʧ��
mocks = mock1, mock2
#ϵͳ��־�ļ������ʽΪ���ļ��� ��־����(file [debug|info|warn|error])
#��־�����ѡ��,�����ã���Ĭ����־������info
log = /home/a/imock/logs/imock-server.log debug
#���̼�¼master����id�ŵ��ļ�
#��ѡ��Ĭ��ֵ: /tmp/imock-server.pid
pid_file = /home/a/imock/bin/imock-server.pid
#########���Ͼ��Ǳ������ļ���ȫ��������#########

#########�����Ǳ������ļ��ĸ���mockģ���������#########
#mockģ������������ֱ��д���������ļ��Ҳ������дһ���ļ���ͨ��include����
#ָ������������������չʾ���������÷�ʽ������mock1��ֱ��д���������У�mock2
#��ͨ��include�ķ�ʽ�������������С�
#�Ƽ�ʹ��include�ķ�ʽ�����������ö��mock��ɫʱ�������໥���š�
#includeָ�����������ȫ����������棬�Ƽ��ŵ��ļ����

#������mock1�Ľ�ɫ�����á�
#ע�⣬ÿ����ɫ��һ����������[]��������������д�����������
#���������mocks���������õ�����һ�¡�
#���⣬����������򣬵���û����mocksָ�����������򲻻�����������������Ӧ��mock��ɫ
[mock1]
#��������Ľ�����
#��ѡ��Ĭ��ֵ: 1
workers = 1
#��������Ӧ�����ݸ�ʽ��xml�ļ�
format = /home/a/imock/server/data/mock1.fmt.xml
#��������Ӧ���������ݵ�xml�ļ�
data = /home/a/imock/server/data/mock1.dat.xml
#server���յ���ԭʼmessageд���ļ�
#��ʽΪ file mode
#����mode֧�֣�w w+ a a+ �ȷ�ʽ�� �ɲ����ã�Ĭ��Ϊw
#ͨ����file����Ϊoff���ɹر�message�ļ�¼����
#��ѡ��Ĭ��ֵ: off w
message = /home/a/imock/logs/mock1.server.message.txt
#�Ƿ������ݻ��� (on|off)
#�û���ֻ���data������ָ����dat.xml��Ч����������������ݻ��棬��ÿ������
#���񶼻��Ӳ�����¼���data������ָ����dat.xml�ļ��������ڲ���ʱ�滻�������ݶ���
#����imock����ʵ�����ݼ�ʱ���¼�ʱ��Ч�������format������ָ����fmt.xml����
#�����޸ģ�����Ҫ����imock���������Ч��
#��ѡ��Ĭ��ֵ: off
cache = on
#��־���壬��������ã���area��̳�ȫ�ֵ�log���ã�����ᣨ�ڱ�area������ȫ�ֵ�log����
log = /tmp/mock1.log debug
#����ʹ��Э�� (http|https)
protocol = http
#�������ã���Բ�ͬ�ķ���ʹ��Э��(protocol)�������죺
#------���http
#http������Ҫ�����Ķ˿ں�
port = 8080
#------���https
#https������Ҫ�����Ķ˿ں�
port = 443
ssl_cert = certificate-chain.pem.txt
ssl_cert_key = private-key.pem.txt
#
######### mock1�����������������ͨ��include��ʽ����mock2������ #########
# includeָ�����д���������ļ���ȫ������֮ǰ���Ƽ�д���ļ����
# ֧��������ʽ�����磺
# include /home/a/imock/conf/server/*.conf
# include /home/a/imock/conf/*/*.conf
# ÿ�������ļ�������һ�������������򣬸�ʽΪ��
#          [��������]
#          ������ = ����ֵ
include /home/a/imock/conf/server/mock2.conf
```
### ��������һ��/��� mock client
��server�����ò�ͬ��client��������û��ȫ�������ֱ�Ӿ���ÿ����ɫ��Ӧ�����������£�

```bash
#########�����Ǳ������ļ��ĸ���mockģ���������#########
#mockģ������������ֱ��д���������ļ��Ҳ������дһ���ļ���ͨ��include����
#ָ������������������չʾ���������÷�ʽ������mock1��ֱ��д���������У�mock2
#��ͨ��include�ķ�ʽ�������������С�
#�Ƽ�ʹ��include�ķ�ʽ�����������ö��mock��ɫʱ�������໥���š�

#������mock1�Ľ�ɫ�����á�
#ע�⣬ÿ����ɫ��һ����������[]��������������д�����������
[mock1]
#��������Ľ�����
#��ѡ��Ĭ��ֵ: 1
workers = 1
#��������Ӧ�����ݸ�ʽ��xml�ļ�
format = /home/a/imock/client/data/mock1.fmt.xml
#��������Ӧ���������ݵ�xml�ļ�
data = /home/a/imock/client/data/mock1.dat.xml
#��־���壬��������ã����������ն�
log = /tmp/mock1.log debug
#client���յ���ԭʼmessageд���ļ�
#��ʽΪ file mode
#����mode֧�֣�w w+ a a+ �ȷ�ʽ�� �ɲ����ã�Ĭ��Ϊw
#ͨ����file����Ϊoff���ɹر�message�ļ�¼����
#��ѡ��Ĭ��ֵ: off w
message = /home/a/imock/logs/mock1.client.message.txt
#���͵ĳ�ʱʱ�䣬������Ӧ��ĳ�ʱʱ�䣬��λ����
#��ѡ��Ĭ��ֵ: 5000
timeout = 5000
#����ʹ��Э�� (http|https)
protocol = http
#�������ã���Բ�ͬ�ķ���ʹ��Э��(protocol)�������죺
#------���http
#http/https������Ҫ����ĵ�ַ
#���Դ��в������߲�������
url = localhost:8080/test?a=1&b=2
#------���http
#http/https�����ܽ��յ���Ӧ���ȣ���λ�ֽڣ��ɲ��Ĭ��ֵ��20480�ֽ�
resp_max_len = 20480

######### mock1�����������������ͨ��include��ʽ����mock2������ #########
# includeָ�֧��������ʽ�����磺
# include /home/a/imock/conf/client/*.conf
# include /home/a/imock/conf/*/*.conf
# ÿ�������ļ�������һ�������������򣬸�ʽΪ��
#          [��������]
#          ������ = ����ֵ
include /home/a/imock/conf/client/mock2.conf
```

## Ӧ�����ݸ�ʽfmt.xml
�����������ļ����format������ָ�����ļ���

fmt.xml�Ǳ�׼��xml��ʽ������ָ��Ӧ�����ݵĸ�ʽ�������л�(serialize)�ͷ����л�(parse)�����ݡ�

fmt.xml��`<fmt>`Ϊ���ڵ㣬�������`<q>`�Ͷ��`<a>`�ڵ㡣����һ��fmt.xml�ļ�֧�ֶ��ָ�ʽ��query�Ͷ��ָ�ʽ��answer������

```xml
<fmt>
    <q fid='q1'>...</q>
    <a fid='a1'>...</a>
    <a fid='a2'>...</a>
    <q fid='q2'>...</q>
</fmt>
```

* q�ڵ㣬��query�ڵ㡣����imock-server��˵����server������յ�����������Ӧ�����ݸ�ʽ������imock-client��˵����client�����ͳ�ȥ����������Ӧ�����ݸ�ʽ��
* a�ڵ㣬��answer�ڵ㡣����imock-server��˵����server����Ӧ�����������Ӧ�����ݸ�ʽ������imock-client��˵����client������յ�����������Ӧ�����ݸ�ʽ��

fmt��q/a�ڵ��fid���ԣ���Ϊ�����ֶ��q/a�ڵ㡣dat.xml�е����ݣ�Ҳ��ͨ�������Ժ�fmt.xml�е�q/a�ڵ��Ӧ�����ġ�fmt.xml�е�����q�ڵ㣬��`fid`��ֵ�����ظ���ͬ������a�ڵ��`fid`ֵҲ�����ظ�����Ȼ��q�ڵ��a�ڵ��`fid`ֵ������ͬ����ֻ��һ��q/a�ڵ�ʱ�����Բ�����`fid`���ԣ�Ҳ�Ƽ���ô����������������`fid`����ʱ��Ĭ��`fid`��ֵΪ�մ������µ������ǺϷ��ģ�

```xml
<fmt>
    <q>...</q>
    <a>...</a>
    <a fid='a2'>...</a>
    <q fid='q2'>...</q>
</fmt>
```
���е�q/a�ڵ㣬˳��������⡣�����ڵ�����ƣ�ȫΪ�û��Զ��塣

imock-client/ imock-server��fmt.xml������Ҫ�����һ�¡�Ϊ��˵�������������Ծɷֿ�������

### ������imock-server
q/a�ڵ���������ƣ�˵�����£�

#### q�ڵ�
imock-server��fmt.xml�������q�ڵ������ˣ���Ϊserver��Ӧ����ν������յ����ַ������ݡ����ݲ�ͬ�ĸ�ʽ���в�ͬ�Ľڵ����͡�

##### ��ͨ���ͽڵ�
������Ҫ��������Ľڵ㡣���磺

```xml
// ���յ����ַ���������һ��ad
// �÷ֺŷָ��һ��Ԫ����img_path���ڶ���Ԫ����click_url
<q>
    <ad sub_def_split=';'>
        <img_path/>
        <click_url/>
    </ad>
</q>
// ������յ����ַ�����http://img.path;http://click.url
// ��ô����������ǣ�
<q>
    <ad>
        <img_path>http://img.path</img_path>
        <click_url>http://click.url</click_url>
    </ad>
</q>
```
������ܸ����ͽڵ������õ����ԣ�

---

* `sub_def_split=';'`

�ڵ���ڲ��ӽڵ�Ĭ�Ϸָ��Ϊ�ֺš�����ķָ����������ڵ����ַ��������Ƕ���ַ���ɵ��ַ�����

---

* `split=','`	

���ڵ�ķָ����Ƕ��š�����ķָ����������ڵ����ַ�������ʹ����ַ���ɵ��ַ��������⣬��������˸�ֵ����ýڵ�ĸ��ڵ������õ�`sub_def_split`���ڱ��ڵ�Ľ����б����ǡ�����

```xml
<ad sub_def_split=';'>
	<title split=','/>
	<img_path/>
	<click_url/>
</ad>
```
���ڽ��зָ�ʱ��title�ǰ��ն������ָ������Ƿֺš�������յ����ַ����ǣ�`Ůװ,img;click`
��ô��������fmt���������Ľ���ǣ�

```xml
<ad>
	<title>Ůװ</title>
	<img_path>img</img_path>
	<click_url>click</click_url>
</ad>
```

��������Ҫ����ĳһ�����߼����ڵ�ķָ�������������

---

* `repeated_split='|'`

��Ǳ��ڵ���һ��repeated�ڵ㣬����ֵ�ڵ㡣�ظ����ֶ�֮��ʹ�����߷ָ�������ķָ����������ڵ����ַ�������ʹ�ö���ַ���ɵ��ַ��������磺

```xml
<ad sub_def_split=';' repeated_split='|'>
	<img_path/>
	<click_url/>
</ad>
```

���ʾ���ad�ֶ���һ���ظ��ֶΡ�������յ����ַ����ǣ�
`img1;click1|img2;click2`
��ô��������fmt���������Ľ���ǣ�

```xml
<ad>
	<img_path>img1</img_path>
	<click_url>click1</click_url>
</ad>
<ad>
	<img_path>img2</img_path>
	<click_url>click2</click_url>
</ad>
```

ע�⣬�����Ե�ֵ����Ϊ�գ������ã�

```xml
<msg repeated_split=''>
    <size split=',' var='$len'/>
    <body length='$len'/>
</msg>
```

��ʾmsg�Ƕ�ֵ���ԣ��ظ��ֶΣ�������û�зָ�����

---

* `var='$varname'`

��ǽ����ڵ��ֵ��ֵ������varname����������������`$`��ͷ��
��������Ҫ����imock-server����Ҫ��ȡ�������ĳ���ֶβ���Ҫʹ����ֵ�����磺imock-server���յ������󴮰���һ���Ựid�ֶΣ���Ӧ���ʱ����Ҫ���ظ��ֶΣ����ֶ��޷�Ԥ֪��ÿ�ζ���һ���������ʱ����صģ���������Ҫ�������еĸ��ֶζ���Ϊ������Ȼ����Ӧ������д�����ã����ֶΡ����磺

```xml
<session_id var='$sid'></session_id>
```

���ǽ�����������session_id�ֶε�ֵ��ֵ������sid

ע�⣺����repeated�ֶΣ�������ø����ԣ������ֵ�����������һ������������ֵ�����磺����ֶ�A��123��456����ֵ�����ֶ�A������var���ԣ���var������ֵ������456���������������Ǹ�����

---

* `length='4'`	

�ڽ���ʱ�����ó��ȵ��ַ�����ֵ�����ڵ㡣���磺

```xml
<msg>
	<type length='4'/>
	<body/>
</msg>
```

��������յ����ַ����ǣ�exchhello����ô��������fmt���������Ľ���ǣ�

```xml
<msg>
	<type>exch</type>
	<body>hello</body>
</msg>
```

ע�⣬����length���Ե�ֵ������һ��������

Ӧ�ó�������������
�������ö��ŷָ�����һ���ֶα�ʾbody�ĳ��ȣ��ڶ����ֶ���body�����ݣ��������ֶ��Ƕ�ֵ���ԣ����£�

```xml
<msg repeated_split=''>
	<len split=',' var='$l'/>
	<body length='$l'/>
</msg>
```
---

* `type='[type]'`

type��ȡֵ�����ǣ�������`|`�ָ����ʹ�ã���

`INT`�������ַ���ֱ�Ӱ���INT��ȡ�����磺���ڶ������ַ�����ע��ת���ַ���`��\x31\x0\x0\x0abcd����`������INT��ȡ������49�����ڽ�����ʱ��Ὣ�̶���ǰ4���ֽ���Ϊһ��int��ȡ�����ó��������������ַ����ǡ�����+���ݡ����ҳ�����һ�������Ƶ�int���̶�����4���ֽڣ���

`JARR`��ֻ���json�ڵ���Ч����ʾ���ڵ��Ǹ�array�ڵ㡣��Ϊ����json�Ĭ�϶��ڵ�ֵ�ڵ������ͨ��json�ڵ㣬���ڵ�ֵ��json����(array)�ڵ㣬��Ҫ���ø����ԡ������Ҫ���ÿ����飬��`��key��:[]`,����ʹ��fmt:`<key type='JARR'/>`; dat:`<key>null</key>`

`JLEAF`��ֻ���json�ڵ���Ч����ʾ���ڵ��Ǹ�Ҷ�ӽڵ㡣���Խڵ�������Ƕ��ʽ�ڵ�ʱ����Ҫ���ø����ԡ����磬ĳ��Json�ڵ���ӽڵ���һ��kv��ʽ�����ݡ�������Ҷ�ӽڵ㣬��������ʱ������ʹ��`type='JARR|JLEAF'`

---

* `from='[where]'`	

��Ǳ��ֶε�ֵ���Ķ���ȡ��where��ȡֵ�����ǣ�

`HTTP_METHOD`:HTTP�����󷽷�������GET/POST��

`HTTP_URI_PATH`:HTTP������uri����������http://www.imock.xx/fk?id=1, ��uri�ǡ�/fk��

`HTTP_URI_QUERY`:HTTP������query����������http://www.imock.xx/fk?id=1, ��query�ǡ�id=1��

`HTTP_HEAD`:HTTPͷ�����ݣ���HTTP��ͷ��key��value���ݣ����磺Cookie:cna=xxx\r\nUser-Agent:xxx

`NULL`:��Դ�ڿգ������shellʹ�á����磬���ڶ���һ���ڵ㣬�ýڵ���������ʱ��������ýڵ�ֵ����Դ���κεط���ֻ���ڲ���shell������
`<pvtime var='$pvtime' op='shell' shell_cmd='/tmp/a.sh' from='NULL'/>`

`BODY`:Ĭ��ֵ��������body������HTTP��GET��������Ϊ�գ�POST��������HTTP��body��������HTTP��Э�飬������������

`ARPC_METHOD`:arpc�����󷽷�����method���֡���Ҫ������һ��service������ͬrequest��response���Ͳ�ͬmethod����������磺һ��service����query��update���ַ�����������request��response������һ�£����綼��message Person������������£�����Ҫ���ֲ�ͬ��method��ָ��dat.xml����������л�����Ϊfmt.xml��dat.xml��ֻ����Ϣ���͵�����������method��Ӧ����Ϣ����һ�£�������Ҫ��method�����֣���

���϶��ֵ����ʹ�����߷ָ���磺��Ҫͬʱ��Ӧ`GET&POST`�������󴮿�����GET�Ĳ�������POST�Ĳ�������body�У�����ô������ô���ã�

```xml
<args fmt='k=v' kv_repeated_split='&#x26;' from='HTTP_URI_QUERY|BODY'>
</args>
```
---

* `op='[operate]'`	

����ڼ�������ƥ��֮ǰ�����л����ݺ󣬶Ա��ֶν��к��ֲ�����Ŀǰ֧�֣�

`nocvt`:Ŀǰֻ���json�ڵ���Ч����������ø����ԣ�Ĭ�Ϸ�ʽ�����������Զ�����������ַ���"null"ת��Ϊ`null`�ڵ㣬��ȫ����ת��Ϊ`int`������+С����ת��Ϊ`float`��`true/false`ת��Ϊ`bool`���͵ȡ������л�ʱ��Ч��

`b64enc/b64enc_safe/b64enc_noappend/b64enc_safe_noappend`:���ַ�����base64���룬����\_safe��ʾurl��ȫ��base64���룬\_noappend��ʾ��׷��=��

`b64dec/b64dec_safe/b64dec_noappend/b64dec_safe_noappend`:���ַ�����base64���룬����\_safe��ʾurl��ȫ��base64���룬\_noappend��ʾ��׷��=��

`urlenc`:���ַ�������urlencode

`urldec`:���ַ�������urldecode
���ó�������������HTTP��GET���󣬾���һ��u���������ƣ�
`http://xxx.com/q?i=1&u=http%3A%2F%2Fxx.com%2Fa%3D1%26b%3D2`
���������Ҫ��u���н�һ������������Ҫ��u����urldecode

`trim`���Ա��ڵ��ֵ����trimȥ�ո���

`rtrim`���Ա��ڵ��ֵ����rtrimȥ�ҿո���

`ltrim`���Ա��ڵ��ֵ����ltrimȥ��ո���

`gzip`���Ա��ڵ��ֵ����gzipѹ������

`gunzip`���Ա��ڵ��ֵ����gunzip��ѹ������

`zip`���Ա��ڵ��ֵ����zipѹ������

`unzip`���Ա��ڵ��ֵ����unzip��ѹ������

`esc`���Ա��ڵ��ֵ����ת�崦�������\x(ʮ������)��\(�˽���)����ת�塣����������strace��ȡ��ת������ݽ�����

`shell`���Ա��ڵ��ֵ����shell���ô���

`head`�����`shell`����ʹ�ã���ʾ�Ƿ���Ҫ����head���ű���������ã�����ִ��shellʱ���Ὣ�洢��head���ݵ��ļ������ݸ�shell�ű�����`<n op='shell, head' shell_cmd='./a.sh args1'></n>`����ʵ�ʵ���a.shʱ������`./a.sh arg1 head_file`��

`body`�����`shell`����ʹ�ã���ʾ�Ƿ���Ҫ����body���ű���������ã�����ִ��shellʱ���Ὣ�洢��body���ݵ��ļ������ݸ�shell�ű�����`<n op='shell, head, body' shell_cmd='./a.sh args1'></n>`����ʵ�ʵ���a.shʱ������`./a.sh arg1 head_file body_file`��ע�⣬�������ͬʱָ��head��body�����̶�����head/body��˳�򴫵ݲ�����������op����ֵ���˳���޹ء�

`nofile`�����shell����ʹ�ã���ָ��������ʱ�����ݸ�shell_cmd�Ĳ��������������ļ���������ʵ�ʲ���ֵ����shell�ű����ֱ�ӻ�ȡ������ͨ�����ļ���ע�⣺����������ж��������ݣ�������`��\0��`�����������ø����ԣ�����ᵼ�¶�ȡ�Ĳ�����ȫ��

`replacevar`���滻����ֵ�����ָ������Խڵ�ֵ����`$`��ʼ�ı��������滻�������`${abc}`����`$abc`�����滻��

`replaceshvar`�����`shell`����ʹ�á��滻����ֵ�����ָ�������`shell_cmd`����`$`��ʼ�ı��������滻�������`${abc}`����`$abc`�����滻��

`rvalue`�����shell����ʹ�ã���ʾ�Ƿ���Ҫ���ݱ��ֶ�ֵ���ű���������ã�����ִ��shellʱ���Ὣ�洢�б��ֶ����ݵ��ļ������ݸ�shell�ű�����`<n op='shell, rvalue, head, body' shell_cmd='./a.sh args1'></n>`����ʵ�ʵ���a.shʱ������`./a.sh arg1 rvalue_file head_file body_file`��ע�⣬�������ͬʱָ��head/body/rvalue�����̶�����rvalue/head/body��˳�򴫵ݲ�����������op����ֵ���˳���޹ء�

`cached`�����shell����ʹ�á�����shellִ�еĽ��������ʹ��shell_cmdΪkey��

---

* `shell_cmd='[cmd]'`

��ָ��`op='shell'`ʱ��Ч�����Ա�ʾ��Ҫ���õ�shell�������д�����������`op='shell,replaceshvar' shell_cmd='a.sh $myvar'`��



##### protobuf��ʽ�Ľڵ�

��������pb���н��������ݽڵ㡣ͨ��`fmt='pb'`��ʾ�����ڼ̳�����ͨ�ڵ㣬������ͨ�ڵ���������Ծ�������pb�ڵ㡣pb�ڵ����Լ��µ��������ã����£�

---

* `message='[name]'`

��pb�ڵ�����Ӧ��pb message����xx.proto�ﶨ���message���֡�ע�⣬��������ֿռ䣬����Ҫдȫ�������磺xx.proto�������£�

```proto
package proto.xx;
message Request {��}
```
��ô��Ҫ��ô���ã�
`<mypbnode message='proto.xx.Request' ��/>`

---

* `file='filename'`	

��pb�ڵ�����Ӧ��protobuf file��������message�Ķ�����xx.proto�ļ������Ҫ�������£�

```proto
<pb message='proto.xx.Request' file='xx.proto'��/>
```

ע�⣬file����ֵ����Ϊ�ļ���������·���������`inc`���ԣ�����Ϊ��·�����ļ���

---

* `inc='path'`

��������Щ·���²��ұ��ڵ����漰��pb file��������xx.proto�ļ�����/tmp/protoĿ¼�£�����Ҫ���壺

```proto
<pb message='proto.xx.Request' file='/tmp/proto/xx.proto' fmt='pb'/>
```
����

```proto
<pb message='proto.xx.Request' file='xx.proto' inc='/tmp/proto' fmt='pb'/>
```
�����������³�����Ҫ�õ�����pb file��ʹ��import�����ⲿpb�ļ�ʱ������xx.proto�������£�����desc.protoλ��/home/a/pbfile/desc.proto����

```proto
import "pbfile/desc.proto"
package proto.xx;
message Request {��}
```

����Ҫ���壺

```proto
<pb message='proto.xx.Request' file='xx.proto' inc='/tmp/proto:/home/a' fmt='pb'/>
```
����

```proto
<pb message='proto.xx.Request' fmt='pb' file='/tmp/proto/xx.proto' inc='/home/a'/>
```

��import��������Ӧ���ļ�����file��������Ӧ��Ŀ¼���ҵ�������Ҫ����inc���ԡ����������������е�desc.protoλ��/tmp/proto/pbfile/desc.protoʱ������Ҫ������inc���ԣ������������£�

```proto
<pb message='proto.xx.Request' file='/tmp/proto/xx.proto' fmt='pb'/>
```
����

```proto
<pb message='proto.xx.Request' file='xx.proto' inc='/tmp/proto' fmt='pb'/>
```

�ļ��������򣺰������õ�·���Ⱥ�˳����в��ң��ҵ���ֹͣ�������²��ҡ�

_ע��_��inc�Ѿ�Ĭ����������������·���������ң���`/home/a/imock/proto` �� `/home/a/imock/dev/proto`
���齫�õ���pb����`/home/a/imock/proto`Ŀ¼�£��Ϳ��Բ����ٴ�����·����`/home/a/imock/dev/proto`������ʹ�ã�imock�ڲ�ʹ��Ŀ¼����

_ע��_��pb�ڵ㱾�������Ժ������Ҫ��pb������κ��ֶν������ã���ʹ�ø��ֶε�������Ϊ�ڵ������ɡ��磺

```xml
// xx.proto�������£�
// package test
// message Request {  
//    optional string id = 1;
//    message MSG {
//        optional bytes head = 1;
//        optional bytes body = 1;
//    }
//    optional MSG msg = 2;
// }
// ��ô���ǿ�����ô���ã�
<q>
    <pb fmt='pb' message='test.Request' file='xx.proto'>
        <id var='$id'/>
        <msg>
        		<body repeated_split=';' sub_def_split=','>
                <title/><click/><img/>
				</body>
        </msg>
    </pb>
</q>
// �������ã�����ȡ��һ������ʱ���Ὣ��ʹ��test.Request���н��������������õ�
// ��pb���id�ֶ�ֵ��ֵ������$id��Ȼ�󽫽�һ������msg�ֶ����body�ֶΣ�body
// �ֶ��ֻ���Ϊһ����ͨ�ڵ����������title/click/img����
// ע�⣺���и�ʽ�Ľڵ㶼��Ƕ�������κθ�ʽ�Ľڵ㡣
// ���磬����Խ�������body�ֶμ�������Ϊһ��pb�ڵ㣬
// ���߽�id����Ϊһ����ͨ�ڵ�ȵȡ�

// �����pb������ֶ�û����������Ľ���Ҫ����ô�������ÿ���Ϊ��
<q>
    <pb fmt='pb' message='test.Request' file='xx.proto'/>
</q>
```
##### json��ʽ�Ľڵ�
��������json���н��������ݽڵ㡣ͨ��`fmt='json'`��ʾ�����ڼ̳�����ͨ�ڵ㣬������ͨ�ڵ���������Ծ�������json�ڵ㡣��pb����ͨ�ڵ㲻ͬ��json�ڵ�������ֶζ�������ʱ���ܻ�ȡ�����ý�Ϊ�򵥣�

```xml
<q>
	<msg fmt='json'>
        <!--�����������json������ӽڵ�-->
        <title var='$tt'/>
	</msg>
</q>
// �ڽ�������ʱ���ᰴ��json�ĸ�ʽ����msg�ڵ㡣�����msg�ڵ��������ýڵ㣬
// �����������������������ã���json���������Ժ������title�ֶΣ���Ὣ
// ���ֶε�ֵ��ֵ��$tt���������û��title�ֶΣ���ôtitle�ֶξ�Ϊnull

// ע�⣺���и�ʽ�Ľڵ㶼��Ƕ�������κθ�ʽ�Ľڵ㡣
// ���ԣ�������msg�ڵ�����������ӽڵ㣬�ӽڵ���ӽڵ�ȵȡ�
```

##### key/value��ʽ�Ľڵ�
��������kv���н��������ݽڵ㡣ͨ��`fmt='k?v'`��ʾ�����е�`?`��ʾkey��value�ķָ��������磬ʹ�õȺŷָ�ģ�����`fmt='k=v'`��ʹ��ð�ŷָ�ľ���`fmt='k:v'`������ָ����������ڵ����ַ��������Զ���`fmt='k::v'`������ʾkv��ͨ��`::`����ð�ŵ����ָ�ġ����ڼ̳�����ͨ�ڵ㣬������ͨ�ڵ���������Ծ�������kv�ڵ㡣��json�ڵ����ƣ�kv�ڵ�������ֶζ�������ʱ���ܻ�ȡ����֧�ֵ��������£�

---

* `kv_repeated_split=';'`

��kv�ڵ������key/value��֮��ķָ��������磺�����ַ���`a=1;b=2;c=3`����ô��Ҫ��ô���ã�

```xml
<mykvnode kv_repeated_split=';' fmt='k=v' ��/>
```

ע�⣺���ͬʱ�����˸����Ժ�`repeated_split`�����磺

```xml
<n kv_repeated_split=';' fmt='k=v' repeated_split='|' ��/>
```
��������ǣ�`a=1;b=2|a=2;b=3`����ô�ᱻ����Ϊ��

```xml
<n>
	<a>1</a>
	<b>2</b>
</n>
<n>
	<a>2</a>
	<b>3</b>
</n>
```

---

kv�ڵ�����ý�Ϊ�򵥣����磺

```xml
<msg fmt=��k=v' kv_repeated_split='&#x26;' from='HTTP_URI_QUERY'>
        <!--�����������kv������ӽڵ�-->
        <title var='$tt'/>
</msg>
// �ڽ�������ʱ���ᰴ��k=v�ĸ�ʽ����msg�ڵ㡣�����msg�ڵ��������ýڵ㣬
// �����������������������ã���kv���������Ժ������keyΪtitle���ֶΣ���
// �Ὣ���ֶε�ֵ��ֵ��$tt���������û��title�ֶΣ���ôtitle�ֶξ�Ϊnull

// ע�⣺���и�ʽ�Ľڵ㶼��Ƕ�������κθ�ʽ�Ľڵ㡣
// ���ԣ�������msg�ڵ�����������ӽڵ㣬�ӽڵ���ӽڵ�ȵȡ�
```

#### a�ڵ�
imock-server��fmt.xml�������a�ڵ������ˣ���Ϊserver��Ӧ��������л�dat.xml���a�ڵ㣬�����л���Ľ������ΪӦ�𷵻ظ�client�ˣ�����q�ڵ�һ����a�ڵ�Ҳ֧�ֶ��ָ�ʽ�Ľڵ㡣

##### ��ͨ���͵Ľڵ�
������Ҫ��������Ľڵ㡣֧�ֵ����Ժ�q�ڵ����һ�¡����£�

---

* `sub_def_split=';'` ����q�ڵ�һ��
* `split=','` ����q�ڵ�һ��
* `repeated_split='|'` ����q�ڵ�һ��

---

* `type='[type]'`	type��ȡֵ�����ǣ�������`|`�ָ����ʹ�ã���

`INT`�������ַ���ֱ�Ӱ���INT���л������磺�����ַ���49����ᱻ���л�Ϊ�������ַ�����ע��ת���ַ���`\x31\x0\x0\x0`�����ڽ�����ʱ��Ὣ�����ַ������л�Ϊ�̶���4���ֽ�int�����ó��������������ַ�����`����+����`���ҳ�����һ�������Ƶ�int���̶�����4���ֽڣ���

`JARR`��ֻ���json�ڵ���Ч����ʾ���ڵ��Ǹ�array�ڵ㡣��Ϊ����json�Ĭ�϶��ڵ�ֵ�ڵ������ͨ��json�ڵ㣬���ڵ�ֵ��json����(array)�ڵ㣬��Ҫ���ø����ԡ������Ҫ���ÿ����飬��`��key��:[]`,����ʹ��fmt:`<key type='JARR'/>`; dat:`<key>null</key>`

`JLEAF`��ֻ���json�ڵ���Ч����ʾ���ڵ��Ǹ�Ҷ�ӽڵ㡣���Խڵ�������Ƕ��ʽ�ڵ�ʱ����Ҫ���ø����ԡ����磬ĳ��Json�ڵ���ӽڵ���һ��kv��ʽ�����ݡ�������Ҷ�ӽڵ㣬��������ʱ������ʹ��`type='JARR|JLEAF'`

---

* `to='[where]'`	��Ǳ��ֶε�ֵ��Ҫд�뵽�Ķ���where��ȡֵ�����ǣ�

`HTTP_HEAD`:HTTPӦ��ͷ�����ݣ���HTTP��ͷ��key��value���ݣ����磺Location:http://www.imock.xx

`HTTP_VERSION_MINOR`:HTTP��Ӧ��汾��Ŀǰ֧�֡�0�����ߡ�1������1.0����1.1

`HTTP_CODE`:HTTPӦ���룬����302��404�ȡ�

`HTTP_CODE_MSG`:HTTPӦ�����Ӧ����Ϣ�����硱Not Found������404��Ӧ����Ϣ�������Բ����ã����Զ���ӣ�ͨ��HTTP_CODE��ȡ��׼��CODE_MSG����

`ARPC_FAILED_MSG`:ARPCӦ���ʧ����Ϣ��

---

##### protobuf��ʽ�Ľڵ�
��q�ڵ������һ�¡������ظ�˵����
##### json��ʽ�Ľڵ�
��q�ڵ������һ�¡������ظ�˵����
##### key/value��ʽ�Ľڵ�
��q�ڵ������һ�¡������ظ�˵����

### ������imock-client
q/a�ڵ���������ƣ�˵������

#### q�ڵ�
imock-client��fmt.xml�������q�ڵ������ˣ���Ϊclient��Ӧ��������л�dat.xml���q�ڵ㡣�����л���Ľ������ΪӦ�𷵻ظ�client�ˣ������ݲ�ͬ�ĸ�ʽ���в�ͬ�Ľڵ����͡�

##### ��ͨ���͵Ľڵ�
��imock-server��a�ڵ����ƣ������ǽ������л�����֧�ֵ��������£�

---

* `sub_def_split=';'`����imock-server��a�ڵ�һ��
* `split=','`����imock-server��a�ڵ�һ��
* `repeated_split='|'`	��imock-server��a�ڵ�һ��
* `type='[type]'`	��imock-server��a�ڵ�һ��

---

* `to='[where]'`	��Ǳ��ֶε�ֵ��Ҫд�뵽�Ķ���where��ȡֵ�����ǣ�

`HTTP_METHOD`��HTTP�����󷽷�������GET/POST��

`HTTP_URI_PATH`��HTTP������uri����������http://www.imock.xx/fk?id=1, ��uri�ǡ�/fk��

_ע��_��imock-client���͵�����url���������ɵģ�
`conf���url + HTTP_URI_PATH + HTTP_URI_QUERY`
�����conf(imock-client.conf)�����õ�url����;���uri����ôƴ�ӳ�����url�����Ǵ���Ľ�������ԣ������Ҫ�õ������ԣ���ô�Ͳ�����conf���url��uri�����磺
conf�����õ�url��:http://www.im.xx, ���õ�HTTP_URI_PATH�ǡ�/item������ô���յ�url���ǣ�
http://www.im.xx/item. ע�⣬���ﲻ�����м���κηָ�������������õ�HTTP_URI_PATH�ǡ�item������ô���յ�url���ǣ�http://www.im.xxitem. 

`HTTP_URI_QUERY`��HTTP������query����������http://www.imock.xx/item?id=1, ��query�ǡ�id=1��
ע�⣬imock-client���͵�����url�Ը����ԵĴ�����ֱ�ӽ����Ϊk=v��ģʽ׷�ӵ�url�����`?`��`&`������ж�conf���õ�url���Ƿ��У��������׷�ӣ�����׷�ӡ����磺
conf�����õ�url�ǣ�http://www.im.xx?i=1, ���õ�`HTTP_URI_QUERY`���л�����`a=1&b=2`����ô���յ�url���ǣ�
`http://www.im.xx?i=1&a=1&b=2`��
���conf�������url�ǣ�http://www.im.xx, ��ô���յ�url���ǣ�`http://www.im.xx?a=1&b=2`

`HTTP_HEAD`��HTTPͷ�����ݣ���HTTP��ͷ��key��value���ݣ����磺Cookie:cna=xxx\r\nUser-Agent:xxx

`HTTP_VERSION_MINOR`��HTTP�İ汾��Ŀǰ֧�֡�0�����ߡ�1������1.0����1.1

`BODY`��Ĭ��ֵ��������body������HTTP��GET��������Ϊ�գ�POST��������HTTP��body��������HTTP��Э�飬������������

`ARPC_METHOD`��arpc�����󷽷�����method���֡�

`ARPC_SERVICE`��arpc������service����service���֡���Ҫʹ��ȫ����������������ռ䣬��Ҫ���������ռ䡣���磺
arp�ķ�����Ϊ xxx�������Ϊ��package test����ô��Ҫ����Ϊ��test.xxx

---

##### protobuf��ʽ�Ľڵ�
��imock-server��a�ڵ������һ�¡������ظ�˵����
##### json��ʽ�Ľڵ�
��imock-server��a�ڵ������һ�¡������ظ�˵����
##### key/value��ʽ�Ľڵ�
��imock-server��a�ڵ������һ�¡������ظ�˵����

#### a�ڵ�
imock-client��fmt.xml�������a�ڵ������ˣ���Ϊclient��Ӧ����ν�������յ���Ӧ�����ݡ���������Ľ�����Ժ�dat.xml�и�����ֵ����ƥ�䣬��ѡ�������ݲ�ͬ�ĸ�ʽ���в�ͬ�Ľڵ�����

##### ��ͨ���͵Ľڵ�
��imock-server��q�ڵ����ƣ������ǽ����ַ����Ľ�������֧�ֵ��������£�

---

* `sub_def_split=';'`����imock-server��q�ڵ�һ��
* `split=','`����imock-server��q�ڵ�һ��
* `repeated_split='|'`����imock-server��q�ڵ�һ��
* `var='$varname'`����imock-server��q�ڵ�һ��
* `length='4'`����imock-server��q�ڵ�һ��
* `type='[type]'`����imock-server��q�ڵ�һ��
* `op='[operate]'`��	��imock-server��qһ��

---

* `from='[where]'`	��Ǳ��ֶε�ֵ���Ķ���ȡ��where��ȡֵ�����ǣ���ֵ��������`|`�ָ�)��

`HTTP_HEAD`��HTTPӦ��ͷ�����ݣ���HTTP��ͷ��key��value���ݣ����磺Location:http://www.imock.xx 

`HTTP_VERSION_MINOR`��HTTP��Ӧ��汾��Ŀǰ֧�֡�0�����ߡ�1������1.0����1.1

`HTTP_CODE`��HTTPӦ���룬����302��404�ȡ�

`HTTP_CODE_MSG`��HTTPӦ�����Ӧ����Ϣ�����硱Not Found������404��Ӧ����Ϣ�������Բ����ã����Զ���ӣ�ͨ��HTTP_CODE��ȡ��׼��CODE_MSG����

`ARPC_FAILED_MSG`��ARPCӦ���ʧ����Ϣ��

`BODY`��Ĭ��ֵ����Ӧ��body��

---

##### protobuf��ʽ�Ľڵ�
��imock-server��q�ڵ������һ�¡������ظ�˵����
##### json��ʽ�Ľڵ�
��imock-server��q�ڵ������һ�¡������ظ�˵����
##### key/value��ʽ�Ľڵ�
��imock-server��q�ڵ������һ�¡������ظ�˵����


## Ӧ����������dat.xml

�����������ļ����data������ָ�����ļ���

dat.xml�Ǳ�׼��xml��ʽ������ָ��Ӧ�����ݵ����ݡ�����Ҫ���л�(serialize)�ͷ����л�(parse)�Ķ���
dat.xml��`<dat>`Ϊ���ڵ㣬�������`<qa>`�ڵ㣬ÿ��`<qa>`�ڵ�������`<q>`�Ͷ��`<a>`�ڵ㡣����

```xml
<dat>
   <qa>
        <q fid='q1'>...</q>
        <a fid='a1'>...</a>
        <a fid='a2'>...</a>
        <q fid='q2'>...</q>
	</qa>
	<qa>��</qa>
</dat>
```


q�ڵ㣬��query�ڵ㡣����imock-server��˵������server������յ������ݽ���ƥ����������ݣ�����imock-client��˵����client�����ͳ�ȥ���������ݡ�

a�ڵ㣬��answer�ڵ㡣����imock-server��˵����server����Ӧ�����������Ӧ���������ݣ�����imock-client��˵������client������յ������ݽ���ƥ����������ݡ�

dat��q/a�ڵ��`fid`���ԣ����ں�fmt.xml�е�q/a�ڵ���ж�Ӧ����ָ��dat.xml�б��ڵ�(q/a)��Ҫʹ�ú��ָ�ʽ���н�������dat.xml����ָ����`fid`���붼����fmt.xml�д��ڡ�

���е�q/a�ڵ�������ڵ㣨�ӽڵ㣩�����fmt.xml�ж�Ӧ���ֶ�˳��������⡣���磺

```xml
<fmt>
<q>
    <title split=';'/>
    <body/>
</q>
<a></a>
<q fid='q1'>
   <msg sub_def_split=':' repeated_split=';'>
        <key/>
        <value/>
	</msg>
</q>
<a fid='a1'>
    <len/>
    <msg/>
</a>
</fmt>
// �������ϵ�fmt.xml���ã����Ӧ��dat.xml�������£�
<dat>
	<qa>
		<q fid='q1'>
            <msg>
                <key>testKey</key>
                <value>testValue</value>
            </msg>
		</q>
		<a fid='a1'>
            <len>5</len>
            <msg>abcde</msg>
		</a>
	</qa>
</dat>
```

_ע��_�����¼���ͬʱ������imock-server��imock-client��

* ����protobuf���ö��ֵ��boolֵ������д����ֵ����ö��ֵ����дö��ֵ���ַ������ݣ�������0/1/2�����֣���boolֵ��дtrue/false��
* �����ظ��ֶΣ�������ͨ��repeated_split����������protobuf�ﶨ���repeated�ֶΣ���ֱ��д����ڵ㼴�ɡ����磺

```xml
<msg>
	<body>Body 1 in msg 1</body>
</msg>
<msg>	
	<body>Body 1 in msg 2</body>
	<body>Body 2 in msg 2</body>
</msg>
```

* �����ظ��ֶε�ƥ�䣬���ǰ�����ϵ��������dat.xml�����õ��ظ��ֶ�������ֵ��ֻҪ������ֵ����ƥ�����������������ƥ�伴��ƥ��ɹ�����ʹƥ���������4�����������ֵ����


imock-client/ imock-server��dat.xml������Ҫ�����һ�¡�Ϊ��˵�������������Ծɷֿ�������

### ������imock-server

�����յ�һ�����󴮺�imock-server�����dat.xml������Ӧ��������߼����£�

1. ����˳�����δ�dat.xml�ж�ȡ`<qa>`�ڵ㡣
2. ��ÿһ��`<qa>`�ڵ㣬ʹ��`<q>`�ڵ�������fid����Ӧ�ĸ�ʽ����������fid��fmt.xml�ж�Ӧ��q�ڵ㣩�������ַ������н�����
3.	�����꣨���ܳɹ�����ʧ�ܣ������dat.xml�еĸ�`<q>`�ڵ����ƥ�䡣ƥ��ɹ����������ڵ�`<qa>`�ڵ��е�`<a>`�ڵ�������л����ء���`<a>`�ڵ�����л���ʽ��Ҳ��`<a>`�ڵ�������fid����Ӧ�ĸ�ʽ������fid��fmt.xml�ж�Ӧ��a�ڵ㣩��
4.	�������û���ҵ��κ�ƥ���q�ڵ㣬�򲻻᷵���κ����ݸ�client�ˡ�

ע�����¼��㣺

* �������ַ����Ľ�������������ɹ�������ƥ��ɹ���񣩣��������������½������������������ַ���������ָ�ʽ�Ľ������Ե�һ�ָ�ʽΪ׼�������˭�ǵ�һ���ǰ���dat.xml�е�q�ڵ��Ӧ��fid�������������ǰ���fmt.xml�е�q�ڵ�˳��
* ����һ��`<qa>`�ڵ���Ķ��q�ڵ㣬ֻҪ����һ��q�ڵ�ƥ��ɹ�����`<qa>`�ڵ�����ƥ��ɹ��������ر�`<qa>`�ڵ��Ӧ��`<a>`�ڵ㡣
* ����һ��`<qa>`�ڵ���Ķ��a�ڵ㣬����Ҫ����ʱ����ᰴ��ÿ��a�ڵ����õ�rate������ֻѡȡһ�����л����ء�

q/a�ڵ���������ƣ�˵�����£�

#### q�ڵ�
imock-server��dat.xml�������q�ڵ������ˣ���Ϊserver��Ӧ����ζԽ��յ����ַ������ݽ���ƥ�䡣��fmt.xml��ͬ��dat.xml�е����еĽڵ㣬�������ݽڵ㡣

���ݽڵ�֧�ֵ��������£�

---

* `id='xx'`	

�����ڵ�ָ��һ��debugID�����idֻ��������¼��־ʹ�á����磺��һ��dat.xml���ж��q�ڵ�ʱ����ÿ��q�ڵ㶨��һ��Ψһ��id���ԣ����ɴ���־�п��ٶ�λƥ����������ĸ�q�ڵ㡣������ֻ����`<q>`�ڵ���Ч���������ڵ���������Ч��

---

* `match_shell_cmd='xx'`

���`match='shell'`����ʹ�á�ԭ��ͬfmt�ڵ��`shell_cmd`����

---

* `match='xx'`

ָ�����ڵ����ƥ�䡣����xx����ȡֵ���£�

`shell`���Զ���shellƥ����򡣱��� `<n match='shell' match_shell_cmd='echo �Cn 1'></n>` ��ʾn�ڵ��ֵ����`match_shell_cmd`ƥ����С����shell����ص��ַ�����һ���ַ���`0`�����ʾƥ��ɹ����������ӣ�����������������`1`������Զƥ��ʧ�ܡ�

`replaceshvar`�����shell����ʹ�á�ԭ��ͬfmt���`op='replaceshvar'`����

`reg`������ƥ�䡣���� `<n match='reg'>[0-9]*</n>` ��ʾn�ڵ��ֵ��������ƥ����У���������ʽ��`[0-9]*`����������ַ�������������`<n>`�ڵ�ֵ��`1234567`����ô����ƥ��ɹ��������`a123`����ƥ��ʧ�ܡ�

`icase`�����Դ�Сд�����ڽ���match�Ƚ�ǰ���Ὣ��Ҫ�ȶԵ������ַ�����ת��ΪСд��

`int`������Ҫ�ȶԵ������ַ�����atoiת��Ϊ���͡�

`'<', '>', '=', '!='`������С�ڡ����ڡ����ڡ�������ƥ�䡣���磺`<n match='<'>10</n>` ��������ַ�������������`<n>`�ڵ�ֵ��20����ôƥ��ʧ�ܡ����Ҫ��������int���Ƚϣ�����Ҫ���intʹ�ã����磺`<n match='<, int'>10</n>`

`fmt_err`��ƥ�����ʧ�ܡ�������ֻ����`<q>`�ڵ����Ч��`<q>`�ӽڵ���Ч��

`fmt_ok`��ƥ������ɹ�������ʽ��ȷ����ƥ�䡣������ֻ����`<q>`�ڵ����Ч��`<q>`�ӽڵ���Ч��

`no_exist`�������ڼ�ƥ�䡣������protobuf����ĳ���ֶβ����ڣ���ƥ��ɹ���

`exist`�����ڼ�ƥ�䡣������protobuf����ĳ���ֶδ��ڣ���ƥ��ɹ���

_ע��_������ֵ����ͨ�����ŷָ���������ʹ�á����磺

`<n match='reg, icase'>aa.*</n>`�� ���Դ�Сд������

`<q match='fmt_err,fmt_ok'></q>`��������ȷ��ƥ�䡣

`<n match='<,=,int'>10</n>`��������С�ڵ���10ƥ��

---

* `from='xx'`

ָ�����ڵ��ֵ���Ժδ�������xx����ȡֵ���£�
`file`�����ڵ��ֵ�������ļ�����`<n from='file'>a.txt</n>`��ʾ���ڵ��ֵ������a.txt�ļ������ݡ�

`var`�����ڵ��ֵ�����ڱ�������`<n from='var'>$id</n>`��ʾ���ڵ��ֵ�����ڱ���`$id`��ֵ��

`cached`�����ڵ��ֵ�Ƿ�ɻ��档��Ҫ���`file/shell`����ʹ�á�Ϊ������Ч�ʣ���ÿ�ζ����¶�ȡ�ļ����߲�ÿ�����µ���shell�����Կ��Լӱ����Լ���file�Ķ�ȡ������shell��ִ�д��������磺`<n from='file,cached'>a.txt</n>`��ʾ���ڵ��ֵ������a.txt�ļ������ݣ�������ֻ�ᱻ��ȡһ�β�cached���ڴ��ע�⣺�������ͨ�����ŷָ���������ʹ�ã�������˳��

---

* `op='xx'`	ͬfmt�ڵ��op����

---

#### a�ڵ�
imock-server��dat.xml�������a�ڵ������ˣ���Ϊserver��Ӧ��Ӧ��ʲô�������ݸ�client�ˡ���fmt.xml��ͬ��dat.xml�е����еĽڵ㣬�������ݽڵ㡣

���ݽڵ�֧�ֵ��������£�

---

* `id='xx'`	��q�ڵ�һ�£���debugID��ֻ����`<a>`�ڵ���Ч��
* `from='xx'`	��q�ڵ�һ�¡�

---

* `op='xx'`	���˼̳�����fmt�ڵ��op�����⣬���У�

`hide`�����ر��ڵ㡣��ҪӦ������ͨ��ʽ������ʹ��`^A`�ָ���ַ����������Ҫģ����һ��`^A`��ȱһ���ֶΣ�������Ҫʹ�ø�����

`no_pack`�������л����ֶΣ��������ڵ��ֱֵ�ӷ��ء����磺`<n op='no_pack'>error format</n>`��Ὣ��error format����Ϊ���ݷ��أ���������n�ڵ�ĸ�ʽ

---

* `rate='����'`

ֻ����`<a>`�ڵ���Ч����һ��`<qa>`�ڵ����ж��`<a>`�ڵ㣬�����������rate���ԣ�����`<a>`���������ͬ����ѡȡһ��`<a>`�ڵ���ΪӦ�������Ҫ���ð��ղ�ͬ��������`<a>`�ڵ㣬����Ҫ����rate������ͬһ��`<qa>`�ڵ��������`<a>`�ڵ������õ�rate��������һ�������������������`<a>`�ڵ㣬���õ�rate�ֱ���2��4��6����ᰴ��2:4:6�ı�������ѡȡ��

---

* `sleep='xx'`	

xx��ȡֵ������10m��10���ӣ�1s��1�룻100ms��100���룻500us��500΢�룻ֻ����`<a>`�ڵ���Ч����Ҫ��Ϊ��ģ��Ӧ�����ʱ��

---

* `repeated_num='xx'`	

xx��ȡֵ�������Ǳ������������������֡���������Ҫ������Ҫ��̬ȷ��repeated�ֶεĸ����ĳ����¡����磬������ids=1,2,3,4����Ҫ�����������ids������������֯Ӧ�𡣿����ڽ�������ʱ����ids�ֶν���shell���������ݴ洢����ʱ�ļ��У��������������ڱ����С���Ӧ��ʱ�������ȡ��ʱ�ļ����ֵ���ɡ�����:

```xml
<ids op='shell' shell_cmd='./cnt.sh' var='$n'></ids>
```
���У�./cnt.sh�ű����ݿ��ԣ�

```bash
num=$(echo "$1" | tr , \\n  | tee /tmp/a | wc -l);
```

��Ӧ������ԣ�

```xml
<n repeated_num='$n' op='shell'  shell_cmd='./get.sh'></n>
```

���У�./get.sh�ű����ݿ��ԣ�

```bash
head -1 /tmp/a  && sed -i '1d'
```
---

### ������imock-client
imock-client�����dat.xml�е����ݣ���server�����������ݡ����߼����£�

1.	����˳�����δ�dat.xml�ж�ȡ`<qa>`�ڵ㡣
2.	��ÿһ��`<qa>`�ڵ㣬ʹ��`<q>`�ڵ�������fid����Ӧ�ĸ�ʽ����������fid��fmt.xml�ж�Ӧ��q�ڵ㣩�Ըýڵ�������л���
3.	�����л����ַ������͸�server��
4.	����server��Ӧ������У�������Ӧ����ַ������н�����ƥ��`<a>`�ڵ㡣�����л���ƥ��ķ�ʽ��imock-server��`<q>`�ڵ�ƥ�����ơ����ƥ��ɹ�������0Ϊ�˳����˳��������Է�0Ϊ�˳����˳���

_ע��_��

* ����һ��`<qa>`�ڵ���Ķ��a�ڵ㣬ֻҪ����һ��a�ڵ�ƥ��ɹ�����`<qa>`�ڵ�����ƥ��ɹ�������0Ϊ�˳����˳��������Է�0�˳����˳���
* ����һ��`<qa>`�ڵ���Ķ��q�ڵ㣬�ᰴ��ÿ��q�ڵ����õ�rate������ֻѡȡһ�����л����͡�

q/a�ڵ���������ƣ�˵�����£�

#### q�ڵ�

imock-client��dat.xml�������a�ڵ������ˣ���Ϊclient��Ӧ�÷���ʲô�������ݸ�server�ˡ���fmt.xml��ͬ��dat.xml�е����еĽڵ㣬�������ݽڵ㡣

���ݽڵ�֧�ֵ��������£�

* `id='xx'`����imock-server��a�ڵ�һ�£���debugID��ֻ����`<q>`�ڵ���Ч��
* `from='xx'`����imock-server��a�ڵ�һ�¡�
* `op='xx'`	��imock-server��a�ڵ�һ�¡�
* `rate='����'`	��imock-server��a�ڵ�һ�¡�
* `repeated_num='����'`	��imock-server��a�ڵ�һ�¡�

#### a�ڵ�
imock-client��dat.xml�������a�ڵ������ˣ���Ϊclient��Ӧ����ζԽ��յ���Ӧ���ַ������ݽ���ƥ�䡣��fmt.xml��ͬ��dat.xml�е����еĽڵ㣬�������ݽڵ㡣

���ݽڵ�֧�ֵ��������£�

* `id='xx'`����imock-server��q�ڵ�һ��
* `match='xx'`����imock-server��q�ڵ�һ��
* `from='xx'`����imock-server��q�ڵ�һ��
* `op='xx'`����imock-server��q�ڵ�һ��

## ��ĳЩ���Ե�����˵��
��������ƫ�࣬������Щ���Լ���server���ã�����client���ã���fmt���ã�Ҳ��dat���ã���q�ڵ����ã�Ҳ��a�ڵ����á�������Щ����˵�����£�

### op����
op���Լ�ָ���ڵ�ľ������������Ĳ���:

1.	����fmt�ڵ���ԣ�����ǽ����������ڽ������ڵ�ǰ���ַ����Ĵ�����������л������������л����ڵ�ֵ�Ժ�
2.	����dat�ڵ���ԣ�(�����ڽ��������)�������ƥ�䣬����ƥ��֮ǰ���dat�ڵ㣨��dat.xml�еĶ�����ʵʱ����request�����ģ����ã���������л������������л����ڵ�ֵ�Ժ�
3.	��shell�������ʹ�õ�rvalue������/Ӧ���dat�ڵ�ֵ������dat.xml�����õġ�
4.	op֧�������������op=��esc, gunzip����ʾ�Ƚ���ת�����Ž���gzip��ѹ��


# Ӧ��ʵ��
## ��ͨ����
### ��������
client���͸�server�����ݸ�ʽ���£�

client��server ��ѯ����ַ�����
		`querysn?ip^Bcookie^Aurl^Aadnum`
		
���磺
`querysn?127.0.0.1^BDe16DbsE50YCAbZc^Awww.test.com^A3`

server��client Ӧ�����ݣ�
`status^Aadboardid,rate^Badboardid,rate^B��`

���磺`0^A487123001,30^B487123002,20^B487123003,50`

### client����

```bash
#/home/a/imock/conf/client/imock-client.conf
[queryAd]
workers = 1
...
format = /home/a/imock/data/client/queryAd-fmt.xml
data = /home/a/imock/data/client/queryAd-dat.xml
message = /tmp/client-msg.txt w
```

```xml
<!--/home/a/imock/data/client/queryAd-fmt.xml--> 
<fmt>
    <q sub_def_split='&#1;'>
        <head split='?'/>
        <user sub_def_split='&#2;'>
            <ip/>
            <cookie/>
        </user>
        <url/>
        <adnum/>
	</q>
	<a>
    	<status split='&#1;'/>
    	<info repeated_split='&#2;'>
        	<adbid split=','/>
        	<rate/>
    	</info>
	</a>
</fmt>

<!--/home/a/imock/data/client/queryAd-dat.xml--> 
<dat>
	<qa>
    	<q>
            <head>querysn</head>
            <user>
                <ip>127.0.0.1</ip>
            </user>
            <url>www.test.com</url>
            <adnum>3</adnum>
		</q>
		<a>
   	 		<status>0</status>
		</a>
	</qa>
</dat>

```

### server����

```bash
#/home/a/imock/conf/server/imock-server.conf
mocks = queryAd
log = /home/a/imock/logs/error.log

[queryAd]
workers = 1
...
format = /home/a/imock/data/client/queryAd-fmt.xml
data = /home/a/imock/data/server/queryAd-dat.xml
message = /tmp/server-msg.txt
```

```xml
<!����client���� /home/a/imock/data/client/queryAd-fmt.xml--> 
<!--/home/a/imock/data/server/queryAd-dat.xml--> 
<dat>
	<qa>
    	<q>
            <head>querysn</head>
            <user>
                <ip>127.0.0.1</ip>
            </user>
		</q>
		<a>
    		<status>0</status>
    		<info>
        		<adbid>487123001</adbid>
        		<rate>30</rate>
    		</info>
    		<info>
        		<adbid>487123002</adbid>
        		<rate>20</rate>
    		</info>
    		<info>
        		<adbid>487123003</adbid>
        		<rate>50</rate>
    		</info>
		</a>
	</qa>
</dat>
```

### ����

```bash
$sudo imock-server
$sudo imock-client �Ca queryAd
$cat /tmp/server-msg.txt  -v
querysn?127.0.0.1^B^Awww.test.com^A3
$cat /tmp/client-msg.txt  -v
0^A487123001,30^B487123002,20^B487123003,50
```

## http+kv����

### ��������
clientͨ��http���͸�server�����ݸ�ʽ���£�

client��server ��ѯ����ַ�����`ip=xx&url=xx`

���磺
`ip=127.0.0.1&url=http%3A%2F%2Fabc.com%2Fa%3D1%26f%3Da.txt`

server��client Ӧ������Ϊ������url��������f������ָ�����ļ����ݡ�����ʾ������a.txt

ע�⣺client���͸�server���п�����GET����Ҳ������POST����

### client����

```bash
#/home/a/imock/conf/client/imock-client.conf
[http_queryFile]
workers = 1
protocol = http
url = localhost:9888/query
format = /home/a/imock/data/client/http_queryFile-fmt.xml
data = /home/a/imock/data/client/http_queryFile-dat.xml
message = /tmp/client-msg.txt w
```

```xml
<!--/home/a/imock/data/client/http_queryFile-fmt.xml--> 
<fmt>
    <q>
        <getArg fmt='k=v' kv_repeated_split='&#38;' to='HTTP_URI_QUERY'>
            <url>
                <uri split='?'/>
                <args fmt='k=v' kv_repeated_split='&#38;'/>
			  </url>
  		  </getArg>
        <pstArg fmt='k=v' kv_repeated_split='&#38;'>
            <url>
                <uri split='?'/>
                <args fmt='k=v' kv_repeated_split='&#38;'/>
			  </url>
        </pstArg>
	</q>
	<a/>
</fmt>

<!--/home/a/imock/data/client/http_queryFile-dat.xml--> 
<dat>
	<qa>
    	<q>
            <getArg>
                <ip>127.0.0.1</ip>
                <url op='urlenc'>
                    <uri>http://abc.com</uri>
                    <args>
                        <a>1</a>
                        <f>a.txt</f>
						</args>
					</url>
				</getArg>
		</q>
		<a match='fmt_ok'/>
	</qa>
	<qa>
    	<q>
            <pstArg>
                <ip>127.0.0.1</ip>
                <url op='urlenc'>
                    <uri>http://abc.com</uri>
                    <args>
                        <a>1</a>
                        <f>a.txt</f>
						</args>
					</url>
				</pstArg>
		</q>
		<a match='fmt_ok'/>
	</qa>
</dat>

```

### server����

```bash
#/home/a/imock/conf/server/imock-server.conf
mocks = http_queryFile
log = /home/a/imock/logs/error.log

[http_queryFile]
workers = 1
protocol = http
port = 9888
format = /home/a/imock/data/server/http_queryFile-fmt.xml
data = /home/a/imock/data/server/http_queryFile-dat.xml
message = /tmp/server-msg.txt
```

```xml
<!--/home/a/imock/data/server/http_queryFile-fmt.xml--> 
<fmt>
    <q>
        <Arg fmt='k=v' kv_repeated_split='&#38;' from='HTTP_URI_QUERY|BODY'>
            <url op='urldec'>
                <uri split='?'/>
                <args fmt='k=v' kv_repeated_split='&#38;'>
                    <f var='$fileName'/>
                </args>
			</url>
		</Arg>
	</q>
	<a/>
</fmt>
<!--/home/a/imock/data/server/http_queryFile-dat.xml--> 
<dat>
	<qa>
    	<q>
        <Arg>
            <url op='urldec'>
                <args>
                    <f match='exist'/>
					</args>
            </url>
        </Arg>
		</q>
		<a from='file,cached'>$fileName</a>
	</qa>
</dat>
```
### ����

```bash
$echo ��content in file�� > a.txt
$sudo imock-server
$sudo imock-client �Ca http_queryFile
```

## arpc+protobuf����

### ��������
clientͨ��arpc��server��protobuf�������£�addressbook.proto����

```proto
import "arpc/proto/rpc_extensions.proto";
package tutorial;
option java_package = "com.example.tutorial";
option java_outer_classname = "AddressBookProtos";
option cc_generic_services = true;
option java_generic_services = true;
message Person {
  required string name = 1;
  optional int32 id = 2;
  optional string email = 3;
  enum PhoneType {
    MOBILE = 0;
    HOME = 1;
    WORK = 2;
  }
  message PhoneNumber {
    required string number = 1;
    optional PhoneType type = 2 [default = HOME];
  }
  repeated PhoneNumber phone = 4;
}
message ACK {
  optional string message = 1 [default = "OK"];
}
service Foo {
  option (arpc.global_service_id) = 65535;
  rpc Query(Person) returns(Person) {
    option (arpc.local_method_id) = 32767;
  }
  rpc Update(Person) returns(ACK) {
    option (arpc.local_method_id) = 32766;
  }
  rpc Delete(Person) returns(ACK) {
    option (arpc.local_method_id) = 32765;
  }
}
```

### client����

```bash
#/home/a/imock/conf/client/imock-client.conf
[arpc_query]
workers = 10
protocol = arpc
address = tcp:localhost:9876
proto_file = /home/a/imock/proto/addressbook.proto
format = /home/a/imock/data/client/arpc_query-fmt.xml
data = /home/a/imock/data/client/arpc_query-dat.xml
message = /tmp/client-msg.txt w
```

```xml
<!--/home/a/imock/data/client/arpc_query-fmt.xml--> 
<fmt>
    <q>
        	<service to='ARPC_SERVICE'/>
			<method to='ARPC_METHOD'/>
			<pb fmt='pb' message='tutorial.Person' file='addressbook.proto'>
			</pb>
	 </q>
	 <a fid='ack'>
	 	<pb fmt='pb' message='tutorial.ACK' file='addressbook.proto'>
	 	</pb>
	 </a>
	 <a>
		<pb fmt='pb' message='tutorial.Person' file='addressbook.proto'>
		</pb>
	 </a>
</fmt>

<!--/home/a/imock/data/client/arpc_query-dat.xml--> 
<dat>
<qa>
    <q>
        <service>tutorial.Foo</service>
        <method>Update</method>
            <pb>
                <name>zhangsan</name>
                <phone>
                    <number>010-12345678</number>
                    <type>HOME</type>
				   </phone>
                <phone>
                    <number>13888888888</number>
                    <type>MOBILE</type>
				  </phone>
			 </pb>
	</q>	
	<a fid='ack' match='fmt_ok'/>
</qa>
<qa>
    <q>
        <service>tutorial.Foo</service>
        <method>Query</method>
            <pb>
                <name>zhangsan</name>
                <phone>
                    <number>010-12345678</number>
                    <type>HOME</type>
				   </phone>
                <phone>
                    <number>13888888888</number>
                    <type>MOBILE</type>
					</phone>
				</pb>
	 </q>
	 <a match='fmt_ok'/>
</qa>
</dat>

```


### server����

```bash
#/home/a/imock/conf/server/imock-server.conf
mocks = arpc_query
log = /home/a/imock/logs/error.log

[arpc_query]
workers = 10
protocol = arpc
address = tcp:localhost:9876
proto_file = /home/a/imock/proto/addressbook.proto
format = /home/a/imock/data/server/arpc_query-fmt.xml
data = /home/a/imock/data/server/arpc_query-dat.xml
message = /tmp/server-msg.txt
```

```xml
<!--/home/a/imock/data/server/arpc_query-fmt.xml--> 
<fmt>
	<q>
		<pb fmt='pb' message='tutorial.Person' file='addressbook.proto'>
		</pb>
		<method from='ARPC_METHOD'/>
	</q>
	<a fid='ack'>
		<pb fmt='pb' message='tutorial.ACK' file='addressbook.proto'>
		</pb>
	</a>
	<a>
		<pb fmt='pb' message='tutorial.Person' file='addressbook.proto'>
		</pb>
	</a>
</fmt>

<!--/home/a/imock/data/server/arpc_query-dat.xml--> 
<dat>
<qa>
    <q>
        <method>Query</method>
	</q>
	<a>
    <pb>
        <name>lisi</name>
	 </pb>
	</a>
</qa>
<qa>
    <q>
        <method>Update</method>
	</q>
	<a>
    <message>update ok.</message>
	</a>
</qa>
</dat>

```

### ����

```bash
$sudo imock-server
$sudo imock-client �Ca arpc_query
```

## json����֧��
����kv���ݣ��ݲ���ϸ����

## �������ܲ���
�������ܲ��ԣ�Ϊ�������imock��Ч�ʣ����Խ��������Ż���

* ����workers���õ��߳�/������
* log����־���������ߵ�error
* message��������Ϊoff������ÿ�������д����
* cache����Ϊon�����Ա���ÿ������ʱ��������dat.xml
* ��������ƥ��ĸ��Ӷȣ��������ʹ��`match=��fmt_ok��`

# �ӿ�API
Ϊ�˷�����չ�͹��ܸ��ã�imock�ṩ��.h��.a/.so�ṩ�û������Զ����̡���ο���
/home/a/imock/dev-interface/include/imock-interface.h
/home/a/imock/dev-interface/libs/libimock-interface.a
/home/a/imock/dev-interface/libs/libimock-interface.so


imock-parse

imock-serialize

imock-diff���ù���ּ���ڶԱȲ�ͬ��ԭʼ�ַ����ļ�����������������־�ļ�����ʽ���Բ�ͬ�����ù��ߵ�ʹ�ã���Ҫע�������ļ��ĸ�ʽ�������װ�����ʾ����

