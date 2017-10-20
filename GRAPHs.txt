#include<stdio.h>
#include<conio.h>
#include<math.h>
#include<string.h>
#include<ctype.h>
#include<graphics.h>

struct node
	{
	 int mode;
	 char oper;
	 float cons;
	};

int round(float p)
	{
	 int q;
	 p=p+0.5;
	 q=p;
	 return q;
	}

void copy(struct node& a, struct node& b)
	{
	 a.mode=b.mode;
	 a.oper=b.oper;
	 a.cons=b.cons;
	}

float rec(struct node s[75], int& x, int& y)
	{
	 float a, b, c=0;
	 while(x<=y)
		{
		 if(s[x].mode==1)
			 {
			  x++;
			  return s[x-1].cons;
			 }
		 else
			{
			 if(s[x].oper=='+')
				{
				 x++;
				 a=rec(s,x,y);
				 b=rec(s,x,y);
				 c=a+b;
				 return c;
				}
			 else if(s[x].oper=='-')
				{
				 x++;
				 a=rec(s,x,y);
				 b=rec(s,x,y);
				 c=a-b;
				 return c;
				}
			 else if(s[x].oper=='*')
				{
				 x++;
				 a=rec(s,x,y);
				 b=rec(s,x,y);
				 c=a*b;
				 return c;
				}
			 else if(s[x].oper=='/')
				{
				 x++;
				 a=rec(s,x,y);
				 b=rec(s,x,y);
				 c=a/b;
				 return c;
				}
			 else if(s[x].oper=='^')
				{
				 x++;
				 a=rec(s,x,y);
				 b=rec(s,x,y);
				 c=pow(a,b);
				 return c;
				}
			 else if(s[x].oper=='S')
				{
				 x++;
				 a=rec(s,x,y);
				 c=sin(a);
				 return c;
				}
			 else if(s[x].oper=='C')
				{
				 x++;
				 a=rec(s,x,y);
				 c=cos(a);
				 return c;
				}
			 else if(s[x].oper=='T')
				{
				 x++;
				 a=rec(s,x,y);
				 c=tan(a);
				 return c;
				}
			 else if(s[x].oper=='O')
				{
				 x++;
				 a=rec(s,x,y);
				 c=1/(tan(a));
				 return c;
				}
			 else if(s[x].oper=='A')
				{
				 x++;
				 a=rec(s,x,y);
				 c=1/(cos(a));
				 return c;
				}
			 else if(s[x].oper=='E')
				{
				 x++;
				 a=rec(s,x,y);
				 c=1/(sin(a));
				 return c;
				}
			 else if(s[x].oper=='I')
				{
				 x++;
				 a=rec(s,x,y);
				 c=asin(a);
				 return c;
				}
			 else if(s[x].oper=='N')
				{
				 x++;
				 a=rec(s,x,y);
				 c=acos(a);
				 return c;
				}
			 else if(s[x].oper=='X')
				{
				 x++;
				 a=rec(s,x,y);
				 c=atan(a);
				 return c;
				}
			 else if(s[x].oper=='Y')
				{
				 x++;
				 a=rec(s,x,y);
				 c=atan(1/a);
				 return c;
				}
			 else if(s[x].oper=='Z')
				{
				 x++;
				 a=rec(s,x,y);
				 c=acos(1/a);
				 return c;
				}
			 else if(s[x].oper=='W')
				{
				 x++;
				 a=rec(s,x,y);
				 c=asin(1/a);
				 return c;
				}
			 else if(s[x].oper=='M')
				{
				 x++;
				 a=rec(s,x,y);
				 if(a<0)
					return a;
				 else
					{
					 c=0-a;
					 return c;
					}
				}
			 else if(s[x].oper=='Q')
				{
				 x++;
				 a=rec(s,x,y);
				 c=sqrt(a);
				 return c;
				}
			 else if(s[x].oper=='L')
				{
				 x++;
				 a=rec(s,x,y);
				 c=log(a);
				 return c;
				}
			 else if(s[x].oper=='G')
				{
				 x++;
				 a=rec(s,x,y);
				 c=log10(a);
				 return c;
				}
			}
		}
	 return c;
	}
