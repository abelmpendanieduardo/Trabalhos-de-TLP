# Trabalhos-de-TLP
Trabalhos feitos com C
#include<stdio.h>
#include<stdlib.h>
#include <locale.h>
#include <time.h>

#define BLUE(char) "\x1b[36m" char "\x1b[0m"
#define RED(char) "\x1b[31m" char "\x1b[0m"
#define GREEN(char) "\x1b[32m" char "\x1b[0m"
#define Yellow(char) "\x1b[33m" char "\x1b[0m"


void inicializarTabuleiro(char tabuleiro[3][3]) {
    int i, j;
    for (i = 0; i < 3; i++) {
        for (j = 0; j < 3; j++) {
            tabuleiro[i][j] = ' ';
        }
    }
}

void exibirTabuleiro(char tabuleiro[3][3]) {
    int i, j;
    printf("\n  0   1   2\n\n");
    for (i = 0; i < 3; i++) {
        for (j = 0; j < 3; j++) {
            printf(RED(" %c "), tabuleiro[i][j]);
            if (j < 2) {
                printf("|");
            }
        }
        printf("  %d\n",i);
        if (i < 2) {
            printf("------------\n");
        }
    }

}

int verificarVencedor(char tabuleiro[3][3]) {
    int j, i;
    for (i = 0; i < 3; i++) {
        if (tabuleiro[i][0] == 'X' && tabuleiro[i][1] == 'X' && tabuleiro[i][2] == 'X') {
            return 1;
        }
        if (tabuleiro[i][0] == 'O' && tabuleiro[i][1] == 'O' && tabuleiro[i][2] == 'O') {
            return 2;
        }
    }

    for (j = 0; j < 3; j++) {
        if (tabuleiro[0][j] == 'X' && tabuleiro[1][j] == 'X' && tabuleiro[2][j] == 'X') {
            return 1;
        }
        if (tabuleiro[0][j] == 'O' && tabuleiro[1][j] == 'O' && tabuleiro[2][j] == 'O') {
            return 2;
        }
    }

    if ((tabuleiro[0][0] == 'X' && tabuleiro[1][1] == 'X' && tabuleiro[2][2] == 'X') ||
            (tabuleiro[0][2] == 'X' && tabuleiro[1][1] == 'X' && tabuleiro[2][0] == 'X')) {
        return 1;
    }

    if ((tabuleiro[0][0] == 'O' && tabuleiro[1][1] == 'O' && tabuleiro[2][2] == 'O') ||
            (tabuleiro[0][2] == 'O' && tabuleiro[1][1] == 'O' && tabuleiro[2][0] == 'O')) {
        return 2;
    }

    return 0;
}

int tabuleiroCheio(char tabuleiro[3][3]) {
    int i, j;
    for (i = 0; i < 3; i++) {
        for (j = 0; j < 3; j++) {
            if (tabuleiro[i][j] == ' ') {
                return 0;
            }
        }
    }
    return 1;
}

