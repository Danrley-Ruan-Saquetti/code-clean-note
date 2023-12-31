# Código Limpo

Código limpo consiste em clareza na leitura do código, boa estruturação, fácil manutenção, "beleza" na escrita, declaração e nomenclatura devem ser intuitivas e de facil entendimento.

## Pensadores

* Bjarne Stroustrup
   - Código elegante - naturalidade na leitura, lógica direta e intuitiva, agilidade no desenvolvimento
* Grady Booch
   - Simples e direto, legível e objetivo
* Dave Thomas
   - Tanto quem criou, como quem continuou, devem manter sempre um código limpo, sempre pensando em melhorá-lo e mantê-lo legível para o próximo dar continuidade. Código testado e sem dependências e com pouco código
* Michael Feathers
   - Importância ao código, dedicação de tempo e concentração
* Ron Jeffries
   - Testes, expressividade no objetivo do código, sem duplicação de código, código pequeno e sem complexidade, número mínimo de classes, entidades, módulos funções, entre outros
* Ward Cunningham
   - Código traz a solução esperada para o problema, programador fazer parecer que a linguagem foi feita para o problema

## 1. Nomenclatura

### 1.1 Evite Números Mágicos

### A Regra do Escoteiro: "Deixe a área do acampamento mais limpa do que você a encontrou"
* Prevenção na degradação do código
   * Melhorias (pequenas ou grandes)
      - Troque o nome da variável
      - Divida uma função que esteja grande demais
      - Simplificação do código
      - Remova repetição de código
      - Reduza uma instrução `if` aninhada (cadeia de `if - else`)

### 1.2 Nomes Significativos
   * Use nomes que revelem seu propósito
      - Nomeie uma variável/função/classe com um nome intuitivo ao seu propósito
      - Altere os nomes para um nome melhor sempre que puder
      - Evite comentários para explicar o que tal variável/função/classe representa (Exemplo 1.1*)

* Exemplo 1.1*
``` Java
// Bad
int d; // tempo decorrido em dias

// Good
// Nome que a variável representa junto de sua unidade
int elapsedTimeInDays;
int daysSinceCreation;
int daysSinceModification;
int fileAgeInDays;
```
### 1.3 Evite informações falsas
   * Evite o uso de palavras que possa gerar ambiguidade
      - Abreviação de palavras pode acarretar em duplo sentido e mal interpretação
      - Evite palavras reservadas para nomeação (Exemplo 1.2*)
      - Evite nomes parecidos, fazendo distinções bem distintas entre elas para que não gere confusão na hora de decidir qual deve chamar (Exemplo 1.3*)

* Exemplo 1.2*
```
Grupo de contas: `accountList` esse nome só deveria ser utilizado se realmente se tratar de um `List`, porém como se trata de um grupo, a nomeação correta deveria ser: `accountGroup` ou `bunchOfAccounts`
```

* Exemplo 1.3*
``` Java
getActiveAccount();
getActiveAccounts();
getActiveAccountInfo();
```

### 1.4 Escreve nomes pronunciáveis
   * Escrever nomes que são difícies de pronunciar não é um hábito (Exemplo 1.4;1.5*)

* Exemplo 1.4*
``` Java
genymdhms // generation date, year, month, day, hour, minute e second
```

* Exemplo 1.5*
``` Java
// Bad
class DtaRcrd102 {
   private Date genymdhms;
   private Date modymdhms;
   private final String pszqint = "102";
   /* ... */
}

// Good
class Customer {
   private Date generationTimestamp;
   private Date modificationTimestamp;
   private final String recordId = "102";
   /* ... */
}
```

### 1.5 Escreve nomes possíveis de busca
   * Utilize nomes com um dígito apenas dentro de escopos locais e em métodos pequenos. "O tamanho de um nome deve ser proposcional ao tamanho do escopo" (Exemplo 1.6*)

* Exemplo 1.6*
``` Java
// Bad
for (int j = 0; j < 34; j++) {
   s += (t[j] * 4) / 5;
}

// Good
int realDaysPerIdealDay = 4;
const int WORK_DAYS_PER_WEEK = 5;
int sum = 0;

for (int j = 0; j < NUMBER_OF_TASKS; j++) {
   int realTaskDays = taskEstimate[j] * realDaysPerIdealDay;
   int realTaskWeeks = realDays / WORK_DAYS_PER_WEEK;

   sum += realTaskWeeks;
}
```

