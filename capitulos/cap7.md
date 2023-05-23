## Capítulo 7: Widgets Avançados e Bibliotecas

Neste capítulo, iremos explorar widgets avançados e a utilização de bibliotecas para expandir as funcionalidades do Flutter. Veremos exemplos detalhados de alguns desses widgets e bibliotecas populares.

### 7.1 Widgets de UI Avançados

#### 7.1.1 DataTable

O widget `DataTable` é útil quando você precisa exibir dados tabulares em forma de tabela. Ele permite criar colunas e linhas para exibir informações organizadas. Veja um exemplo de uso do `DataTable`:

```dart
import 'package:flutter/material.dart';

class DataTableExample extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return DataTable(
      columns: [
        DataColumn(label: Text('ID')),
        DataColumn(label: Text('Nome')),
        DataColumn(label: Text('Idade')),
      ],
      rows: [
        DataRow(cells: [
          DataCell(Text('1')),
          DataCell(Text('João')),
          DataCell(Text('25')),
        ]),
        DataRow(cells: [
          DataCell(Text('2')),
          DataCell(Text('Maria')),
          DataCell(Text('30')),
        ]),
        DataRow(cells: [
          DataCell(Text('3')),
          DataCell(Text('Pedro')),
          DataCell(Text('35')),
        ]),
      ],
    );
  }
}

void main() {
  runApp(MaterialApp(
    home: Scaffold(
      appBar: AppBar(
        title: Text('Exemplo de DataTable'),
      ),
      body: Center(
        child: DataTableExample(),
      ),
    ),
  ));
}
```

Neste exemplo, criamos um `DataTable` com três colunas: ID, Nome e Idade. Em seguida, adicionamos três linhas de dados utilizando o `DataRow` e `DataCell`. Isso resulta em uma tabela exibindo as informações de forma organizada.

#### 7.1.2 Stepper

O widget `Stepper` é útil quando você precisa criar um processo de etapas sequenciais em seu aplicativo. Cada etapa é representada por um widget filho do `Stepper`. Veja um exemplo de uso do `Stepper`:

```dart
import 'package:flutter/material.dart';

class StepperExample extends StatefulWidget {
  @override
  _StepperExampleState createState() => _StepperExampleState();
}

class _StepperExampleState extends State<StepperExample> {
  int _currentStep = 0;

  List<Step> _steps = [
    Step(
      title: Text('Passo 1'),
      content: Text('Conteúdo do passo 1'),
    ),
    Step(
      title: Text('Passo 2'),
      content: Text('Conteúdo do passo 2'),
    ),
    Step(
      title: Text('Passo 3'),
      content: Text('Conteúdo do passo 3'),
    ),
  ];

  @override
  Widget build(BuildContext context) {
    return Stepper(
      currentStep: _currentStep,
      onStepContinue: () {
        if (_currentStep < _steps.length - 1) {
          setState(() {
            _currentStep++;
          });
        }
      },
      onStepCancel: () {
        if (_currentStep > 0) {
          setState(() {
            _currentStep--;
          });
        }
      },
      steps: _steps,
    );
  }
}

void main() {
  runApp(MaterialApp(
    home: Scaffold(
      appBar: AppBar(
        title: Text('Exemplo de Stepper'),
      ),
      body: Center

(
        child: StepperExample(),
      ),
    ),
  ));
}
```

Neste exemplo, criamos um `Stepper` com três etapas representadas pelo widget `Step`. Cada etapa possui um título e um conteúdo associado. Os botões de avançar (`onStepContinue`) e voltar (`onStepCancel`) são controlados por funções que atualizam o estado da variável `_currentStep`, permitindo a navegação entre as etapas.

### 7.2 Utilizando Bibliotecas e Pacotes Externos

O Flutter possui uma comunidade ativa que contribui com bibliotecas e pacotes para facilitar o desenvolvimento de aplicativos. Aqui estão alguns exemplos de bibliotecas populares do Flutter:

#### 7.2.1 Dio

O pacote `dio` é uma biblioteca para fazer requisições HTTP no Flutter de forma fácil e eficiente. Ele fornece uma API simples e poderosa para lidar com solicitações HTTP, incluindo suporte a autenticação, envio de dados em JSON, controle de cookies, entre outros recursos. Veja um exemplo de uso do pacote `dio`:

