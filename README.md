# Listagc2

### __1) Descreva com suas próprias palavras de quais formas o uso de técnicas de Continuous Integrations (CI) é capaz de facilitar o trabalho em equipe e garantir que as mudanças feitas por diferentes pessoas no código não resultem em caos durante o desenvolvimento de software.__

__R=__ No geral, o uso de técnicas de CI ajuda a manter um fluxo de trabalho suave e organizado, reduzindo a possibilidade de conflitos no código e permitindo que a equipe entregue software de qualidade com mais eficiência.

1. Integração frequente: CI permite que as alterações no código sejam integradas e testadas com frequência, o que ajuda a identificar e corrigir problemas de forma mais rápida, antes que se tornem maiores e mais complexos.

2. Testes automatizados: CI automatiza a execução de testes de unidade, integração e sistema, garantindo que o código funcione como esperado e não introduza novos erros.

3. Feedback rápido: CI fornece feedback imediato aos desenvolvedores sobre as mudanças feitas no código, permitindo que eles corrijam problemas rapidamente e evitem conflitos no código.

4. Redução de erros: CI ajuda a identificar e corrigir erros mais cedo no ciclo de vida do desenvolvimento, evitando a propagação de erros e a necessidade de grandes correções no futuro.

5. Colaboração: CI promove a colaboração entre os membros da equipe, incentivando-os a trabalhar juntos para garantir que o código funcione corretamente e atenda às necessidades do usuário final.

### __2) Desenvolva um workflow contendo apenas um job que deve executar uma rotina de teste 1) em cada pull request feito na branch master, 2) em cada push nas branches cujos nomes começam com a string release, e 3) manualmente, conforme necessidade dos desenvolvedores. Considere que, para executar o step de testes, basta rodar o comando npm teste dentro do job.__

### __4) Descreva as diferenças entre Actions e Workflows.__
__R=__ Actions são tarefas executáveis que podem ser acionadas por eventos, enquanto Workflows são uma sequência de Actions organizadas para automatizar um fluxo de trabalho completo. As Actions podem ser executadas independentemente ou em um Workflow, enquanto os Workflows usam Actions para realizar tarefas específicas dentro de um processo automatizado.

* __Actions:__ são tarefas executáveis que podem ser acionadas por eventos, como push em um repositório, criação de um pull request ou ocorrência de um problema. As Actions são executadas em um ambiente isolado de contêineres e podem ser criadas pelo desenvolvedor ou por terceiros. Elas podem ser usadas para realizar tarefas específicas, como testes de unidade, criação de artefatos de compilação, envio de notificações ou implantação de código.

* __Workflows:__ são um conjunto de Actions organizadas em uma sequência lógica para automatizar um fluxo de trabalho completo. Um Workflow é acionado por um evento, como push em um repositório, e define uma série de etapas que devem ser executadas para concluir uma tarefa específica, como a implantação de uma atualização de software. As etapas em um Workflow são definidas em um arquivo YAML e podem incluir a execução de múltiplas Actions em um ambiente isolado de contêineres.

### __6) Descreva o que são artefatos e de que forma eles podem ser usados em workflows.__
__R=__ Os artefatos são uma maneira eficaz de compartilhar informações entre diferentes etapas de um Workflow ou entre diferentes Workflows. Eles são especialmente úteis em fluxos de trabalho complexos, em que a geração de arquivos intermediários ou a compartilhamento de informações é importante para o sucesso do processo automatizado.

Os artefatos podem ser usados em Workflows do GitHub para várias finalidades, como:

1. Compartilhar arquivos gerados em diferentes etapas do Workflow: os artefatos podem ser usados para compartilhar arquivos gerados em diferentes etapas do Workflow. Por exemplo, um Workflow que realiza a compilação de código pode gerar um artefato com os binários compilados, que pode ser usado em uma etapa posterior de implantação.

2. Fornecer informações de depuração: os artefatos podem ser usados para fornecer informações de depuração adicionais sobre o Workflow, como logs de execução ou screenshots gerados durante a execução.

3. Armazenar pacotes de terceiros: os artefatos podem ser usados para armazenar pacotes de terceiros, como bibliotecas e dependências, que podem ser usados em diferentes etapas do Workflow.

4. Enviar notificações: os artefatos podem ser usados para enviar notificações para equipes ou usuários específicos, permitindo que eles acompanhem o progresso do Workflow.

### __9) Descreva a função da opção continue-on-error dentro de um workflow.__ 
__R=__ A opção continue-on-error permite que um Workflow continue a ser executado, mesmo que ocorra uma falha em uma etapa, mas deve ser usada com cautela para evitar resultados inesperados. É importante considerar cuidadosamente as implicações de usar essa opção em seu Workflow antes de implementá-la. 

Quando definida como true, ela indica que o Workflow deve continuar a ser executado, mesmo que uma etapa falhe. útil em situações em que uma falha em uma etapa não impede necessariamente o restante do processo automatizado.

### __10) Desenvolva um workflow contendo apenas um job que execute um step de testes em três ambientes distintos: ubuntu-18.04, ubuntu-20.04 e ubuntu-22.04. Considere que, para executar o step de testes, basta rodar o comando npm teste dentro do job.__

~~~yaml
name: Test Workflow

on: [push]

jobs:
  test:
    name: Run Tests
    runs-on: ${{ matrix.os }}
    strategy:
      matrix:
        os: [ubuntu-18.04, ubuntu-20.04, ubuntu-22.04]
    steps:
      - name: Checkout code
        uses: actions/checkout@v2
      - name: Install dependencies
        run: npm install
      - name: Run tests
        run: npm test

~~~

O Workflow contém um job chamado "Run Tests", que é executado em três ambientes diferentes: ubuntu-18.04, ubuntu-20.04 e ubuntu-22.04. Esses ambientes são definidos por meio da matriz strategy no YAML do Workflow.

O job tem três etapas (steps): a primeira etapa é usada para verificar o código (comando checkout) e a segunda etapa instala as dependências do projeto (npm install). A terceira etapa é responsável por executar os testes com o comando npm test.

Com este exemplo de Workflow, é possível executar testes em três ambientes distintos, garantindo assim a compatibilidade do código com diferentes versões do sistema operacional Ubuntu.