### 1.6 Interface e Implementações
   * Ao criar um `ABSTRACT FACTORY`, é comum usar `IShapeFactory` para a interafce e `ShapeFactory` para a implamentação. Ao invéz disso, é melhor usar `ShapeFactoryImp` e `CShaperFactory`

### 1.7 Evite mapeamento mental
   * Declaração de variáveis com uma só letra dentro de um iterador (`i, j, k...`), apesar de parecer convencional, em iteradores aninhados, é uma pratica ruim usar o nome `c` só porque o `a` e `b` já foram usados, dificultando o conceito original da variável.

### 1.8 Nomes de Classes
   * Use nomes com substantivos, como `Cliente`, `PaginaWiki`, `Conta`, `AnaliseEndereco`...
   * Evite nomes como `Gerente`, `Processador`, `Dados`, `Info`... que também não deve ser um verbo

### 1.9 Nomes de Métodos
   * O nome de um método deve possuir um verbo, como `postarPagamento`, `excluirPagina`, `salvar`...
   * Quando nomes de construtores estiverem sobrecarregados, use métodos factory estáticos com nomes de descrevam os parâmetros (Exemplo 1.7*)
      - OBS: Nestes casos, recomenda-se tornar os construtores privados

* Exemplo 1.7*
``` Java
// Bad
Complex fullcrumPoint = Complex.FromRealNumber(23.0);

// Good
Complex fullcrumPoint = new Complex(23.0);
```

### 1.10 Não dê uma de espertinho
   * Não use nomes que apenas o seu grupo interno saibam o significado, gírias, coloquialismos ou palavras de baixo calão (Exemplo 1.8*)

* Exemplo 1.8*
``` Java
// Bad
firmar();
cairFora();
holyHandGrenade();

// Good
terminar();
abortar();
deleteItems();
```

### 1.11 Selecione uma palavra por conceito
   * Evite usar termos diferentes para o mesmo propósito como `pegar`, `obter` e `recuperar` ou `controlador` e `gerenciador` (Exemplo 1.9*)

* Exemplo 1.9*
``` Java
GerenciadorDeDispositivo
ControladorDeProtocolo

// Qual a diferença no obtivo entre eles, se ambos partem do mesmo 'conceito'
```

### 1.12 Não faça trocadilhos
   * Evite usar a mesma palavra para dois conceitos diferentes (oposto da regra 'Selecione uma palavra por conceito' (1.11))

### 1.13 Use nomes a partir do domínio da solução
   * Não é um mau hábito utilizar termos técnicos de informática, algoritmo e outros termos que pessoas leigas não entenderiam, já que apenas outros programadores lerão nosso código.

### 1.14 Adicione um contexto significativo
   * Nomear classes, funções e namespaces pode funcionar na maioria dos casos, mas, em últimos casos, quando não há um contexto definido, colocar um preixo pode ajudar (Exemplo 1.10*) Porém não adicione contexto exageradamente sem a necessidade

* Exemplo 1.10*
``` Java
/*
Ao ver as varíaveis `firstName`, `lastName`, `stret`, `houseNumber`, `city`, `state` e `zipCode` juntas, é facíl de ver que se trata de um endereço.
Mas se ver apenas `state` solto em um método, pode ser difícil associá-lo à um contexto. Então, ao adicionar um prefixo, como `addrState`, ficou mais fácil de reconhecer do que se trata.
*/
```

## 2. Funções

### 2.1 Funções devem ser pequenas
   * As funções devem ser pequenas, objetivas e não tendo mais do que 20 linhas de códigos

### 2.2 Blocos e endentação
   * Blocos de instrução `if`, `else`, `while` e outros devem ter apenas uma linha, possivelmente uma chamada de uma função. Isso facilita pois, o nome da função por si só, muitas vezes, possui um valor auto descritivo e intuitivo

### 2.3 Faça apenas uma coisa
   * As funções devem fazer apenas uma coisa, devem fazê-las bem e devem fazer apenas ela

### 2.4 Ler o código de cima para baixo: Regra Decrescente
   * O código deve ser lido de cima para baixo, onde cada função seja seguida para o próximo nível conforme a ordem das funções seguindo uma 'hierarquia' (Regra Decrescente)

### 2.4 Parâmetros de funções
   * A quantidade ideal de parêmetros para uma função é zero (nulo); depois vem um (mônade); depois dois (díade). Sempre evite três (tríade) parêmtros se possível. Para mais parâmetros (políade), deve se ter um motivo bem especial

