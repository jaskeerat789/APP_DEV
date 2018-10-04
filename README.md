# APP_DEV
app development for TIET 


#include<iostream.h>
#include<conio.h>
#include<stdlib.h>

void ini()
{
	int j;
	for(int i=0;i<4;i++)
	{
		for(j=0; j<13; j++)
		{
			deck[i][j]=i*100+j+2;
		}
	}
}

void dist()
{
	int temp;
	for(int i=0;i<4;i++)
	{
		for(j=0; j<13; j++)
		{
			deckcpy[i][j]=i*100+j+2;
		}
	}
	randomize();
	for(i=0; i<15; i++)
	{
		r=random(4);
		c=random(13);
		if(deckcpy[r][c]>0)
		{
			user[i]=deckcpy[r][c];
			deckcpy[r][c]=-1;
		}
		else
		i--;
	}

	for(i=0; i<15; i++)
	{
		for(j=0; j<15-i; j++)
		{
			if(user[j]<user[j+1])//desc
			{
				temp=user[j];
				user[j]=user[j+1];
				user[j+1]=temp;
			}
	}



	for(i=0; i<15; i++)
	{
		r=random(4);
		c=random(13);
		if(deckcpy[r][c]>0)
		{
			cpu[i]=deckcpy[r][c];
			deckcpy[r][c]=-1;
		}
		else
		i--;
	}
	for(i=0; i<15; i++)
	{
		for(j=0; j<15-i; j++)
		{
			if(cpu[j]<cpu[j+1])//desc
			{
				temp=cpu[j];
				cpu[j]=cpu[j+1];
				cpu[j+1]=temp;
			}
	}

}

void disp()
{
	for (int i=0;i<15; i++)
	{
		if(user[i]/100==0)
		{
			cout<<i+1<<") Spades ";
		}
		else if(user[i]/100==1)
		{
			cout<<i+1<<") Hearts ";
		}
		else if(user[i]/100==2)
		{
			cout<<i+1<<") Clubs ";
		}
		else if(user[i]/100==3)
		{
			cout<<i+1<<") Diamonds ";
		}
		if(user[i]%100<11)
			cout<<user[i]%100;
		else if(user[i]%100==11)
			cout<<"J";
		else if(user[i]%100==12)
			cout<<"Q";
		else if(user[i]%100==13)
			cout<<"K";
		else if(user[i]%100==14)
			cout<<"A";

		cout<<"\n";
	}
}

void set_trmp()
{
	int tr;
	cout<<"Trump choose kar bc	\n1)Spades\n2)Hearts\n3)Clubs\n4)Diamonds\n";
	cin>>tr;
	tr--;
	if(tr>4||tr<0)
	{
		cout<<"Chutiya bhar theek se. Spades set as trump.";
		tr=0;
	}


}

void usrtrn()
{
		cout<<"Patte phek bsdk";
		cin>>ch;
		ch--;

		//start
		if(user[ch]/100==0)
		{
			cout<<"Spades ";
		}
		else if(user[ch]/100==1)
		{
			cout<<"Hearts ";
		}
		else if(user[ch]/100==2)
		{
			cout<<"Clubs ";
		}
		else if(user[ch]/100==3)
		{
			cout<<"Diamonds ";
		}
		if(user[ch]%100<11)
			cout<<user[ch]%100;
		else if(user[ch]%100==11)
			cout<<"J";
		else if(user[ch]%100==12)
			cout<<"Q";
		else if(user[ch]%100==13)
			cout<<"K";
		else if(user[ch]%100==14)
			cout<<"A";
		//end
}

void cputrn()
{
	int flag=0;
	for(i=15; i>0; i--)
	{
		if(cpu[i]/100==ucrd/100)
		{
			ccrd=cpu[i];
			cpu[i]=-1;
			flag=1;
			break;
		}
	}
	if(flag==0)
	{
		for(i=15; i>0; i--)
		{
			if(tr==cpu[i]/100)
			{
				ccrd=cpu[i];
				cpu[i]=-1;
				flag=1;
				break;
			}

		}
	}
	if(flag==0)
	{
		for(i=15; i>0; i++)
		{
			if(cpu[i]!=-1)
			{
				ccrd=cpu[i];
				cpu[i]=-1;
				flag=1;
				break;
			}
		}
	}
}

void trnwin()
{
	if(ccrd/100==ucrd/100)
	{
		if(ccrd>ucrd)
		{
			clp=1;
			cp++;
		}
		else
		{
			ulp=1;
			up++;
		}
	}
	else if(ccrd/100==tr)
	{
		clp=1;
		cp++;
	}
	else if(ucrd/100==tr)
	{
		ulp=1;
		up++;
	}
	else if(f==0)
	{
		ulp=1;
		up++;
	}
	else if(f==1)
	{
		clp=1;
		cp++;
	}
}

void game()
{
	int up=0, cp=0,ch;
	for (int i=0; i<15; i++)
	{
		clrscr();
		cout<<"User points:	"<<up<<"\n";
		cout<<"CPU points:	"<<cp<<"\n";
		display();

		//chance
		if(ulp>clp)
		{
			f=0;//check which loop is run
			ulp=0;
			usrtrn();
			cout<<" vs ";
			cputrn();
			trnwin();

		}

		else
		{
			f=1;
			clp=0;
			cputrn();
			cout<<" vs ";
			usrtrn();
			trnwin();

		}
		ulp=clp=0;
	}


}




void main()
{

	clrscr();
	getch();
}