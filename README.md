#include <stdio.h>

#define TAMANHO_TABULEIRO 10
#define TAMANHO_NAVIO 3

int main() {
    // ----------------------------
    // Inicio do tabuleiro
    // ----------------------------
    int tabuleiro[TAMANHO_TABULEIRO][TAMANHO_TABULEIRO];

    // Preenche o tabuleiro com 0 (água)
    for (int linha = 0; linha < TAMANHO_TABULEIRO; linha++) {
        for (int coluna = 0; coluna < TAMANHO_TABULEIRO; coluna++) {
            tabuleiro[linha][coluna] = 0;
        }
    }

    // ----------------------------
    // Códigos das coordenadas dos navios 
    // ----------------------------
    int navioHorizontal[TAMANHO_NAVIO] = {3, 3, 3}; // navio horizontal
    int navioVertical[TAMANHO_NAVIO] = {3, 3, 3};   // navio vertical

    int linhaH = 2;   // linha inicial do navio horizontal
    int colunaH = 4;  // coluna inicial do navio horizontal

    int linhaV = 5;   // linha inicial do navio vertical
    int colunaV = 1;  // coluna inicial do navio vertical

    // ----------------------------
    // Validação: dentro dos limites do tabuleiro
    // ----------------------------
    if (colunaH + TAMANHO_NAVIO > TAMANHO_TABULEIRO || linhaV + TAMANHO_NAVIO > TAMANHO_TABULEIRO) {
        printf("Erro: Navios fora dos limites do tabuleiro.\n");
        return 1;
    }

    // ----------------------------
    // Validação: sobreposição
    // ----------------------------
    int sobreposicao = 0;
    for (int i = 0; i < TAMANHO_NAVIO; i++) {
        if (linhaH == linhaV + i && colunaH + i == colunaV) {
            sobreposicao = 1;
            break;
        }
    }

    if (sobreposicao) {
        printf("Erro: Navios se sobrepõem.\n");
        return 1;
    }

    // ----------------------------
    // Navio em posição horizontal
    // ----------------------------
    for (int i = 0; i < TAMANHO_NAVIO; i++) {
        tabuleiro[linhaH][colunaH + i] = navioHorizontal[i];
    }

    // ----------------------------
    // Navio em posição vertical
    // ----------------------------
    for (int i = 0; i < TAMANHO_NAVIO; i++) {
        tabuleiro[linhaV + i][colunaV] = navioVertical[i];
    }

    // ----------------------------
    // Exibição do tabuleiro
    // ----------------------------
    printf("\nTabuleiro de Batalha Naval (0 = água, 3 = navio):\n\n");

    for (int linha = 0; linha < TAMANHO_TABULEIRO; linha++) {
        for (int coluna = 0; coluna < TAMANHO_TABULEIRO; coluna++) {
            printf("%d ", tabuleiro[linha][coluna]);
        }
        printf("\n");
    }

    return 0;
}
