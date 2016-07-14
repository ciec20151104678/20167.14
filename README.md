# 20167.14
出数据
#include<stdio.h>
#include<stdlib.h>
#include<string.h>
int main()
{
	FILE *fp1, *fp2;

	char *text;
	int len;
	char lat[100];
	char lon[100];
	char time[100]; 
	int i=0;
	int n=0;
	fp1=fopen("C:\\Users\\q\\Desktop\\export.gpx","r");
	fp2=fopen("C:\\Users\\q\\Desktop\\export.csv","w");
	if((fp1 =fopen("C:\\Users\\q\\Desktop\\export.gpx","r"))==0) 
	{
		printf("文件读取错误");
		return (-1);
	}
	fseek(fp1,0,SEEK_END);
	len=ftell(fp1);
	text=(char*)malloc(len);//	printf("length=%d\n",len);

	fseek(fp1,0,SEEK_SET);//fread(text,1,len,fp1);
	
	fread(text,sizeof(char),len,fp1);
	while(!((*(text+i)=='<')&&(*(text+i+1)=='/')&&(*(text+i+2)=='g')&&(*(text+i+3)=='p')&&(*(text+i+4)=='x')&&(*text+i+5)=='>'))
	{
		if(((*(text+i)==' ')&&(*(text+i+1)=='l')&&(*(text+i+2)=='a')&&(*(text+i+3)=='t')))
		{
			
	        strncpy(lat,&text[i+6],9);
	        lat[9]='\0';
	        printf("%s\t",lat);
	        strncpy(lon,&text[i+22],10);
	        lon[10]='\0';
	        printf("%s\t",lon);
	        strncpy(time,&text[i+44],20);
	        time[20]='\0';
	        printf("%s\n",time);
	        fprintf(fp2,"经度              纬度                  时间\n");
	        fprintf(fp2," %s          %s           %s\n",lat,lon,time); 
     	}
     	i++;
    }
    fclose(fp1);
    fclose(fp2);
	return 0;
} 
