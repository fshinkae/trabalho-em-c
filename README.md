# Resumo: Listas Dinâmicas em C

## Definição de Lista Dinâmica

Segundo o livro, uma **lista dinâmica** é uma estrutura de dados que permite armazenar elementos de forma sequencial, mas com a capacidade de ajustar seu tamanho conforme necessário durante a execução do programa. Ao contrário das listas estáticas (como arrays), uma lista dinâmica pode crescer ou diminuir em tempo de execução sem a necessidade de pré-alocar um número fixo de elementos.

### Comparação entre Listas Estáticas (Arrays) e Listas Dinâmicas

As Listas Estáticas possuem tamanho fixo, determinado no momento da criação, e não podem ser alteradas após a alocação inicial. Elas permitem fácil acesso aos elementos por meio de indexação, o que proporciona um acesso rápido. 

No entanto, se o tamanho dos dados mudar frequentemente, elas tornam-se menos eficientes. Já as **Listas Dinâmicas** têm tamanho variável, permitindo a adição e remoção de elementos conforme necessário, com alocação de memória dinâmica. 

Elas requerem o uso de ponteiros para gerenciar os elementos e, embora ofereçam mais flexibilidade, o acesso aos elementos é mais lento em comparação com arrays, devido à necessidade de navegação através dos ponteiros.

### Vantagens e Desvantagens

**Vantagens das Listas Dinâmicas:**
-   Flexibilidade no tamanho, permitindo adicionar ou remover elementos durante a execução do programa.
 -   Uso eficiente de memória, já que não é necessário reservar memória para elementos não utilizados.
        
**Desvantagens das Listas Dinâmicas:**
-   Acesso sequencial aos elementos, o que pode tornar as operações mais lentas do que em arrays.
-   A alocação e liberação de memória pode ser mais complexa e sujeita a erros, como vazamentos de memória.

## Estrutura de uma Lista Dinâmica

### Criação e Inicialização de uma Lista Dinamica

```
struct Car {
    char model[50];   // Modelo do carro
    int year;         // Ano do carro
    struct Car* next; // Ponteiro para o próximo carro
};

struct Car* head = NULL; 
```
### Criação e Inicialização

A criação de uma lista dinâmica começa com a inicialização da cabeça da lista como `NULL`, indicando que a lista está vazia.
### Inserção

Para inserir um carro no início da lista, alocamos memória para um novo nó e o adicionamos à frente da lista.
```
void insertAtBeginning(struct Car** head, char* model, int year) {
    struct Car* newCar = (struct Car*) malloc(sizeof(struct Car)); // Aloca memória para o novo carro
    strcpy(newCar->model, model); // Copia o modelo do carro
    newCar->year = year;          // Define o ano do carro
    newCar->next = *head;         // O próximo carro será o atual "head"
    *head = newCar;               // O novo carro se torna o "head" da lista
}
```
### Remoção

Para remover o primeiro carro da lista, ajustamos o ponteiro da cabeça para o próximo carro e liberamos a memória do nó removido.
```
void deleteAtBeginning(struct Car** head) {
    if (*head != NULL) {
        struct Car* temp = *head;
        *head = (*head)->next; // Atualiza o ponteiro da cabeça
        free(temp);            // Libera a memória do carro removido
    }
}
```

## Implementação em C
Aqui está o código completo que implementa uma lista dinâmica de carros, com funções para inserir, imprimir e remover carros.

```
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

// Definição da estrutura do nó
struct Car {
    char model[50];
    int year;
    struct Car* next; // Ponteiro para o próximo carro
};

// Função para inserir um carro no início da lista
void insertAtBeginning(struct Car** head, char* model, int year) {
    struct Car* newCar = (struct Car*) malloc(sizeof(struct Car)); // Aloca memória para um novo carro
    strcpy(newCar->model, model); // Copia o modelo do carro
    newCar->year = year;          // Define o ano do carro
    newCar->next = *head;         // O próximo carro será o atual "head"
    *head = newCar;               // O novo carro se torna o "head" da lista
}

// Função para imprimir a lista de carros
void printCars(struct Car* head) {
    struct Car* temp = head;
    while (temp != NULL) {
        printf("Carro: %s, Ano: %d\n", temp->model, temp->year);
        temp = temp->next; // Move para o próximo carro na lista
    }
}

// Função para deletar o primeiro carro da lista
void deleteAtBeginning(struct Car** head) {
    if (*head != NULL) {
        struct Car* temp = *head;
        *head = (*head)->next;
        free(temp);
    }
}

int main() {
    struct Car* head = NULL; // Lista de carros inicialmente vazia

    // Inserir alguns carros na lista
    insertAtBeginning(&head, "Fusca", 1979);
    insertAtBeginning(&head, "Civic", 2020);
    insertAtBeginning(&head, "Gol", 2015);

    // Imprimir a lista de carros
    printf("Lista de carros:\n");
    printCars(head);

    // Remover o primeiro carro da lista
    deleteAtBeginning(&head);
    printf("\nLista de carros após remoção do primeiro carro:\n");
    printCars(head);

    return 0;
}
```

### Referencia
Damas, Luís. Linguagem C.
