# INSTRUÇÕES (GENERICAS)
## 01) VISÃO GERAL
### O que é o React ChatBot Kit?
O React ChatBot Kit é uma biblioteca projetada para facilitar a criação de chatbots em aplicações React. Ele fornece componentes prontos e uma arquitetura flexível para que desenvolvedores possam rapidamente construir chatbots interativos e responsivos.

### Recursos Principais
- **Componentes Reutilizáveis**: Oferece uma coleção de componentes prontos para uso.
- **Integração com React**: Fácil de integrar em projetos React existentes.
- **Customização**: Extensivamente personalizável para atender às necessidades específicas do projeto.
- **Documentação e Comunidade**: Fornece documentação detalhada e é suportado por uma comunidade ativa.

### Passos para Instalação e Configuração
#### 1. Instalações Necessárias
- **Node.js e npm**: Certifique-se de que Node.js e npm estão instalados.
- **Create React App**: Ferramenta para inicializar um novo projeto React.
- **React ChatBot Kit**: Biblioteca específica para criação de chatbots.

#### 2. Instalar o Create React App
```bash
npm install -g create-react-app
```

#### 3. Criar um Novo Projeto React
```bash
create-react-app my-chatbot
cd my-chatbot
```

#### 4. Instalar o React ChatBot Kit
No diretório do projeto, execute:
```bash
npm install react-chatbot-kit
```

### Criando o Primeiro Projeto
#### Estrutura do Projeto
Seu projeto deve ter uma estrutura básica como esta:
```
my-chatbot/
├── node_modules/
├── public/
├── src/
│   ├── components/
│   ├── App.js
│   ├── index.js
├── package.json
├── README.md
```

#### Configuração do ChatBot
Crie uma pasta `components` dentro de `src` e adicione os seguintes arquivos:

##### 1. src/components/ActionProvider.js
```javascript
class ActionProvider {
  constructor(createChatBotMessage, setStateFunc) {
    this.createChatBotMessage = createChatBotMessage;
    this.setState = setStateFunc;
  }

  greet() {
    const greetingMessage = this.createChatBotMessage("Hello, how can I help you?");
    this.setState(prev => ({
      ...prev, messages: [...prev.messages, greetingMessage]
    }));
  }
}

export default ActionProvider;
```

##### 2. src/components/MessageParser.js
```javascript
class MessageParser {
  constructor(actionProvider) {
    this.actionProvider = actionProvider;
  }

  parse(message) {
    const lowercase = message.toLowerCase();
    if (lowercase.includes("hello")) {
      this.actionProvider.greet();
    }
  }
}

export default MessageParser;
```

##### 3. src/components/config.js
```javascript
import { createChatBotMessage } from "react-chatbot-kit";

const config = {
  botName: "ReactBot",
  initialMessages: [createChatBotMessage("Hello! How can I assist you today?")],
  customStyles: {
    botMessageBox: {
      backgroundColor: "#376B7E",
    },
    chatButton: {
      backgroundColor: "#5ccc9d",
    },
  },
};

export default config;
```

#### Integrando o ChatBot ao App
Atualize seu `src/App.js` para integrar o ChatBot:
```javascript
import React from "react";
import Chatbot from "react-chatbot-kit";
import "react-chatbot-kit/build/main.css";
import ActionProvider from "./components/ActionProvider";
import MessageParser from "./components/MessageParser";
import config from "./components/config";

function App() {
  return (
    <div className="App">
      <header className="App-header">
        <Chatbot 
          config={config} 
          actionProvider={ActionProvider} 
          messageParser={MessageParser} 
        />
      </header>
    </div>
  );
}

export default App;
```

### Executando o Projeto
No diretório do seu projeto, execute:
```bash
npm start
```

O aplicativo será aberto no navegador em `http://localhost:3000`, e você verá seu chatbot em funcionamento.

### Resumo
Seguindo esses passos, você instala as ferramentas necessárias, configura o ambiente e cria um chatbot básico com o React ChatBot Kit. A partir daí, você pode personalizar e expandir seu chatbot conforme as necessidades do seu projeto.

