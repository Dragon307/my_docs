
/proc/sys/vm/swappiness ���ֵ��ʾ�ڴ滹ʣ���ٰٷֱȵ�ʱ��ʼʹ�� swap ����������Ĭ��ֵ�� 60��

	$ cat /proc/sys/vm/swappiness
	60

�����޸�Ϊ 10������ϵͳ��ϵͳ�ڴ滹ʣ 10�� ��ʱ��Ż�ʹ�� swap ����������������ڴ��Ч�ʣ�

	$ sudo sysctl vm.swappiness=10
