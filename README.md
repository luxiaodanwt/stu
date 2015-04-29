# stu
#include <stdio.h>
#include <io.h>
#include <stdlib.h>
#include <conio.h>
#include <string.h>
#define N sizeof(struct st)
#define M 100
#define FORMAT "%s    %s   %d   %d   %d\n",snum,name,math,english,physics
struct st{
			char snum[11];    //学号
			char name[11];    //姓名
			int math;		  //数学
			int english;	  //英语
			int physics;	  //物理
			struct st *next;
			};
			
			
struct st *head;                        //头指针
char filename[11];                      //文件名
void creat_user(void);                  //创建账户
void entry(void);                       //登录账户
void input_txt(struct st *head);        //存储进文件
void insert_im(struct st *head);        //按学号顺序插入信息
struct st *creat(void);                 //创建链表
void inquiry(struct st *head);          //按学号查询函数
void inquiry_by_name(struct st *head);  //按姓名查询函数
void delete1(struct st *head);          //按学号删除链表结点
void display(struct st *head);          //打印函数
int num(struct st *head);               //学生的个数
void _sort(struct st *head);            //排序并输入存储于新文件
void revise_by_snum(struct st *head);   //根据学号修改学生成绩
void revise_by_name(struct st *head);   //根据姓名修改学生成绩
void display_by_sort(struct st *head);  //按平均成绩打印学生信息
void census_of_math(struct st *head);   //统计数学成绩大于多少分学生的信息
void census_of_english(struct st *head);//统计英语成绩大于多少分学生的信息
void census_of_physics(struct st *head);//统计物理成绩大于多少分学生的信息
void rate(struct st *head);             //各科成绩及格的比率
void free_of_link(struct st *head);     //清除链表
void read_file(void);                   //读取文件信息
void about_this_software(void);         //关于此软件的信息
void interface1(void);                  //界面1
void quit(void);                        //退出
void interface2(void);                  //界面2
void interface3(void);                  //界面3
void interface4(void);                  //界面4


void interface1(void)                   //界面1
{
    int x;
    printf("****************************************\n");
    printf("1、创建链表                            *\n");
    printf("2、打印学生成绩                        *\n");
    printf("3、查询                                *\n");
    printf("4、排序并输入存储于新文件              *\n");
    printf("5、修改成绩                            *\n");
    printf("6、统计                                *\n");
    printf("7、各科成绩及格比率                    *\n");
    printf("8、清除链表                            *\n");
    printf("9、插入学生信息                        *\n");
    printf("10、存储进文件                         *\n");
    printf("11、按学号删除链表结点                 *\n");
    printf("12、按平均成绩打印学生信息             *\n");
    printf("13、读取我的文件信息                   *\n");
    printf("14、关于此软件                         *\n");
    printf("15、退出程序                           *\n");
    printf("****************************************\n");
    printf("PS:要使用2—12功能必须先创建链表\n");
    printf("请根据菜单选择您要使用的功能:");
    scanf("%d",&x);
    while(1)
    {
        if(x<1||x>15)
        {
            printf("输入有误，请重新输入：");
            scanf("%d",&x);
        }
        if(x>=1&&x<=15)
            break;
    }
    switch(x)
    {
        case 1:head=creat();break;
        case 2:display(head);break;
        case 3:interface2();break;
        case 4:_sort(head);break;
        case 5:interface3();break;
        case 6:interface4();break;
        case 7:rate(head);break;
        case 8:free_of_link(head);break;
        case 9:insert_im(head);break;
        case 10:input_txt(head);break;
        case 11:delete1(head);break;
        case 12:display_by_sort(head);break;
        case 13:read_file();break;
        case 14:about_this_software();break;
        case 15:quit();break;
    }
}


void quit()
{
    exit(1);
}