#### 2.1.1 Parâmetros lógicos
   * Passar valores booleano como parâmetro não é uma boa prática, pois é um indicativo de que a função faz uma coisa (se for `true`) ou outra (se for `false`)

#### 2.1.2 Parâmetros Mônades
   * Pode ser usado no contexto de uma pergunta para aquele parâmetro (Exemplo 2.1*) ou você pode estar tranformando-o em outra coisa e retornando-o (Exemplo 2.2*)

* Exemplo 2.1*
``` java
boolean fileExists("MyFile");
```

* Exemplo 2.2*
``` java
InputStream fileOpen("MyFile"); // Transforma a `String` do nome de um arquivo em um valor retornado por InputStream
```

#### 2.1.3 Parâmetros Díades
   * Utiliza-se parâmetros díades quando ambos os valores são 'componentes de um único valor'! (Exemplo 2.3;2.4*)

* Exemplo 2.3*
``` java
// Bad
// `outputStream` e `name` não são components do mesmo valor
writeField(outputStream, name);

// Good
outputStream.writeField(name); // Dessa forma, você transforma o `writeField` em um membro de `outputStream`
```

* Exemplo 2.4*
``` java
new Point(0, 0); // Considerando um plano cartesiano, é natural que receba as coordenadas 'x' e 'y'
```

### 2.2 Evite efeitos colaterais
   * "Sua função promete fazer apenas, mas ela também faz outras coisas encondidas" (Exemplo 2.5*). Garanta que a sua função faça apenas aquilo que ele diz que faz, pois, corre o risco de fazer outra coisa sem perceber

* Exemplo 2.4*
``` java
/*
A função `checkPassword` efetua uma validaçã da senha de um usuário, porém esta executando a inicialização da sessão ao chamar `Session.initialize()`. Esse é o efeito colateral!
*/
public class UserValidator {
   private Cryptographer cryptographer;

   public boolean checkPassword(String userName, String password) {
      user user = UserGateway.findByName(userName);
      if (user != User.NULL) {
         String codedPhrase = user.getPhraseEncodedByPassword();
         String phrase = cryptographer.decrypt(codedPhrase, password);
         if ("Valid Password".equals(phare)) {
            Session.initialize();
            return true;
         }
      }
      return false;
   }
}

/*
Dessa forma previne o efeito colateral, apesar de que vai contra o "Faça apenas uma coisa" (2.3)
*/
public class UserValidator {
   private Cryptographer cryptographer;

   public boolean checkPasswordAndInitializeSession(String userName, String password) {
      user user = UserGateway.findByName(userName);
      if (user != User.NULL) {
         String codedPhrase = user.getPhraseEncodedByPassword();
         String phrase = cryptographer.decrypt(codedPhrase, password);
         if ("Valid Password".equals(phare)) {
            Session.initialize();
            return true;
         }
      }
      return false;
   }
}
```

### 2.3 Separação comando-consulta
   * As funções devem apenas fazer ou responder algo, mas nunca ambos. Ela deve apenas alterar o estado ou buscar o valor do estado (Exemplo 2.5*)

* Exemplo 2.4*
``` java
// Bad
public boolean set(String attribute, String value);

/*
Difícil interpretar o que está sendo verificado nesta condição, ele está verificando se o atributo "username" receberu anteriormente o valor "unclebob" ou se o atributo "username" obteve êxito ao receber o valor "unclebob"?
*/
if (set("username", "unclebob")) {
   /* ... */
}

// Good
if (attributeExists("username")) {
   setAttribute("username", "unclebob")
   /* ... */
}
```

## 3. Estrutura Switch

### 3.1 Evite quando puder
   * É difícil criar uma estrutura `switch` pequena, pois elas sempre fazem 'n' coisas, o que vai contra a regra 'Faça apenas uma coisa' (2.3), além de ir contra o princípio de 'Aberto-Fechado', pois precisa alterá-lo, adicionando novos `cases` sempre que um novo argumento é adicionado

## 4. Exceções

### 4.1 Prefira exceções a retorno de códigos de erro (Reler)

### 4.2 Extraia os blocos `try/catch`

## 5. Evite repetição
   * POO; Programação Estruturada; Programação Orientada a Aspectos; programação Orientada a Componentes
   * Acima alguns exemplos de estruturas que ajudam na redução e eleminação de repetição de código