```dart
import 'package:dio/dio.dart';

void main() async {
  final dio = Dio();
  
  try {
    final response = await dio.get('https://api.example.com/posts');
    print(response.data);
  } catch (e) {
    print('Erro na requisição: $e');
  }
}
```

Neste exemplo, utilizamos o pacote `dio` para fazer uma requisição GET para uma API fictícia. O resultado é exibido no console.

#### 7.2.2 Provider

O pacote `provider` é uma biblioteca popular para gerenciamento de estado no Flutter. Ele segue o padrão de design "InheritedWidget" do Flutter, permitindo compartilhar dados entre widgets de forma eficiente. O `provider` simplifica o gerenciamento de estado e reduz a necessidade de usar widgets como `setState` e `InheritedWidget` diretamente. Veja um exemplo de uso do pacote `provider`:

```dart
import 'package:flutter/material.dart';
import 'package:provider/provider.dart';

class Counter with ChangeNotifier {
  int _count = 0;

  int get count => _count;

  void increment() {
    _count++;
    notifyListeners();
  }
}

class CounterApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return ChangeNotifierProvider(
      create: (context) => Counter(),
      child: MaterialApp(
        home: Scaffold(
          appBar: AppBar(
            title: Text('Exemplo de Provider'),
          ),
          body: Center(
            child: Column(
              mainAxisAlignment: MainAxisAlignment.center,
              children: [
                Consumer<Counter>(
                  builder: (context, counter, child) => Text(
                    'Contagem: ${counter.count}',
                    style: TextStyle(fontSize: 24),
                  ),
                ),
                SizedBox(height: 16),
                ElevatedButton(
                  onPressed: () {
                    final counter = Provider.of<Counter>(context, listen: false);
                    counter.increment();
                  },
                  child: Text('Incrementar'),
                ),
              ],
            ),
          ),
        ),
      ),
    );
  }
}

void main() {
  runApp(CounterApp());
}
```

Neste exemplo, utilizamos o pacote `provider` para gerenciar o estado do contador. O `Counter` é uma classe que estende `ChangeNotifier` e notifica os ouvintes sempre que o valor do contador é alterado. O

 widget `Consumer<Counter>` atualiza automaticamente o texto exibido com a contagem atualizada. O botão de incremento utiliza `Provider.of<Counter>` para acessar o objeto `Counter` e chamar o método `increment()`.


### 7.3 Construindo seus Próprios Widgets Reutilizáveis

Uma das grandes vantagens do Flutter é a capacidade de criar seus próprios widgets personalizados e reutilizáveis. Ao construir seus próprios widgets, você pode encapsular lógica e comportamento específicos, facilitando o desenvolvimento e a manutenção do código. Aqui está um exemplo de como construir um widget personalizado no Flutter:

```dart
import 'package:flutter/material.dart';

class CustomButton extends StatelessWidget {
  final String text;
  final VoidCallback onPressed;

  const CustomButton({required this.text, required this.onPressed});

  @override
  Widget build(BuildContext context) {
    return ElevatedButton(
      onPressed: onPressed,
      child: Text(text),
    );
  }
}
```

Neste exemplo, criamos um widget chamado `CustomButton` que exibe um botão personalizado com texto. Ele recebe dois parâmetros obrigatórios: `text`, que é o texto exibido no botão, e `onPressed`, uma função de retorno de chamada que é executada quando o botão é pressionado.

Você pode usar esse widget personalizado em qualquer lugar do seu aplicativo, fornecendo o texto e a função de retorno de chamada adequados. Aqui está um exemplo de uso do `CustomButton`:

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MaterialApp(
    home: Scaffold(
      appBar: AppBar(
        title: Text('Exemplo de Widget Personalizado'),
      ),
      body: Center(
        child: CustomButton(
          text: 'Clique Aqui',
          onPressed: () {
            print('Botão Clicado!');
          },
        ),
      ),
    ),
  ));
}
```

Neste exemplo, usamos o `CustomButton` no corpo de um aplicativo Flutter. Quando o botão é pressionado, a função de retorno de chamada imprime uma mensagem no console.

Ao construir seus próprios widgets personalizados, você pode adicionar qualquer lógica e personalização necessárias para atender aos requisitos do seu aplicativo. Isso ajuda a manter seu código organizado, reutilizável e facilita a manutenção no longo prazo.