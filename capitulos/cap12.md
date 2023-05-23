# Capítulo 12: Gerenciamento de Estado com Provider

No desenvolvimento de aplicativos Flutter, o gerenciamento de estado é um aspecto crucial para garantir a consistência e a atualização correta dos dados em toda a aplicação. O Flutter oferece várias soluções para o gerenciamento de estado, e uma delas é a biblioteca Provider.

## 12.1 Introdução ao Gerenciamento de Estado

O gerenciamento de estado refere-se à forma como os dados são armazenados e compartilhados entre os diferentes componentes de um aplicativo. Em vez de armazenar o estado diretamente em cada widget ou passá-lo manualmente por meio de parâmetros, é preferível utilizar uma abordagem centralizada para facilitar a atualização e o acesso aos dados.

## 12.2 Gerenciamento de Estado com Provider

O Provider é uma biblioteca popular e poderosa para o gerenciamento de estado em aplicativos Flutter. Ele utiliza o conceito de Injeção de Dependência (DI - Dependency Injection) para fornecer acesso ao estado em diferentes partes do aplicativo.

### Instalação do Provider

Antes de começarmos a utilizar o Provider, é necessário adicionar a dependência correspondente ao arquivo `pubspec.yaml` do projeto:

```yaml
dependencies:
  flutter:
    sdk: flutter
  provider: ^6.0.0
```

Após adicionar a dependência, execute o comando `flutter pub get` para atualizar as dependências do projeto.

### Criando um Provider

O primeiro passo para utilizar o Provider é criar uma classe que represente o estado que desejamos gerenciar. Essa classe é conhecida como `ChangeNotifier` e deve estender a classe `ChangeNotifier` fornecida pelo Provider. Vamos criar um exemplo simples de um contador:

```dart
import 'package:flutter/foundation.dart';

class Counter extends ChangeNotifier {
  int _count = 0;

  int get count => _count;

  void increment() {
    _count++;
    notifyListeners();
  }
}
```

No exemplo acima, criamos a classe `Counter` que estende `ChangeNotifier`. Ela possui um atributo `_count` que representa o valor do contador e um método `increment()` que incrementa o contador e notifica os ouvintes sobre a mudança utilizando o método `notifyListeners()`.

### Fornecendo o Estado

Para disponibilizar o estado do contador para os widgets do aplicativo, devemos fornecê-lo como um `ChangeNotifierProvider`. Podemos fazer isso no widget raiz do aplicativo, normalmente no método `build()` da classe `MaterialApp`. Veja um exemplo:

```dart
import 'package:flutter/material.dart';
import 'package:provider/provider.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return ChangeNotifierProvider(
      create: (context) => Counter(),
      child: MaterialApp(
        title: 'Gerenciamento de Estado com Provider',
        theme: ThemeData(
          primarySwatch: Colors.blue,
        ),
        home: MyHomePage(),
      ),
    );
  }
}
```

No exemplo acima, envolvemos o widget `MaterialApp` com o `ChangeNotifierProvider` e fornecemos uma instância de `Counter` utilizando o parâmetro `create`. Dessa forma, o estado do contador estará disponível para todos os widgets descendentes desse `ChangeNotifierProvider`.

### Consumindo o Estado

Agora que fornecemos o estado do contador,

 podemos consumi-lo nos widgets que precisam acessar e exibir o valor do contador. Para isso, utilizamos o widget `Consumer` fornecido pelo Provider. Veja um exemplo de como utilizar o `Consumer` para exibir o valor do contador em um `Text`:

```dart
import 'package:flutter/material.dart';
import 'package:provider/provider.dart';

class MyHomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Gerenciamento de Estado com Provider'),
      ),
      body: Center(
        child: Consumer<Counter>(
          builder: (context, counter, child) {
            return Text(
              'Contagem: ${counter.count}',
              style: TextStyle(fontSize: 24),
            );
          },
        ),
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: () {
          Provider.of<Counter>(context, listen: false).increment();
        },
        child: Icon(Icons.add),
      ),
    );
  }
}
```

No exemplo acima, utilizamos o `Consumer<Counter>` para acessar o estado do contador. O método `builder` é chamado sempre que o estado do contador é atualizado, permitindo a atualização do widget que exibe o valor do contador.

Além disso, adicionamos um `FloatingActionButton` que incrementa o contador quando pressionado. Utilizamos `Provider.of<Counter>(context, listen: false)` para obter a instância do contador e chamamos o método `increment()`.

### Conclusão

O Provider é uma biblioteca poderosa para o gerenciamento de estado em aplicativos Flutter. Ele simplifica a comunicação entre os componentes do aplicativo, permitindo a atualização e o acesso aos dados de forma eficiente. Com o Provider, você pode desenvolver aplicativos Flutter escaláveis e de fácil manutenção.

Neste capítulo, exploramos os conceitos básicos do gerenciamento de estado com Provider e criamos um exemplo simples de um contador. Agora você está pronto para utilizar o Provider em seus próprios aplicativos e aproveitar seus benefícios no desenvolvimento Flutter.