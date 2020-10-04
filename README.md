# Estrutura de Dados utilizando JavaScript

Neste repositório, você encontrará as Estruturas de Dados do tipo:

1. Fila
2. Pilha
3. Lista Encadeada
4. Fila Duplamente Encadeada
5. Lista Duplamente Encadeada
6. Árvore de Busca Binária

As estruturas de dados serão reproduzidas utilizando a sintaxe de classes padronizada pelo ECMAScript. Bom proveito!

## Fila

Filas são estruturas de dados onde o primeiro a entrar é o primeiro a sair. É chamado de FIFO (First In First Out). As operações em Fila são análogas ao que ocorre em filas reais, como a fila de um banco, por exemplo, com a exceção de que os elementos na fila não se movem, conforme o primeiro elemento é retirado. Na estrutura de dados Fila, o algoritmo indica quem está na primeira posição.

![fila](https://user-images.githubusercontent.com/56840825/95017414-97816000-062f-11eb-817b-aae7fa1d9fc5.png)

Utilizaremos as classes que foram implementadas no ECMAScript 2015 para criação de nossa fila. A nossa estrutura terá os seguintes métodos:

- Enqueue (inserção na fila);
- Dequeue (remoção da fila);
- MostrarTudo;
- VisualizarEm.

Para começar, precisamos criar uma classe chamada Fila, onde teremos o início da fila (head), fim da fila (tail) e um contador (count). Como a fila está vazia, o nosso head e nosso tail recebem o valor null, e nosso contador começa em 0. Precisamos também de um método Get para nosso contador:

...
class Fila {
    constructor(head = null, tail = null, count = 0){
        this.head = head;
        this.tail = tail;
        this.count = count;
    }
    GetContador(){
        return this.count;
    }
}
...
