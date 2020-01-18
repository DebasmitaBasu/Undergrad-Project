#include<conio.h>
#include<math.h>
#include<stdio.h>
#include<stdlib.h>


int main()
{
FILE *fp1,*fp2,*fp3,*fp,*fp4, *fp5;
int k,i,j,a,b,c,d,sum[50],s=0,index[5],r,w,q,count1,m,a2[2],z,paroff[5],best[5],mmm;
int len=0,k1,count,p,minsum,optindex[50],position_in_file,q1,temp1,temp2,t,x;
int gencount=0,gen,o,g,m1,cst[25][15],count2,position_in_file2,sumop[30],sumorg[50],r3,k3,e,count3,count4,position_in_file3,position_in_file4;
char A,B,C,D,E,num[50][50],n,mum[50][50],ch,n1;
char crs[50][50],temp[50],no,a1,ch1,n2,opt[30][30],ham[30][30];
int mut,mutcount,a3[5],mutparoff[10],mutbest[10],mutcount1,mutcount2,mutposition_in_file,mutposition_in_file2,invcount,a4[5],a44[2],invbest[10],invcount1,invcount2;
char modcity[30][30],inval[30][30],inv;
int modcst[30][30],mm,a22[2],a33[2],optsum[30],invposition_in_file,invposition_in_file2;
clrscr();

fp2=fopen("cost.txt","r");
fp1=fopen("efgh.txt","r");

if(NULL==fp2)
{
 printf("Cant open cost file for reading\n");
 exit(0);
 }
else if(NULL==fp1)
{
printf("Cant open city file for reading\n");
exit(0);
}

//reading each path and their correspondind cost:




for(i=0;i<24;i++)
{
for(j=0;j<4;j++)
{
fscanf(fp2,"%d",&cst[i][j]);
}
}


for(i=0;i<25;i++)
{
for(j=0;j<10;j++)
{
if((n=getc(fp1))!=EOF)
num[i][j]=n;
else
continue;
}
}
fclose(fp1);
fclose(fp2);


fp2=fopen("cost.txt","r");

for(i=0;i<24;i++)
{
a=b=c=d=0;
fscanf(fp1,"%c %c %c %c %c\n", &A, &B , &C, &D, &E);
fscanf(fp2,"%d %d %d %d\n",&a,&b,&c,&d);
sumorg[i]=a+b+c+d;
//printf("Cost for route: %c->%c->%c->%c->%c is %d\r\n",A,B,C,D,E,sum[i]);
}

fclose(fp2);

//sum of cost of all paths:

for(i=0;i<24;i++)
{
  s=sumorg[i]+s;
}
printf("total sum:%d\n",s);


//min cost path:

minsum=sumorg[0];
for(i=1;i<24;i++)
{
if(sumorg[i]<minsum)
minsum=sumorg[i];
}
printf("minsum=%d\n",minsum);
//printf("optimal index:");
j=0;
for(i=0;i<24;i++)
{
if(sumorg[i]==minsum)
{
optindex[j]=i;
//printf("%d\t",optindex[j]);
j++;
}
}

printf("enter number of generation:");
scanf("%d",&gen);

randomize();

while(gencount<gen)
{

//Reading updated cost from cost1::

fp3=fopen("cost1.txt","r");
for(i=0;i<24;i++)
{
for(j=0;j<4;j++)
{
fscanf(fp3,"%d",&modcst[i][j]);
}
}
fclose(fp3);

fp3=fopen("cost1.txt","r");

for(i=0;i<24;i++)
{
a=b=c=d=0;
fscanf(fp2,"%d %d %d %d\n",&a,&b,&c,&d);
sum[i]=a+b+c+d;
//sum[i]=sumorg[i];
//printf("Cost for route: %c->%c->%c->%c->%c is %d\r\n",A,B,C,D,E,sum[i]);
}
fclose(fp3);

//Reading updated city from city1::

 fp1=fopen("city1.txt","r");
  for(i=0;i<24;i++)
 {
  for(j=0;j<10;j++)
 {
  if((n=getc(fp1))!=EOF)
  {
  modcity[i][j]=n;
  }
  else
   continue;
 }
 }

fclose(fp1);






//selecting any two random index values::--->1.selection(roulette wheel)


 for(w=0;w<=1;w++)
{
r=rand()%24+1;
k=ceil(s/r);
//printf("r=%d\n",r);
//printf("k=%d\n",k);
index[w]=(k%24);
printf("\npicked index=%d\n",index[w]);

}

/*for(w=0;w<=1;w++)
{
//display the selected path:
fp1=fopen("C:\\Tc\\BIN\\efgh.txt","r");

for(i=0;i<25;i++){
for(j=0;j<10;j++){
if((n=getc(fp1))!=EOF)
num[i][j]=n;
else
continue;
}
}*/
q=index[w];
for(j=0;j<10;j++)
{
printf("%c",modcity[q][j]);
//fclose(fp1);
}


//2.crossover:

//choosing position for crossover:

k1=rand()%5;
printf("\ncrsover pos=%d\n",k1);

for(w=0;w<=1;w++)
{
for(j=0;j<10;j++)
{
q=index[w];
crs[w][j]=modcity[q][j];
}
crs[w][j-1]='\0';
}

//length of array:
w=0;
len=0;
while(crs[0][w]!='\0')
{
len++;
w++;
}
 printf("length=%d\n",len-1);
k1=k1*2;

for(j=0;j<10;j++)
{
if(j==k1)
{
temp[j]=crs[0][j];
crs[0][j]=crs[1][j];
crs[1][j]=temp[j];
k1++;
}
}

//printing crossover offsprings

 printf("crossover offspring1:\n");
 for(j=0;j<10;j++)
 {
   printf("%c",crs[0][j]);

 }
   printf("\n");

  printf("\ncrossover offspring2:\n");
   for(j=0;j<10;j++)
   {
   printf("%c",crs[1][j]);

   }
 printf(" %d\t%d\n",index[0],index[1]);

   /*  fp1=fopen("efgh.txt","r");
  for(i=0;i<24;i++)
 {
  for(j=0;j<10;j++)
 {
  if((n=getc(fp1))!=EOF)
  {
  num[i][j]=n;
  }
  else
   continue;
 }
 }

fclose(fp1); */


/*fp3=fopen("cost.txt","r");
for(i=0;i<24;i++)
{
for(j=0;j<4;j++)
{
fscanf(fp3,"%d",&cst[i][j]);
}
}

fclose(fp3);*/

/*for(i=0;i<24;i++)
{
for(j=0;j<4;j++)
{
printf("%d\t",cst[i][j]);
}
printf("\n");
} */


 //crossover checking:
count=0;
for(i=0;i<=1;i++)
{
if(crs[i][0]==crs[i][len-1])
{
 for(j=0;j<(len-1);j++)
 {
 for(w=j+1; w<(len-1);w++)
 {
 if(j%2==0 && w%2==0)
 {
  if(crs[i][j]==crs[i][w])
  {
  count++;
  }
  }
  }
}
if(count>0)
  {
  printf("\ninvalid path::\n");
 // printf("goto nxt gen after invalid crsover\n");
  //break;
 // printf("\t%d",count);

printf("\nDo boundary mutation:");

for(j=0;j<10;j++)
 inval[i][j]=crs[i][j];




 printf("\nEnter 1 for A,2 for B, 3 for C,4 for D\n");

printf("\nEnter user choice:\n");

scanf("%d",&inv);



switch(inv)
{
case 1:
inval[i][0]='A';
inval[i][len-1]='A';
break;
case 2:
inval[i][0]='B';
inval[i][len-1]='B';
break;
case 3:
inval[i][0]='C';
inval[i][len-1]='C';
break;
case 4:
inval[i][0]='D';
inval[i][len-1]='D';
break;
default:
printf("\n wrong choice\n");
break;


}




  for(j=0;j<10;j++)
 printf("%c",inval[i][j]);
 invcount=0;

  for(j=0;j<(len-2);j++)
 {
 for(w=j+1; w<(len-2);w++)
 {
 if(j%2==0 && w%2==0)
 {
  if(inval[i][j]==inval[i][w])
  {
  invcount++;
  }
  }
  }
}
if(invcount>0)
  {
  printf("\ninvalid path again:rejected:\n");
 // printf("\t%d",count);
// printf("goto next generation\n");
// break;
  }
else
{

//check whether child is better than parent or not::
//finding original index of mutated child from efgh:

 for(j=0;j<24;j++)
   {
    for(w=0;w<10;w++)
    {

    if(w%2==0)
    {
      if(num[j][w]==inval[i][w])
      {
       mmm=1;


      }
      else
      {
       mmm=0;
       break;
      }
    }
    }
  if(mmm==1)
  {
   a4[i]=j;
   printf("\nmatched index of modchild inv=%d\n",a4[i]);
   break;
  }

   }


   //finding original index of parent from efgh:

   for(j=0;j<24;j++)
   {
    for(w=0;w<10;w++)
    {

    if(w%2==0)
    {
      if(num[j][w]==modcity[index[i]][w])
      {
       mmm=1;


      }
      else
      {
       mmm=0;
       break;
      }
    }
    }
  if(mmm==1)
  {
   a44[i]=j;
   printf("\nmatched index modparent inv=%d\n",a44[i]);
   break;
  }

   }
//if(i==1)
//{
 printf("\n after boundary mutation\n");

//printf("\nlets see: %d",i);
/*mutparoff[0]=sumorg[a33[0]];
mutparoff[1]=sumorg[a33[1]];
mutparoff[2]=sumorg[a33[0]];
mutparoff[3]=sumorg[a3[1]];
mutbest[0]=a33[0];
mutbest[1]=a33[1];
mutbest[2]=a3[0];
mutbest[3]=a3[1];


for(t=0;t<3;t++)
{
 for(x=0;x<4-t-1;x++)
 {
  if(mutparoff[x]>mutparoff[x+1])
  {
  temp1=mutparoff[x];
  temp2=mutbest[x];
  mutparoff[x]=mutparoff[x+1];
  mutbest[x]=mutbest[x+1];
  mutparoff[x+1]=temp1;
  mutbest[x+1]=temp2;
  }
 }
}*/

if(sumorg[a44[i]]>sumorg[a4[i]])
invbest[i]=a4[i];
else if(sumorg[a4[i]]>sumorg[a44[i]])
invbest[i]=a44[i];
else
invbest[i]=a44[i];


//printf("\n%d %d %d %d\n",mutparoff[0],mutparoff[1],mutparoff[2],mutparoff[3]);
//printf("\n%d %d %d %d\n",mutbest[0],mutbest[1],mutbest[2],mutbest[3]);
//printf("\n %d %d %d %d\n",mutparoff[0],mutparoff[1],mutbest[0],mutbest[1]);

printf("\nafter b.mutation better index=%d\t",invbest[i]);



// for(o=0;o<=1;o++)
  //{
  printf("\noverwrite after b.mutation:");

   // writing offsprings over parents in initial pool:
   fp=fopen("city1.txt","r+");
   fp2=fopen("cost1.txt","r+");
   invcount1=0;
   invcount2=0;

   while(invcount1!=index[i])
   {
    if((ch = fgetc(fp)) == '\n')
    invcount1++;
   }

   while(invcount2!=index[i])
   {

    if((ch1=fgetc(fp2))=='\n')
    invcount2++;

   }





   // Store the position
   invposition_in_file = ftell(fp);
   invposition_in_file2=ftell(fp2);

   printf("current pos=%d\t%d\n",invposition_in_file,invposition_in_file2);
   // Reposition it
   fseek(fp,invposition_in_file,SEEK_SET); // Or fseek(file,ftell(file),SEEK_SET);
   fseek(fp2,invposition_in_file2,SEEK_SET);



   for(w=0;w<len;w++)
   {
    fprintf(fp, "%c",num[invbest[i]][w]);

   }
   fprintf(fp,"\n");


   for(w=0;w<4;w++)
   {
   if(w<3)
   fprintf(fp2,"%d\t",cst[invbest[i]][w]);
   else
   fprintf(fp2,"%d",cst[invbest[i]][w]);
   }
    fprintf(fp2,"\n");

/* for(i=0;i<24;i++)
{
a=b=c=d=0;
fscanf(fp2,"%d %d %d %d\n",&a,&b,&c,&d);
sum[i]=a+b+c+d;
//printf("Cost for route: %c->%c->%c->%c->%c is %d\r\n",A,B,C,D,E,sum[i]);
} */


   fclose(fp);
   fclose(fp2);
   //}


//}

  }
}

  else if(count==0)
{
    //checking if offsprings produced are better than parent or not:

    //finding original index of child;

   for(j=0;j<24;j++)
   {
    for(w=0;w<10;w++)
    {

    if(w%2==0)
    {
      if(num[j][w]==crs[i][w])
      {
       m=1;

      }
      else
      {
       m=0;
       break;
      }
    }
    }
  if(m==1)
  {
   a2[i]=j;
   printf("\nmatched index of modchild crs=%d\n",a2[i]);
   break;
  }

   }
//q1=index[i];
//z=a2[i];


  //finding original index of parent:


  for(j=0;j<24;j++)
   {
    for(w=0;w<10;w++)
    {

    if(w%2==0)
    {
      if(num[j][w]==modcity[index[i]][w])
      {
       m=1;

      }
      else
      {
       m=0;
       break;
      }
    }
    }
  if(m==1)
  {
   a22[i]=j;
   printf("\nmatched indiex of modparent crs=%d\n",a22[i]);
   break;
  }

   }



/*if(i==1)
{
//printf("\nlets see: %d",i);
paroff[i]=sumorg[a22[i]];
paroff[1]=sumorg[a22[1]];
paroff[i]=sumorg[a2[i]];
paroff[3]=sumorg[a2[1]];
best[i]=a22[i];
best[1]=a22[1];
best[i]=a2[i];
best[3]=a2[1];


for(t=0;t<3;t++)
{
 for(x=0;x<4-t-1;x++)
 {
  if(paroff[x]>paroff[x+1])
  {
  temp1=paroff[x];
  temp2=best[x];
  paroff[x]=paroff[x+1];
  best[x]=best[x+1];
  paroff[x+1]=temp1;
  best[x+1]=temp2;
  }
 }
}*/


if(sumorg[a22[i]]>sumorg[a2[i]])
best[i]=a2[i];
else if(sumorg[a2[i]]>sumorg[a22[i]])
best[i]=a22[i];
else
best[i]=a22[i];

//printf("\n%d %d %d %d\n",paroff[0],paroff[1],paroff[2],paroff[3]);

//printf("\n%d %d %d %d\n",best[0],best[1],best[2],best[3]);

//printf("\n %d %d %d %d\n",paroff[0],paroff[1],best[0],best[1]);

printf("\n better index after crsovr=%d\t",best[i]);

//for(o=0;o<=1;o++)
  //{
  printf("\noverwrite:");

   // writing offsprings over parents in initial pool:
   fp=fopen("city1.txt","r+");
   fp2=fopen("cost1.txt","r+");
   count1=0;
   count2=0;

   while(count1!=index[i])
   {
    if((ch = fgetc(fp)) == '\n')
    count1++;
   }

   while(count2!=index[i])
   {

    if((ch1=fgetc(fp2))=='\n')
    count2++;

   }





   // Store the position
   position_in_file = ftell(fp);
   position_in_file2=ftell(fp2);

   printf("current pos=%d\t%d\n",position_in_file,position_in_file2);
   // Reposition it
   fseek(fp,position_in_file,SEEK_SET); // Or fseek(file,ftell(file),SEEK_SET);
   fseek(fp2,position_in_file2,SEEK_SET);



   for(w=0;w<len;w++)
   {
    fprintf(fp, "%c",num[best[i]][w]);

   }
   fprintf(fp,"\n");


   for(w=0;w<4;w++)
   {
   if(w<3)
   fprintf(fp2,"%d\t",cst[best[i]][w]);
   else
   fprintf(fp2,"%d",cst[best[i]][w]);
   }
    fprintf(fp2,"\n");

/* for(i=0;i<24;i++)
{
a=b=c=d=0;
fscanf(fp2,"%d %d %d %d\n",&a,&b,&c,&d);
sum[i]=a+b+c+d;
//printf("Cost for route: %c->%c->%c->%c->%c is %d\r\n",A,B,C,D,E,sum[i]);
} */


   fclose(fp);
   fclose(fp2);
   //}
// }

}
}
 else {
 printf("\nnot hamiltonian cycle:do boundary mutation:");

 for(j=0;j<10;j++)
 ham[i][j]=crs[i][j];




 printf("\nEnter 1 for A,2 for B, 3 for C,4 for D\n");

printf("\nEnter user choice:\n");

scanf("%d",&mut);



switch(mut)
{
case 1:
ham[i][0]='A';
ham[i][len-1]='A';
break;
case 2:
ham[i][0]='B';
ham[i][len-1]='B';
break;
case 3:
ham[i][0]='C';
ham[i][len-1]='C';
break;
case 4:
ham[i][0]='D';
ham[i][len-1]='D';
break;
default:
printf("\n wrong choice\n");
break;


}




  for(j=0;j<10;j++)
 printf("%c",ham[i][j]);
 mutcount=0;

  for(j=0;j<(len-2);j++)
 {
 for(w=j+1; w<(len-2);w++)
 {
 if(j%2==0 && w%2==0)
 {
  if(ham[i][j]==ham[i][w])
  {
  mutcount++;
  }
  }
  }
}
if(mutcount>0)
  {
  printf("\ninvalid path again:rejected:\n");
 // printf("\t%d",count);
// printf("goto next generation\n");
// break;
  }
else
{

//check whether child is better than parent or not::
//finding original index of mutated child from efgh:

 for(j=0;j<24;j++)
   {
    for(w=0;w<10;w++)
    {

    if(w%2==0)
    {
      if(num[j][w]==ham[i][w])
      {
       mm=1;


      }
      else
      {
       mm=0;
       break;
      }
    }
    }
  if(mm==1)
  {
   a3[i]=j;
   printf("\nmatched index h=%d\n",a3[i]);
   break;
  }

   }


   //finding original index of parent from efgh:

   for(j=0;j<24;j++)
   {
    for(w=0;w<10;w++)
    {

    if(w%2==0)
    {
      if(num[j][w]==modcity[index[i]][w])
      {
       mm=1;


      }
      else
      {
       mm=0;
       break;
      }
    }
    }
  if(mm==1)
  {
   a33[i]=j;
   printf("\nmatched index h=%d\n",a33[i]);
   break;
  }

   }
//if(i==1)
//{
 printf("\n after boundary mutation\n");

//printf("\nlets see: %d",i);
/*mutparoff[0]=sumorg[a33[0]];
mutparoff[1]=sumorg[a33[1]];
mutparoff[2]=sumorg[a33[0]];
mutparoff[3]=sumorg[a3[1]];
mutbest[0]=a33[0];
mutbest[1]=a33[1];
mutbest[2]=a3[0];
mutbest[3]=a3[1];


for(t=0;t<3;t++)
{
 for(x=0;x<4-t-1;x++)
 {
  if(mutparoff[x]>mutparoff[x+1])
  {
  temp1=mutparoff[x];
  temp2=mutbest[x];
  mutparoff[x]=mutparoff[x+1];
  mutbest[x]=mutbest[x+1];
  mutparoff[x+1]=temp1;
  mutbest[x+1]=temp2;
  }
 }
}*/

if(sumorg[a33[i]]>sumorg[a3[i]])
mutbest[i]=a3[i];
else if(sumorg[a3[i]]>sumorg[a33[i]])
mutbest[i]=a33[i];
else
mutbest[i]=a33[i];


//printf("\n%d %d %d %d\n",mutparoff[0],mutparoff[1],mutparoff[2],mutparoff[3]);
//printf("\n%d %d %d %d\n",mutbest[0],mutbest[1],mutbest[2],mutbest[3]);
//printf("\n %d %d %d %d\n",mutparoff[0],mutparoff[1],mutbest[0],mutbest[1]);

printf("\nafter b.mutation better index=%d\t",mutbest[i]);



// for(o=0;o<=1;o++)
  //{
  printf("\noverwrite after b.mutation:");

   // writing offsprings over parents in initial pool:
   fp=fopen("city1.txt","r+");
   fp2=fopen("cost1.txt","r+");
   mutcount1=0;
   mutcount2=0;

   while(mutcount1!=index[i])
   {
    if((ch = fgetc(fp)) == '\n')
    mutcount1++;
   }

   while(mutcount2!=index[i])
   {

    if((ch1=fgetc(fp2))=='\n')
    mutcount2++;

   }





   // Store the position
   mutposition_in_file = ftell(fp);
   mutposition_in_file2=ftell(fp2);

   printf("current pos=%d\t%d\n",mutposition_in_file,mutposition_in_file2);
   // Reposition it
   fseek(fp,mutposition_in_file,SEEK_SET); // Or fseek(file,ftell(file),SEEK_SET);
   fseek(fp2,mutposition_in_file2,SEEK_SET);



   for(w=0;w<len;w++)
   {
    fprintf(fp, "%c",num[mutbest[i]][w]);

   }
   fprintf(fp,"\n");


   for(w=0;w<4;w++)
   {
   if(w<3)
   fprintf(fp2,"%d\t",cst[mutbest[i]][w]);
   else
   fprintf(fp2,"%d",cst[mutbest[i]][w]);
   }
    fprintf(fp2,"\n");

/* for(i=0;i<24;i++)
{
a=b=c=d=0;
fscanf(fp2,"%d %d %d %d\n",&a,&b,&c,&d);
sum[i]=a+b+c+d;
//printf("Cost for route: %c->%c->%c->%c->%c is %d\r\n",A,B,C,D,E,sum[i]);
} */


   fclose(fp);
   fclose(fp2);
   //}


//}
}





}
}




/*//Mutation:



fp1=fopen("city1.txt","r");

for(i=0;i<24;i++)
{
for(j=0;j<10;j++)
{
if((n1=fgetc(fp1))!=EOF)
mum[i][j]=n1;
else
continue;
}
}
fclose(fp1);

r3=rand()%24+1;
//k=ceil(s/r);
//printf("r=%d\n",r);
//printf("k=%d\n",k);
//index[w]=(k%24);
printf("\npicked index=%d\n",r3);

printf("\n route selected for mutation:\n");

for(j=0;j<10;j++)
printf("%c",mum[r3][j]);

k3=rand()%5;
k3=(k3*2);
printf("\nSelected position for mutation: %d\n",k3);

printf("\nEnter 1 for A,2 for B, 3 for C,4 for D\n");

printf("\nEnter user choice:\n");

scanf("%d",&e);



switch(e)
{
case 1:
mum[r3][k3]='A';
break;
case 2:
mum[r3][k3]='B';
break;
case 3:
mum[r3][k3]='C';
break;
case 4:
mum[r3][k3]='D';
break;
default:
printf("\n wrong choice\n");
break;


}


for(j=0;j<10;j++)
printf("%c",mum[r3][j]);

//checking for mutation:


if(mum[r3][0]==mum[r3][len-1])
{
 for(j=0;j<(len-1);j++)
 {
 for(w=j+1; w<(len-1);w++)
 {
 if(j%2==0 && w%2==0)
 {
  if(mum[r3][j]==mum[r3][w])
  {
  count++;
  }
  }
  }
}
if(count>0)
  {
  printf("\nmutated invalid path:\n");
 // printf("\t%d",count);

  }

  else if(count==0)
{
    //writing mutated path to pool:

    printf("overwrite mutated path:");

    fp4=fopen("city1.txt","r+");
    fp5=fopen("cost1.txt","r+");
    count3=0;
    count4=0;

   while(count3!=r3)
   {
    if((ch = fgetc(fp4)) == '\n')
    count3++;
   }

   while(count4!=r3)
   {

    if((ch1=fgetc(fp5))=='\n')
    count4++;

   }





   // Store the position
   position_in_file3 = ftell(fp4);
   position_in_file4=ftell(fp5);

   printf("current pos=%d\t%d\n",position_in_file3,position_in_file4);
   // Reposition it
   fseek(fp4,position_in_file3,SEEK_SET); // Or fseek(file,ftell(file),SEEK_SET);
   fseek(fp5,position_in_file4,SEEK_SET);

    for(w=0;w<len;w++)
   {
    fprintf(fp4, "%c",mum[r3][w]);

   }
   fprintf(fp,"\n");

   fp=fopen("efgh.txt","r");

   for(j=0;j<24;j++)
   {
    for(w=0;w<10;w++)
    {

    if(w%2==0)
    {
      if(num[j][w]==mum[r3][w])
      {
       m1=1;

      }
      else
      {
       m1=0;
       break;
      }
    }
    }
  if(m1==1)
  {
   g=j;
   printf("\nmatched indicesin mutation z=%d\n",g);
   break;
  }

   }

  fclose(fp);

   for(w=0;w<4;w++)
   {
   if(w<3)
   fprintf(fp5,"%d\t",cst[g][w]);
   else
   fprintf(fp5,"%d",cst[g][w]);
   }
    fprintf(fp5,"\n");

   fclose(fp4);
   fclose(fp5);


}
}
 else {
 printf("\nmutated route isnt a hamiltonian cycle\n");
}

    */




//Storing each generation:


fp2=fopen("cost1.txt","r");


for(i=0;i<24;i++)
{
a=b=c=d=0;
fscanf(fp2,"%d %d %d %d\n",&a,&b,&c,&d);
optsum[i]=a+b+c+d;
//printf("Cost for route: %c->%c->%c->%c->%c is %d\r\n",A,B,C,D,E,sum[i]);
}
fclose(fp2);

fp1=fopen("city1.txt","r");

for(i=0;i<24;i++)
{
for(j=0;j<10;j++)
{
if((n2=getc(fp1))!=EOF)
opt[i][j]=n2;
else
continue;
}
}
fclose(fp1);


/*for(i=0;i<24;i++)
{
for(j=0;j<10;j++)
{
printf("%c",opt[i][j]);
}
printf("\n");
} */


if(fp1==NULL)
{
printf("\nCannot open file for reading:\n");
exit(0);
}
fp=fopen("genop.txt","a");
if(fp==NULL)
{
printf("\nCannot find file for writing");
fclose(fp1);
exit(0);
}
for(i=0;i<24;i++)
{
for(j=0;j<9;j++)
{
fprintf(fp,"%c",opt[i][j]);
}
fprintf(fp,"\t%d\n",optsum[i]);
}

fprintf(fp,"\n\n");

fclose(fp);

gencount++;
}



getch();
return 0;
}

