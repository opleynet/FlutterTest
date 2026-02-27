# flutter_application_1

A new Flutter project.

## Getting Started

This project is a starting point for a Flutter application.

A few resources to get you started if this is your first Flutter project:

- [Learn Flutter](https://docs.flutter.dev/get-started/learn-flutter)
- [Write your first Flutter app](https://docs.flutter.dev/get-started/codelab)
- [Flutter learning resources](https://docs.flutter.dev/reference/learning-resources)

For help getting started with Flutter development, view the
[online documentation](https://docs.flutter.dev/), which offers tutorials,
samples, guidance on mobile development, and a full API reference.

## Installation

Comment installer
- Installer VS Code
- INstaller SDK Flutter
- Connecter projet to Git

## Tutorial Flutter

- Le fichier pubspec.yaml définit les informations de base de votre application, comme sa version actuelle, ses dépendances et les éléments utilisés pour son implémentation.
- Analyse_options.yaml Le fichier détermine la rigueur de Flutter lorsqu'il analyse votre code. Puisqu'il s'agit d'une entrée en matière à Flutter, vous allez indiquer à l'analyseur d'y aller doucement. Vous pourrez toujours personnaliser cela par la suite. En réalité, vous aurez certainement envie d'augmenter la rigueur de l'analyseur à mesure que vous approcherez de la publication de la véritable application de production.

- Fichier Main --> lib/main.dart

## fichier main
- La fonction main() se trouve tout en haut du fichier. Dans sa forme actuelle, elle ne fait qu'indiquer à Flutter d'exécuter l'application définie dans MyApp.
- La classe MyApp étend le StatelessWidget. Les widgets sont les éléments que vous devez utiliser pour développer une application Flutter. Notez que l'application elle-même est un widget.

Remarque : Nous décrirons le StatelessWidget (comparé au StatefulWidget) ultérieurement.

Le code dans MyApp configure l'ensemble de l'application. Il crée l'état au niveau de l'application (vous en saurez plus par la suite), nomme l'application, définit le thème visuel et configure le widget "home" (Accueil) (le point de départ de votre application).

- Ensuite, la classe MyAppState définit l'état d'intégrité de l'application. Puisqu'il s'agit d'une entrée en matière à Flutter, cet atelier de programmation se veut simple et précis. Il existe de nombreuses méthodes efficaces pour gérer l'état d'une application dans Flutter. L'une des plus simples est l'approche ChangeNotifier que nous allons adopter pour cette application.

MyAppState détermine les données dont l'application a besoin pour fonctionner. Pour le moment, elle ne comporte qu'une seule variable avec l'actuelle paire de mots aléatoires. Vous la compléterez ultérieurement.
La classe d'état étend ChangeNotifier qui peut alors informer les autres widgets de ses propres modifications. Par exemple, certains widgets de l'application doivent être informés en cas de modification de l'actuelle paire de mots.
L'état est créé et transmis à l'ensemble de l'application avec un ChangeNotifierProvider (voir le code ci-dessus dans MyApp). Cela permet de communiquer l'état à tous les widgets de l'application. 

- MyHomePage

class MyHomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {           // ← 1
    var appState = context.watch<MyAppState>();  // ← 2

    return Scaffold(                             // ← 3
      body: Column(                              // ← 4
        children: [
          Text('A random AWESOME idea:'),        // ← 5
          Text(appState.current.asLowerCase),    // ← 6
          ElevatedButton(
            onPressed: () {
              print('button pressed!');
            },
            child: Text('Next'),
          ),
        ],                                       // ← 7
      ),
    );
  }
}

// ...
Enfin, vous avez le widget MyHomePage que vous avez déjà modifié. Chaque puce numérotée ci-dessous correspond à un commentaire avec numéro de ligne dans le code ci-dessus :

Chaque widget définit une méthode build() automatiquement appelée dès que les conditions du widget changent, de sorte qu'il soit toujours à jour.
MyHomePage suit les modifications de l'état actuel de l'application avec la méthode watch.
Chaque méthode build doit renvoyer un widget ou (plus généralement) une arborescence de widgets imbriquée. Dans ce cas, le widget de premier niveau est Scaffold. Dans cet atelier de programmation, vous n'allez pas utiliser Scaffold. Néanmoins, ce widget est pratique et utilisé dans la plupart des applications Flutter du monde réel.
Column est l'un des principaux widgets de mise en page de Flutter. Il accepte un nombre illimité d'enfants et les place dans une colonne, de haut en bas. Par défaut, la colonne place visuellement ses enfants en haut. Vous allez apprendre à modifier cela pour que la colonne soit centrée.
Vous avez modifié le widget Text à la première étape.
Ce second widget Text accepte appState et accède au seul membre de la classe, current (qui est une WordPair). WordPair fournit plusieurs getters utiles, comme asPascalCase ou asSnakeCase. Dans notre cas, nous utilisons asLowerCase. Vous pouvez modifier cela si vous préférez l'une des autres solutions.
Notez que le code Flutter utilise massivement les virgules de fin. Ce type de virgule n'est pas nécessaire ici, car children est le dernier (et le seul) membre de cette liste de paramètres Column spécifiques. L'utilisation des virgules de fin est généralement adaptée : elle simplifie l'ajout de membres et sert de repère lorsque le formateur automatique Dart doit insérer une nouvelle ligne. Pour en savoir plus, consultez Code formatting (Formatage du code).