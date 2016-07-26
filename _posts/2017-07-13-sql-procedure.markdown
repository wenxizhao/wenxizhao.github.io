---
layout: post
title:  "存储过程笔记"
date:   2016-07-13 15:42:32 +0800
categories: work notes
---

######  一、变量初始化
let语句，或者select into

###### 二、执行
` execute function f() into v_bianliang;`

` call f(); `

###### 三、调试 
set debug file to '目录/文件名'

trace on;

例子:
``` 
drop function sp_ckt_check;
CREATE FUNCTION ccpqry.sp_ckt_check(v_licenseno varchar(8))
returning date as operateDate,int as clausecode,int as clausetype,
int as enrolldate,int as seatcount,int as purchaseprice,
int as chesun,int as sanzhe,int as zuowei


define v_proposalno char(22);
define v_clausecode int;
define v_clausetype	int;
define v_enrolldate	int;
define v_seatcount	int;
define v_purchaseprice	int;
define v_kindcode_cs int;
define v_kindcode_sz int;
define v_kindcode_zw int;
define v_operateDate date;
define v_procname	varchar(50);

let v_proposalno = null;	
let v_procname = 'sp_ckt_check';
--SET DEBUG FILE TO 'proctrace/trace_'||v_procname||'.out';
--trace on;

select b.proposalno into v_proposalno
from prpcitem_car a,prpcmain b,prpcopymain c
where licenseno=v_licenseno
and b.riskcode='DAA'
and a.proposalno = b.proposalno 
and c.applyno=b.proposalno
and date(c.inserttimeforhis)>='20160201'
and b.underwriteflag in ('1','3')
and b.othflag[3]<>'1'
and b.othflag[4]<>'1'
and b.othflag[6]<>'1';
--trace v_proposalno;

select count(*) into v_clausecode
from prpcengage
where proposalno=v_proposalno
and clausecode in ('9900444','9900445','9900446');
--trace v_clausecode;

select count(*) into v_clausetype
from prpcitem_car
where proposalno=v_proposalno
and clausetype = "F42";
--trace v_clausetype;

select count(*) into v_seatcount
from prpcitem_car
where proposalno=v_proposalno
and seatcount <= "7";
--trace v_seatcount;

select count(*) into v_purchaseprice
from prpcitem_car
where proposalno=v_proposalno
and purchaseprice < 500000;		
--trace v_purchaseprice;

select count(*) into v_enrolldate
from prpcitem_car c,prpcopymain d
where c.proposalno=d.applyno
and c.proposalno=v_proposalno
and date(d.inserttimeforhis)-date(c.enrolldate)<2920;
--trace v_enrolldate;

select date(d.inserttimeforhis) into v_operateDate
from prpcopymain d
where d.applyno=v_proposalno;

select count(distinct proposalno) into v_kindcode_cs
from prpcitemkind
where proposalno=v_proposalno
and kindcode = "050202";
select count(distinct proposalno) into v_kindcode_sz
from prpcitemkind
where proposalno=v_proposalno
and kindcode = "050602"--三者险（限额50万以上）
and amount >= "500000";
--trace v_kindcode_sz;

select count(distinct proposalno) into v_kindcode_zw
from prpcitemkind
where proposalno=v_proposalno
and kindcode = "050712";RETURN 	v_operateDate,v_clausecode,v_clausetype,v_enrolldate,v_seatcount,v_purchaseprice,v_kindcode_cs,v_kindcode_sz,v_kindcode_zw;

end function;                                              
```