void deriv(struct node s[75], int& x, int& y);

float draw(char s[75], float x, int p=0)
	{
	 int i, k, m, a, b, j=1, l=0;
	 float y=0.0;
	 struct node t[75]; struct node temp[75];
	 char stack[50];
	 t[0].mode=2;
	 t[0].oper='(';
	 for(i=0; i<strlen(s); j++)
		{
		 if(s[i]=='x')
			{
			 t[j].mode=1;
			 if(p==0)
				t[j].cons=x;
			 else
				t[j].cons=8954;
			 i++;
			}
		 else if(s[i]=='p')
			{
			 t[j].mode=1;
			 t[j].cons=3.1415926;
			 i++;
			}
		 else if(s[i]=='e')
			{
			 t[j].mode=1;
			 t[j].cons=2.7182818;
			 i++;
			}
			/* sin -- S         asin -- I
			   cos -- C         acos -- N
			   tan -- T         atan -- X
			   cot -- O         acot -- Y
			   sec -- A         asec -- Z
			   cosec -- E       acosec -- W
			   mod -- M
			   sqrt -- Q
			   log -- L
			   log10 -- G
			*/
		 else if(s[i]=='a')
			{
			 if(s[i+1]=='s')
				{
				t[j].mode=0;
				if(s[i+2]=='i')
					{
					 t[j].oper='I';
					 i=i+4;
					}
				else if(s[i+2]=='e')
					{
					t[j].oper='Z';
					i=i+4;
					}
				}
			 else if(s[i+1]=='c')
				{
				t[j].mode=0;
				if(s[i+4]=='e')
					{
					t[j].oper='W';
					i=i+6;
					}
				else if(s[i+3]=='s')
					{
					t[j].oper='N';
					i=i+4;
					}
				else
					{
					t[j].oper='Y';
					i=i+4;
					}
				}
			else if(s[i]=='t')
				{
				t[j].mode=0;
				t[j].oper='X';
				i=i+4;
				}
			}
		 else if(s[i]=='s')
			{
			 t[j].mode=0;
			 if(s[i+1]=='i')
				{
				 t[j].oper='S';
				 i=i+3;
				}
			 else if(s[i+1]=='e')
				{
				 t[j].oper='A';
				 i=i+3;
				}
			 else
				{
				 t[j].oper='Q';
				 i=i+4;
				}
			}
		 else if(s[i]=='c')
			{
			 t[j].mode=0;
			 if(s[i+3]=='e')
				{
				 t[j].oper='E';
				 i=i+5;
				}
			 else if(s[i+2]=='s')
				{
				 t[j].oper='C';
				 i=i+3;
				}
			 else
				{
				 t[j].oper='O';
				 i=i+3;
				}
			}
		 else if(s[i]=='t')
			{
			 t[j].mode=0;
			 t[j].oper='T';
			 i=i+3;
			}
		 else if(s[i]=='m')
			{
			 t[j].mode=0;
			 t[j].oper='M';
			 i=i+3;
			}
		 else if(s[i]=='l')
			{
			 t[j].mode=0;
			 if(s[i+3]=='1')
				{
				 t[j].oper='G';
				 i=i+5;
				}
			 else
				{
				 t[j].oper='L';
				 i=i+3;
				}
			}
		 else if(isdigit(s[i]))
			{
			 t[j].mode=1;
			 t[j].cons=0;
			 for(k=0; isdigit(s[i+k])!=0; k++);
			 i=i+k;
			 for( ; k!=0; k--)
				 t[j].cons=t[j].cons+((s[i-k]-48)*pow(10,(k-1)));
			 if(s[i]=='.')
				{
				 i++;
				 for(k=0; isdigit(s[i+k])!=0; k++);
				 i=i+k;
				 for(m=-1; k!=0; m--, k--)
					t[j].cons=t[j].cons+((s[i-k]-48)*pow(10,m));
				}
			}
		 else if(s[i]=='('||s[i]==')')
			{
			 t[j].mode=2;
			 t[j].oper=s[i];
			 i=i+1;
			}
		 else
			{
			 t[j].mode=0;
			 t[j].oper=s[i];
			 i++;
			}
		}
	 t[j].mode=2;
	 t[j].oper=')';
	 j++;
	 for(i=0; i<j; i++)
		 copy(temp[i],t[j-i-1]);
	 //preorder sorting
	 for(i=0, k=0; i<j; i++)
		{
		 if(temp[i].mode==1)
			 {
			  copy(t[k], temp[i]);
			  k++;
			 }
		 else if(temp[i].mode==2)
			{
			 if(temp[i].oper==')')
				{
				 stack[l]=')';
				 l++;
				}
			 else
				{
				 do
					{
					 l--;
					 if(stack[l]!=')')
						{
						 t[k].mode=0;
						 t[k].oper=stack[l];
						 k++;
						}
					}while(stack[l]!=')');
				}
			}
		 else if(temp[i].oper=='^')
			{
			 stack[l]='^';
			 l++;
			}
		 else if(temp[i].oper=='*'|| temp[i].oper=='/')
			{
			 l--;
			 while(stack[l]=='^')
				{
				 t[k].mode=0;
				 t[k].oper=stack[l];
				 k++;
				 l--;
				}
			 l++;
			 stack[l]=temp[i].oper;
			 l++;
			}
		 else if(temp[i].oper=='+'|| temp[i].oper=='-')
			{
			 l--;
			 while(stack[l]!=')' && stack[l]!='+' && stack[l]!='-')
				{
				 t[k].mode=0;
				 t[k].oper=stack[l];
				 k++;
				 l--;
				}
			 l++;
			 stack[l]=temp[i].oper;
			 l++;
			}
		 else
			{
			 t[k].mode=0;
			 t[k].oper=temp[i].oper;
			 k++;
			}
		}
	 for(i=0; i<k; i++)
		 copy(temp[i],t[k-i-1]);
	 a=0;
	 b=k-1;
	 if(p==1)
		deriv(temp,a,b);
	 else
		y=rec(temp,a,b);
	 return y;
	}

