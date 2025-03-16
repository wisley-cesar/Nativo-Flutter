# 📱 Integração de Código Nativo no Flutter

## 🚀 Sobre o Projeto
Este repositório explora a integração de código nativo no Flutter para aprimorar a interação com funcionalidades específicas do dispositivo. O objetivo é demonstrar como utilizar código nativo (Swift no iOS) dentro de um aplicativo Flutter, proporcionando uma experiência mais fluida e otimizada.

## 📌 Funcionalidades
✅ Uso de código nativo para acessar funcionalidades específicas do sistema operacional;
✅ Comunicação entre Dart e Swift utilizando Method Channels;
✅ Exemplos práticos de integração para expandir as capacidades do Flutter;
✅ Otimização da performance e melhoria da experiência do usuário.

## 🛠️ Tecnologias Utilizadas
- **Flutter** - Framework principal do projeto
- **Dart** - Linguagem utilizada no Flutter
- **Swift** - Código nativo para iOS
- **Method Channels** - Para comunicação entre Flutter e código nativo

## 📂 Estrutura do Projeto
```
📂 flutter_native_integration
├── 📁 lib
│   ├── main.dart  # Código principal do Flutter
├── 📁 ios
│   ├── Runner
│   │   ├── AppDelegate.swift  # Configuração inicial do iOS com código nativo
│   │   ├── native_code.swift  # Código nativo implementado
├── pubspec.yaml  # Dependências do projeto
```

## 📖 Como Rodar o Projeto
1. **Clone o repositório:**
   ```bash
   git clone git@github.com:wisley-cesar/Nativo-Flutter.git
   ```
2. **Acesse o diretório:**
   ```bash
   cd NATIVO
   ```
3. **Instale as dependências:**
   ```bash
   flutter pub get
   ```
4. **Execute o projeto:**
   ```bash
   flutter run
   ```

⚠️ *Para rodar no iOS, certifique-se de ter um Mac com Xcode instalado.*

## 📜 Exemplos de Código
### 🔗 Comunicação entre Flutter e Swift
#### Flutter (Dart)
```dart
const platform = MethodChannel('com.example.nativo');

Future<int> calcSum(int a, int b) async {
  try {
    final int result = await platform.invokeMethod('calcSum', {'a': a, 'b': b});
    return result;
  } catch (e) {
    return -1;
  }
}
```
#### Swift (iOS)
```swift
import Flutter
import UIKit

@main
@objc class AppDelegate: FlutterAppDelegate {
  override func application(
    _ application: UIApplication,
    didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?
  ) -> Bool {
      
      let controller : FlutterViewController = window?.rootViewController as! FlutterViewController
      let nativoChannel = FlutterMethodChannel(name: "com.example.nativo", binaryMessenger: controller.binaryMessenger)
      
      nativoChannel.setMethodCallHandler { (call: FlutterMethodCall, result: @escaping FlutterResult) in
          
          guard call.method == "calcSum" else {
              result(FlutterMethodNotImplemented)
              return
          }
          
          if let args = call.arguments as? [String: Any],
             let a = args["a"] as? Int,
             let b = args["b"] as? Int {
              result(a + b)
          } else {
              result(-1)
          }
      }
      
      GeneratedPluginRegistrant.register(with: self)
      return super.application(application, didFinishLaunchingWithOptions: launchOptions)
  }
}
```

## ✨ Contribuição
Sinta-se à vontade para contribuir com melhorias e novas funcionalidades! 
1. Faça um fork do repositório.
2. Crie uma branch com a sua feature:
   ```bash
   git checkout -b minha-feature
   ```
3. Commit suas alterações:
   ```bash
   git commit -m "Adicionando nova funcionalidade"
   ```
4. Envie para o repositório:
   ```bash
   git push origin minha-feature
   ```
5. Abra um Pull Request.


---
📌 **Desenvolvido por [Wisley César](https://github.com/wisley-cesar) 💙**
