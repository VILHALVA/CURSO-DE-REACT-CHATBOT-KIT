# MANUAL
## INSTALAÇÃO E CONFIGURAÇÃO:
1. **Node.js e npm**: Certifique-se de que o Node.js e o npm estão instalados em seu sistema. Você pode baixá-los de [nodejs.org](https://nodejs.org/).

2. **Instale o Create React App**:
   ```bash
   npm install -g create-react-app
   ```

3. **Crie um Novo Projeto React**:
   ```bash
   create-react-app my-chatbot
   cd my-chatbot
   ```

4. **Instale o React ChatBot Kit**:
   No diretório do seu projeto, execute:
   ```bash
   npm install react-chatbot-kit
   ```

## PRIMEIRO PROJETO:
1. **Estrutura do Projeto**:
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

2. **Configuração do ChatBot**:
   Crie uma pasta `components` dentro de `src` e adicione os seguintes arquivos:

   **1. src/components/ActionProvider.js**:
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

   **2. src/components/MessageParser.js**:
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

   **3. src/components/config.js**:
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

3. **Integrando o ChatBot ao App**:
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

4. **Executando o Projeto**:
   No diretório do seu projeto, execute:
   ```bash
   npm start
   ```

   O aplicativo será aberto no navegador em `http://localhost:3000`, e você verá seu chatbot em funcionamento.

Seguindo esses passos, você terá um chatbot básico funcionando com o React ChatBot Kit. A partir daí, você pode personalizar e expandir o chatbot conforme suas necessidades.