float der(char s[75], float x)
	{
	 float y1, y2, y;
	 y1=draw(s,(x-0.00001));
	 y2=draw(s,(x+0.00001));
	 y=(y2-y1)/(0.00002);
	 return y;
	}

void rprin(struct node s[75], int& x, int& y)
	{
	 float b;
	 while(x<=y)
		{
		 if(s[x].mode==0)
			{
			 b=x;
			 if(s[x].oper=='+'||s[x].oper=='-'||s[x].oper=='*'||s[x].oper=='/'||s[x].oper=='^')
				{
				 x++;
				 printf("(");
				 rprin(s,x,y);
				 printf(")");
				 printf("%c(", s[b].oper);
				 rprin(s,x,y);
				 printf(")");
				 return;
				}
			 else
				{
				 if(s[x].oper=='S')
					printf("sin(");
				 else if(s[x].oper=='C')
					printf("cos(");
				 else if(s[x].oper=='T')
					printf("tan(");
				 else if(s[x].oper=='O')
					printf("cot(");
				 else if(s[x].oper=='A')
					printf("sec(");
				 else if(s[x].oper=='E')
					printf("cosec(");
				 else if(s[x].oper=='I')
					printf("asin(");
				 else if(s[x].oper=='N')
					printf("acos(");
				 else if(s[x].oper=='X')
					printf("atan(");
				 else if(s[x].oper=='Y')
					printf("acot(");
				 else if(s[x].oper=='Z')
					printf("asec(");
				 else if(s[x].oper=='W')
					printf("acosec(");
				 else if(s[x].oper=='Q')
					printf("sqrt(");
				 else if(s[x].oper=='L')
					printf("log(");
				 else if(s[x].oper=='G')
					printf("log10(");
				 x++;
				 rprin(s,x,y);
				 printf(")");
				 return;
				}
			}
		 else
			{
			 if(s[x].cons==8954)
				printf("x");
			 else
				printf("%f", s[x].cons);
			 x++;
			 return;
			}

		}
	}