void interface2(void)
{
     int x;
     printf("****************************************\n");
     printf("1、按学号查询学生成绩                  *\n");
     printf("2、按姓名查询学生成绩                  *\n");
     printf("3、返回主菜单                          *\n");
     printf("****************************************\n");
     printf("请根据子菜单选择您要使用的功能：");
            scanf("%d",&x);
     while(1)
     {
        if(x<1||x>3)
        {

            printf("输入有误，请重新输入：");
            scanf("%d",&x);
        }
        if(x==1||x==2||x==3)
            break;
     }
    switch(x)
    {
        case 1:inquiry(head);interface2();break;
        case 2:inquiry_by_name(head);interface2();break;
        case 3:interface1();break;
    }
}


void interface3(void)
{
    int x;
    printf("****************************************\n");
    printf("1、根据学号修改学生成绩                *\n");
    printf("2、根据姓名修改学生成绩                *\n");
    printf("3、返回主菜单                          *\n");
    printf("****************************************\n");
    printf("请根据子菜单选择您要使用的功能:");
    scanf("%d",&x);
    while(1)
    {
        if(x>3||x<1)
        {
            printf("输入有误，请重新输入：");
            scanf("%d",&x);
        }
        if(x>=1&&x<=3)
            break;
    }
    switch(x)
    {
        case 1:revise_by_snum(head);interface3();break;
        case 2:revise_by_name(head);interface3();break;
        case 3:interface1();break;
    }
}


void interface4(void)
{
    int x;
    printf("*******************************************\n");
    printf("1、统计数学成绩大于60分的人数比           *\n");
    printf("2、统计英语成绩大于60分的人数比           *\n");
    printf("3、统计物理成绩大于60分的人数比           *\n");
    printf("4、返回主菜单                             *\n");
    printf("*******************************************\n");
    printf("请根据子菜单选择您要使用的功能:");
        scanf("%d",&x);
    while(1)
    {
        if(x>4||x<1)
        {
            printf("输入有误，请重新输入：");
            scanf("%d",&x);
        }
        if(x<=4&&x>=1)
            break;
    }
    switch(x)
    {
        case 1:census_of_math(head);interface4();break;
        case 2:census_of_english(head);interface4();break;
        case 3:census_of_physics(head);interface4();break;
        case 4:interface1();break;
    }

}


void about_this_software(void)
{
    printf("*****************************\n");
    printf("名称：学生成绩管理系统      *\n");
    printf("制作人：WT                  *\n");
    printf("制作日期：2015年3月25日     *\n");
    printf("*****************************\n");
    getchar();
}


void creat_user(void)    //创建账户
{
    int i=0,j;
    FILE *fp;
    char user[20],password[20],unpassword[20];
    fp=fopen("e:\\user.txt","a+");
    printf("请输入用户名(用户名不超过7位):");
    scanf("%s",user);
    while(1)
    {

    if(strlen(user)>7)
      {
        fflush(stdin);
        printf("输入有误，请重新输入：");
            scanf("%s",user);
      }
    if(strlen(user)<=7)
        break;
    }
    fputs(user,fp);
    fputc('\n',fp);
    fflush(stdin);
    printf("请输入密码（密码不超过7位）：");
    for(j=0;j<7;j++)
    {
        password[j]=getch();
        putchar('*');
    }
    password[j]=0;
    getchar();
    while(1)
    {
          if(strlen(password)>7)
          {
                fflush(stdin);
                printf("输入有误，请重新输入：");
                for(j=0;j<7;j++)
                {
                    password[j]=getch();
                    putchar('*');
                }
                password[j]=0;
                getchar();
                if(strlen(password)<=7)
                    break;
        }
    if(strlen(password)<=7)
        break;
    }
    for(i=0;i<7;i++)
        unpassword[i]=password[i];
    for(i=0;i<7;i++)                //加密
        password[i]=unpassword[6-i];
    password[7]=0;
    fputs(password,fp);
    fputc('\n',fp);
    fclose(fp);
    printf("创建账户成功\n");
}


