����������
�˴�����Ϊ��ɸѡ�������һ�����ڣ��㶫ʡ�������εĸ߶��û���

������
1���㶫ʡ��
2����ƽ�����Ѵ���8��
3���������λ��Ѵ���0��

Ŀ�꣺
�����㶫ʡ�߶�����ͨ����¼����temp.ZZ0806_1  �ֶ�(PhoneNumber string)��
ʹ�õı�
1.tag_1104_user_building_province
2.tag_1202_arpu
3.tag_1202_myth_fee

ScriptCode:

hive -e"
create tables if not exists temp.ZZ0806_1 as 
select TT.id as PhoneNumber from
(
     select distinct T1.id from tags.tag_1104_user_building_province T1 INNER JOIN 
     select T2.id from 
     (
         select t2.id from tags.tag_1202_arpu t2 INNER JOIN
         select t3.id from tags.tag_1202_myth_fee t3 on
             (t2.id=t3.id and t2.tag_value>8 and t3.tag_value>0 and t2.dated='2018-06' and t3.dated='2018-06'))T2
      on(T1.id=T2.id and T1.tag_value='�㶫ʡ' and T1.dated='2018-06')
) TT;
"