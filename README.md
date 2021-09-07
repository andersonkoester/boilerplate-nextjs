## Configurando o ambiente
Criando uma aplicação NextJS com yarn

```$ yarn create next-app```

Estrutura inicial manipulada
```
├── .husky
│   ├── _
│   │   |── .gitignore
│   │   └── husky.sh
│   └── pre-commit
├── .vscode
│   └── settings.json
├── node_modules
├── public
├── src
│   └── pages
│       └── index.tsx
├── .editorconfig
├── .eslintrc.json
├── .prettierrc
├── next-env.d.ts
├── tsconfig.json
└── package.json
```

### Typescript e NextJS
Criar o arquivo ```tsconfig.json``` na raiz do projeto para permitir que o framework utilize por padrão o Typescript.

Executar o comando ```yarn dev``` e efetuar a instalação dos pacotes necessários, que são indicados na tela, para que o projeto identifique e rode com Typescript. Executar novamente o comando ```yarn dev``` para que o projeto seja reconfigurado e os arquivos necessários sejam criados.

Modificar o arquivo ```tsconfig.json``` indicando a propriedade ```"strict" : true```

### .editorconfig (editorconfig.org)
Criar o arquivo ```.editorconfig``` e aplicar dentro dele as configurações para o padrão do projeto.

### ESLint (eslint.org)
É interessante ter o plugin instalado no editor para que os erros possam ser apresentados em tempo de escrita do código.

Instalar o ESLint no projeto através do comando ```$ npx eslint --init```

Selecionar as Opções:
```
? How would you like to use ESLint?
"To check syntax and find problems"

? What type of modules dows your project use?
"Javascript modules (import/export)"

? Which framework does your project use?
"React"

? Does your project use TypeScript? (Y)

? Where does your code run?
"Browser"

? What format do you want your config file to be in?
"JSON"

? Would you like to install them now with npm? (N)
```

Efetuar a instalação dos plugins indicados na tela através do comando ```$ yarn add --dev <pacotes>```

Informar dentro da estrutura de configuração a auto-detecção da versão do React
```
...
"settings" : {
  "react" : {
    "version" : "detect"
  }
},
...
```

#### Plugins ESLint (plugins/rules)

eslint-plugin-react-hooks (```$ yarn add eslint-plugin-react-hooks --dev```)

Plugin para suportar análise dos React Hooks

react/prop-types

Plugin para evitar erros de prop types do TypeScript

react/react-in-jsx-scope

React no NextJS é definido globalmente, define a não necessidade da importação do React nos componentes

@typescript-eslint/explicit-module-boundary-types

Não é necessário explicitar o retorno dos métodos quando o TypeScript já consegue inferir o tipo de retorno

Criar dentro do ```package.json``` a entrada de script ```"lint" : "eslint src"``` que indica que, ao rodar o comando ```$ yarn lint``` o ESLint possa varrer toda a pasta src a procura de erros/warnings.

### Prettier com ESLint (prettier.io)
Instalando ```$ yarn add --dev --exact prettier```

Criar o arquivo ```.prettierrc```

Incluir as regras de formatação de código.

Instalar os plugins ```$ yarn add --dev eslint-plugin-prettier eslint-config-prettier``` e configurar dentro do ```extends``` do ESLint a importação dos plugins

Configurar o arquivo ```.vscode/settings.json``` de forma que o ESLint dispare a formação do código.

### git hook com Husky e Lint-Staged
Previne que sejam enviados para o repositório códigos ruins ou com lixo. Sendo necessário a correção destes warnings para que o código possa assim ser versionado.

Instalando
```
$ yarn add husky --dev
$ yarn add pinst --dev
$ yarn husky install
$ yarn add --dev lint-staged
```

Criar o comando e entradas no ```package.json```:
```
...
"scripts": [
 ...
 "postinstall" : "husky install"
 ...
],
"lint-staged" : {
  "src/**/*" : [
    "yarn lint --fix"
  ]
},
...
```

### Jest com Typescript
```
yarn add --dev jest
yarn add --dev @babel/preset-typescript
yarn add --dev @types/jest
```
