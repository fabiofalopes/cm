# Resumo: Aula 8 - Conectividade e Dados

## 1. Tecnologias de Comunicação Wireless

A conectividade móvel depende de várias tecnologias sem fios, cada uma com características específicas que as tornam adequadas para diferentes casos de uso.

| Tecnologia | Alcance | Segurança | Diferenciador / Caso de Uso Principal |
|:---|:---|:---|:---|
| **RFID** | < 12 m (passivo) | Fraca | **Identificação de produtos** em massa, substituindo o código de barras. |
| **NFC** | **< 10 cm** | **Elevada** | **Pagamentos** e identificação segura, graças ao alcance extremamente curto. |
| **IrDA** | < 5 m (direcional) | Fraca | Comunicação direcional (Line-of-Sight), usada em comandos remotos antigos. |
| **Bluetooth LE**| < 240 m | Elevada | Conexão de periféricos (fones, smartwatches) com baixo consumo de energia. |
| **UWB** | < 100 m | Elevada | **Localização precisa** e direcional de dispositivos (e.g., Apple AirTags). |
| **Wi-Fi** | ~100 m | Elevada | Acesso à Internet de alta velocidade em redes locais (WLAN). |
| **Celular (5G)**| > 10 km | Elevada | Acesso à Internet de longo alcance, garantindo conectividade "em todo o lado". |

---

## 2. Lidar com a Instabilidade da Rede em Flutter

A conectividade móvel é, por natureza, instável. Uma app robusta deve ser desenhada a pensar no cenário "offline first", tratando a conectividade como um extra e não como uma garantia.

### A) Interrogar vs. Observar o Estado da Rede

Existem duas estratégias para lidar com a rede, que devem ser usadas em conjunto:

1.  **Interrogar (Pull):** Verificar o estado da rede no momento de uma ação iniciada pelo utilizador.
    - **Caso de uso:** Antes de tentar fazer uma **leitura** de dados (e.g., carregar num botão "Atualizar").
    - **Implementação:** `final status = await Connectivity().checkConnectivity();`

2.  **Observar (Listen/Push):** "Ouvir" as mudanças de estado da rede para reagir automaticamente.
    - **Caso de uso:** Quando a app fica online, aproveitar para fazer **escritas** pendentes (e.g., sincronizar um post que o utilizador criou offline).
    - **Implementação:**
        ```dart
        // Idealmente, no arranque da app (e.g., no initState de um widget principal)
        connectivitySubscription = Connectivity().onConnectivityChanged.listen((result) {
          if (result != ConnectivityResult.none) {
            // A app ficou online. Sincronizar dados pendentes...
          }
        });
        ```

### B) Estratégias de Cache e Sincronização de Dados

Para a app funcionar offline, precisa de uma cópia local dos dados (uma **cache** ou **réplica**).

- **Cache Temporária:** Dados guardados para acesso rápido que podem ser descartados. Ex: Imagens de perfil.
- **Cache Permanente (Réplica):** Uma cópia dos dados do servidor que deve ser mantida e sincronizada. Ex: Posts de um blog, documentos.

Quando a réplica local é alterada, essa mudança precisa de ser propagada. Existem dois modelos para isso:

- **Modelo Pull:** O cliente (a app) interroga periodicamente o servidor para verificar se há novas atualizações.
    - **Vantagem:** Mais simples de implementar e funciona melhor com dispositivos que estão frequentemente offline.
    - **Exemplo:** Git. `git pull` é uma ação manual para obter as últimas alterações.
- **Modelo Push:** O servidor notifica ativamente os clientes sempre que há uma atualização.
    - **Vantagem:** As atualizações são em tempo real.
    - **Desvantagem:** Mais complexo e requer uma conexão persistente (e.g., WebSockets), o que consome mais bateria.

### C) Exemplo de Requisição HTTP (`http` e `async/await`)

- Para comunicar com APIs REST, usa-se o pacote `http` e o padrão `async/await` do Dart.
- O fluxo típico é: fazer o pedido, verificar o `statusCode`, descodificar o JSON para um `Map`, e converter o `Map` para um objeto Dart fortemente tipado.

```dart
import 'package:http/http.dart' as http;
import 'dart:convert';

Future<Album> fetchAlbum() async {
  final response = await http.get(Uri.parse('https://jsonplaceholder.typicode.com/albums/1'));

  if (response.statusCode == 200) { // 200 OK
    // Descodifica a String JSON para um Map e depois converte para um objeto Album.
    return Album.fromJson(jsonDecode(response.body));
  } else {
    throw Exception('Falha ao carregar o álbum');
  }
}
```

### D) Padrão de Repositório (Repository Pattern)

- **Conceito:** Uma camada de abstração que isola a UI e a lógica de negócio das fontes de dados (API, base de dados, etc.).
- **Funcionamento:** A UI nunca fala diretamente com o `http` ou com a base de dados. Ela pede os dados a um `Repository`. O repositório é que decide de onde os vai buscar (da rede, da cache local, etc.).
- **Principal Vantagem:** **Testabilidade e Flexibilidade.** Permite trocar a fonte de dados (ex: de uma API para uma base de dados local) sem alterar uma única linha de código na UI. Nos testes, podemos "injetar" um repositório falso (`MockRepository`) que devolve dados pré-definidos instantaneamente.
    ```dart
    // A UI depende desta abstração (contrato).
    abstract class AbstractAlbumRepository {
      Future<Album> fetchAlbum(int id);
    }

    // A implementação real que usa a API.
    class AlbumApiRepository implements AbstractAlbumRepository {
      @override
      Future<Album> fetchAlbum(int id) {
        // ...lógica com http.get e fromJson...
      }
    }

    // Uma implementação para testes que não usa a rede.
    class MockAlbumRepository implements AbstractAlbumRepository {
      @override
      Future<Album> fetchAlbum(int id) {
        return Future.value(Album(id: id, title: 'Album de Teste', userId: 1));
      }
    }
    ``` 