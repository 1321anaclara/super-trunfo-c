# super-trunfo-c

#include <stdio.h>
#include <stdlib.h>
#include <time.h>

#define NUM_CARTAS 5

// Estrutura para representar uma carta
typedef struct {
    char nome[30];
    int forca;
    int velocidade;
    int inteligencia;
} Carta;

// Função para inicializar as cartas
void inicializarCartas(Carta baralho[]) {
    Carta cartasPredefinidas[NUM_CARTAS] = {
        {"Guerreiro", 80, 60, 50},
        {"Mago", 40, 50, 90},
        {"Arqueiro", 60, 90, 60},
        {"Gigante", 90, 30, 40},
        {"Assassino", 70, 80, 70}
    };
    for (int i = 0; i < NUM_CARTAS; i++) {
        baralho[i] = cartasPredefinidas[i];
    }
}

// Função para escolher uma carta aleatória
typedef struct {
    Carta carta;
    char jogador[20];
} Rodada;

// Função para comparar atributos
void compararCartas(Rodada jogador1, Rodada jogador2, int atributo) {
    int valor1, valor2;
    switch (atributo) {
        case 1: valor1 = jogador1.carta.forca; valor2 = jogador2.carta.forca; break;
        case 2: valor1 = jogador1.carta.velocidade; valor2 = jogador2.carta.velocidade; break;
        case 3: valor1 = jogador1.carta.inteligencia; valor2 = jogador2.carta.inteligencia; break;
        default: printf("Atributo inválido!\n"); return;
    }

    printf("%s escolheu: %s (Valor: %d)\n", jogador1.jogador, jogador1.carta.nome, valor1);
    printf("%s escolheu: %s (Valor: %d)\n", jogador2.jogador, jogador2.carta.nome, valor2);
    
    if (valor1 > valor2)
        printf("%s venceu a rodada!\n", jogador1.jogador);
    else if (valor2 > valor1)
        printf("%s venceu a rodada!\n", jogador2.jogador);
    else
        printf("A rodada empatou!\n");
}

int main() {
    srand(time(NULL));
    Carta baralho[NUM_CARTAS];
    inicializarCartas(baralho);

    Rodada jogador1 = {baralho[rand() % NUM_CARTAS], "Jogador 1"};
    Rodada jogador2 = {baralho[rand() % NUM_CARTAS], "Jogador 2"};

    int atributo;
    printf("Escolha um atributo para comparar:\n");
    printf("1 - Força\n2 - Velocidade\n3 - Inteligência\n");
    scanf("%d", &atributo);

    compararCartas(jogador1, jogador2, atributo);

    return 0;
}
