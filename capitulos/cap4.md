## Capítulo 4: Temas Avançados de UI

Neste capítulo, exploraremos alguns temas avançados de UI no Flutter. Vamos aprender sobre personalização de componentes, responsividade, animações avançadas e efeitos de transição. Esses conceitos ajudarão você a criar interfaces de usuário sofisticadas e envolventes para seus aplicativos.

### 4.1 Personalização de Componentes

A personalização de componentes no Flutter permite que você adapte a aparência e o comportamento dos widgets de acordo com suas necessidades. Você pode alterar as cores, fontes, espaçamento e muito mais. Veja um exemplo de personalização de um botão:

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
          title: Text('Exemplo de Personalização de Componentes'),
        ),
        body: Center(
          child: ElevatedButton(
            style: ElevatedButton.styleFrom(
              primary: Colors.blue, // Define a cor de fundo do botão
              textStyle: TextStyle(fontSize: 20), // Define o estilo do texto do botão
              padding: EdgeInsets.symmetric(horizontal: 16, vertical: 8), // Define o espaçamento interno do botão
            ),
            onPressed: () {
              // Ação do botão
            },
            child: Text('Clique Aqui'),
          ),
        ),
      ),
    );
  }
}
```

### 4.2 Responsividade e Layout Responsivo

O Flutter oferece recursos poderosos para criar interfaces responsivas que se adaptam a diferentes tamanhos de tela e orientações. Você pode utilizar media queries, layouts flexíveis e regras de posicionamento para criar interfaces fluidas e dimensionadas corretamente em dispositivos diferentes. Veja um exemplo de uso do MediaQuery para tornar um texto responsivo:

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
          title: Text('Exemplo de Responsividade'),
        ),
        body: Center(
          child: MediaQuery.of(context).size.width > 600 // Verifica a largura da tela
              ? Text(
                  'Tela grande',
                  style: TextStyle(fontSize: 24),
                )
              : Text(
                  'Tela pequena',
                  style: TextStyle(fontSize: 16),
                ),
        ),
      ),
    );
  }
}
```

### 4.3 Design Responsivo com MediaQuery

O MediaQuery é uma classe no Flutter que fornece informações sobre a mídia atual, como tamanho da tela, orientação e densidade de pixels. Você pode usar o MediaQuery para criar designs responsivos que se adaptam automaticamente às características do dispositivo. Veja um exemplo de uso do MediaQuery para exibir diferentes layouts com base na orientação da tela:

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
          title: Text('Exemplo de Design Responsivo'),
        ),
        body: OrientationBuilder(
          builder: (context, orientation) {
            return Center(
              child: MediaQuery.of(context).orientation == Orientation.portrait // Verifica a orientação da tela
                  ? Text

(
                      'Modo Retrato',
                      style: TextStyle(fontSize: 24),
                    )
                  : Text(
                      'Modo Paisagem',
                      style: TextStyle(fontSize: 24),
                    ),
            );
          },
        ),
      ),
    );
  }
}
```

### 4.4 Animações Avançadas

As animações são uma parte essencial de qualquer interface de usuário atraente. O Flutter oferece uma variedade de recursos para criar animações suaves e interativas em seus aplicativos. Você pode animar propriedades como posição, tamanho, rotação, opacidade e muito mais. Veja um exemplo de animação simples de um contêiner:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatefulWidget {
  @override
  _MyAppState createState() => _MyAppState();
}

class _MyAppState extends State<MyApp> with SingleTickerProviderStateMixin {
  AnimationController _animationController;
  Animation<double> _animation;

  @override
  void initState() {
    super.initState();

    _animationController = AnimationController(
      duration: Duration(seconds: 2),
      vsync: this,
    );

    _animation = Tween<double>(begin: 0, end: 200).animate(_animationController);

    _animationController.repeat(reverse: true);
  }

  @override
  void dispose() {
    _animationController.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Exemplo de Animação'),
        ),
        body: Center(
          child: AnimatedBuilder(
            animation: _animation,
            builder: (context, child) {
              return Container(
                width: _animation.value,
                height: _animation.value,
                color: Colors.blue,
              );
            },
          ),
        ),
      ),
    );
  }
}
```

### 4.5 Efeitos de Transição

Os efeitos de transição são uma ótima maneira de fornecer feedback visual durante a navegação entre telas ou ao exibir/modificar conteúdo. O Flutter oferece uma variedade de transições pré-definidas, como fade, slide e scale, além da capacidade de criar transições personalizadas. Veja um exemplo de uso da transição de fade entre duas telas:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Screen1(),
    );
  }
}

class Screen1 extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Tela 1'),
      ),
      body: Center(
        child: ElevatedButton(
          onPressed: () {
            Navigator.push(
              context,
              PageRouteBuilder(
                pageBuilder: (context, animation, secondaryAnimation) => Screen2(),
                transitionsBuilder: (context, animation, secondaryAnimation, child) {
                  return FadeTransition(
                    opacity: animation,
                    child: child,
                  );
                },
              ),
            );
          },
          child: Text('Ir para Tela 2'),
        ),
      ),
    );
  }
}

class Screen2 extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Tela 2'),
      ),
      body: Center(
        child: Text('Tela 2'),
      ),
    );
 

 }
}
```

Neste capítulo, você aprendeu sobre personalização de componentes, responsividade, animações avançadas e efeitos de transição. Esses são apenas alguns dos temas avançados de UI que o Flutter oferece. Continue explorando e experimentando esses conceitos para criar interfaces de usuário incríveis em seus aplicativos Flutter.