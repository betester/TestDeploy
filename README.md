# 1.��ʾdemo
http://42.192.227.196:8080/
�˺ţ�gaohuajun
���룺gaohuajun

��ע������������δʵ����ȫ���Զ�������jenkins���������á���ʱ������������õȣ������ֶ�������

# 2.Ŀ��
�����ṩ���Ա�׼��������
�ٽ��������̸�Ч���ȶ���

# 3.���ԭ��
* ��Ч���Զ����ͱ�׼��
* �򵥵ļ���ջ���߿�ά����
* ӵ����Դ������������е���������

# 4.����ܹ����
![Ч��](https://github.com/qtracer/TestDeploy/blob/main/data/%E8%BF%90%E7%BB%B4%E5%B9%B3%E5%8F%B0%E6%9E%B6%E6%9E%84%E5%9B%BE00.png)

# 5.�����ص�
* ���Docker����������������Ч
* ���伴�ã��򻯲��Ե�ִ�й��̣��ṩ���������汾���ƻ���
* ����Httprunner2.X/Locust1.4.X�ȹ�������
* �ṩ����CI/CD��ˮ�ߵ�ͳһ���ɻ���
* ��󻯲���ִ�л�������Դ������


# 6.��ο��ٿ�ʼ
* main-cli.sh��������Ŀ��Ŀ¼�£�����Ϊ**PRJ_ROOT_DIR**
* ���� $PRJ_ROOT_DIR/ini/hosts.ini
* cli����$PRJ_ROOT_DIR��ͨ��������������񹹽�ͳһ���ִ�г�ʼ��**bash $PRJ_ROOT_DIR/main-cli.sh**���״γ�ʼ��ʱ��CIƽ̨Jenkins
* ����Jenkins�������ڵ�
* Jenkins����������������
#### �Զ��������������Ҫ����
��1��ѡ�񡰲������������̡���git��������**BRANCH**��ѡ���������**appointedHost**
��2�����õ�master-slaveģʽ��ͬʱҪ��ѡ��������Ŀ����������
��3����Դ���������дҪ��ȡ�Ĵ���ֿ�
��4������ѡ��ִ��Shell�������� **bash $PRJ_ROOT_DIR/main-cli.sh $JOB_NAME $BRANCH 0**
��5������������
#### ���ܲ����������Ҫ����
��1��ѡ�񡰲������������̡���git��������**BRANCH**
��2����Դ���������дҪ��ȡ�Ĵ���ֿ�
��3������ѡ��ִ��Shell�������� **bash $PRJ_ROOT_DIR/main-cli.sh $JOB_NAME $BRANCH 6����������ֵ��**
��4������������


# 7.������������񹹽�ͳһ���
> bash $PRJ_ROOT_DIR/main-cli.sh **$JOB_NAME** **$BRANCH** **$workerNum** **$appointedHost** $appointedCase

���У�**���񹹽�ʱ**����ѡ������
* $JOB_NAME ����Ŀ����Jenkins����������ֱ������
* $BRANCH : �����֧��git���������������������̡��ж��壬��������
* $workerNum : ����worker����������ΪInterger�����ֶ��������ֵ
* $appointedHost: ѡ����������������������̡��ж��壬�������á���д��Ҫִ���Զ������Ե����л������뿪�������Ӧ�����ܲ���ʱ����ѡ�������
```
# tips:
if [ $workerNum -ge 1 ];then
  "performance test"
else
  "interface automation test"
fi
```

��ѡ������
* $appointedCase��ָ��·����������·����д $PRJ_ROOT_DIR ���·������ testcases/create_user.yml


# 8.������Ҫ�����ļ�
## 8.1.���Լ�Ⱥ����hosts.ini
����**$PRJ_ROOT_DIR/ini/hosts.ini**����ʽ��$host,$account,$password,$constant,$MasterOrSlave

* $host��slave�ڵ��IP��ַ
* $account��slave�ڵ��������˺�
* $password��slave�ڵ�����������
* $constant������ֵΪ��isnew�����ߡ�notnew�������������������Ҫ����ʼ����������ǡ�isnew������ʼ������Ϊ��notnew��
* $MasterOrSlave������ֵΪ��master�����ߡ�slave����ָ����master����slave�ڵ㡣

hosts.iniΪJenkins Master-Slave�Լ�Locust Master-Slaveģʽ����slave���ļ������״γ�ʼ��ǰ���ã���������slave��Ҫ����ִ��һ�γ�ʼ��**bash $PRJ_ROOT_DIR/main-cli.sh**��

## 8.2.config.ini���ֲ���˵��
* installedEnv���Ƿ�װ�˻����������������ֶ��޸ġ�
* installedCI���Ƿ�װ��CIƽ̨Jenkins���������ֶ��޸ġ�
* remaincores��ִ�����ܲ���ʱ��ÿ���ӻ�Ԥ����cores���������������Ĭ��Ԥ��2����֧���޸ġ�
* hrun_path���ӿ��Զ���Ĭ��ִ�е�ָ��·����Ĭ��Ϊtestcases/��֧���޸ģ�Ҳ����ͳһִ�����ָ����


# 9.�����ĵ���֯�ṹ
* HttpRunner2.X�ο���https://github.com/qtracer/HttpRunner_demo
* Locust1.4.1�ο���https://docs.locust.io/en/1.4.1/running-locust-docker.html

# 10.Jenkins������
����ϵͳĬ�ϰ�װ����⣬���ｨ�鰲װ���²��
* Node and Label parameter	
* Extended Choice Parameter
* Git Parameter
* Git
* Email Extension Plugin
* Role-based Authorization Strategy

# 11.NGINXת������ִ��shell
> Jenkins���ã�curl -H "dirpath:$PWD" -H "shellpath:${shellpath}" ${host}:81/api/run?name=${JOB_NAME}%20${BRANCH}%200
* PWDΪshellϵͳ��������ʾ�Զ�����Ŀ�����·��������host��ӦNginx����ip address������shellpath��Ӧ·��+TestDeploy������BRANCH��Ӧ�Զ���������Ŀ�����֧��
* �÷�ʽ��֧�֣������Ƽ�ʹ�ã�Ĭ��Ϊ�ر�״̬������Ҫʹ�ã�����views/buildEnvDepend.sh ȡ��ע�ͣ�������
