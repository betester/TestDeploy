# ��ʾdemo
http://42.192.227.196:8080/
�˺ţ�gaohuajun
���룺gaohuajun

��ע������������δʵ����ȫ���Զ�������jenkins�������������á���ʱ������������õȣ������ֶ�������

# Ŀ��
�����ṩ���Ա�׼��������
�ٽ��������̸�Ч���ȶ���

# ���ԭ��
* ��Ч���Զ����ͱ�׼��
* �򵥵ļ���ջ���߿�ά����
* ӵ����Դ������������е���������

# ����ܹ����
![Ч��](https://github.com/qtracer/TestDeploy/blob/main/data/%E8%BF%90%E7%BB%B4%E5%B9%B3%E5%8F%B0%E6%9E%B6%E6%9E%84%E5%9B%BE00.png)

# �����ص�
* ����DevOps˼�룬�������ɳ�������
* ��Shell�ű�Ϊ���������������֧��PipeLine
* ���Docker���������������ṩ������Ի���
* ����Httprunner2/Locust1.4�ȹ�������
* Jenkins����ʽ����slave�ڵ��Զ����������������
* ֧��ִ�зֲ�ʽѹ��ͽӿ��Զ���

# ���ٿ�ʼ��������
* ����Ҫ�õ�Master-Slaveģʽ����ô��Ҫ�ֶ�����ini/hosts.ini
* ����${ShellDir}����cliͨ��**���������ִ��ͳһ���**ִ�г�ʼ�������CIƽ̨Jenkins
* ����Jenkins��������Ŀ


# ���������ִ��ͳһ���
> bash ${ShellDir}/main-cli.sh **$JOB_NAME** **$tag** **$workerNum** $appointedCase

���У���ѡ������
* $JOB_NAME ����Ŀ�� 
* $tag : �汾��
* $workerNum : ����������Interger
```
# tips:
if [ $workerNum -ge 1 ];then
  echo "performance test"
else
  echo "api test"
fi
```

��ѡ������
* $appointedCase �� ָ��·��������

������ʵ��PipeLine������Ҫ��װ��ֱ�ӵ���views��func�����Shell�ű���


# ���Լ�Ⱥ����
��Ҫ�ֶ�����**ini/hosts.ini**�ļ�����ʽ��${host ip},${account},${password},${constant}

���У�${constant}Ϊ��isnew�����ߡ�notnew�������������������Ҫ����ʼ����������ǡ�isnew������ʼ������Ϊ��notnew����

host.iniΪJenkins Master-Slave�Լ�Locust Master-Slaveģʽ����slave���ļ������״γ�ʼ��ǰ���ã���������slave��Ҫͨ��**ͳһִ�����**����ִ��һ��slave�ĳ�ʼ����

����ѹ��ʱ����������$workerNum������Ҫ��������̨�����������ֶ���д��


# store.ini���ֲ���˵��
* installedEnv���Ƿ�װ�˻����������������ֶ��޸ġ�
* installedCI���Ƿ�װ��CIƽ̨Jenkins���������ֶ��޸ġ�
* remaincores��ִ�����ܲ���ʱ��ÿ���ӻ�Ԥ����cores���������������Ĭ��Ԥ��2����֧���޸ġ�
* hrun_path���ӿ��Զ���Ĭ��ִ�е�ָ��·����Ĭ��Ϊtestcases/��֧���޸ģ�Ҳ����ͳһִ�����ָ����


# NGINXת������ִ��shell
> Jenkins���ã�curl -H "dirpath:$PWD" -H "shellpath:${shellpath}" ${host}:81/api/run?name=${JOB_NAME}%20${BRANCH}%200
* PWD����Ҫ�ģ���ʾ�Զ�����Ŀ�����·��������host��ӦNginx����ip������shellpath��Ӧ·��+TestDeploy������BRANCH��Ӧ�Զ���������Ŀ�����֧��
* �÷�ʽ��֧�֣������Ƽ�ʹ�ã�Ĭ��Ϊ�ر�״̬������Ҫʹ�ã�����views/buildEnvDepend.sh ȡ��ע�ͣ�������
