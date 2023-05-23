# Capítulo 14: Gerenciamento de Estado com Redux e MobX

O gerenciamento de estado é uma parte essencial no desenvolvimento de aplicativos Flutter e existem diferentes abordagens para lidar com esse desafio. Neste capítulo, exploraremos duas dessas abordagens populares: Redux e MobX. Veremos como implementar o Redux em um aplicativo Flutter e também como utilizar o MobX para gerenciar o estado de forma eficiente.

## 14.1 Introdução ao Redux

O Redux é uma biblioteca de gerenciamento de estado baseada em fluxo de dados unidirecional. Ele segue o princípio de que o estado de um aplicativo deve ser armazenado em uma única árvore de estado, tornando-o previsível e fácil de rastrear. O Redux é composto por três partes principais: **store**, **actions** e **reducers**.

- **Store**: é um objeto que armazena o estado do aplicativo e permite acessá-lo e modificá-lo.
- **Actions**: são objetos que representam uma intenção de alterar o estado do aplicativo. Eles são despachados para o store.
- **Reducers**: são funções puras que recebem uma ação e o estado atual do aplicativo e retornam um novo estado com base nessa ação.

## 14.2 Implementando Redux em um aplicativo Flutter

Para utilizar o Redux em um aplicativo Flutter, é necessário adicionar algumas dependências ao arquivo `pubspec.yaml`:

```yaml
dependencies:
  flutter_redux: ^0.8.2
  redux: ^5.0.0
```

Após adicionar as dependências, podemos criar as classes que representam o Redux em nosso aplicativo. Vamos criar um exemplo simples de um contador utilizando o Redux:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_redux/flutter_redux.dart';
import 'package:redux/redux.dart';

// Actions
enum CounterAction { increment, decrement }

// Reducer
int counterReducer(int state, dynamic action) {
  if (action == CounterAction.increment) {
    return state + 1;
  } else if (action == CounterAction.decrement) {
    return state - 1;
  }
  return state;
}

// Store
final store = Store<int>(counterReducer, initialState: 0);

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return StoreProvider<int>(
      store: store,
      child: MaterialApp(
        title: 'Gerenciamento de Estado com Redux',
        theme: ThemeData(
          primarySwatch: Colors.blue,
        ),
        home: MyHomePage(),
      ),
    );
  }
}

class MyHomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Gerenciamento de Estado com Redux'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            Text(
              'Contagem:',
              style: TextStyle(fontSize: 24),
            ),
            StoreConnector<int, String>(
              converter: (store) => store.state.toString(),
              builder: (context, count) {
                return Text(
                  count,
                  style: TextStyle(fontSize: 48, fontWeight: FontWeight.bold),
                );
              },
            ),
          ],
        ),
      ),
      floatingActionButton: Column(
        mainAxisAlignment: MainAxisAlignment.end,
        crossAxisAlignment: CrossAxisAlignment.end,
        children: [
          FloatingActionButton(
            onPressed: () {
              store

.dispatch(CounterAction.increment);
            },
            child: Icon(Icons.add),
          ),
          SizedBox(height: 16),
          FloatingActionButton(
            onPressed: () {
              store.dispatch(CounterAction.decrement);
            },
            child: Icon(Icons.remove),
          ),
        ],
      ),
    );
  }
}
```

No exemplo acima, criamos as seguintes partes do Redux:

- Definimos as ações no enum `CounterAction`, representando o incremento e decremento do contador.
- Implementamos a função `counterReducer` que recebe uma ação e o estado atual e retorna o novo estado com base na ação.
- Criamos o store com o reducer e o estado inicial.
- No widget `MyApp`, envolvemos a `MaterialApp` com o `StoreProvider` e fornecemos a instância do store.
- Utilizamos o `StoreConnector` para acessar o estado do store e atualizar a interface do usuário de acordo.

O exemplo acima demonstra como utilizar o Redux em um aplicativo Flutter. O estado é armazenado no store e pode ser acessado e modificado por meio das ações e reducers.

## 14.3 Introdução ao MobX

O MobX é uma biblioteca de gerenciamento de estado que utiliza o conceito de observáveis e reações para manter o estado consistente e atualizado. Com o MobX, é possível declarar quais partes do seu código dependem de um determinado estado e o MobX se encarrega de atualizá-las automaticamente quando o estado muda.

## 14.4 Implementando MobX em um aplicativo Flutter

Para utilizar o MobX em um aplicativo Flutter, é necessário adicionar algumas dependências ao arquivo `pubspec.yaml`:

```yaml
dependencies:
  flutter_mobx: ^2.0.2
  mobx: ^3.0.1
```

Após adicionar as dependências, podemos criar as classes que representam o MobX em nosso aplicativo. Vamos criar um exemplo simples de um contador utilizando o MobX:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_mobx/flutter_mobx.dart';
import 'package:mobx/mobx.dart';

// Store
class CounterStore = _CounterStore with _$CounterStore;

abstract class _CounterStore with Store {
  @observable
  int count = 0;

  @action
  void increment() {
    count++;
  }

  @action
  void decrement() {
    count--;
  }
}

void main() {
  final counterStore = CounterStore();
  runApp(MyApp(counterStore: counterStore));
}

class MyApp extends StatelessWidget {
  final CounterStore counterStore;

  MyApp({required this.counterStore});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Gerenciamento de Estado com MobX',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: MyHomePage(counterStore: counterStore),
    );
  }
}

class MyHomePage extends StatelessWidget {
  final CounterStore counterStore;

  MyHomePage({required this.counterStore});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Gerenciamento de Estado com MobX'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            Text(
              'Contagem:',
              style: TextStyle(fontSize: 24),
            ),
            Observer(
              builder: (_) {
                return Text(
                  counterStore.count.toString(),
                  style: TextStyle(fontSize: 48, fontWeight: FontWeight.bold),
                );
             

 },
            ),
          ],
        ),
      ),
      floatingActionButton: Column(
        mainAxisAlignment: MainAxisAlignment.end,
        crossAxisAlignment: CrossAxisAlignment.end,
        children: [
          FloatingActionButton(
            onPressed: () {
              counterStore.increment();
            },
            child: Icon(Icons.add),
          ),
          SizedBox(height: 16),
          FloatingActionButton(
            onPressed: () {
              counterStore.decrement();
            },
            child: Icon(Icons.remove),
          ),
        ],
      ),
    );
  }
}
```

No exemplo acima, criamos uma classe `CounterStore` que utiliza as anotações do MobX para tornar a propriedade `count` observável e as funções `increment` e `decrement` como ações. Criamos uma instância do `CounterStore` no `main` e a fornecemos ao `MyApp` como parâmetro.

No widget `MyHomePage`, utilizamos o `Observer` do MobX para observar as mudanças no estado do `CounterStore` e atualizar automaticamente a interface do usuário quando o estado é modificado.

O exemplo acima demonstra como utilizar o MobX em um aplicativo Flutter. As propriedades observáveis e as ações garantem que o estado seja atualizado automaticamente e que as partes dependentes sejam notificadas corretamente.

Com o Redux, o MobX e o Provider, você tem uma variedade de opções para gerenciar o estado em seus aplicativos Flutter. Cada abordagem tem suas vantagens e é importante escolher a que melhor se adequa às necessidades do seu projeto.

## Conclusão

Neste capítulo, exploramos o Redux, o MobX e suas implementações em aplicativos Flutter. Vimos como utilizar essas bibliotecas para gerenciar o estado de forma eficiente, mantendo uma arquitetura previsível e escalável. Compreender e dominar essas técnicas de gerenciamento de estado é fundamental para criar aplicativos Flutter robustos e de alto desempenho.

Continue aprendendo e explorando essas bibliotecas, pois elas são ferramentas poderosas para facilitar o desenvolvimento de aplicativos complexos e garantir a consistência do estado em toda a sua aplicação.