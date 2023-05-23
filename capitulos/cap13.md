# Capítulo 13: Gerenciamento de Estado com BLoC (Business Logic Component)

O gerenciamento de estado é uma parte fundamental no desenvolvimento de aplicativos Flutter, e o padrão BLoC (Business Logic Component) é uma abordagem popular para esse propósito. Neste capítulo, exploraremos o conceito de BLoC e como implementá-lo em um aplicativo Flutter.

## 13.1 Introdução ao BLoC

O BLoC é um padrão arquitetural que separa a lógica de negócios (business logic) da interface do usuário. Ele facilita o gerenciamento de estado, a reatividade e a comunicação entre os diferentes componentes de um aplicativo. O BLoC é baseado em streams e eventos, onde os eventos são enviados para o BLoC, a lógica de negócios processa esses eventos e emite estados atualizados que são consumidos pela interface do usuário.

## 13.2 Implementando um BLoC

Para implementar um BLoC em um aplicativo Flutter, geralmente são necessárias as seguintes dependências:

```yaml
dependencies:
  flutter:
    sdk: flutter
  bloc: ^7.0.0
  flutter_bloc: ^7.0.0
```

Após adicionar as dependências, podemos criar a classe que representa o BLoC. Vamos criar um exemplo simples de um contador usando o BLoC:

```dart
import 'dart:async';
import 'package:bloc/bloc.dart';
import 'package:meta/meta.dart';

// Eventos
abstract class CounterEvent {}

class IncrementEvent extends CounterEvent {}

// Estados
abstract class CounterState {}

class CounterInitialState extends CounterState {}

class CounterUpdatedState extends CounterState {
  final int count;

  CounterUpdatedState(this.count);
}

// BLoC
class CounterBloc extends Bloc<CounterEvent, CounterState> {
  CounterBloc() : super(CounterInitialState());

  int _count = 0;

  @override
  Stream<CounterState> mapEventToState(CounterEvent event) async* {
    if (event is IncrementEvent) {
      _count++;
      yield CounterUpdatedState(_count);
    }
  }
}
```

No exemplo acima, criamos a classe `CounterBloc` que estende a classe `Bloc` fornecida pelo pacote `bloc`. Definimos os eventos através da classe `CounterEvent` e os estados através da classe `CounterState`. Em seguida, implementamos a lógica do BLoC no método `mapEventToState`, onde incrementamos o contador quando o evento `IncrementEvent` é recebido e emitemos o estado `CounterUpdatedState` com o novo valor do contador.

Para utilizar o BLoC em um widget, precisamos adicionar o `BlocProvider` como um ancestral desse widget. Podemos fazer isso no widget raiz do aplicativo, normalmente no método `build()` da classe `MaterialApp`. Veja um exemplo:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_bloc/flutter_bloc.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return BlocProvider(
      create: (context) => CounterBloc(),
      child: MaterialApp(
        title: 'Gerenciamento de Estado com BLoC',
        theme: ThemeData(
          primarySwatch: Colors.blue,
        ),
        home: MyHomePage(),
      ),
    );
  }
}
```

No exemplo acima, envolvemos o widget

 `MaterialApp` com o `BlocProvider` e fornecemos a instância do `CounterBloc` através do parâmetro `create`. Isso tornará o BLoC disponível para todos os widgets descendentes desse `BlocProvider`.

Agora podemos utilizar o BLoC em um widget, assim como fizemos com o Provider no Capítulo anterior. Podemos consumir o estado do BLoC e atualizar a interface do usuário de acordo. Veja um exemplo:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_bloc/flutter_bloc.dart';

class MyHomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Gerenciamento de Estado com BLoC'),
      ),
      body: Center(
        child: BlocBuilder<CounterBloc, CounterState>(
          builder: (context, state) {
            if (state is CounterInitialState) {
              return Text(
                'Contagem: 0',
                style: TextStyle(fontSize: 24),
              );
            } else if (state is CounterUpdatedState) {
              return Text(
                'Contagem: ${state.count}',
                style: TextStyle(fontSize: 24),
              );
            }
            return Container();
          },
        ),
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: () {
          context.read<CounterBloc>().add(IncrementEvent());
        },
        child: Icon(Icons.add),
      ),
    );
  }
}
```

No exemplo acima, utilizamos o `BlocBuilder<CounterBloc, CounterState>` para consumir o estado do BLoC e atualizar a interface do usuário de acordo. O método `builder` é chamado sempre que o estado do BLoC é atualizado, permitindo a atualização do widget que exibe o valor do contador.

Além disso, adicionamos um `FloatingActionButton` que envia o evento `IncrementEvent` para o BLoC quando pressionado. Utilizamos `context.read<CounterBloc>().add(IncrementEvent())` para obter a instância do BLoC e enviar o evento.

### Conclusão

O padrão BLoC é uma abordagem poderosa para o gerenciamento de estado em aplicativos Flutter. Ele separa a lógica de negócios da interface do usuário, facilitando a manutenção e a escalabilidade do código. Com o BLoC, você pode criar aplicativos Flutter com uma arquitetura robusta e de fácil manutenção.

Neste capítulo, introduzimos o conceito de BLoC e mostramos como implementá-lo em um aplicativo Flutter. Criamos um exemplo simples de um contador usando o BLoC e explicamos como consumir o estado do BLoC em um widget.

Agora você está preparado para utilizar o padrão BLoC em seus próprios aplicativos Flutter e aproveitar os benefícios do gerenciamento de estado eficiente e reativo.