## 02) INSTALAÇÃO
### Pré-requisitos
1. **Node.js e npm**: Certifique-se de que você tem o Node.js e o npm instalados em seu sistema. Você pode baixá-los de [nodejs.org](https://nodejs.org/).

### 1. Instalar o Create React App
O Create React App é uma ferramenta que configura rapidamente um novo projeto React com uma estrutura de pastas padrão e dependências básicas.

Execute o seguinte comando para instalar o Create React App globalmente:
```bash
npm install -g create-react-app
```

### 2. Criar um Novo Projeto React
Use o Create React App para criar um novo projeto React chamado `my-chatbot`:
```bash
create-react-app my-chatbot
cd my-chatbot
```

### 3. Instalar o React ChatBot Kit
Dentro do diretório do seu projeto (`my-chatbot`), instale o React ChatBot Kit usando o npm:
```bash
npm install react-chatbot-kit
```

## 03) CSS NO CHATBOT
Para aplicar estilos personalizados ao seu chatbot usando o React ChatBot Kit, você pode aproveitar as opções de personalização oferecidas pela biblioteca. Aqui estão os passos básicos para aplicar CSS ao seu chatbot:

### 1. Configuração Inicial
Primeiro, certifique-se de ter configurado o seu chatbot usando o React ChatBot Kit. Você deve ter um arquivo `config.js` ou similar onde configurou o nome do bot, mensagens iniciais e estilos personalizados.

### Exemplo de Configuração (`config.js`)
```javascript
import { createChatBotMessage } from "react-chatbot-kit";

const config = {
  botName: "ReactBot",
  initialMessages: [createChatBotMessage("Hello! How can I assist you today?")],
  customStyles: {
    botMessageBox: {
      backgroundColor: "#376B7E",
    },
    chatButton: {
      backgroundColor: "#5ccc9d",
    },
  },
};

export default config;
```

### 2. Adicionando Estilos CSS
Você pode adicionar estilos CSS personalizados para modificar a aparência do chatbot. O React ChatBot Kit permite personalizar os estilos de diferentes elementos do chatbot, como a caixa de mensagens do bot (`botMessageBox`) e os botões de interação (`chatButton`).

No exemplo acima, `customStyles` é um objeto onde você pode definir estilos CSS. Aqui estão alguns exemplos de estilos que você pode adicionar:

```javascript
const config = {
  // ...
  customStyles: {
    botMessageBox: {
      backgroundColor: "#376B7E", // Cor de fundo da caixa de mensagens do bot
      borderRadius: "20px",       // Borda arredondada
      padding: "10px",            // Espaçamento interno
    },
    chatButton: {
      backgroundColor: "#5ccc9d", // Cor de fundo dos botões de interação
      borderRadius: "10px",       // Borda arredondada
      color: "#fff",              // Cor do texto
    },
  },
};
```

### 3. Aplicando os Estilos no Componente Chatbot
No seu componente `App.js` (ou onde você estiver renderizando o chatbot), certifique-se de passar esses estilos personalizados através da propriedade `config`:

```javascript
import React from "react";
import Chatbot from "react-chatbot-kit";
import "react-chatbot-kit/build/main.css"; // Importante para estilos básicos

import ActionProvider from "./components/ActionProvider";
import MessageParser from "./components/MessageParser";
import config from "./components/config"; // Importe seu arquivo de configuração

function App() {
  return (
    <div className="App">
      <header className="App-header">
        <Chatbot
          config={config}
          actionProvider={ActionProvider}
          messageParser={MessageParser}
        />
      </header>
    </div>
  );
}

export default App;
```

### 4. Estilos Avançados
Além das propriedades básicas como `backgroundColor`, você pode aplicar estilos mais avançados usando CSS. Por exemplo, você pode adicionar `padding`, `margin`, `font-size`, `font-family` e outras propriedades CSS conforme necessário para personalizar completamente a aparência do seu chatbot.

### Considerações Finais
- Certifique-se de usar nomes de classe ou IDs únicos para evitar conflitos de estilo com outras partes do seu aplicativo.
- Experimente diferentes combinações de cores, bordas arredondadas, sombras e tamanhos de fonte para alcançar o estilo desejado para o seu chatbot.

Seguindo esses passos, você poderá personalizar efetivamente a aparência do seu chatbot criado com o React ChatBot Kit.

## 04) WIDGETS
No contexto do desenvolvimento de chatbots com o React ChatBot Kit, os "widgets" se referem aos componentes visuais e interativos que você pode integrar ao seu chatbot para oferecer funcionalidades específicas e melhorar a experiência do usuário. Esses widgets podem incluir desde simples botões de ação até elementos mais complexos como formulários interativos.

### Exemplos de Widgets Comuns
1. **Botões de Ação**: São utilizados para iniciar uma conversa, responder a uma pergunta específica ou acionar um comando no chatbot.

2. **Formulários**: Permitem coletar informações do usuário, como nome, email ou outras informações relevantes para o contexto do chatbot.

3. **Galerias de Imagens**: Exibem uma série de imagens ou thumbnails que podem ser clicadas para exibir em tamanho maior ou para iniciar ações específicas.

4. **Carrosséis**: Mostram uma série de cartões ou itens que o usuário pode navegar horizontalmente para visualizar mais detalhes ou opções.

5. **Seletores de Opções**: Como dropdowns ou listas de opções, utilizados para permitir que o usuário escolha entre diferentes alternativas.

### Implementando Widgets no React ChatBot Kit
Para implementar widgets no React ChatBot Kit, você geralmente cria componentes React personalizados que são chamados pelo seu `ActionProvider` ou `MessageParser` em resposta às interações do usuário. Aqui está um exemplo simplificado de como você pode integrar um widget de botão de ação:

1. **Criando um Botão de Ação**
```javascript
// Exemplo de ActionProvider.js
import React from "react";

class ActionProvider {
  constructor(createChatBotMessage, setStateFunc) {
    this.createChatBotMessage = createChatBotMessage;
    this.setState = setStateFunc;
  }

  handleGreeting = () => {
    const message = this.createChatBotMessage("Hello! How can I assist you today?");
    this.updateChatbotState(message);
  };

  updateChatbotState = (message) => {
    // Atualiza o estado do chatbot com a nova mensagem
    this.setState(prevState => ({
      ...prevState,
      messages: [...prevState.messages, message]
    }));
  };

  render() {
    return (
      <div>
        <button onClick={this.handleGreeting}>Say Hello</button>
      </div>
    );
  }
}

export default ActionProvider;
```

2. **Integrando no Componente do Chatbot**
```javascript
// Exemplo de App.js
import React from "react";
import Chatbot from "react-chatbot-kit";
import "react-chatbot-kit/build/main.css";

import ActionProvider from "./components/ActionProvider";
import MessageParser from "./components/MessageParser";
import config from "./components/config";

function App() {
  return (
    <div className="App">
      <header className="App-header">
        <Chatbot
          config={config}
          actionProvider={ActionProvider}
          messageParser={MessageParser}
        />
      </header>
    </div>
  );
}

export default App;
```

### Considerações Finais
- **Personalização**: Você pode personalizar completamente a aparência e comportamento dos widgets de acordo com as necessidades do seu chatbot e do seu projeto.
  
- **Componentização**: Ao criar widgets, é importante seguir práticas de componentização do React para manter o código limpo, modular e fácil de manter.

Integrando widgets ao seu chatbot, você pode criar interações mais ricas e intuitivas para os usuários, melhorando assim a experiência geral de uso da sua aplicação.


## 05) ACTIONSPROVIDER E MESSAGEPARSER
No desenvolvimento de chatbots com o React ChatBot Kit, `ActionProvider` e `MessageParser` são componentes essenciais para gerenciar a lógica das ações do bot e interpretar as mensagens recebidas do usuário, respectivamente.

### ActionProvider
O `ActionProvider` é responsável por definir as ações que o chatbot pode realizar em resposta às interações do usuário. Ele geralmente contém métodos que criam mensagens de resposta e atualizam o estado do chatbot. Aqui está um exemplo simplificado de como você pode implementar um `ActionProvider`:

```javascript
// Exemplo de ActionProvider.js
import React from "react";

class ActionProvider {
  constructor(createChatBotMessage, setStateFunc) {
    this.createChatBotMessage = createChatBotMessage;
    this.setState = setStateFunc;
  }

  greet() {
    const greetingMessage = this.createChatBotMessage("Hello, how can I help you?");
    this.updateChatbotState(greetingMessage);
  }

  handleUserMessage = (message) => {
    // Lógica para processar a mensagem do usuário
    if (message.toLowerCase() === "hello") {
      this.greet();
    } else {
      const defaultMessage = this.createChatBotMessage("I'm sorry, I don't understand.");
      this.updateChatbotState(defaultMessage);
    }
  };

  updateChatbotState = (message) => {
    // Atualiza o estado do chatbot com a nova mensagem
    this.setState(prevState => ({
      ...prevState,
      messages: [...prevState.messages, message]
    }));
  };
}

export default ActionProvider;
```

### MessageParser
O `MessageParser` é responsável por interpretar as mensagens recebidas do usuário e decidir como processá-las. Ele pode conter lógica para analisar a mensagem e decidir qual ação deve ser acionada no `ActionProvider`. Aqui está um exemplo de como você pode implementar um `MessageParser`:

```javascript
// Exemplo de MessageParser.js
import React from "react";

class MessageParser {
  constructor(actionProvider) {
    this.actionProvider = actionProvider;
  }

  parse(message) {
    const lowercaseMessage = message.toLowerCase();

    if (lowercaseMessage.includes("hello")) {
      this.actionProvider.greet();
    } else {
      this.actionProvider.handleUserMessage(message);
    }
  }
}

export default MessageParser;
```

### Integrando no Componente do Chatbot
No seu componente principal onde você renderiza o chatbot (por exemplo, `App.js`), você deve integrar o `ActionProvider` e o `MessageParser` junto com a configuração do chatbot:

```javascript
// Exemplo de App.js
import React, { useState } from "react";
import Chatbot from "react-chatbot-kit";
import "react-chatbot-kit/build/main.css";

import ActionProvider from "./components/ActionProvider";
import MessageParser from "./components/MessageParser";
import config from "./components/config";

function App() {
  const [messages, setMessages] = useState([]);

  const handleNewUserMessage = (newMessage) => {
    setMessages([...messages, newMessage]);
  };

  return (
    <div className="App">
      <header className="App-header">
        <Chatbot
          config={config}
          actionProvider={new ActionProvider(createChatBotMessage, setMessages)}
          messageParser={new MessageParser(new ActionProvider(createChatBotMessage, setMessages))}
          handleNewUserMessage={handleNewUserMessage}
        />
      </header>
    </div>
  );
}

export default App;
```

### Considerações Finais
- **Personalização**: Você pode personalizar a lógica dentro do `ActionProvider` e `MessageParser` para lidar com uma ampla variedade de interações e necessidades do seu chatbot.
  
- **Escalabilidade**: À medida que seu chatbot cresce em complexidade, você pode adicionar mais métodos e lógica ao `ActionProvider` e `MessageParser` para lidar com casos de uso adicionais.

Esses componentes formam o núcleo da funcionalidade do seu chatbot no React ChatBot Kit, permitindo que você crie interações dinâmicas e responsivas com os usuários.


## 06) FAST & SLOW BUTTON
Para criar um botão "Fast & Slow" que permita ao usuário controlar a velocidade de resposta do chatbot no React ChatBot Kit, você pode implementar um componente personalizado que alterne entre duas velocidades predefinidas. Aqui está um exemplo de como você pode fazer isso:

### 1. Adicionar Botões no Config.js
Primeiro, atualize o arquivo `config.js` para incluir botões "Fast" e "Slow" que o usuário pode clicar para ajustar a velocidade de resposta do chatbot.

```javascript
// Exemplo de config.js
import { createChatBotMessage } from "react-chatbot-kit";

const config = {
  botName: "ReactBot",
  initialMessages: [createChatBotMessage("Hello! How can I assist you today?")],
  customStyles: {
    botMessageBox: {
      backgroundColor: "#376B7E",
    },
    chatButton: {
      backgroundColor: "#5ccc9d",
    },
  },
  widgets: [
    {
      widgetName: "fastButton",
      widgetFunc: (props) => <FastButton {...props} />,
    },
    {
      widgetName: "slowButton",
      widgetFunc: (props) => <SlowButton {...props} />,
    },
  ],
};

export default config;
```

### 2. Criar Componentes para os Botões
Crie dois componentes, `FastButton` e `SlowButton`, que alternem a velocidade de resposta do chatbot quando clicados.

```javascript
// FastButton.js
import React from "react";

const FastButton = (props) => {
  const handleFastClick = () => {
    // Ajustar a velocidade do chatbot para rápido
    props.actionProvider.adjustBotSpeed("fast");
  };

  return (
    <button className="chat-button" onClick={handleFastClick}>
      Fast
    </button>
  );
};

export default FastButton;
```

```javascript
// SlowButton.js
import React from "react";

const SlowButton = (props) => {
  const handleSlowClick = () => {
    // Ajustar a velocidade do chatbot para lento
    props.actionProvider.adjustBotSpeed("slow");
  };

  return (
    <button className="chat-button" onClick={handleSlowClick}>
      Slow
    </button>
  );
};

export default SlowButton;
```

### 3. Atualizar ActionProvider
Atualize seu `ActionProvider.js` para incluir um método `adjustBotSpeed` que ajuste a velocidade do chatbot com base no botão clicado.

```javascript
// ActionProvider.js
import React from "react";

class ActionProvider {
  constructor(createChatBotMessage, setStateFunc) {
    this.createChatBotMessage = createChatBotMessage;
    this.setState = setStateFunc;
    this.botSpeed = "normal"; // Velocidade inicial
  }

  greet() {
    const greetingMessage = this.createChatBotMessage("Hello, how can I help you?");
    this.updateChatbotState(greetingMessage);
  }

  handleUserMessage = (message) => {
    // Lógica para processar a mensagem do usuário
    if (message.toLowerCase() === "hello") {
      this.greet();
    } else {
      const defaultMessage = this.createChatBotMessage("I'm sorry, I don't understand.");
      this.updateChatbotState(defaultMessage);
    }
  };

  adjustBotSpeed = (speed) => {
    this.botSpeed = speed;
    const speedMessage = this.createChatBotMessage(`Bot speed set to ${speed}.`);
    this.updateChatbotState(speedMessage);
  };

  updateChatbotState = (message) => {
    // Atualiza o estado do chatbot com a nova mensagem
    this.setState(prevState => ({
      ...prevState,
      messages: [...prevState.messages, message]
    }));

    // Simular tempo de resposta baseado na velocidade
    if (this.botSpeed === "fast") {
      setTimeout(() => {
        // Lógica para resposta rápida
        const fastResponse = this.createChatBotMessage("Fast response!");
        this.setState(prevState => ({
          ...prevState,
          messages: [...prevState.messages, fastResponse]
        }));
      }, 500); // Tempo de resposta rápido (500ms)
    } else if (this.botSpeed === "slow") {
      setTimeout(() => {
        // Lógica para resposta lenta
        const slowResponse = this.createChatBotMessage("Slow response...");
        this.setState(prevState => ({
          ...prevState,
          messages: [...prevState.messages, slowResponse]
        }));
      }, 2000); // Tempo de resposta lento (2000ms)
    } else {
      // Resposta normal
      setTimeout(() => {
        const normalResponse = this.createChatBotMessage("Normal response.");
        this.setState(prevState => ({
          ...prevState,
          messages: [...prevState.messages, normalResponse]
        }));
      }, 1000); // Tempo de resposta normal (1000ms)
    }
  };
}

export default ActionProvider;
```

### 4. Integrar os Componentes no App.js
Finalmente, integre os widgets e componentes no seu componente principal onde você renderiza o chatbot (`App.js`).

```javascript
// App.js
import React, { useState } from "react";
import Chatbot from "react-chatbot-kit";
import "react-chatbot-kit/build/main.css";

import ActionProvider from "./components/ActionProvider";
import MessageParser from "./components/MessageParser";
import config from "./components/config";
import FastButton from "./components/FastButton";
import SlowButton from "./components/SlowButton";

function App() {
  const [messages, setMessages] = useState([]);

  const handleNewUserMessage = (newMessage) => {
    setMessages([...messages, newMessage]);
  };

  return (
    <div className="App">
      <header className="App-header">
        <Chatbot
          config={{
            ...config,
            customComponents: {
              // Adicionar os botões ao chatbot
              header: () => (
                <div className="chatbot-header">
                  <FastButton actionProvider={new ActionProvider(createChatBotMessage, setMessages)} />
                  <SlowButton actionProvider={new ActionProvider(createChatBotMessage, setMessages)} />
                </div>
              ),
            },
          }}
          actionProvider={new ActionProvider(createChatBotMessage, setMessages)}
          messageParser={new MessageParser(new ActionProvider(createChatBotMessage, setMessages))}
          handleNewUserMessage={handleNewUserMessage}
        />
      </header>
    </div>
  );
}

export default App;
```

### Considerações Finais
- **Personalização**: Você pode ajustar os tempos de resposta rápida e lenta conforme necessário no `ActionProvider` para atender aos requisitos específicos do seu chatbot.
  
- **Usabilidade**: Adicionar botões de controle de velocidade como widgets no chatbot pode melhorar a experiência do usuário, permitindo que eles ajustem a interação de acordo com suas preferências.

Seguindo esses passos, você implementará botões "Fast & Slow" no seu chatbot usando o React ChatBot Kit, proporcionando ao usuário controle sobre a velocidade das respostas do bot.

## 07) ÚLTIMA MENSAGEM
Para adicionar uma mensagem de despedida ao seu bot no React ChatBot Kit, você pode ajustar o comportamento do `ActionProvider` para lidar com mensagens de despedida específicas. Aqui está um exemplo de como você pode implementar isso:

### 1. Atualizar o ActionProvider
Atualize o seu `ActionProvider.js` para incluir um método `farewell` que envia uma mensagem de despedida quando o usuário indica que deseja encerrar a conversa.

```javascript
// ActionProvider.js
import React from "react";

class ActionProvider {
  constructor(createChatBotMessage, setStateFunc) {
    this.createChatBotMessage = createChatBotMessage;
    this.setState = setStateFunc;
  }

  greet() {
    const greetingMessage = this.createChatBotMessage("Hello, how can I help you today?");
    this.updateChatbotState(greetingMessage);
  }

  handleUserMessage = (message) => {
    // Lógica para processar a mensagem do usuário
    if (message.toLowerCase() === "hello") {
      this.greet();
    } else if (message.toLowerCase() === "bye" || message.toLowerCase() === "goodbye") {
      this.farewell();
    } else {
      const defaultMessage = this.createChatBotMessage("I'm sorry, I don't understand.");
      this.updateChatbotState(defaultMessage);
    }
  };

  farewell = () => {
    const farewellMessage = this.createChatBotMessage("Goodbye! Have a great day!");
    this.updateChatbotState(farewellMessage);
  };

  updateChatbotState = (message) => {
    // Atualiza o estado do chatbot com a nova mensagem
    this.setState(prevState => ({
      ...prevState,
      messages: [...prevState.messages, message]
    }));
  };
}

export default ActionProvider;
```

### 2. Integrar no Componente do Chatbot
No seu componente principal onde você renderiza o chatbot (`App.js`), certifique-se de passar o `ActionProvider` atualizado para lidar com as mensagens de despedida.

```javascript
// App.js
import React, { useState } from "react";
import Chatbot from "react-chatbot-kit";
import "react-chatbot-kit/build/main.css";

import ActionProvider from "./components/ActionProvider";
import MessageParser from "./components/MessageParser";
import config from "./components/config";

function App() {
  const [messages, setMessages] = useState([]);

  const handleNewUserMessage = (newMessage) => {
    setMessages([...messages, newMessage]);
  };

  return (
    <div className="App">
      <header className="App-header">
        <Chatbot
          config={{
            ...config,
          }}
          actionProvider={new ActionProvider(createChatBotMessage, setMessages)}
          messageParser={new MessageParser(new ActionProvider(createChatBotMessage, setMessages))}
          handleNewUserMessage={handleNewUserMessage}
        />
      </header>
    </div>
  );
}

export default App;
```

### Considerações Finais
- **Personalização**: Você pode ajustar a mensagem de despedida conforme necessário para se adequar ao tom e personalidade do seu chatbot.
  
- **Interação**: Adicionar uma mensagem de despedida ajuda a encerrar a conversa de forma amigável e oferece uma experiência de usuário mais completa.

Ao seguir esses passos, você terá adicionado uma mensagem de despedida ao seu bot no React ChatBot Kit, garantindo uma interação mais natural e positiva com os usuários finais.