void prin(struct node s[75], int x, int y)
	{
	 rprin(s,x,y);
	}

void deriv(struct node s[75], int& x, int& y)
	{
	 float b, c;
	 int i;
	 while(x<=y)
		{
		 if(s[x].mode==0)
			{
			 if(s[x].oper=='+')
				{
				 x++;
				 printf("(");
				 deriv(s,x,y);
				 printf(")");
				 printf("+");
				 printf("(");
				 deriv(s,x,y);
				 printf(")");
				}
			 else if(s[x].oper=='-')
				{
				 x++;
				 printf("(");
				 deriv(s,x,y);
				 printf(")");
				 printf("-");
				 printf("(");
				 deriv(s,x,y);
				 printf(")");
				}
			 else if(s[x].oper=='*')
				{
				 x++;
				 b=x;
				 printf("(");
				 deriv(s,x,y);
				 printf("*");
				 prin(s,x,y);
				 printf(")");
				 printf("+");
				 printf("(");
				 deriv(s,x,y);
				 printf("*");
				 prin(s,b,y);
				 printf(")");
				}
			 else if(s[x].oper=='/')
				{
				 x++;
				 b=x;
				 printf("((");
				 deriv(s,x,y);
				 printf("*");
				 prin(s,x,y);
				 printf(")-(");
				 prin(s,b,y);
				 printf("*");
				 b=x;
				 deriv(s,x,y);
				 printf("))/((");
				 prin(s,b,y);
				 printf(")^2)");
				}
			 else if(s[x].oper=='^')
				{
				 printf("(");
				 prin(s,x,y);
				 x++;
				 b=x;
				 printf("((");
				 deriv(s,x,y);
				 printf("*");
				 prin(s,x,y);
				 printf(")/(");
				 prin(s,b,y);
				 printf(")+(log ");
				 prin(s,b,y);
				 printf(")*");
				 deriv(s,x,y);
				 printf("))");
				}
			 else if(s[x].oper=='S')
				{
				 x++;
				 printf("cos(");
				 prin(s,x,y);
				 printf(")*");
				 deriv(s,x,y);
				}
			/* sin -- S         asin -- I
			   cos -- C         acos -- N
			   tan -- T         atan -- X
			   cot -- O         acot -- Y
			   sec -- A         asec -- Z
			   cosec -- E       acosec -- W
			   mod -- M
			   sqrt -- Q
			   log -- L
			   log10 -- G
			*/
			 else if(s[x].oper=='C')
				{
				 x++;
				 printf("(-sin(");
				 prin(s,x,y);
				 printf("))*");
				 deriv(s,x,y);
				}
			 else if(s[x].oper=='T')
				{
				 x++;
				 printf("(sec(");
				 prin(s,x,y);
				 printf("))^2*");
				 deriv(s,x,y);
				}
			 else if(s[x].oper=='O')
				{
				 x++;
				 printf("(-(cosec(");
				 prin(s,x,y);
				 printf("))^2)*");
				 deriv(s,x,y);
				}
			 else if(s[x].oper=='A')
				{
				 x++;
				 printf("tan(");
				 prin(s,x,y);
				 printf(")* sec(");
				 prin(s,x,y);
				 printf(")*");
				 deriv(s,x,y);
				}
			 else if(s[x].oper=='E')
				{
				 x++;
				 printf("(-cosec(");
				 prin(s,x,y);
				 printf("))* cot(");
				 prin(s,x,y);
				 printf(")*");
				 deriv(s,x,y);
				}
			 else if(s[x].oper=='I')
				{
				 x++;
				 printf("(1/(sqrt(1-(");
				 prin(s,x,y);
				 printf(")^2)))*");
				 deriv(s,x,y);
				}
			 else if(s[x].oper=='N')
				{
				 x++;
				 printf("(-1/(sqrt(1-(");
				 prin(s,x,y);
				 printf(")^2)))*");
				 deriv(s,x,y);
				}
			 else if(s[x].oper=='X')
				{
				 x++;
				 printf("(1/(1+(");
				 prin(s,x,y);
				 printf(")^2))*");
				 deriv(s,x,y);
				}
			 else if(s[x].oper=='Y')
				{
				 x++;
				 printf("(-1/(1+(");
				 prin(s,x,y);
				 printf(")^2))*");
				 deriv(s,x,y);
				}
			 else if(s[x].oper=='Z')
				{
				 x++;
				 printf("(1/(|");
				 prin(s,x,y);
				 printf("|*sqrt((");
				 prin(s,x,y);
				 printf(")^2-1)))*");
				 deriv(s,x,y);
				}
			 else if(s[x].oper=='W')
				{
				 x++;
				 printf("(-1/(|");
				 prin(s,x,y);
				 printf("|*sqrt((");
				 prin(s,x,y);
				 printf(")^2-1)))*");
				 deriv(s,x,y);
				}
			 else if(s[x].oper=='Q')
				{
				 x++;
				 printf("(1/(2*sqrt(");
				 prin(s,x,y);
				 printf(")))*");
				 deriv(s,x,y);
				}
			 else if(s[x].oper=='L')
				{
				 x++;
				 printf("(1/(");
				 prin(s,x,y);
				 printf("))*");
				 deriv(s,x,y);
				}
			 else if(s[x].oper=='G')
				{
				 x++;
				 printf("(1/(log(10)*(");
				 prin(s,x,y);
				 printf("))*");
				 deriv(s,x,y);
				}
			 return;
			}
		 else
			{
			 if(s[x].cons==8954)
				{
				 x++;
				 printf("1");
				 return;
				}
			 else
				{
				 printf("0");
				 x++;
				 return;
				}
			}
		}
	}


