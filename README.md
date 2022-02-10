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

## LISTA DUPLAMENTE ENCADEADA:

A Lista Duplamente Encadeada permite que seja percorrida em duas direções, direita e esquerda, diferentemente da Lista Encadeada simples, que permite que seja percorrido em apenas uma direção. Na Lista Duplamente Encadeada, cada elemento possui uma referência para o próximo elemento e para o elemento anterior, se esse elemento estiver disponível. Assim, podemos viajar para trás e para frente de cada elemento da lista.

![deque](https://miro.medium.com/max/700/0*Fll9Q9H9xj8JegC_.png)

Para criar nossa Lista, precisaremos de uma classe principal chamada ListaDuplamenteEncadeada e um classe que nos servirá de apoio, evitando reescrever código, chamada Node. A nossa lista terá um contador, que começará em 0 e, também, uma cabeça (head) e uma cauda (tail), que inicialmente terão o valor null:

```
class ListaDuplamenteEncadeada {
    constructor(head = null, tail = null, count = 0){
        this.head = head;
        this.tail = tail;
        this.count = count;
    }
}
class Node{
    constructor(data, next = null, previous = null){
        this.data = data;
        this.next = next;
        this.previous = previous;
    }
}
```

Precisamos também implementar os métodos getHead, getTail e getCount:

```
getHead(){
    if (this.head) {
        return this.head.data;
    }
    return null;
}
getTail(){
    if (this.tail) {
        return this.tail.data;
    }
    return null;
}
GetCount(){
    return this.count;
}
```

A nossa lista terá os seguintes métodos:
- MostrarTudo();
- MostrarFimInicio();
- VisualizarEm(index);
- AdicionarInicio(data);
- AdicionarFinal(data);
- AdicionarEm(data, index);
- RemoverInicio();
- RemoverFinal();
- RemoverEm(index).

#### Vamos lá!

### MostrarTudo():

Como o próprio nome já diz, esse método nos mostrará todo o conteúdo da Lista Duplamente Encadeada. Para isso, utilizaremos um Array que conterá todos os dados da lista e percorreremos esse array com um laço FOR. Caso não ocorra a existência de dados na lista, retornará null:


```
MostrarTudo(){
    if (this.head){
        let arr = [];
        let current = this.head;
        for (let i = 0; i < this.count; i++){
            arr[i] = current.data;
            current = current.next;
        }
        return arr;
    } else {
        return null;
    }
}
```

### MostrarFimInicio():

Esse método retorna um array que contém os dados de trás para frente, ou seja, da cauda para a cabeça (tail to head). Caso esteja vazio, retornará null:

```
MostrarFimInicio(){
    if (this.head){
        let arr = [];
        let current = this.tail;
        for (let i = 0; i < this.count; i++){
            arr[i] = current.data;
            current = current.previous;
        }
        return arr;
    } else {
        return null;
    }
}
```

### VisualizarEm(index):

Esse método retorna o item no índice indicado. Caso esse índice não exista, retornará null:

```
VisualizarEm(index){
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

Adiciona o elemento ao início da lista. Se a lista estiver vazia, o elemento adicionado será o único da lista:


```
AdicionarInicio(data){
    let no = new Node(data);
    no.next = this.head;
    this.head = no;
    if (this.count === 0){
        this.tail = this.head;
    } else {
        this.head.next.previous = this.head;
    }
    this.count++;
}
```

### AdicionarFinal(data):

Funciona de maneira semelhante ao método anterior, mas adiciona o elemento ao final da lista:

```
AdicionarFinal(data){
    let no = new Node(data);
    no.previous = this.tail;
    if (this.count === 0){
        this.head = no;
    } else {
        this.tail.next = no;
    }
    this.tail = no;
    this.count++;
}
```

### AdicionarEm(data, index):

Adiciona o elemento no índice indicado:

```
AdicionarEm(data, index){
    if (index > 0 && index < this.count){
        let no = new Node(data);
        let current = this.head;
        let i = 0;
        while(i++ < index){
            current = current.next;
        }
        current.previous.next = no;
        no.next = current;
        no.previous = current.previous;
        current.previous = no;
            
        this.count++;
    } else if (index < 1){
        this.AdicionarInicio(data);
    } else {
        this.AdicionarFinal(data);
    }
}
```

### RemoverInicio():

Remove o elemento situado no início da lista:

```
RemoverInicio(){
    if (this.head){
        this.head = this.head.next;
        this.count--;
        if (this.count === 0){
            this.tail = null;
        } else {
            this.head.previous = null;
        }
    }
}
```

### RemoverFinal():

Remove o elemento situado no final da fila. Não esqueça de decrementar o contador:

```
RemoverFinal(){
    if(this.head){
        if(this.count === 1){
            this.head = null;
            this.tail = null;
        } else {
            this.tail.previous.next = null;
            this.tail = this.tail.previous;
        }
        this.count--;
    }
}
```

### RemoverEm(index):

Remove o elemento no índice indicado:

```
RemoverEm(index){
    if (index > 0 && index < this.count-1){
        let current = this.head;
        let i = 0;
        while( i++ < index){
            current = current.next;
        }
        current.previous.next = current.next;
        current.next.previous = current.previous;
        this.count--;
    } else if (index < 1){
        this.RemoverInicio();
    } else {
        this.RemoverFinal();
    }
}
```

Teste no seu navegador:

```
let lista = new ListaDuplamenteEncadeada();
lista.AdicionarInicio(1);
lista.AdicionarInicio(4);
lista.AdicionarInicio(5);
lista.AdicionarInicio(6);
lista.AdicionarFinal(2);
lista.AdicionarEm(3, 1);
console.log(lista.VisualizarEm(1));
console.log(lista.MostrarFimInicio());
lista.RemoverEm(2);
lista.RemoverInicio();
lista.RemoverFinal();
console.log(lista.MostrarTudo());
```

E a saída será:

![deque](https://miro.medium.com/max/334/0*zsbUiiDphb0nXZ-X.png)

## BINARY SEARCH TREE (Árvore de Busca Binária):

Dando sequência aos nossos artigos de Estruturas de Dados com JavaScript, hoje implementaremos uma Árvore de Busca Binária (Binary Search Tree). Uma árvore é uma coleção de nós conectados por arestas e é uma estrutura não-linear. Uma das principais características de uma árvore binária é que os nós com menor valor são armazenados na sua esquerda, e os nos de valor mais alto são armazenados na direita.

### Para começar, criaremos uma classe chamada nó, que servirá de apoio para a criação da nossa Árvore Binária:

```
class No{
    constructor(data, esquerda = null, direita = null){
        this.data = data;
        this.esquerda = esquerda;
        this.direita = null;
    }
}
```

Você pode perceber que o nó que criamos possui um dado e mais duas propriedades: esquerda e direita, que possuem valor nulo.

### Agora, vamos criar a nossa Árvore:

```
class ArvoreBuscaBinaria{
    constructor(root = null){
        this.root = null;
    }
}
```

A nossa árvore possui um nó raiz, que é definido como tendo valor nulo pelo construtor.

#### Também teremos os métodos principais da nossa árvore binária, que são:
- Insercao(data);
- InserirNo(no, novoNo);
- Remover(data);
- RemoverNo(no, key).
#### E os métodos auxiliares, que são:
- EncontrarMenorNo();
- EncontrarNoRaiz();
- EmOrdem(no);
- PreOrdem(no);
- PosOrdem(no);
- Pesquisar(no, data).

### Insercao(data) e InserirNo(no, novoNo):

Com o método Insercao(data), inseriremos um novo nó na nossa árvore binária com o valor especificado. Esse método cria um nó a ser inserido e chamará o método InserirNo para isso. Então precisamos: Criar um novo nó e inicializá-lo com o dado a ser utilizado e, se a raiz estiver vazia, esse novo dado será a raiz da árvore. Senão, chamaremos o método InserirNo para achar a posição correta na árvore e adicionar o nó.

```
Insercao(data){
    let novoNo = new No(data);
    
    if (this.root === null){
        this.root = novoNo;
    } else {
        this.InserirNo(this.root, novoNo);
    }
}
```

O método InserirNo(no, novoNo) verifica em qual parte da árvore o nó deve ser inserido e coloca-o no lugar correto. Se o dado a ser inserido for menor que o nó raiz, o novo dado deve ir para a esquerda. Senão, o novo dado deve ir para a direita. O mesmo vale para os outros nós que já estão posicionados, ou seja, acontece uma comparação dos dados fornecidos com os dados do nó atual, movendo-se para a esquerda ou para a direita e recorrendo até encontrar um nó correto para qual o novo nó possa ser adicionado.


```
InserirNo(no, novoNo){
    if (novoNo.data < no.data){
        if (no.esquerda === null){
            no.esquerda = novoNo;
        } else {
            this.InserirNo(no.esquerda, novoNo);
        }
    } else {
        if (no.direita === null){
            no.direita = novoNo;
        } else {
            this.InserirNo(no.direita, novoNo);
        }
    }
}
```

### Remover(data) e RemoverNo(no, key):

Para remover dados da nossa árvore binária, utilizamos os métodos Remover(data) e RemoverNo(no, key). O método Remover chama o método RemoverNo passando o nó raiz e dados fornecidos, atualizando a raiz da árvore com o valor que é retornado pela função. O método RemoverNo procura um nó com o dado passado e executa as etapas para excluí-lo. Podemos excluir um nó passando por três cenários diferentes:

- Apenas um nó folha, que é um nó que não possui filhos. Eles são facilmente removidos.
- Um nó com filho, que se o nó tiver um filho na parte esquerda, atualizaremos o ponteiro (referência) do nó pai para o filho esquerdo do nó a ser excluído. O mesmo acontece com o filho da parte direita.
- Um nó com dois filhos, onde encontramos o nó com valor mínimo na parte direita e substituímos esse nó pelo nó com valor mínimo e removemos da árvore.

```
Remover(data){
    this.root = this.RemoverNo(this.root, data);
}
RemoverNo(no, key){
    if (no === null){
        return null;
    } else if (key > no.data){
        no.direita = this.RemoverNo(no.direita, key);
        return no;
    } else {
        if (no.esquerda === null && no.direita === null){
            no = null;
            return no;
        } 
        if(no.esquerda === null){
            no = no.direita;
            return no;
        } else if (no.direita === null){
            no = no.esquerda;
            return no;
        }
        let aux = this.EncontrarMenorNo(no.direita);
        no.data = aux.data;
        no.direita = this.RemoverNo(no.direita, aux.data);
        return no;
    }
}
```

Agora, precisamos percorrer a nossa árvore, e isso pode ser feito de diversas formas. Começaremos com o método:

#### EmOrdem(no):

Esse método percorre a árvore a partir de um nó. Percorre a subárvore esquerda, visita a raiz e percorre a subárvore direita.


```
EmOrdem(no){
    if (no !== null){
        this.EmOrdem(no.esquerda);
        console.log(no.data);
        this.EmOrdem(no.direita);
    }
}
```

### PreOrdem(no):

Esse método percorre a árvore visitando primeiro o nó raiz e, então, percorre a subárvore esquerda. Após percorrer o lado esquerdo, o método percorre a subárvore direita.


```
PreOrdem(no){
    if (no !== null){
        console.log(no.data);
        this.PreOrdem(no.esquerda);
        this.PreOrdem(no.direita);
    }
}
```

### PosOrdem(no):

Começa percorrendo a subárvore esquerda, depois, percorre a subárvore direita e por último, visita o nó root.

```
PosOrdem(no){
    if (no !== null){
        this.PosOrdem(no.esquerda);
        this.PosOrdem(no.direita);
        console.log(no.data);
    }
}
```

#### Agora, precisamos declarar métodos auxiliares.

### EncontrarMenorNo(no):

Procura o nó com menor valor na árvore binária. Esse método começa a busca a partir de um nó e move-se pela subárvore esquerda até encontrar um nó cujo filho esquerdo é nulo. Uma vez encontrado, retornamos.

```
EncontrarMenorNo(no){
    if (no.esquerda===null){
        return no;
    } else {
        return this.EncontrarMenorNo(no.esquerda);
    }
}
```

### EncontrarNoRaiz():

Retorna o nó raiz de nossa árvore:

```
EncontrarNoRaiz(){
    return this.root;
}
```

### Pesquisar(no, data):

Pesquisa o nó com dados que tenham o valor em toda a árvore:

```
Pesquisar(no, data){
    if (no === null){
        return null;
    }
    else if (data < no.data){
        return this.Pesquisar(no.esquerda, data);
    } else if (data > no.data){
        return this.Pesquisar(no.direita, data);
    } else {
        return no;
    }
}
```

Agora, precisamos criar uma nova árvore e implementar seus métodos:

```
let arvoreBinaria = new ArvoreBuscaBinaria();
arvoreBinaria.Insercao(20);
arvoreBinaria.Insercao(25);
arvoreBinaria.Insercao(15);
arvoreBinaria.Insercao(10);
arvoreBinaria.Insercao(28);
arvoreBinaria.Insercao(27);
arvoreBinaria.Insercao(9);
arvoreBinaria.Insercao(7);
arvoreBinaria.Insercao(2);
arvoreBinaria.Insercao(28);
let raiz = arvoreBinaria.EncontrarNoRaiz();
arvoreBinaria.EmOrdem(raiz);
arvoreBinaria.Remover(2);
arvoreBinaria.PosOrdem(raiz);
arvoreBinaria.PreOrdem(raiz);
```

E nossa saída será:

![deque](https://miro.medium.com/max/659/0*GX6kvHJhGmcH9EvC.png)

Referências:

https://www.codeproject.com/Articles/669131/Data-Structures-with-JavaScript

https://www.geeksforgeeks.org/implementation-binary-search-tree-javascript/
