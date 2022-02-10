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

```
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
```
### Enqueue:

Para adicionarmos um item no início da nossa fila, precisamos criar um nó, que conterá o dado e uma referência à próxima posição da fila, que deverá ser null. Quando inserirmos nosso primeiro elemento, o início e o final da fila serão o mesmo elemento, e precisaremos incrementar o contador:

```
Enqueue(data){
    let no = {
        data: data,
        next: this.head
    };
    if (this.head === null){
        this.tail = no;
    }
    this.head = no;
    this.count++;
}
```
### Dequeue:
Removeremos o primeiro elemento da fila e retornaremos o último item inserido e armazenado no final da fila. Fazendo isso, teremos que, enquanto houver um próximo elemento, avançaremos na fila. A ideia é ter um atual no final da fila e um anterior e, então, teremos que decrementar o contador:

```
Dequeue(){
    if (this.count === 0){
        return;
    } else {
        let current = this.head;
        let previous = null;
        while (current.next){
            previous = current;
            current = current.next;
        }
        if (this.count > 1){
            previous.next = null;
            this.tail = previous;
        } else {
            this.head = null;
            this.tail = null;
        }
        this.count--;
    }
}
```

### MostrarTudo:

O próprio nome já diz: mostraremos todos os elementos da fila. Utilizaremos um vetor para isso e, com um laço de repetição, iremos inserir cada valor em sua respectiva posição neste vetor. Também precisamos verificar se há elementos na fila:

```
MostrarTudo(){
    if (this.head === null){
        return null;
    } else {
        let arr = [];
        let current = this.head;
        for (let i = 0; i < this.count; i++) {
            arr[i] = current.data;
            current = current.next;
        }
        return arr;
    }
}
```

### VisualizarEm:

No método VisualizarEm, iremos procurar o elemento na nossa fila, buscando-o e exibindo-o. Utilizaremos um laço de repetição para percorrer nossa fila e encontrar o elemento que buscamos:

```
VisualizarEm(index){
    if (index > -1 && index < this.count){
        let current = this.head;
        for (let i = 0; i < index; i++) {
            current = current.next;
        }
        return current.data;
    } else {
        return null;
    }
}
```

Agora, vamos testar:

```
let fila = new Fila();
fila.Enqueue(1);
fila.Enqueue(2);
fila.Enqueue(3);
fila.Enqueue(4);
fila.Enqueue(5);
fila.Enqueue(6);
fila.Dequeue();
fila.Dequeue();
console.log(fila.VisualizarEm(1));
console.log(fila.MostrarTudo());
console.log(fila);
```
E a nossa saída será:

![fila](https://miro.medium.com/max/331/0*UUAYxtMwo9VGn6qc.png)
