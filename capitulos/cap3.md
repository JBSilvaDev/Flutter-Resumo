# Capítulo 3: Componentes do Flutter

Neste capítulo, vamos explorar os componentes do Flutter, que são os blocos de construção fundamentais para criar interfaces de usuário ricas e interativas. O Flutter oferece uma ampla variedade de componentes pré-construídos que você pode usar em seus aplicativos. Veremos os principais tipos de componentes e como utilizá-los. Vamos começar!

## 3.1 Componentes Básicos
Os componentes básicos do Flutter são os elementos de interface de usuário mais simples, como texto, botões e imagens. Esses componentes são amplamente utilizados em qualquer aplicativo Flutter. Veremos alguns exemplos dos componentes básicos mais comuns:

### 3.1.1 Texto
O componente Texto permite exibir texto na interface do usuário. É possível definir a fonte, tamanho, estilo e alinhamento do texto. Veja um exemplo:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Exemplo de Texto'),
        ),
        body: Center(
          child: Text(
            'Olá, Flutter!',
            style: TextStyle(
              fontSize: 24,
              fontWeight: FontWeight.bold,
            ),
          ),
        ),
      ),
    );
  }
}
```

### 3.1.2 Botão
O componente Botão permite adicionar interatividade ao seu aplicativo. Você pode criar botões com diferentes estilos e comportamentos. Veja um exemplo:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  void _onButtonPressed() {
    print('Botão pressionado!');
  }

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Exemplo de Botão'),
        ),
        body: Center(
          child: RaisedButton(
            onPressed: _onButtonPressed,
            child: Text('Clique aqui'),
          ),
        ),
      ),
    );
  }
}
```

### 3.1.3 Imagem
O componente Imagem permite exibir imagens em seu aplicativo. Você pode carregar imagens de diferentes fontes, como da internet ou do sistema de arquivos local. Veja um exemplo:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Exemplo de Imagem'),
        ),
        body: Center(
          child: Image.network(
            'https://exemplo.com/imagem.jpg',
          ),
        ),
      ),
    );
  }
}
```

## 3.2 Componentes de Layout
Os componentes de layout são responsáveis por organizar e posicionar os componentes em uma tela. O Flutter oferece uma variedade de componentes de layout flexíveis que se adaptam a diferentes necessidades de design. Veremos alguns exemplos dos componentes de layout mais comuns:

### 3.2.1 Container
O componente Container é um dos componentes de layout mais versáteis do Flutter. Ele permite definir o tamanho, a cor, as margens e os preenchimentos dos componentes filhos. Veja um exemplo:

```dart
import 'package:flutter/material.dart';



void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Exemplo de Container'),
        ),
        body: Center(
          child: Container(
            width: 200,
            height: 200,
            color: Colors.blue,
            child: Text(
              'Conteúdo do Container',
              style: TextStyle(
                color: Colors.white,
                fontSize: 24,
              ),
            ),
          ),
        ),
      ),
    );
  }
}
```

### 3.2.2 Column e Row
Os componentes Column e Row permitem organizar componentes em colunas ou linhas, respectivamente. Eles são muito úteis quando você precisa exibir vários componentes verticalmente ou horizontalmente. Veja um exemplo:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Exemplo de Column e Row'),
        ),
        body: Center(
          child: Column(
            mainAxisAlignment: MainAxisAlignment.center,
            children: [
              Text('Texto 1'),
              Text('Texto 2'),
              Row(
                mainAxisAlignment: MainAxisAlignment.center,
                children: [
                  Icon(Icons.star),
                  Icon(Icons.star),
                  Icon(Icons.star),
                ],
              ),
            ],
          ),
        ),
      ),
    );
  }
}
```

## 3.3 Componentes de Entrada
Os componentes de entrada permitem aos usuários inserir dados e interagir com o aplicativo. O Flutter oferece uma variedade de componentes de entrada prontos para uso, como campos de texto, botões de opção e caixas de seleção. Veremos alguns exemplos dos componentes de entrada mais comuns:

