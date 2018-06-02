#include<stdio.h>
#include<stdlib.h>
#include<unistd.h>
#include<ncurses.h>

#define MAX 10

void impri(char matriz[MAX][MAX+1]);
void andar(char matriz[MAX][MAX+1],int l,int c,int det);

int main(void)
{
    initscr();
    start_color();
    init_pair(1,COLOR_RED,COLOR_BLACK);
    init_pair(2,COLOR_BLUE,COLOR_BLACK);

    char matriz[MAX][MAX+1] = { "##########",
                                "#x       #",
                                "# # # ## #",
                                "# # # ##C#",
                                "# # # ####",  /*labirinto de 10 por 11*/
                                "# ### #  #",
                                "#  #  ## #",
                                "# ### ## #",
                                "#   #    #",
                                "##########" };

   int det = 1;         /*so pra tirar um pequeno bug na hora de printar o "comecando"*/

   bkgd(COLOR_PAIR(1));
   printf("O objetivo do PC sera sair do ponto x do labirinto e chegar no ponto C");
   printf("                       tecle enter para continuar...");
   getchar();
   system("clear");

   int l = 1,c = 1;
   andar(matriz,l,c,det);

}
void andar(char matriz[MAX][MAX+1],int l,int c,int det) /*funcao para fazer o PC andar*/
{
    int teste = 0,x,y;

    if(det == 1)
    {
        printw("\n\n\nComeçando!\n");
        impri(matriz);
        det = 0; /*so pra quando ele voltar,e passar pela posicao onde começou,nao printar començando dnv*/
    }
    else
    impri(matriz);
    for(x = 1;x >= -1;x--) /*variacao da linha*/
    {
        for(y = 1;y >= -1;y--) /*variacao da coluna*/
        {                      /*condicoes nas quais ele nao deve fazer nd,apenas partir pra proxima possibilidade*//*essas ultimas sao as diagonais*/
            if(matriz[l+x][c+y] == '#'|| matriz[l+x][c+y] == 'T' || (l == 0 && y == 0)|| (x == 1 && (y == -1 || y == 1))|| (x == -1 && (y == -1 || y == 1)))
                continue;
            else
            {   if(matriz[l+x][c+y] == 'x') /*caso a posicao que o PC pretende ir tenha x*/
                {
                    if(matriz[l-1][c] != ' ' && matriz[l+1][c] != ' ' && matriz[l][c-1] != ' ' && matriz[l][c+1] != ' ')/*so pra saber se ele esta sem saida*/
                    {
                        if(x == -1 && y == 0) /*caso acima da posicao do PC tenha um x e o PC esteja sem saida*/
                        {
                            matriz[l][c] = 'T';
                            printw("\n\n\nVoltando\n");
                            teste = 1; /*so pra poder sair do laco da variacao da linha*/
                            break;
                        }
                        else
                        {
                            if(x == 0 && y == -1) /*caso ao lado esquerdo do PC tenha um x e o PC esteja sem saida*/
                            {
                                matriz[l][c] = 'T';
                                printw("\n\n\nVoltando\n");
                                teste = 1; /*so pra poder sair do laco da variacao da linha*/
                                break;
                            }
                            else
                            {
                                if(x == 0 && y == 1) /*caso a direita do PC esteja um x, e o PC esteja sem saida*/
                                {
                                    matriz[l][c] = 'T';
                                    printw("\n\n\nVoltando\n");
                                    teste = 1; /*so pra poder sair do laco da variacao da linha*/
                                    break;
                                }
                                else
                                {
                                    if(x == 1 && y == 0) /*caso abaixo do PC tenha um x, e el esteja sem saida*/
                                    {
                                        matriz[l][c] = 'T';
                                        printw("\n\n\nVoltando\n");
                                        teste = 1; /*so pra poder sair do laco da variacao da linha*/
                                        break;
                                    }
                                }
                            }
                        }
                    }
                    else
                        continue; /*caso tenha x e o PC nao esteja sem saida*/

                }
                else
                {
                    matriz[l+x][c+y] = 'x'; /*caso o caminho esteja livre, anda pra ele*/
                    printw("\n\n\nTentando (%d,%d)\n",l+x,c+y);
                    teste = 2; /*so pra poder sair do laco da variacao da linha*/
                    break;
                }
            }
        }
        if(teste == 1 || teste == 2) /*pra poder sair do laco da variacao da linha*/
            break;
        else
            continue;  /*roda o laco da variacao da linha*/


    }
    if((l+x) == 3 && (c+y) == 8) /*condicao para terminar o labirinto*/
    {
        impri(matriz);
        printw("\n\nTerminou!\n\n");
    }
    else
    {
        if(teste == 2)
            andar(matriz,l+x,c+y,det);
        else
        {                                   /*OBS:aparentemente é redundante essas duas chamadas de funcao, dps tentar com 1 apenas*/
            if(teste == 1)
                andar(matriz,l+x,c+y,det);
        }
    }

}
void impri(char matriz[MAX][MAX+1]) /*funcao para imprimir o labirinto*/
{
    int i,j;
    for(i = 0;i < MAX;i++)
    {
        for(j = 0;j < MAX+1;j++)
        {
            if(matriz[i][j] == 'T')
            {
                matriz[i][j] = ' ';
                printf(" %c",matriz[i][j]);
                matriz[i][j] = 'T';
            }
            else
            {
                bkgd(COLOR_PAIR(1));
                printf(" %c",matriz[i][j]);
            }
        }
        printf("\n");
    }
    printf("\n\n");
}