void entry(void)            //登录账户
{
    FILE *fp;
    int n=1,i=0,j;
    char user[20],password[20],temp[20],unpassword[20],ch;
    fp=fopen("e:\\user.txt","r");
    printf("请输入用户名(用户名不超过7位):");
    fflush(stdin);
    scanf("%s",user);
    while(1)
    {
         if(strlen(user)>7)
        {
            fflush(stdin);
            printf("输入有误，请重新输入：");
            scanf("%s",user);
        }
        if(strlen(user)<=7)
        {
            rewind(fp);
            while(fgets(temp,8,fp)!=NULL)
            {
                if(strcmp(user,temp)==0)
                {
                    i=1;
                    break;
                }
               fgetc(fp);


            }
            if(i==0)
            {
                printf("账号不存在，请重新输入：");
                scanf("%s",user);
                while(1)
                {
                    if(strlen(user)>7)
                    {
                        fflush(stdin);
                        printf("输入有误，请重新输入：");
                        scanf("%s",user);
                    }
                    if(strlen(user)<=7)
                        break;
                }
            }
        }
        if(i==1)
            break;
   }

    while(1)
    {

        if(strcmp(temp,user)==0)
        {
            fgetc(fp);
            fflush(stdin);
            printf("请输入密码(密码不超过7位)：");
            for(j=0;j<7;j++)
            {
                password[j]=getch();
                putchar('*');
            }
             password[j]=0;
             getchar();
            if(strlen(password)>7)
                while(1)
                {
                    fflush(stdin);
                    printf("输入有误，请重新输入：");
                    for(j=0;j<7;j++)
                    {
                        password[j]=getch();
                        putchar('*');
                    }
                    password[j]=0;
                    getchar();
                    if(strlen(password)>7)
                        n++;
                    if(n>5)
                    {
                        printf("密码输入错误已超过5次，程序自动结束");
                        exit(1);
                    }
                    if(strlen(password)<=7)
                        break;
                }
           for(i=0;i<7;i++)
                unpassword[i]=password[i];
           for(i=0;i<7;i++)                      //解密
                password[i]=unpassword[6-i];
                password[7]=0;
           if(strcmp(password,fgets(temp,8,fp))==0)
                interface1();
		   else
		   {
                fflush(stdin);
				printf("密码有误，请重新输入密码(密码不超过7位):");
				for(j=0;j<=7;j++)
                {
                    password[j]=getch();
                    putchar('*');
                }
                password[j]=0;
                getchar();
				if(strlen(password)>7)
					while(1)
					{
						fflush(stdin);
						printf("输入有误，请重新输入：");
						for(j=0;j<=7;j++)
                        {
                            password[j]=getch();
                            putchar('*');
                        }
                        password[j]=0;
                        getchar();
						if(strlen(password)>7)
							n++;
					    if(n>5)
						{
							printf("密码输入错误已超过5次，程序自动结束");
							exit(1);
					    }
						if(strlen(password)<=7)
							if(strcmp(password,temp)==0)
							interface1();
					}
                else
                   while(1)
					{
						fflush(stdin);
						printf("输入有误，请重新输入：");
						for(j=0;j<=7;j++)
                        {
                            password[j]=getch();
                            putchar('*');
                        }
                        password[j]=0;
                        getchar();
						if(strlen(password)>7)
							n++;
					    if(n>5)
						{
							printf("密码输入错误已超过5次，程序自动结束");
							exit(1);
					    }
						if(strlen(password)<=7)
                        {
                            for(i=0;i<7;i++)
                                unpassword[i]=password[i];
                            for(i=0;i<7;i++)                      //解密
                                password[i]=unpassword[6-i];
                                password[7]=0;

							if(strcmp(password,temp)==0)
                                interface1();
                        }
					}

		   }
        }
    }
}


void read_file(void)
{
    char array1[100];
    char snum[11];
    char name[11];
    int math;
    int english;
    int physics;
    FILE *fp;
    fp=fopen(filename,"r");
    if(fp==NULL)
    {
        printf("文件打开失败");
        getch();
        exit(1);
    }
    fgets(array1,100,fp);
    printf("%s",array1);
    while(1)
    {

        fscanf(fp,"%s    %s   %d   %d   %d",snum,name,&math,&english,&physics);
        fgetc(fp);
        if(feof(fp)!=0)
            break;
        printf(FORMAT);

    }
}

