# Filipe
/******************************************************************************

                            Online C Compiler.
                Code, Compile, Run and Debug C program online.
Write your code in this editor and press "Run" button to compile and execute it.

*******************************************************************************/

#include <stdio.h>
#include <math.h>
#include <stdlib.h>
#include <time.h>
# define max 16
typedef struct champ {
    int atk;
    int def ;
    int id ;
    int car;
    int life;
} champ;
int rd(){
    int soma,i ;
    soma =0;
        for(i=0;i<3;i++){
            soma += 1+ rand()%6;
       }

     
     return soma;
}
int carbonus(int carisma){
    int bonus;
   
    if (carisma == 18)
        bonus = 3;
        else if  (carisma >=16)
             bonus = 2;
            else if  (carisma >=14)
                 bonus = 1;
                else if  (carisma <=7)
                     bonus = -1;
                    else if  (carisma <=5)
                         bonus = -2;
                        else if  (carisma <=4)
                             bonus = - 3;
        
        else bonus = 0;
       // printf ("\n bonus  = %i",bonus );
        return bonus;
    }

void champe(champ *p,int id){
    int i , soma = 0;
    p->atk = rd();
    p->def = rd();
    p->id =id;
    p->car = rd();
    
    for(i=0;i<3;i++){
     soma += rd();
    }
    p-> life = soma;
      printf("\n boneco %d id %d",id,p->id );
    printf("\n  boneco %d atk %d",id,p->atk );
    printf("\n  boneco %d def %d",id,p->def );
    printf("\n boneco %d car %d",id,p->car );
    printf("\n  boneco %d vida %d ",id,p->life );
    
}
void criachamp (champ p[max]){
    int i;
    for (i=0;i<max;i++){
        champe(&p[i],i);
 
    }
}
void atk (champ *p1,champ *p2){
    int dano = rd() + p1-> atk + carbonus (p1->car );
    printf ("\ndano causado %d ",dano  );
    int escudo = rd() + p2-> def + carbonus (p2->car );
    printf ("\ndefesa executada %d ",escudo  );
    if (escudo>= dano){
         printf ("\n o atacante errou "  );
    }
    else p2->life += escudo - dano;
    printf ("\n vida restante do atacado %d",p2->life  );
}


int luta (champ *p1, champ *p2)

{
    
  printf( " \n******INICIO DA BATALHA***********");

    while ( p1->life > 0 && p2->life > 0 )
    {
              

        atk (p1,p2);
        if (p2->life <= 0)
        {
            return p1->id;
        }
        atk (p2,p1);
        if (p1->life <= 0)
        {
            return p2->id;
        }
    }
}


    
    
    
    
    

int main()
{   srand(time(NULL));
    int ide, camp [max], i,l;
    
    champ n [max];
     champ *pointer =n ;
    criachamp (n);
   // printf(" ***********************%d*********************  ", pointer-> life  );
 
      l=max;
       ide=0;
     for(i=0;i<l/2;i++){
            printf(" \n %d", ide);
            camp[i]  =  luta (&n[ide], &n[ide +1]);
        printf("\n o vencedor da luta entre  %d e %d foi: %d ", ide, ide +1,camp[i]);
        
        ide += 2;
    }
    l= l/2;
    
    while (l > 1){
ide = 0;
     for(i=0;i<l/2;i++){

         int s = camp[ide];

             camp[i]  =  luta (&n[camp[ide]], &n[camp[ide +1]]);
        printf("\n o vencedor da luta entre  %d e %d foi: %d ",s, camp [ide +1],camp[i]);
        
        ide += 2;
    }
    l= l/2;
    printf("\nlutadores restantes : %d", l);
    }
    printf("\n o GRANDE CAMPEÃO DO CAMPEONATO é: %d ", camp[0]);
    return 0;
    

    
}