### 3.3.1 TextField
O componente TextField permite que os usuários digitem texto em seu aplicativo. Você pode definir várias propriedades, como tipo de teclado, limite de caracteres e ação a ser executada quando o usuário pressionar "Enter". Veja um exemplo:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  final TextEditingController _textEditingController = TextEditingController();

  void _onButtonPressed() {
    String enteredText = _textEditingController.text;
    print('Texto digitado: $enteredText');
  }

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Exemplo de TextField'),
        ),
        body: Center(
          child: Column(
            mainAxisAlignment: MainAxisAlignment.center,
            children: [
              TextField(
                controller: _textEditingController,
                decoration: InputDecoration(
                  labelText: 'Digite algo',
                ),
              ),
              RaisedButton(
                onPressed: _onButtonPressed,
                child: Text('Clique aqui'),
              ),
            ],
          ),
        ),
      ),
    );
  }
}
```

### 3.3.2 Checkbox
O componente Checkbox permite que os usuários selecionem uma ou mais opções em um conjunto de opções. Você pode definir o estado inicial do checkbox e também executar uma ação quando o estado do checkbox for alterado. Veja um exemplo:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatefulWidget {
  @override
  _MyAppState createState() => _MyAppState();
}

class

 _MyAppState extends State<MyApp> {
  bool _isChecked = false;

  void _onCheckboxChanged(bool value) {
    setState(() {
      _isChecked = value;
    });
  }

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Exemplo de Checkbox'),
        ),
        body: Center(
          child: Checkbox(
            value: _isChecked,
            onChanged: _onCheckboxChanged,
          ),
        ),
      ),
    );
  }
}
```

## 3.4 Componentes de Listagem
Os componentes de listagem são usados para exibir uma lista de itens em seu aplicativo. O Flutter oferece componentes de listagem flexíveis e eficientes que podem lidar com listas grandes de maneira eficaz. Veremos alguns exemplos dos componentes de listagem mais comuns:

### 3.4.1 ListView
O componente ListView é usado para exibir uma lista rolável de itens. Ele pode ser usado tanto para listas verticais quanto horizontais. Veja um exemplo de ListView vertical:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  final List<String> items = [
    'Item 1',
    'Item 2',
    'Item 3',
    'Item 4',
    'Item 5',
  ];

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Exemplo de ListView'),
        ),
        body: ListView(
          children: items.map((item) => ListTile(title: Text(item))).toList(),
        ),
      ),
    );
  }
}
```

### 3.4.2 GridView
O componente GridView é usado para exibir uma grade de itens. Ele é útil quando você precisa exibir itens em uma grade regular, como uma galeria de imagens. Veja um exemplo de GridView:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  final List<String> items = [
    'Item 1',
    'Item 2',
    'Item 3',
    'Item 4',
    'Item 5',
  ];

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Exemplo de GridView'),
        ),
        body: GridView.count(
          crossAxisCount: 2,
          children: items.map((item) => Card(child: Center(child: Text(item)))).toList(),
        ),
      ),
    );
  }
}
```

## 3.5 Componentes de Rolagem
Os componentes de rolagem são usados quando você precisa exibir um conteúdo maior do que o espaço disponível na tela. O Flutter oferece diferentes tipos de componentes de rolagem que podem ser usados para lidar com diferentes cenários. Veremos alguns exemplos dos componentes de rolagem mais comuns:

### 3.5.1 SingleChildScrollView
O componente SingleChildScrollView é usado quando você precisa rolar apenas um único componente filho, como um formulário longo. Veja um exemplo:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Exemplo de SingleChildScrollView'),
        ),
        body: SingleChildScrollView(
          child: Column(
            children: List

.generate(
              20,
              (index) => Text('Item $index'),
            ),
          ),
        ),
      ),
    );
  }
}
```

### 3.5.2 ListView.builder
O componente ListView.builder é usado quando você precisa exibir uma lista grande e dinâmica de itens. Ele cria os itens conforme necessário, economizando recursos e melhorando o desempenho. Veja um exemplo:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  final List<String> items = List.generate(1000, (index) => 'Item $index');

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Exemplo de ListView.builder'),
        ),
        body: ListView.builder(
          itemCount: items.length,
          itemBuilder: (context, index) => ListTile(
            title: Text(items[index]),
          ),
        ),
      ),
    );
  }
}
```

Parabéns! Agora você conhece os principais componentes do Flutter e como utilizá-los. No próximo capítulo, abordaremos tópicos mais avançados, como navegação, gerenciamento de estado e chamadas de API. Continue aprendendo e explorando o mundo do desenvolvimento de aplicativos com Flutter!