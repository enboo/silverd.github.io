---
layout: post
title: flickr ��ȫ���������ɷ���
---

# flickr ��ȫ���������ɷ���

�����ڴ󺽺��ĵ����ݿ���ƣ����ǵ��û��ֿ��� voyage_1/2/3/4 ...
��ôuid�������ɣ�

���ڵ�����������һ�������� voyage_share.user_index ȡ������������insert_id ����uid����ȱ���ǣ��е��㸺�صķ��ա�

flickr�ṩ��һ����չ�ĸ��õķ�����
���ǰ� user_index ���һ��ר���������� uid �ı�����ȡ���� uid_sequence����������ɵ��ֱ�������������Ϊ2��������Ŀ���������ű���Է��ڲ�ͬ����������ϡ�
����һ��������������uid����һ����������ż��uid

![](http://ww1.sinaimg.cn/large/67a6a651gw1dujgqcx9ncj.jpg)

## uid_sequence ������

���紴��64λ������id��  

    CREATE TABLE `uid_sequence` (  
      `id` bigint(20) unsigned NOT NULL auto_increment,  
      `stub` char(1) NOT NULL default '',  
      PRIMARY KEY  (`id`),  
      UNIQUE KEY `stub` (`stub`)  
    ) ENGINE=MyISAM;

SELECT * from uid_sequence �����  
  
    +-------------------+------+  
    | id                | stub |  
    +-------------------+------+  
    | 72157623227190423 |    a |  

�������Ҫһ��ȫ�ֵ�Ψһ��64λuid����ִ�У�  

    REPLACE INTO uid_sequence (stub) VALUES ('a');  
    SELECT LAST_INSERT_ID();  

- �� REPLACE INTO ���� INSERT INTO �ĺô��Ǳ��������̫�󣬻�Ҫ���ⶨ������
- stub �ֶ�Ҫ��ΪΨһ��������� sequence ��ֻ��һ����¼����Ҳ����ͬʱΪ���ű�����ȫ������������ user_ship_id����������Ҫ��������������ģ���ô����һ�� user_ship_id_sequence ��
- ����ʵ�ʶԱȲ��ԣ�ʹ�� MyISAM �� Innodb �и��ߵ����ܡ�

����flickrʹ����̨���ݿ���Ϊ�����������ɣ�ͨ������̨�����������͸��ؾ��⡣  
  
    TicketServer1: 
    auto-increment-increment = 2  
    auto-increment-offset = 1  
  
    TicketServer2:
    auto-increment-increment = 2  
    auto-increment-offset = 2  

## MySQL �� last_insert_id() �Ĳ�������

��Ϊ������SQL��䣬�������������֮��᲻���в������⣿

���ǲ��ᣬ��Ϊ last_insert_id() �� Connection ����ģ��ǵ������ӿͻ�����ִ�е�insert������һ�����ͻ���֮���ǲ���Ӱ�죬û��Ҫ������������

