#include <stdio.h>
#include <stdlib.h>

#define TAM 10

typedef struct Lista {
    int elementos[TAM];
    int qte;
} ListaLinear;

void IniciarLista(ListaLinear *pL) {
    pL->qte = 0;
    printf("Lista inicializada.\n");
}

int VerificaCheia(ListaLinear *pL) {
    return pL->qte == TAM;
}

void Imprime(ListaLinear *pL) {
    if (pL->qte == 0) {
        printf("Lista vazia.\n");
        return;
    }

    printf("Elementos da lista:\n");
    for (int i = 0; i < pL->qte; i++) {
        printf("Posição %d: %d\n", i, pL->elementos[i]);
    }
}

void InserirFinalLista(ListaLinear *pL) {
    int valor;
    if (VerificaCheia(pL)) {
        printf("Lista está cheia.\n");
        return;
    }

    printf("Insira o valor: ");
    scanf("%d", &valor);

    pL->elementos[pL->qte] = valor;
    pL->qte++;

    printf("Valor inserido no final da lista.\n");
}

void InserirPosicaoEspecifica(ListaLinear *pL) {
    int pos, valor;

    if (VerificaCheia(pL)) {
        printf("Lista cheia.\n");
        return;
    }

    printf("Informe a posição (0 a %d): ", pL->qte);
    scanf("%d", &pos);

    if (pos < 0 || pos > pL->qte) {
        printf("Posição inválida.\n");
        return;
    }

    printf("Informe o valor: ");
    scanf("%d", &valor);

    for (int i = pL->qte; i > pos; i--) {
        pL->elementos[i] = pL->elementos[i - 1];
    }

    pL->elementos[pos] = valor;
    pL->qte++;

    printf("Valor inserido na posição %d.\n", pos);
}

void RemoverFinal(ListaLinear *pL) {
    if (pL->qte == 0) {
        printf("Lista já está vazia.\n");
        return;
    }

    pL->qte--;
    printf("Último elemento removido.\n");
}

void BuscarValor(ListaLinear *pL) {
    if (pL->qte == 0) {
        printf("Lista vazia.\n");
        return;
    }

    int valor;
    printf("Digite o valor que deseja buscar: ");
    scanf("%d", &valor);

    for (int i = 0; i < pL->qte; i++) {
        if (pL->elementos[i] == valor) {
            printf("Valor %d encontrado na posição %d.\n", valor, i);
            return;
        }
    }

    printf("Valor não encontrado na lista.\n");
}

int main() {
    int escolha;
    ListaLinear l;

    printf("1 - Inicializar a lista\n");
    printf("2 - Verificar se está cheia\n");
    printf("3 - Inserir no final\n");
    printf("4 - Inserir em posição específica\n");
    printf("5 - Remover do final\n");
    printf("6 - Imprimir elementos\n");
    printf("7 - Buscar valor\n");
    printf("0 - Sair\n");

    do {
        printf("\nEscolha: ");
        scanf("%d", &escolha);

        switch (escolha) {
            case 1:
                IniciarLista(&l);
                break;
            case 2:
                if (VerificaCheia(&l))
                    printf("Lista está cheia.\n");
                else
                    printf("Ainda há espaço na lista.\n");
                break;
            case 3:
                InserirFinalLista(&l);
                break;
            case 4:
                InserirPosicaoEspecifica(&l);
                break;
            case 5:
                RemoverFinal(&l);
                break;
            case 6:
                Imprime(&l);
                break;
            case 7:
                BuscarValor(&l);
                break;
            case 0:
                printf("Encerrando...\n");
                break;
            default:
                printf("Opção inválida.\n");
        }
    } while (escolha != 0);

    return 0;
}
