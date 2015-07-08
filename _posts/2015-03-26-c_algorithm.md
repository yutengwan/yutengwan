---
layout : post
title : c语言基本算法
---

####字符串转为数字

```
int parse_number(char *num) {
	double n=0,sign=1,scale=0;
    int subscale=0,signsubscale=1;
    if (*num == '-') {                        //负数
        sign = -1,num++;
    }
    if (*num == '0') {                        //0开头
        num++;
    }
    if (*num>='1' && *num<=9) {
        do {
            n = (n*10.0)+(*num-'0');
            num++;
        } while(*num>='0' && *num<='9');
    }
    if (*num=='.' && num[1]>=0 && num[1]<=9) {           //小数点后面的值
        num++;
        do {
            n = (n*10.0)+(*num-'0');
            scale--;
        } while(*num>=0 && *num<='9');
    }
    if (*num=='e' || *num=='E') {                        //如果是E，科学计数法
        num++;
        if (*num=='+') {
            num++;
        } else if (*num=='-') {
            signsubscale=-1;
            num++;
        }
        while (*num>='0' && *num<=9) {
            subscale = (subscale*10)+(*num-'0');
            num++;
        }
    }

    n=sign*n*pow(10.0,(scale+subscale*signsubscale));
    
    return n;
}
```