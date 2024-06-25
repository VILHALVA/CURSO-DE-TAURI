## 1. INSTALAÇÃO DO TAURI
### INSTALAÇÃO VIA NPM (NODE PACKAGE MANAGER):
Certifique-se de ter o Node.js e o Cargo (gerenciador de pacotes do Rust) instalados antes de prosseguir.

#### WINDOWS:
Abra o Prompt de Comando e execute os seguintes comandos:
```bash
npm install -g @tauri-apps/cli
cargo install tauri-cli
```

#### MACOS E LINUX:
Abra o terminal e execute os seguintes comandos:
```bash
sudo npm install -g @tauri-apps/cli
cargo install tauri-cli
```

## 2. CRIANDO UM PROJETO TAURI
### APENAS COM TAURI:
1. Abra o terminal ou Prompt de Comando.
2. Navegue até o diretório onde deseja criar o projeto.
3. Execute o seguinte comando para criar um novo projeto com Vite (um bundler rápido para projetos front-end):
```bash
npm create tauri-app
```
4. Siga as instruções interativas para configurar o projeto.

### TAURI COM REACT:
1. **Criar um novo projeto frontend (React, Vue, Svelte, etc.)**:
   Vamos usar o Create React App como exemplo. Execute o seguinte comando no terminal:

   ```bash
   npx create-react-app meu-projeto
   cd meu-projeto
   ```

2. **Adicionar o Tauri ao projeto**:
   Depois de entrar no diretório do seu projeto, adicione o Tauri com o seguinte comando:

   ```bash
   npx tauri init
   ```

3. **Configurar o Tauri**:
   Durante o processo de inicialização, você será solicitado a fornecer algumas informações sobre o seu projeto. As opções padrão geralmente são suficientes para começar. Após a configuração, o arquivo `tauri.conf.json` será criado na pasta `src-tauri`.

## 3. EXECUTANDO O PROJETO TAURI
### PASSO A PASSO PARA EXECUTAR O PROJETO:
1. Navegue até o diretório do seu projeto usando o terminal.
2. Execute o seguinte comando para iniciar o aplicativo Tauri:
```bash
npm run tauri dev
```

### ESTRUTURA DO PROJETO:
O projeto criado terá uma estrutura básica de arquivos, incluindo um arquivo `tauri.conf.json` que configura o comportamento do Tauri e um diretório `src` onde você pode colocar seus arquivos HTML, CSS e JavaScript para a interface do usuário.

### DIRETÓRIOS:
A estrutura dos diretórios em um projeto Tauri geralmente segue um padrão que facilita a organização e manutenção do código.

```
my-tauri-app/
├── src/
│   ├── main.rs
│   ├── index.html
│   ├── styles.css
│   └── index.js
├── src-tauri/
│   ├── tauri.conf.json
│   └── Cargo.toml
├── .gitignore
├── package.json
├── package-lock.json
└── README.md
```