struct st *creat(void)       //创建链表
{
	int i=1,n;
	struct st *p1,*p2;
	printf("请输入学生的人数:");
	scanf("%d",&n);
	p1=head=(struct st *)malloc(N);
	printf("请按次序输入学生的学号，姓名，数学成绩，英语成绩，物理成绩(用空格隔开):");
	p2=(struct st *)malloc(N);
	scanf("%s%s%d%d%d",p2->snum,p2->name,&p2->math,&p2->english,&p2->physics);
	while(i<n)
	{
		p1->next=p2;
		p1=p2;
		p2=(struct st *)malloc(N);
		printf("请按次序输入学生的学号，姓名，数学成绩，英语成绩，物理成绩(用空格隔开):");
		scanf("%s%s%d%d%d",p2->snum,p2->name,&p2->math,&p2->english,&p2->physics);
		i++; //人数变化量
	}
	p1->next=p2;
	p2->next=NULL;
	printf("创建链表成功\n");
	return head;
	getchar();
}


void input_txt(struct st *head)   //创建存储文件并将学生成绩输入存储
{
	FILE *fp;
	struct st *p;
	getchar();
	printf("请输入文件路径及文件名:");
    gets(filename);
	fp=fopen(filename,"w");
	if(fp==NULL)
	{
		printf("文件创建失败");
		getch();
		exit(1);
	}
	p=head->next;
	fputs("学号 姓名 数学 英语 物理\n",fp);
	while(p!=NULL)
	{
		fprintf(fp,"%s    %s   %d   %d   %d\n",p->snum,p->name,p->math,p->english,p->physics);
		p=p->next;
	}
	printf("存储成功\n");
    fclose(fp);
    getchar();
}


void inquiry(struct st *head)    //按学号查询函数
{
    struct st *p;
    char no[11];
    int i=0;
    fflush(stdin);
    printf("请输入学号:");
    gets(no);
    p=head->next;
    while(p!=NULL)
    {
        if(strcmp(no,p->snum)==0)
            {
                i=1;
                printf("学号:%s  姓名:%s  数学:%d  英语:%d  物理:%d\n",p->snum,p->name,p->math,p->english,p->physics);
            }
        p=p->next;
    }
    if(i==0)
        printf("未查询到此学号\n");
    getchar();
}


void inquiry_by_name(struct st *head)    //按照姓名查询成绩
{
    struct st *p;
    char name[11];
    int i=0;
    fflush(stdin);
    printf("请输入姓名:");
    gets(name);
    p=head->next;
    while(p!=NULL)
    {
        if(strcmp(name,p->name)==0)
            {
                i=1;
                printf("学号:%s  姓名:%s  数学:%d  英语:%d  物理:%d\n",p->snum,p->name,p->math,p->english,p->physics);
            }
        p=p->next;
    }
    if(i==0)
        printf("未查询到此姓名\n");


getchar();
}


void delete1(struct st *head)  //删除
{
	struct st *p,*p2=head;
	int i=0;
	char snum[11];
	printf("请输入要删除的学生成绩的学号:");
	scanf("%s",snum);
	p=head->next;
	while(p!=NULL)
	{
		if(strcmp(snum,p->snum)==0)
		{
            i=1;
            p2->next=p->next;
            free(p);
            return;
		}
        p2=p;
        p=p->next;
	}
    if(i==0)
        printf("出错，输入的学号有误\n");
    getchar();
}


void display(struct st *head)       //打印函数
{
    struct st *p=head;
	while(p->next!=NULL)
	{
		p=p->next;
		printf("学号:%s 姓名:%s 数学:%d 英语:%d 物理:%d\n",p->snum,p->name,p->math,p->english,p->physics);

	}
	getchar();
}


