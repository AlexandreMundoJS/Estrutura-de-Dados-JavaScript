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

## PILHA:

A pilha é uma estrutura de dados que implementa o conceito de último a entrar, primeiro a sair (LIFO (Last in First Out)), ou seja, o último elemento adicionado será o primeiro elemento a ser removido. Utilizaremos também, na nossa estrutura de dados, a palavra-chave class, que foi introduzida no ECMAScript 2015. Mas isso não significa que JavaScript é uma linguagem orientada e objetos. O JavaScript continua sendo orientado a protótipos, ou seja, o prototype continua agindo “por baixo dos panos”, e a palavra-chave class apenas “mascara” toda essa prototipagem, tornando o código mais simples de ser lido.

Abaixo temos uma imagem do funcionamento da pilha:

![pilha](https://miro.medium.com/max/500/0*kk8SpMo8Ya78u441.jpg)

Então, para começarmos a implementar a pilha, precisamos construir a nossa classe Pilha e seu construtor. Vamos implementar também um contador, que será útil para nos mostrar a quantidade de itens na pilha. No nosso construtor, precisamos setar nossos valores do contador e do topo da pilha. Como ainda não há nada na pilha, o topo é null e o contador é 0:

```
class Pilha {
    constructor(top = null, count = 0){
        this.top = top;
        this.count = count;
    }
    GetContador(){
        return this.count;
    }
}
```

Nossa pilha terá os seguintes métodos:

- Push;
- Visualizar;
- Remover;
- MostrarTodos.

### Push:

Para criar nosso método push, precisamos criar um nó. Cada nó precisa ter o dado e a referência para o próximo nó, que precisa ser null, pois cada vez que inserirmos algo na pilha, esse elemento inserido deverá ser o primeiro a ser removido. Então, cada nó inserido deve virar o topo da pilha.

```
Push(data){
    let no = {
       data: data,
       next: null
    };
    no.next = this.top;
    this.top = no;
    this.count++;
}
```

### Visualizar:

Para visualizarmos o item que está no topo da pilha, precisamos nos certificar de que a pilha não está vazia. Caso a pilha não estiver vazia, retornaremos o dado que está no topo de nossa estrutura:

```
Visualizar(){
    if (this.top === null){
        return null;
    } else {
        return this.top.data;
    }
}
```

### Remover:

Para remover o elemento do topo da pilha, precisamos entender que a pilha não poderá estar vazia. Caso ela não esteja vazia, removeremos o elemento do topo e diminuiremos o nosso contador em 1.

```
Remover(){
    if (this.top === null){
        return null;
    } else {
        let remover = this.top;
        this.top = this.top.next;
        if (this.count > 0){
            this.count--;
        }
        return remover.data;
    }
}
```

### MostrarTodos:

Iremos adicionar os dados em um vetor, para então exibi-los. Precisamos ter certeza que nossa pilha não está vazia e, então, criamos um vetor, Utilizaremos um laço de repetição que irá inserir cada elemento de nossa pilha em sua respectiva posição:

```
MostrarTodos(){
    if (this.top === null){
        return null;
    } else {
        let arr = [];
        let current = this.top;
        for (let i = 0; i < this.count; i++){
            arr[i] = current.data;
            current = current.next;
        }
        return arr;
    }
}
```

E podemos testar a nossa estrutura de dados, instanciando uma nova pilha:

```
let pilha = new Pilha();
pilha.Push(1);
pilha.Push(2);
pilha.Push(3);
pilha.Push(4);
pilha.Push(5);
pilha.Push(6);
pilha.Push(7);
pilha.Remover();
console.log(pilha.Visualizar());
console.log(pilha.MostrarTodos());
console.log(pilha);
```

E a saída será:


![pilha](https://miro.medium.com/max/414/0*IShnMhggb7bxPig8.png)

## LISTA ENCADEADA:

Uma lista encadeada é uma sequência de objetos, onde cada elemento da sequência é armazenado em uma célula (nó) desta lista. O primeiro fica na primeira célula, o segundo na segunda célula e assim, sucessivamente. Cada célula possui seu próprio conteúdo. Você vai perceber as semelhanças entre Lista Encadeada, Fila e Pilha, visto que estas duas últimas foram criadas usando a ideia básica da Lista Encadeada. Seguindo nossa sequência, criaremos esta estrutura usando CLASS. Vamos definir nossa Lista Encadeada. Ela precisará de um Head para iniciar a lista e também um contador:

![pilha](https://miro.medium.com/max/455/0*piawxG4gbVqUAdBE.png)

```
class ListaEncadeada{
    constructor(head = null, count = 0){
        this.head = head;
        this.count = count;
    }
    GetContador(){
        return this.count;
    }
}
```

Nossa lista terá os seguintes métodos:
- MostrarTudo;
- MostrarEm;
- AdicionarInicio;
- AdicionarNaPosicao;
- RemoverInicio;
- RemoverNaPosicao.

#### Vamos lá!

### MostrarTudo():

Como o próprio nome já diz, esse método mostra todos os elementos que estão na lista. Ele retornará um array contendo os dados e, se a lista estiver vazia, retorna null:

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

### MostrarEm(index):

Nosso método MostrarEm nos retorna o elemento que está na posição desejada (index). Caso a posição buscada seja inexistente, o método retornará null:

```
MostrarEm(index){
    if (index > -1 && index < this.count){
        let current = this.head;
        let i = 0;
        while (i++ < index){
                current = current.next;
        }
        return current.data;
    } else {
        return null;
    }
}
```

### AdicionarInicio(data):

O nosso método adicionará o dado no início da lista. Caso esteja se perguntando, o início da lista é onde o índice é 0 e é referenciado pelo head. Precisamos incrementar o contador ao realizar a inserção:

```
AdicionarInicio(data){
    let no = {
        data: data,
        next: this.head
    };
    this.head = no;
    this.count++;
}
```

### AdicionarNaPosicao(data, index):

Adiciona um item na posição determinada. Precisamos verificar se não está fora dos limites da nossa lista encadeada. Caso não exista essa posição, mostraremos uma mensagem no console:

```
AdicionarNaPosicao(data, index){
    if (index === 0) {
        this.AdicionarInicio(data);
    } else if (index > -1 && index < this.count){
        let no = {
            data: data,
            next: null
        };
        let previous;
        let current = this.head;
        let i = 0;
        while (i++ < index){
            previous = current;
            current = current.next;
        }
        previous.next = no;
        no.next = current;
        this.count++;
    } else {
        console.log("Não existe esta posição na lista.")
    }
}
```

### RemoverInicio():

O método RemoverInicio() remove o primeiro item da lista. Caso a lista esteja vazia, o método retorna null.

```
RemoverInicio(){
    if (this.head === null){
        return null;
    } else {
        let out = this.head;
        this.head = this.head.next;
        if (this.count > 0){
            this.count--;
        }
        return out.data;
    }
}
```

### RemoverNaPosicao(index):

Remove o item que está na posição especificada. Precisamos novamente verificar se o índice está dentro dos limites da nossa lista:

```
RemoverNaPosicao(index){
    if (index === 0) {
        return this.RemoverInicio(this);
    } 
        
    else if ( index > -1 && index < this.count){
            
        let current = this.head;
        let previous;
        let i = 0;
        while (i++ < index){
            previous = current;
            current = current.next;
        }
        previous.next = current.next;
        this.count--;
        return current.data;
    } else {
        return null;
    }    
}
```

### DEQUE (Fila Duplamente Encadeada):

O Deque (Fila duplamente Encadeada) funciona basicamente com uma fila, com a diferença de que você pode adicionar e remover dados de qualquer extremidade da fila. Isso torna o nosso código um pouco mais difícil, mas chegaremos lá. Continuaremos usando class para realizar nossa estrutura de dados. Precisamos, inicialmente, criar a nossa classe Deque. Ela precisará de um início (head), um final (tail) e um contador:

![deque](https://miro.medium.com/max/602/0*cA6vmVjmUgYdf5nF.jpg)

```
class Deque {
    constructor(head = null, tail = null, count = 0){
        this.head = head;
        this.tail = tail;
        this.count = count;
    }
}
```

Também precisaremos criar os métodos GetHead, GetTail e GetCount:


```
GetHead(){
    if (this.head){
        return this.head.data;
    }
    return null;
}
GetTail(){
    if (this.tail){
        return this.tail.data;
    }
    return null;
}
GetCount(){
    return this.count;
}
```

A nossa fila duplamente encadeada terá os seguintes métodos:

- MostrarInicioFim();
- MostrarFimInicio();
- AdicionarInicio(data);
- AdicionarFim(data);- 
- RemoverInicio();
- RemoverFim().

Para criarmos nossos métodos, criaremos nosso código de forma diferente aos anteriores. Utilizaremos uma Classe de auxílio, para evitar reescrever código:

```
class Node{
    constructor(data, next = null){
        this.data = data;
        this.next = next;
    }
}
```

### MostrarInicioFim():

Esse método retorna um array com os dados, percorrendo do início ao fim:

```
MostrarInicioFim(){
    if (this.head != null){
        let arr = [];
        let current = this.head;
        
        while (current){
            arr.push(current.data);
            current = current.next;
        }
        return arr;
    } else {
        return null;
    }
}
```

### MostrarFimInicio():

Semelhante ao nosso método anterior, ele retorna um array com os dados da fila, porém, percorrendo do fim ao início. Para isso, utilizaremos o reverse():

```
MostrarFimInicio(){
    if (this.head != null){
        let arr = this.MostrarInicioFim();
        return arr.reverse();
    } else {
        return null;
    }
}
```

### AdicionarInicio(data):

Adiciona o dado no início de nossa fila e, para isso, usaremos nossa classe Node criada anteriormente para auxílio. Precisamos também incrementar o nosso contador:

```
AdicionarInicio(data){
    let no = new Node(data);
    no.next = this.head;
    this.head = no;
    if (!this.tail) {
        this.tail = this.head;
    }
    this.count++;
}
```

### AdicionarFim(data):

Esse método adicionar o dado no fim da fila. Semelhante ao nosso método anterior, usaremos a nossa classe Node de apoio. Precisamos também, nesse método, incrementar nosso contador.

```
AdicionarFim(data){
    let no = new Node(data);
    if (!this.head){
        this.head = no;
    } else {
        this.tail.next = no;
    }
    this.tail = no;
    this.count++;
}
```

### RemoverInicio():

Remove o dado que está no início (head) de nossa fila duplamente encadeada.

```
RemoverInicio(){
    if (this.head){
        if (this.count === 1){
            this.head = null;
            this.tail = null;
        } else {
            this.head = this.head.next;
        }
        this.count--;
    }
}
```

### RemoverFim():

Remove o dado que está na posição final da nossa fila:

```
RemoverFim(){
    if (this.head){
        if (this.count === 1){
            this.head = null;
            this.tail === null;
        } else {
            let current = this.head;
            while(current.next.next){
                current = current.next;
            }
            this.tail = current;
            this.tail.next = null;
        }
        this.count--;
    }
}
```