1. **src/**:
   - Diretório principal do código fonte da aplicação.
   - `main.rs`: Arquivo principal do Rust que inicializa a aplicação Tauri.
   - `index.html`: O arquivo HTML principal que é carregado na janela do Tauri.
   - `index.js`: O código JavaScript específico para a interface gráfica e a lógica do frontend.
   - `styles.css`: Arquivo de estilos CSS para a interface.

2. **src-tauri/**:
   - Diretório contendo a configuração do Tauri e arquivos relacionados ao backend da aplicação.
   - `tauri.conf.json`: Arquivo de configuração do Tauri.
   - `Cargo.toml`: Arquivo de configuração do Cargo para gerenciar dependências Rust.

3. **.gitignore**:
   - Arquivo que especifica quais arquivos e diretórios devem ser ignorados pelo Git.

4. **package.json**:
   - Arquivo de configuração do npm que contém informações sobre o projeto e suas dependências.

5. **package-lock.json**:
   - Arquivo gerado automaticamente pelo npm para garantir que as instalações sejam reproduzíveis, bloqueando as versões das dependências.

6. **README.md**:
   - Arquivo de documentação do projeto, geralmente contém informações sobre como configurar e executar o projeto.

## CRIANDO UM EXECUTÁVEL COM TAURI:
Para converter seu projeto Tauri em um aplicativo executável ou instalador, você pode usar a CLI do Tauri para empacotar a aplicação.

1. **Configurar o `tauri.conf.json`**:
   Certifique-se de que o arquivo `tauri.conf.json` está configurado corretamente com as informações do seu aplicativo.

   ```json
   {
     "package": {
       "productName": "MyTauriApp",
       "version": "0.1.0"
     },
     "tauri": {
       "bundle": {
         "active": true,
         "targets": ["all"],
         "identifier": "com.example.mytauriapp",
         "icon": ["src/assets/icon.png"]
       }
     }
   }
   ```

2. **Rodar o Build**:
   Execute o comando de build para gerar os executáveis e instaladores.

   ```bash
   npm run tauri build
   ```

   Isso criará os arquivos de instalação na pasta `src-tauri/target/release`.

### EXEMPLOS DE CONFIGURAÇÕES:
#### WINDOWS:
Para Windows, o alvo comum é `msi`.

```json
"bundle": {
  "active": true,
  "targets": ["msi"],
  "identifier": "com.example.mytauriapp",
  "icon": ["src/assets/icon.ico"]
}
```

#### MACOS:
Para macOS, você pode usar o alvo `dmg`.

```json
"bundle": {
  "active": true,
  "targets": ["dmg"],
  "identifier": "com.example.mytauriapp",
  "icon": ["src/assets/icon.icns"]
}
```

#### LINUX:
Para Linux, o alvo `AppImage` é bastante popular.

```json
"bundle": {
  "active": true,
  "targets": ["AppImage"],
  "identifier": "com.example.mytauriapp",
  "icon": ["src/assets/icon.png"]
}
```

### PERSONALIZAÇÃO ADICIONAL:
Você pode personalizar ainda mais o processo de build com várias opções disponíveis no `tauri.conf.json`. Consulte a [documentação oficial](https://tauri.app/) para uma lista completa de opções e exemplos avançados.

## SOBRE O ICONE:
Para criar instaladores e executáveis para sua aplicação Tauri, é essencial ter ícones em formatos e tamanhos específicos para garantir que eles sejam exibidos corretamente em diferentes plataformas.

### REQUISITOS DE ÍCONE POR PLATAFORMA:
#### WINDOWS:
- **Formato**: `.ico`
- **Tamanho**: Deve incluir múltiplos tamanhos dentro do arquivo `.ico`, mas o tamanho mínimo requerido é 256x256 pixels.

#### MACOS:
- **Formato**: `.icns`
- **Tamanho**: Deve incluir múltiplos tamanhos dentro do arquivo `.icns`, com o maior sendo 512x512 pixels (ou 1024x1024 para suportar alta resolução Retina).

#### LINUX:
- **Formato**: `.png` ou vetor (`.svg`), embora `.png` seja mais comum.
- **Tamanho**: Múltiplos tamanhos podem ser especificados, mas 256x256 pixels é um tamanho comum.

### CRIANDO ÍCONES APROPRIADOS:
#### FERRAMENTAS PARA CRIAR ÍCONES:
1. **RealWorld Icon Editor**:
   - Pode criar arquivos `.ico` com múltiplas resoluções.
   - [RealWorld Icon Editor](http://www.rw-designer.com/online_icon_maker)

2. **IcoFX**:
   - Ferramenta paga para criar e editar ícones.
   - [IcoFX](https://icofx.ro/)

3. **Icon Slate** (para macOS):
   - Pode criar arquivos `.icns` e outros formatos.
   - [Icon Slate](https://www.kodlian.com/apps/icon-slate)

4. **GIMP**:
   - Editor de imagens gratuito que pode ser usado para criar ícones PNG.
   - [GIMP](https://www.gimp.org/)

5. **Inkscape**:
   - Editor de gráficos vetoriais que pode ser usado para criar ícones SVG.
   - [Inkscape](https://inkscape.org/)

#### PASSO A PASSO PARA CRIAR UM ÍCONE `.ICO` COM MÚLTIPLAS RESOLUÇÕES:
1. **Criar Imagens PNG em Diferentes Resoluções**:
   - Crie imagens PNG nas resoluções: 16x16, 32x32, 48x48, 64x64, 128x128, e 256x256.

2. **Usar um Editor de Ícones**:
   - Abra o RealWorld Icon Editor.
   - Importe cada PNG para adicionar diferentes resoluções ao ícone.
   - Exporte o arquivo como `.ico`.

3. **Configurar o Caminho do Ícone no `tauri.conf.json`**:
   Certifique-se de que o caminho do ícone está correto no campo `bundle.icon` do `tauri.conf.json`.

   ```json
   {
     "bundle": {
       "active": true,
       "targets": ["msi"],
       "identifier": "com.example.mytauriapp",
       "icon": ["src/assets/icon.ico"]
     }
   }
   ```

## CONCLUSÃO:
Agora você instalou o Tauri e criou um novo projeto Tauri. A partir daqui, você pode explorar mais sobre o desenvolvimento de aplicativos de desktop usando tecnologias da web e personalizar seu projeto conforme necessário.