int num(struct st *head)  //学生的个数
{
    struct st *p=head;
    int i=0;
    p=p->next;
    while(p!=NULL)
    {
        i++;
        p=p->next;
    }
    return i;
}


void _sort(struct st *head)    //排序并输入存储于新文件
{
    FILE *fp;
    struct st s[M],temp,*p=head;
    int i=0,j,n=num(head);
    double  ave[M],t;
    char filename1[11];
    p=p->next;
    while(p!=NULL)
    {
        strcpy(s[i].snum,p->snum);
        strcpy(s[i].name,p->name);
        s[i].math=p->math;
        s[i].english=p->english;
        s[i].physics=p->physics;
        i++;
        p=p->next;
    }
    for(i=0;i<n;i++)
        ave[i]=(s[i].math+s[i].english+s[i].physics)/3.0;
    for(i=0;i<n-1;i++)
        for(j=0;j<n-1-i;j++)
            if(ave[j]<ave[j+1])
            {
                temp=s[j];
                s[j]=s[j+1];
                s[j+1]=temp;
                t=ave[j];
                ave[j]=ave[j+1];
                ave[j+1]=t;
            }
    printf("请输入要存储的文件名:");
    getchar();
    gets(filename1);
    fp=fopen(filename,"w");
    if(fp==NULL)
    {
        printf("文件未创建成功");
        getch();
        exit(1);
    }
    fputs("学号 姓名 数学 英语 物理\n",fp);
    for(i=0;i<n;i++)
    fprintf(fp,"%s    %s   %d   %d   %d\n",s[i].snum,s[i].name,s[i].math,s[i].english,s[i].physics);
    printf("存储成功\n");
    getchar();
}


void revise_by_snum(struct st *head)    //根据学号修改学生成绩
{
    struct st *p=head;
    char no[11];
    fflush(stdin);
    printf("请输入要修改成绩学生的学号:");
    gets(no);
    p=p->next;
    while(p!=NULL)
    {
        if(strcmp(no,p->snum)==0)
        {
            fflush(stdin);
            printf("是否修改此学生的数学成绩(y/n):");
                if(getchar()=='y')
                {
                    printf("请输入数学成绩:");
                    scanf("%d",&p->math);
                    printf("%d",p->math);
                    printf("修改成功\n");
                }
            printf("是否修改此学生的英语成绩(y/n):");
            fflush(stdin);
            if(getchar()=='y')
                {
                    printf("请输入英语成绩:");
                    scanf("%d",&p->english);
                    printf("修改成功\n");
                }
            printf("是否修改此学生的物理成绩(y/n):");
            fflush(stdin);
            if(getchar()=='y')
                {
                    printf("请输入物理成绩:");
                    scanf("%d",&p->physics);
                    printf("修改成功\n");
                }

        }
     p=p->next;
    }
    getchar();
}


void revise_by_name(struct st *head)    //根据学号修改学生成绩
{
    struct st *p=head;
    char name[11];
    fflush(stdin);
    printf("请输入要修改成绩学生的姓名:");
    gets(name);
    p=p->next;
    while(p!=NULL)
    {
        if(strcmp(name,p->name)==0)
        {
            printf("是否修改此学生的数学成绩(y/n):");
                if(getchar()=='y')
                {
                    printf("请输入数学成绩:");
                    scanf("%d",&p->math);
                    printf("修改成功\n");
                }
            printf("是否修改此学生的英语成绩(y/n):");
            fflush(stdin);
            if(getchar()=='y')
                {
                    printf("请输入英语成绩:");
                    scanf("%d",&p->english);
                    printf("修改成功\n");
                }
            printf("是否修改此学生的物理成绩(y/n):");
            fflush(stdin);
            if(getchar()=='y')
                {
                    printf("请输入物理成绩:");
                    scanf("%d",&p->physics);
                    printf("修改成功\n");
                }
        }
     p=p->next;
    }
    getchar();
}


