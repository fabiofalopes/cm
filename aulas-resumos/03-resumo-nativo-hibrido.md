# Resumo: Aula 3 - Nativo, Híbrido-Nativo e Comparação

## 1. Arquitetura Nativa Pura

- **Conceito:** Desenvolver aplicações usando as ferramentas e linguagens oficiais de cada sistema operativo, resultando em apps separadas para cada plataforma.
    - **iOS:** **Swift** (ou Objective-C) com Xcode. O resultado é um ficheiro `.ipa` encriptado.
    - **Android:** **Kotlin** (ou Java) com Android Studio. O resultado é um ficheiro `.apk`.
- **Principal Desvantagem:** **Custo duplicado.** Manter duas bases de código, duas equipas e dois processos de desenvolvimento é caro e lento.

- **Vantagens Competitivas:**
    - **Flexibilidade Máxima:** Acesso total, imediato e sem restrições a todas as APIs e funcionalidades do SO. Se uma funcionalidade é possível no dispositivo, é possível em nativo.
    - **Melhor Desempenho:** Otimização máxima ao nível do compilador e acesso a ferramentas de profiling avançadas, resultando na maior fluidez possível.
    - **Maior Estabilidade e Comunidade:** Beneficia dos SDKs oficiais, que têm menos bugs que frameworks de terceiros, e de uma comunidade de developers maior e mais experiente.

---

## 2. Arquitetura Híbrida-Nativa

- **Conceito:** Escrever o código numa única base de código (e.g., em Dart, JavaScript, C#) que depois gera uma aplicação com componentes de interface (UI) nativos para cada plataforma. **O ponto-chave é que não usa WebViews.**
- **Objetivo:** "O melhor dos dois mundos": reduzir o custo do desenvolvimento multiplataforma mantendo um desempenho e aparência próximos do nativo.
- **Frameworks Populares:** **Flutter** (da Google, usa Dart) e **React Native** (do Facebook, usa JavaScript) são os principais concorrentes no mercado. Outros exemplos incluem .NET MAUI e Kotlin Multiplatform.

Existem duas abordagens técnicas distintas para alcançar este objetivo:

### A) Ponte JavaScript (JS Bridge) - Abordagem *Runtime*

- **Como funciona:** O código da aplicação (escrito em JavaScript) é empacotado juntamente com um motor de JavaScript (JS Engine). Em tempo de execução (runtime), este motor interpreta o código JS e envia comandos através de uma "ponte" assíncrona para a API nativa, que por sua vez cria os componentes de UI.
- **Framework Principal:** React Native.
- **Vantagens:**
    - **Code Push:** Permite atualizar a lógica de negócio da app (o código JS) remotamente, sem precisar de submeter uma nova versão à loja.
    - Desenvolvimento rápido com *live/hot reload*.
- **Desvantagens:**
    - A "ponte" pode ser um **gargalo de desempenho**, especialmente em animações complexas ou listas longas.
    - O binário da app é maior, pois precisa de incluir o motor de JS.

### B) Cross-Compiler - Abordagem *Compile-Time*

- **Como funciona:** O código fonte é **compilado para código nativo** da plataforma-alvo *antes* da distribuição (em tempo de compilação). Não há pontes nem interpretação em runtime.
- **Como a UI é desenhada (Diferença Crucial):**
    - **Widgets OEM (Original Equipment Manufacturer):** Frameworks como **React Native** e **.NET MAUI** mapeiam o seu código para os componentes de UI nativos do sistema operativo. Um `<Button>` torna-se um `Button` nativo do Android ou um `UIButton` do iOS. A aparência é 100% nativa.
    - **Widgets Custom (Personalizados):** **Flutter** segue uma abordagem radicalmente diferente. Ele não cria widgets nativos do SO. Em vez disso, compila o código Dart para código máquina (ARM) e usa o seu próprio motor de renderização de alta performance (Skia) para desenhar cada pixel do seu próprio conjunto de widgets numa tela (Canvas) que o SO lhe fornece.
        - **Vantagem do Flutter:** Garante **consistência visual total** ("pixel-perfect") entre plataformas e controlo absoluto sobre a UI.
        - **Desvantagem do Flutter:** A aparência e comportamento dos widgets podem não corresponder 100% à versão mais recente do SO.
- **Vantagens (gerais):** **Desempenho excelente**, muito próximo do nativo puro, pois não há a sobrecarga da ponte em runtime.
- **Desvantagens (gerais):** Atualizações exigem sempre uma nova submissão à loja de apps (não há Code Push).

---

## 3. Tabela Comparativa e Nuances

| Característica | Nativa Pura | Híbrida-Nativa (Flutter/MAUI) | Híbrida-Nativa (React Native) | Híbrida-Web | HTML5 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Custo Desenvolvimento** | Elevado | Médio | Médio | Reduzido | Reduzido |
| **Acesso a Features**| Total e Imediato | Quase Total (com *delay*) | Quase Total (com *delay*) | Médio | Reduzido |
| **Interface Gráfica** | Nativa do SO | Custom (Skia) | Nativa do SO | Web | Web |
| **Fluidez/Desempenho** | **Excelente** | Elevada | Média a Elevada | Baixa | Baixa |
| **Funcionamento Offline** | Sim | Sim | Sim | Parcial | Não |
| **Atualizações** | Lentas (via Loja) | Lentas (via Loja) | **Imediatas (Code Push)** | Rápidas | Imediatas |

#### **Notas e Explicações da Tabela:**
- **Custo Híbrida-Nativo:** Embora o código seja partilhado, a UI muitas vezes precisa de ajustes específicos por plataforma, e os developers com skills nestas tecnologias são mais especializados (e caros).
- **Acesso a Features:** Quando uma nova funcionalidade sai no iOS ou Android, as frameworks híbridas dependem dos seus mantenedores para criar a "ponte" ou o wrapper, o que pode demorar. Em nativo, o acesso é no dia 1.
- **Fluidez React Native:** A performance é geralmente boa, mas a ponte JS pode ser um bottleneck em cenários de UI intensivos (animações, gestos, listas longas), tornando-a "semi-elevada" nesses casos.
- **Offline Híbrida-Web:** Funciona se os ficheiros estiverem na cache local da `WebView`, mas a gestão dessa cache é menos robusta que numa app totalmente nativa.
- **Atualizações Híbrida-Web:** São "quase" imediatas, pois dependem do tempo de expiração da cache do cliente para obter a nova versão do servidor. 