float closer(float a, float b)
	{
	 if(a<0)
		a=-a;
	 if(b<0)
		b=-b;
	 if(a<b)
		return a;
	 else
		return b;
	}


void main()
	{
	 int i, j, n, ch, a, b;
	 char o='y';
	 float x, x0, x1, x2, y0, y1, y2, y=0;
	 int gd=DETECT, gm, maxx, maxy, dig;
	 float stepx, stepy, mind, minr, maxd, maxr, ax, ay, xi[30], yi[10], integ=0.0;
	 char st[75];
	 clrscr();
	 printf("Input the equation:\n1. For writing ax^n, type:a*x^n\n2. Type: sin(x), e^x, mod(x), log(x), log10(x), sqrt(x) in this form only\n3. Always mention multiplication operator where required, like, x^(2*x)\n5. Use 'p' for pi\n6. Use asin, atan, acos, etc for inverse trigo fn\n   f(x)= ");
	 gets(st);
	 printf("\nInput the min and max values for domain: ");
	 scanf("%f %f", &mind, &maxd);
	 printf("\nInput the min and max values for range: ");
	 scanf("%f %f", &minr, &maxr);
	 while(o=='y')
	 {
	 clrscr();
	 printf("\n\n  1. Show Graph\n  2. Find X and Y intercepts only\n  3. Find slope(derivative) at a point\n  4. Find the value of fn for a given value\n  5. Find Definite Integral\n  6. Differentiate w.r.t. x (Note: Dont add mod fn)\nChoose: ");
	 scanf("%d", &ch);
	 clrscr();
	 initgraph(&gd, &gm, "c://turboc3//bgi");
	 maxx=getmaxx();
	 maxy=getmaxy();
	 stepx=(maxd-mind)/(maxx-1);
	 stepy=(maxr-minr)/(maxy-1);
	 switch(ch)
		{
		 case 1 :
			if((mind<0) && (maxd>0))
				{
				 ax=(0-mind)/stepx;
				 line(round(ax),0,round(ax),maxy);
				}
			if((minr<0) && (maxr>0))
				{
				 ay=(0-minr)/stepy;
				 line(0,round(maxy-ay),maxx,round(maxy-ay));
				}
			for(x=mind; x<=maxd; x=x+stepx)
				{
				 y=draw(st,x);
				 a=(x*maxx)/(maxd-mind);
				 b=(y*maxy)/(maxr-minr);
				 if((y>=minr) && (y<=maxr))
					putpixel(round(a+ax),round(maxy-ay-b), RED);
				}
			getch();
			closegraph();
			clrscr();
			break;
		 case 2:
			n=1;
			xi[0]=mind;
			for(x0=mind; x0<=maxd; x0=x0+stepx)
				{
				 x1=x0+stepx;
				 y0=draw(st,x0);
				 y1=draw(st,x1);
				 if((y0*y1)<0)
					{
					 if(y1<0)
						{
						 j=x0; x0=x1; x1=j;
						 j=y0; y0=y1; y1=j;
						}
					 for(i=0; i<30; i++)
						{
						 x2=((x0*y1)-(x1*y0))/(y1-y0);
						 y2=draw(st,x2);
						 if(y2<0)
							{
							 x0=x2;
							 y0=y2;
							}
						 else
							{
							 x1=x2;
							 y1=y2;
							}
						}
					}
				 else if((round(y0)*round(y1))==0)
					{
					 if(round(y0)==0 && round(x0)!=round(xi[n-1]) && closer(y0,draw(st,xi[n-1]))==y0)
						{
						if(n!=1)
							n--;
						x2=round(x0);}
					 else if(round(y1)==0 && round(x1)!=round(xi[n-1]) && closer(y1,draw(st,xi[n-1]))==y1)
						{
						if(n!=1)
							n--;
						x2=round(x1);
						}
					 else
						continue;
					}
				// else if((y0*y1)<0.2 && round(x0)!=round(xi[n-1]))
				  //	 x2=round(x0);
				 else
					continue;
				 xi[n]=x2; n++;
				}
			if(n!=1)
				{
				 printf("\nThe X intercepts are:\n");
				 for(i=1; i<n; i++)
					printf("%d. %f\n", i, xi[i]);
				}
			if(mind<0 && maxd>0)
				{
				 x=0;
				 yi[0]=draw(st,x);
				 printf("\nY intercept is at y=%f\n", yi[0]);
				}
			break;
		 case 3:
			printf("\nEnter the point you want to calculate derivative at:");
			scanf("%f", &x);
			y=der(st,x);
			printf("\nThe derivative is %f", y);
			break;
		 case 4:
			printf("\nEnter the point you want value of fn at:");
			scanf("%f", &x);
			y=draw(st, x);
			printf("\nThe value is: %f", y);
			break;
		 case 5:
			printf("Enter the boundary limits for the integral: ");
			scanf("%d %d", &a, &b);
			for(x=a; x<=b; x=x+stepx)
				{
				 y=draw(st,x);
				 if(y<0)
					y=0-y;
				 integ=integ+(y*stepx);
				}
			printf("The value of this definite integral is: %f", integ);
			break;
		 case 6:
			y=draw(st,x,1);
			getch();
			break;
		 default:
			printf("WRONG CHOICE");
			break;
		}
		printf("\nWanna continue?: ");
		fflush(stdin);
		scanf("%c", &o);
		}
	 closegraph();
	}

