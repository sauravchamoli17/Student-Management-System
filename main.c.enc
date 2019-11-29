#include<stdio.h>
#include<conio.h>
#include<string.h>
#include<stdlib.h>

FILE *fp, *ft;
int i, j, k, l, C, ctr, found, len, flag=0;
char temp[40], pass[10],pass1[10],ch;

struct  student
{	char std_id[10], course[20], name[40], add[40], email[40];
	int phon[12];
	long fee;
	struct  student *nxt;
};

struct  student *E=NULL;

struct  student *newstd()
{
	struct  student *x=NULL;
	x=(struct  student *)malloc(sizeof(struct  student));
	x->nxt=NULL;
	return x;
}


void Add_student()
{
	struct  student *tmp=NULL;
	struct  student *t2=E;
	E=NULL;
	clrscr();
	fp=fopen("student.txt","a");
	printf("================================================================================");
	printf("                                **ADD  STUDENTS**                               ");
	printf("================================================================================");
	printf("\n  Enter  student Details. To EXIT leave name field empty.\n");
	while(1)
	{

		t2=E;
		tmp=newstd();
		printf("\n  Name:");
		fflush(stdin);	//To flush the input buffer
		gets(tmp->name);
		if(strlen(tmp->name)==0)	//To break the loop if field is left empty
			break;

		printf("   student ID:");
		fflush(stdin);	//To flush the input buffer
		gets(tmp->std_id);

		printf("  course:");
		fflush(stdin);	//To flush the input buffer
		gets(tmp->course);


		printf("  Fee:");
		fflush(stdin);	//To flush the input buffer
		scanf("%d",&tmp->fee);

		printf("  Phone Number:");
		fflush(stdin);	//To flush the input buffer
		scanf("%s",&tmp->phon);	//To input an array of any type of element except '\n'

		printf("  Address:");
		fflush(stdin);
		gets(tmp->add);


		printf("  Email:");
		fflush(stdin);
		gets(tmp->email);



		if(E==NULL)
		{
			E=tmp;
		}
		else
		{
			while(t2->nxt!=NULL)
			{
				t2=t2->nxt;
			}
			t2->nxt=tmp;
		}


		printf("\n   student added sucessfully!!\n");
		printf("  Add more  student or press Enter.\n");

	}


	while(E!=NULL)
	{
		fwrite(E,sizeof(struct  student),1,fp);
		E=E->nxt;
	}

	fclose(fp);
}


void View_student()
{
	struct  student *tmp=NULL;

	clrscr();
	printf("================================================================================");
	printf("                               **VIEW  STUDENTS**                               ");
	printf("================================================================================");

	tmp=(struct  student *)malloc(sizeof(struct  student));

	fp=fopen("student.txt","r");
	flag=0;
	for(i='a';i<='z';i++)	//Checking the  student list for all alphabets
	{

		ctr=0;	//To count the number of  student starting with an alphabet
		while(fread(tmp,sizeof(struct  student),1,fp)==1)
			if(tmp->name[0]==i || tmp->name[0]==i-32)
				ctr++;
		if(ctr!=0)
		printf("\n\n\n==[%c]-(%d)=======================================================================",i-32,ctr);

		rewind(fp);	//To go to the begining of the file

		while(fread(tmp,sizeof(struct  student),1,fp)==1)
		{	if(tmp->name[0]==i || tmp->name[0]==i-32)
			{
				printf("\n  Name\t\t: %s\n   student ID\t: %s\n  course\t: %s\n ",tmp->name,tmp->std_id,tmp->course);
				printf("  fee\t\t: %d",tmp->fee);
				printf("\n  Phone\t\t:%s",tmp->phon);
				printf("\n Address\t: ");
				puts(tmp->add);
				printf(" Email\t\t: ");
				puts(tmp->email);
				flag=1;
				getch();
			}
		}
		rewind(fp);

	}

	if(flag==0)
	{
		printf("  Sorry,  student record NOT Found!!!");
		getch();
	}

	fclose(fp);

}


