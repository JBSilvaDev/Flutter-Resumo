# Capítulo 16: Internacionalização e Localização

Neste capítulo, exploraremos a internacionalização e localização em aplicativos Flutter. Vamos aprender como oferecer suporte a múltiplos idiomas e como formatar datas, moedas e números de acordo com as preferências do usuário.

## 16.1 Suporte a Múltiplos Idiomas

Oferecer suporte a múltiplos idiomas em seu aplicativo Flutter é uma maneira eficaz de alcançar usuários em diferentes regiões e culturas. Para habilitar a internacionalização, siga estas etapas:

1. Importe a biblioteca `flutter_localizations` em seu arquivo `pubspec.yaml`.

```yaml
dependencies:
  flutter_localizations:
    sdk: flutter
```

2. Defina os idiomas suportados em seu aplicativo. Isso pode ser feito no arquivo `main.dart`:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_localizations/flutter_localizations.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      localizationsDelegates: [
        GlobalMaterialLocalizations.delegate,
        GlobalWidgetsLocalizations.delegate,
      ],
      supportedLocales: [
        const Locale('en', 'US'), // Inglês (Estados Unidos)
        const Locale('es', 'ES'), // Espanhol (Espanha)
        const Locale('pt', 'BR'), // Português (Brasil)
      ],
      // Resto da configuração do aplicativo...
    );
  }
}
```

3. Crie arquivos de tradução para cada idioma suportado. Por exemplo, `app_en_US.json` para inglês (Estados Unidos), `app_es_ES.json` para espanhol (Espanha) e `app_pt_BR.json` para português (Brasil). Esses arquivos devem conter as chaves e os valores das traduções correspondentes.

```json
// app_en_US.json
{
  "title": "My App",
  "welcome_message": "Welcome to my app!"
}
```

```json
// app_es_ES.json
{
  "title": "Mi Aplicación",
  "welcome_message": "¡Bienvenido a mi aplicación!"
}
```

```json
// app_pt_BR.json
{
  "title": "Meu App",
  "welcome_message": "Bem-vindo ao meu app!"
}
```

4. Em seu código, utilize a classe `Localizations` para obter as traduções correspondentes com base no idioma definido pelo dispositivo:

```dart
import 'package:flutter/material.dart';
import 'package:flutter_localizations/flutter_localizations.dart';
import 'package:flutter_gen/gen_l10n/app_localizations.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      localizationsDelegates: [
        GlobalMaterialLocalizations.delegate,
        GlobalWidgetsLocalizations.delegate,
        AppLocalizations.delegate,
      ],
      supportedLocales: [
        const Locale('en', 'US'),
        const Locale('es', 'ES'),
        const Locale('pt', 'BR'),
      ],
      // Resto da configuração do aplicativo...
    );
  }
}

class MyHomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final localizations = AppLocalizations.of(context);
    return Scaffold(
      appBar: AppBar(
        title: Text(localizations.title),
     

 ),
      body: Center(
        child: Text(localizations.welcomeMessage),
      ),
    );
  }
}
```

Com isso, seu aplicativo estará preparado para fornecer traduções adequadas com base no idioma definido pelo usuário.

## 16.2 Formatação de Datas, Moedas e Números

Além de suportar múltiplos idiomas, é importante apresentar datas, moedas e números de acordo com as convenções culturais do usuário. O Flutter fornece formatação fácil e flexível para esses casos.

### 16.2.1 Formatação de Datas

Para formatar datas, utilize a classe `DateFormat` da biblioteca `intl`. Veja um exemplo de formatação de uma data para exibição:

```dart
import 'package:intl/intl.dart';

void main() {
  final now = DateTime.now();
  final formattedDate = DateFormat('dd/MM/yyyy').format(now);
  print(formattedDate); // Exemplo de saída: 22/05/2023
}
```

### 16.2.2 Formatação de Moedas

A formatação de moedas pode ser realizada usando a classe `NumberFormat`. Veja um exemplo de formatação de um valor monetário:

```dart
import 'package:intl/intl.dart';

void main() {
  final value = 1234.56;
  final formattedCurrency = NumberFormat.currency(locale: 'pt_BR', symbol: 'R\$').format(value);
  print(formattedCurrency); // Exemplo de saída: R$1.234,56
}
```

### 16.2.3 Formatação de Números

Para formatar números, utilize a classe `NumberFormat`. Veja um exemplo de formatação de um número decimal:

```dart
import 'package:intl/intl.dart';

void main() {
  final value = 1234.56;
  final formattedNumber = NumberFormat.decimalPattern('pt_BR').format(value);
  print(formattedNumber); // Exemplo de saída: 1.234,56
}
```

Com essas técnicas de formatação, você pode apresentar datas, moedas e números de maneira adequada aos usuários em diferentes regiões e culturas.

Parabéns por explorar a internacionalização e localização em seus aplicativos Flutter! Agora você pode oferecer uma experiência personalizada para usuários de diferentes idiomas e regiões.

Continue aprendendo e aprimorando suas habilidades de desenvolvimento com Flutter. Há muitos recursos disponíveis para ajudá-lo a criar aplicativos incríveis e impactantes!

Boa sorte em sua jornada como desenvolvedor Flutter!