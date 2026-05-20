
#include <stdio.h>

#define MAX 100

int vetor[MAX];
int tamanho = 0;

// Função para ordenar o vetor
void ordenar() {
    int i, j, temp;

    for(i = 0; i < tamanho - 1; i++) {
        for(j = i + 1; j < tamanho; j++) {
            if(vetor[i] > vetor[j]) {
                temp = vetor[i];
                vetor[i] = vetor[j];
                vetor[j] = temp;
            }
        }
    }
}

// Inserir elemento
void inserir() {
    int valor;

    if(tamanho >= MAX) {
        printf("\nVetor cheio!\n");
        return;
    }

    printf("\nDigite o valor para inserir: ");
    scanf("%d", &valor);

    vetor[tamanho] = valor;
    tamanho++;

    ordenar();

    printf("Valor inserido com sucesso!\n");
}

// Mostrar vetor
void apresentar() {
    int i;

    if(tamanho == 0) {
        printf("\nVetor vazio!\n");
        return;
    }

    printf("\nElementos do vetor:\n");

    for(i = 0; i < tamanho; i++) {
        printf("%d ", vetor[i]);
    }

    printf("\n");
}

// Busca binária
int buscaBinaria(int valor) {

    int inicio = 0;
    int fim = tamanho - 1;

    while(inicio <= fim) {

        int meio = (inicio + fim) / 2;

        if(vetor[meio] == valor) {
            return meio;
        }

        else if(vetor[meio] < valor) {
            inicio = meio + 1;
        }

        else {
            fim = meio - 1;
        }
    }

    return -1;
}

// Buscar elemento
void buscar() {

    int valor;

    if(tamanho == 0) {
        printf("\nVetor vazio!\n");
        return;
    }

    printf("\nDigite o valor para buscar: ");
    scanf("%d", &valor);

    int posicao = buscaBinaria(valor);

    if(posicao != -1) {
        printf("Valor encontrado na posição %d\n", posicao);
    }

    else {
        printf("Valor não encontrado!\n");
    }
}

// Remover elemento
void remover() {

    int valor;
    int posicao;
    int i;

    if(tamanho == 0) {
        printf("\nVetor vazio!\n");
        return;
    }

    printf("\nDigite o valor para remover: ");
    scanf("%d", &valor);

    posicao = buscaBinaria(valor);

    if(posicao == -1) {
        printf("Valor não encontrado!\n");
        return;
    }

    for(i = posicao; i < tamanho - 1; i++) {
        vetor[i] = vetor[i + 1];
    }

    tamanho--;

    printf("Valor removido com sucesso!\n");
}

// Programa principal
int main() {

    int opcao;

    do {

        printf("\n============================\n");
        printf("MENU - BUSCA BINARIA\n");
        printf("============================\n");
        printf("1 - Inserir elemento\n");
        printf("2 - Remover elemento\n");
        printf("3 - Buscar elemento\n");
        printf("4 - Apresentar elementos\n");
        printf("0 - Encerrar programa\n");
        printf("Escolha uma opção: ");
        scanf("%d", &opcao);

        switch(opcao) {

            case 1:
                inserir();
                break;

            case 2:
                remover();
                break;

            case 3:
                buscar();
                break;

            case 4:
                apresentar();
                break;

            case 0:
                printf("\nPrograma encerrado!\n");
                break;

            default:
                printf("\nOpção inválida!\n");
        }

    } while(opcao != 0);

    return 0;
}