void fazerJogadaDoCPU(char tabuleiro[3][3]) {
    int linha, coluna;

    do {
        linha = rand() % 3;
        coluna = rand() % 3;
    } while (tabuleiro[linha][coluna] != ' ');

    tabuleiro[linha][coluna] = 'O';
}
int main()
{
    int linha, coluna;
    srand(time(NULL));

    char mat[3][3];
    int l, c, op, a, b, opcao;
    int jogador, vencedor, vezes;

    system ("color f0");
    setlocale (LC_ALL,"portuguese");

    do {

        printf(GREEN("\t\t\t\tBEM-VINDO AO JOGO DA VELHA\n\n\n"));
        printf(GREEN("MENU PRINCIPAL\n"));
        printf("-----------------------\n");
        printf(BLUE("0. Jogar a dois\n"));
        printf(BLUE("1. Jogar com Computador\n"));
        printf(BLUE("2. Sair do Jogo\n"));
        printf("-----------------------\n");
        scanf("%i",&op);

        system("cls");

        if(op == 0) {
            do {
                jogador = 1;
                vencedor = 0;
                vezes = 0;
                for( l = 0; l < 3; l++) {
                    for( c = 0; c < 3; c++) {
                        mat[l][c] = ' ';
                    }
                }


                do {
                    printf("\t\tJOGO DA VELHA\n\n");
                    printf("  0   1   2\n\n");
                    for( l = 0; l < 3; l++) {
                        for( c = 0; c < 3; c++) {
                            printf(BLUE(" %c"),mat[l][c]);

                            if(c < 2)
                                printf(Yellow(" | "));
                            if(c == 2)
                                printf("  %d ",l);

                        }

                        if(l < 2)
                            printf(Yellow("\n-------------"));


                        printf("\n");
                    }


                    do {
                        do {
                            printf("\n\nJogador %d, insira a linha e coluna (0-2): ",jogador);
                            scanf("%d",&a);
                            scanf("%d",&b);
                        } while(a > 2 || a < 0 || b > 2 || b < 0) ;
                    } while(mat[a][b] != ' ');


                    if(jogador == 1) {
                        mat[a][b] = 'X';
                        jogador++;
                    } else {
                        mat[a][b] = 'O';
                        jogador = 1;
                    }

                    vezes++;
                    system("cls");
                    for(l = 0; l < 3; l++) {
                        if(mat[l][0] == 'X' && mat[l][1] == 'X' && mat[l][2] == 'X') {
                            vencedor = 1;
                        }
                    }

                    for(l = 0; l < 3; l++) {
                        if(mat[l][0] == 'O' && mat[l][1] == 'O' && mat[l][2] == 'O') {
                            vencedor = 2;
                        }
                    }

                    for(c = 0; c < 3; c++) {
                        if(mat[0][c] == 'X' && mat[1][c] == 'X' && mat[2][c] == 'X') {
                            vencedor = 1;
                        }
                    }

                    for(c = 0; c < 3; c++) {
                        if(mat[0][c] == 'O' && mat[1][c] == 'O' && mat[2][c] == 'O') {
                            vencedor = 2;
                        }
                    }

                    if(mat[0][0] == 'X' && mat[1][1] == 'X' && mat[2][2] == 'X')
                        vencedor = 1;

                    if (mat[0][0] == 'O' && mat[1][1] == 'O' && mat[2][2] == 'O')
                        vencedor = 2;

                    if(mat[0][2] == 'X' && mat[1][1] == 'X' && mat[2][0] == 'X')
                        vencedor = 1;

                    if(mat[0][2] == 'O' && mat[1][1] == 'O' && mat[2][0] == 'O')
                        vencedor = 2;
                } while(vencedor == 0 && vezes < 9);


                printf("\tJOGO DA VELHA\n\n");
                printf("  0   1   2\n");
                printf("-------------\n");

                for( l = 0; l < 3; l++) {
                    for( c = 0; c < 3; c++) {
                        printf(" %c",mat[l][c]);

                        if(c < 2)
                            printf(" | ");
                        if(c == 2)
                            printf("  %d",l);
                    }

                    if(l < 2)
                        printf("\n-------------");


                    printf("\n");
                }
                printf("-------------\n");

                if(vencedor == 1)
                    printf("\nParab�ns Jogador 1, voc� ganhou o jogo...");

                if(vencedor == 2)
                    printf("\nParab�ns Jogador 2, voc� ganhou o jogo...");

                if(vencedor == 0)
                    printf("\nHouve um empate, ningu�m ganhou...");

                printf("\n\nDigite 1 para jogar Novamente...\nOu qualquer outro digito para  voltar  ao  MENU PRINCIPAL...\n");
                scanf("%d",&opcao);
                system("cls");
            } while(opcao == 1);


        }
        else if(op == 1) {

            do {
                inicializarTabuleiro(mat);
                jogador = 1;
                vencedor = 0;

                do {
                    printf("\t\tJOGO DA VELHA\n\n");
                    exibirTabuleiro(mat);

                    if (jogador == 1) {
                        do {
                            printf("\nJogador 1 (X), insira a linha e coluna (0-2): ");
                            scanf("%d %d", &linha, &coluna);
                            if (mat[linha][coluna] == ' ') {
                                mat[linha][coluna] = 'X';
                                jogador = 2;
                            }
                            system("cls");
                            printf("\t\tJOGO DA VELHA\n\n");
                            exibirTabuleiro(mat);
                        } while(linha > 2 || linha < 0 || coluna > 2 || coluna < 0);
                    }
                    else {
                        fazerJogadaDoCPU(mat);
                        jogador = 1;
                    }
                    system("cls");

                    vencedor = verificarVencedor(mat);

                    if (vencedor == 1) {
                        printf("\t\tJOGO DA VELHA\n\n");
                        exibirTabuleiro(mat);
                        printf("Jogador 1 (X) venceu!\n");
                    } else if (vencedor == 2) {
                        exibirTabuleiro(mat);
                        printf("Jogador 2 (O) venceu (CPU)!\n");
                    } else if (tabuleiroCheio(mat)) {
                        exibirTabuleiro(mat);
                        printf("Empate! O tabuleiro está cheio.\n");
                        vencedor = 3;
                    }
                } while (vencedor == 0);

                printf("\nDigite 1 para jogar novamente...\nOu qualquer outro digito para voltar ao MENU PRINCIPAL...\n");
                scanf("%d", &opcao);
                system("cls");
            } while(opcao == 1);
        }
        else if (op == 2) {
            printf("\t\tSA�STE DO JOGO");
        }

    }  while(opcao != 1 && op != 2);
    return 0;
}
/* Grupo 1 II11A 
   Membros....
   N° 1
   N° 2
   N° 3
   N° 4
   N° 5
   N° 6
   N° 7
   N° 8
   N° 9 
   N° 10
   N° 11
   N° 12
   N° 13 */
   