void Search_student()
{

	struct  student *tmp=NULL;
	tmp=(struct  student *)malloc(sizeof(struct  student));

	do
	{	clrscr();
		printf("================================================================================");
		printf("                                **SEARCH  STUDENTS**                            ");
		printf("================================================================================");

		found=0;	//To count the number of matches found

		printf("\n  Enter the  student Detail to be searched. Press ENTER to EXIT.");
		printf("\n\n  Name or  student ID:");
		fflush(stdin);
		gets(temp);
		len=strlen(temp);
		if(len==0)	//To exit if the field is left empty
		break;
		fp=fopen("student.txt","r");
		printf("\n  Search Result:\n");
		while(fread(tmp,sizeof(struct  student),1,fp)==1)
		{
			for(i=0;i<len;i++)
			{	if(temp[i]==tmp->name[i]||(temp[i]==tmp->name[i]+32)||temp[i]==tmp->name[i]-32)
					flag=1;
				if(temp[i]==tmp->std_id[i]||(temp[i]==tmp->std_id[i]+32)||temp[i]==tmp->std_id[i]-32)
					flag=1;
				else
				{	flag=0;
					break;
				}

			}
			if(flag==1)
			{	printf("\n  Name\t\t: %s\n   student ID\t: %s\n  course\t: %s",tmp->name,tmp->std_id,tmp->course);
				printf("\n  fee\t: %d",tmp->fee);
				printf("\n  Phone\t\t:%ld ",tmp->phon);
				printf("  Address\t: ");
				puts(tmp->add);
				printf("  Email\t\t: ");
				puts(tmp->email);

				found++;

			}

			getch();
		}
		if(found==0)
		printf("\n  No Matching  student Found!!!");
		else
		printf("\n  %d match(s) found!!!",found);
		fclose(fp);
		printf("\n  Search Again?(Press y):");
		C=getch();

	}while(C=='y'||C=='Y');
}


void Edit_student()
{

	struct  student *tmp=NULL;
	tmp=(struct  student *)malloc(sizeof(struct  student));

	clrscr();
	fp=fopen("student.txt","r");
	ft=fopen("temp.txt","w");
	printf("================================================================================");
	printf("                               **EDIT  STUDENTS**                               ");
	printf("================================================================================");

	printf("\n  Enter the  student you want to Edit");
	printf("\n  Leave the Name EMPTY to EXIT.");
	printf("\n\n  Name:");
	fflush(stdin);
	gets(temp);
	if(strlen(temp)==0)
	return;

	flag=0;
	while(fread(tmp,sizeof(struct  student),1,fp)==1)
	{
		if(stricmp(temp,tmp->name)==0)
		flag=1;
		else
		fwrite(tmp,sizeof(struct  student),1,ft);	//Copying all  students except the one editing

	}

	if(flag==1)
	{	printf("\n\n  Editing '%s'\n\n",temp);

		printf("\n  Name:");
		fflush(stdin);	//To flush the input buffer
		gets(tmp->name);

		printf("   student ID:");
		fflush(stdin);	//To flush the input buffer
		gets(tmp->std_id);

		printf("  course:");
		fflush(stdin);	//To flush the input buffer
		gets(tmp->course);


		printf("  fee:");
		fflush(stdin);	//To flush the input buffer
		scanf("%d",&tmp->fee);

		printf("  Phone Number:");
		fflush(stdin);	//To flush the input buffer
		scanf("%[^\n]",&tmp->phon);	//To input an array of any type of element except '\n'

		printf("  Address:");
		fflush(stdin);
		gets(tmp->add);

		printf("  Email:");
		fflush(stdin);
		gets(tmp->email);

		fwrite(tmp,sizeof(struct  student),1,ft);
		printf("\n\n   student Edited Succesfully.");
	}
	else
	printf("\n  NO such  student exist.");



	fclose(fp);
	fclose(ft);

	remove("student.txt");
	rename("temp.txt"," student.txt");

	getch();
}