void display_by_sort(struct st *head)
{
    struct st s[M],temp,*p=head;
    int i=0,j,n=num(head),k;
    double ave[M],t;
    p=p->next;
    while(p!=NULL)
    {
        strcpy(s[i].snum,p->snum);
        strcpy(s[i].name,p->name);
        s[i].math=p->math;
        s[i].english=p->english;
        s[i].physics=p->physics;
        i++;
        p=p->next;
    }
    for(i=0;i<n;i++)
        ave[i]=(s[i].math+s[i].english+s[i].physics)/3.0;
    for(i=0;i<n-1;i++)
        for(j=0;j<n-1-i;j++)
            if(ave[j]<ave[j+1])
            {
                temp=s[j];
                s[j]=s[j+1];
                s[j+1]=temp;
                t=ave[j];
                ave[j]=ave[j+1];
                ave[j+1]=t;
            }
    printf("要查询第几名学生的成绩:");
    scanf("%d",&k);
    printf("学号:%s  姓名:%s  数学:%d  英语:%d  物理:%d\n",s[k-1].snum,s[k-1].name,s[k-1].math,s[k-1].english,s[k-1].physics);
    getchar();
}


void census_of_math(struct st *head)  //统计数学成绩大于多少分学生的信息
{
    struct st *p=head;
    int  score;
    p=p->next;
    printf("请输入统计学生数学成绩的最低分数:");
    scanf("%d",&score);
    while(p!=NULL)
    {
        if(p->math>=score)
            printf("数学成绩:%f\n",p->math);
        p=p->next;
    }
    getchar();
}


void census_of_english(struct st *head)  //统计英语成绩大于多少分学生的信息
{
    struct st *p=head;
    int score;
    p=p->next;
    printf("请输入统计学生英语成绩的最低分数:");
    scanf("%d",&score);
    while(p!=NULL)
    {
        if(p->english>=score)
            printf("英语成绩:%d\n",p->english);
        p=p->next;
    }
    getchar();
}


void census_of_physics(struct st *head)  //统计物理成绩大于多少分学生的信息
{
    struct st *p=head;
    int score;
    p=p->next;
    printf("请输入统计学生物理成绩的最低分数:");
    scanf("%d",&score);
    while(p!=NULL)
    {
        if(p->physics>=score)
            printf("物理成绩:%d\n",p->physics);
        p=p->next;
    }
    getchar();
}


void rate(struct st *head)   //各科成绩及格的比率
{
    struct st *p=head;
    int i=0,rate_of_math=0,rate_of_english=0,rate_of_physics=0,rate_of_ave=0,n=num(head);
    double ave;
    p=p->next;
    while(p!=NULL)
    {
        if((ave=(p->math+p->english+p->physics)/3.0)>=60.0)
            rate_of_ave++;
        if(p->english>=60)
            rate_of_english++;
        if(p->physics>=60)
            rate_of_physics++;
        p=p->next;
    }
    printf("平均分大于60的人数占%%%f\n数学成绩大于60的人数占%%%f\n英语成绩大于60的人数占%%%f\n物理成绩大于60的人数占%%%f\n",rate_of_ave*1.0/n,rate_of_math*1.0/n,rate_of_english*1.0/n,rate_of_physics*1.0/n);
    getchar();
}


void free_of_link(struct st *head)
{
    struct st *p,*p2=head;
    p=head->next;
    while(p!=NULL)
    {
        p=p2->next;
        free(p2);
        p2=p;
    }
    printf("清除链表成功\n");
    getchar();
}


void insert_im(struct st *head)      //按学号顺序插入信息
{

    struct st *p=(struct st *)malloc(N),*p2=head;
    printf("请按次序输入学生的学号，姓名，数学成绩，英语成绩，物理成绩(用空格隔开):");
    scanf("%s%s%d%d%d",p->snum,p->name,&p->math,&p->english,&p->physics);
    while(p2->next!=NULL&&strcmp(p2->next->snum,p->snum)<0)
        p2=p2->next;
    p->next=p2->next;
    p2->next=p;
    printf("插入成功\n");
    getchar();
}


int main()
{
    system("color A");
    creat_user();
    entry();
	return 0;
}