void Delete_student()
{

	struct  student *tmp=NULL;
	tmp=(struct  student *)malloc(sizeof(struct  student));

	clrscr();
	printf("================================================================================");
	printf("                             **DELETE  STUDENTS**                               ");
	printf("================================================================================");

	printf("  Enter  student Name you want to Delete.");
	printf("\n  Leave the name EMPTY to EXIT.");
	printf("\n\n  Name:");
	fflush(stdin);
	gets(temp);
	if(strlen(temp)==0)
	return;
	fp=fopen("student.txt","r");
	ft=fopen("temp.txt","w");
	flag=0;
	while(fread(tmp,sizeof(struct  student),1,fp)!=0)
	{		if (stricmp(temp,tmp->name)==0)
			flag=1;
			else
			fwrite(tmp,sizeof(struct  student),1,ft);
	}
	fclose(fp);

	fclose(ft);

	remove("student.txt");
	rename("temp.txt"," student.txt");
	if(flag==1)
	printf("\n   student record DELETED");
	else
	printf("\n  NO such  student record exist");
	getch();

}

void ChangePassword()
{
	clrscr();
	printf("================================================================================");
	printf("                             **CHANGE PASSWORD**                                ");
	printf("================================================================================");


	fp=fopen("password.dat","r");
	if(fp!=NULL)	//If the Password is already set
	{
		printf("\n  To Exit Leave Password Empty.\n  Enter the current Password:");
		fflush(stdin);
		gets(pass1);
		if(strlen(pass1)==0)
		{
			fclose(fp);
			return;
		}

		fscanf(fp,"%s",pass);
		if(strcmp(pass1,pass)==0)//If the correct Password is inputted
		{	fclose(fp);
			fp=fopen("password.dat","w");
			printf("  Enter New Password:");
			fscanf(stdin,"%s",pass);
			fprintf(fp,"%s",pass);
			printf("\n  Password Changed Sucessfully!!");
		}
		else
		printf("\n  Wrong Password!!");
		fclose(fp);
	}
	else	//The Password is not Setted up
	{       fclose(fp);
		fp=fopen("password.dat","w");
		printf("  Enter New Password:");
		fscanf(stdin,"%s",pass);
		fprintf(fp,"%s",pass);
		fclose(fp);
		printf("\n  Password Created Sucessfully!!");
	}
	getch();
}

void MenuBorder()
{
	clrscr();
	printf("*******************************************************************************\n");
	printf("**                 !!Welcome to  student Manager Application!!               **\n");
	printf("*******************************************************************************\n");

}


void main()
{
	fp=fopen("password.dat","r");
	if(fp!=NULL)
	{
		fscanf(fp,"%s",pass);
		do
		{

			MenuBorder();
			gotoxy(4,4);
			printf("\n||  Press Backspace to EXIT\n||  Enter the password:");
			for(i=0;i<10;i++)
			{
				fflush(stdin);
				ch=getch();
				if(ch=='\r'||ch=='\b')
				break;
				pass1[i]=ch;
				putchar('*');
			}



			if(strlen(pass1)==0)
			exit(0);

			if(strcmp(pass1,pass)!=0)
			{	printf("\n||  Wrong Password!!! Try Again.");
				getch();
			}


		}while(strcmp(pass1,pass)!=0);
	}
	fclose(fp);
	while(1)
	{
		clrscr();
		MenuBorder();
		gotoxy(4,4);
		printf("\n\t\t[1] Add a New  student.\n");
		printf("\t\t[2] View  student List.\n");
		printf("\t\t[3] Search for a  student.\n");
		printf("\t\t[4] Edit a  student.\n");
		printf("\t\t[5] Delete a  student.\n");
		if(fp==NULL)
		printf("\t\t[6] Create Password.\n");
		else
		printf("\t\t[6] Change Password.\n");
		printf("\t\t[0] EXIT.\n");
		printf("\n  Enter your Choice:");

		C=getche();
		switch(C)
		{
			case '0': exit(0);
				  break;

			case '1': Add_student();
				  break;

			case '2': View_student();
				  break;

			case '3': Search_student();
				  break;

			case '4': Edit_student();
				  break;

			case '5': Delete_student();
				  break;

			case '6': ChangePassword();
				  break;
			default : printf("\n||  Wrong choice entered!! Try Again...");
				  getch();
		}

	}
}
