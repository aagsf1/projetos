# Projetos TRT-16 — HTML estático com editor local

## Uso

1. Extraia os arquivos do ZIP.
2. Abra index.html no navegador. Não precisa de servidor, Google Sheets, credencial ou conexão para funcionar.
3. Use Tabela, Cards ou Painel. Busca, filtro por progresso e ordenação funcionam sobre os dados incorporados.
4. Clique em “Abrir editor”. Selecione um projeto e clique em “Editar projeto selecionado”, ou use “Adicionar projeto”. Edite os campos e clique em “Aplicar alterações”.
5. Para excluir, selecione o projeto e confirme “Excluir projeto selecionado”.
6. Clique em “Baixar HTML atualizado”. Confirme o download e abra a cópia baixada para conferir. O navegador poderá acrescentar um número ao nome se já existir outro arquivo.
7. Guarde essa cópia como a nova versão. O arquivo original não é sobrescrito automaticamente.

As alterações aplicadas permanecem apenas na memória da aba até o download. Fechar ou recarregar sem baixar perde as alterações. A página solicita aviso de saída quando há mudanças, sujeito às regras do navegador. “Cancelar” no formulário descarta as alterações ainda não aplicadas. O download é solicitado pelo código; a confirmação de que foi salvo cabe ao usuário.

Não há salvamento automático, localStorage, envio a servidor nem sincronização com a planilha. O arquivo baixado contém a versão integral dos dados incorporada no próprio HTML. Pode ser copiado, encaminhado e hospedado sem dependências.

## Dados iniciais

Extração da aba Projetos em 17/10/2026: 14 projetos e 11 colunas, com cabeçalho na linha 5. Identificador gid: 588070577. Planilha de referência:
https://docs.google.com/spreadsheets/d/1O-UZtvBdfOJbXXjXgtDbrghtuGojKo0BO2gRNYnOBx0/edit?usp=sharing

O nome da planilha indica 2022–2025. Não houve revisão de conteúdo nem declaração de atualização do portfólio para 2026. A conexão ao Google foi removida. O único link externo visível é uma referência opcional à planilha original; URLs HTTP/HTTPS completas em células também podem ser abertas por ação do usuário.

Os dados iniciais foram obtidos como valores formatados diretamente da aba, preservando “Em andamento”, “100% concluído”, quebras de linha e mês/ano. Datas sem dia não recebem um dia inventado. Células vazias são mostradas como “Não informado”. Nomes de arquivos sem URL permanecem texto; nenhum endereço foi inventado.

A ordem inicial é a da extração. Novos projetos são acrescentados ao fim. A ordenação é apenas visual; “Restaurar ordem da planilha” restaura a sequência incorporada, que pode ter recebido adições e exclusões locais. O editor modifica valores, sem adicionar ou remover colunas. A arquitetura de 11 colunas mantém o significado dos campos de data, orçamento e progresso.

No painel, os percentuais são interpretados para contagens e barras, sem transformar a redação original. Não se calculam atraso ou execução financeira. Todos os campos permanecem acessíveis em “Ver todos os campos”.

## Incorporar no portal

Hospede index.html em uma URL HTTPS institucional e substitua a URL de exemplo em incorporacao.html. Insira o trecho no portal. Não há endpoint de dados ou backend de aplicação a instalar.

Após cada edição local, a equipe responsável deverá substituir o HTML hospedado pela nova cópia. Editar uma página aberta no portal apenas muda aquela sessão: não altera o arquivo no servidor.

O editor está disponível a quem abrir o HTML, inclusive visitantes caso esse mesmo arquivo seja publicado. Isso não lhes concede permissão de gravação no portal: somente cria cópias locais. O botão não é autenticação. Se for necessário ocultar o editor para o público, deve-se produzir uma versão de publicação separada; não se deve tratar ocultação de botão como controle de acesso.

As políticas do servidor devem permitir frame-ancestors https://www.trt16.jus.br e a política frame-src do portal deve permitir o endereço de hospedagem. Verificar conflitos com X-Frame-Options. Scripts e estilos estão incorporados; a política CSP institucional deve autorizá-los por hashes apropriados ou outra configuração aprovada pela TI. Nenhuma política de segurança foi alterada no portal.

O trecho não usa sandbox. Se o portal exigir sandbox, a TI deve testar allow-scripts (interações), allow-downloads (download do HTML), allow-modals (confirmação de exclusão e aviso de saída), e as permissões de abertura de links em nova aba quando necessárias. Como não há fetch ou armazenamento, allow-same-origin não é necessário para os dados estáticos. Políticas do navegador ainda podem limitar downloads em iframes; a edição por abertura direta do HTML é a forma principal de manutenção.

Altura fixa configurável no atributo height; largura de 100%. Não há postMessage, ajuste automático de altura ou acesso à página pai.

## Segurança e manutenção

Os textos das células são inseridos com textContent. Somente URLs HTTP/HTTPS completas são convertidas em links; protocolos executáveis não são aceitos. Na exportação, os caracteres <, > e & dos dados são escapados para não encerrar o bloco JSON nem injetar marcação. Não coloque dados sigilosos em arquivo destinado à publicação pública.

O HTML inclui uma seção CONFIG no script, seguida das funções de apresentação e edição. Os dados iniciais estão no bloco application/json identificado como project-data; a manutenção cotidiana pode ser feita pelo editor sem editar código.

## Verificação

Realizados: conferência da estrutura e dos 14 registros com a leitura da aba; sintaxe JavaScript; interpretação de percentuais e datas; preservação dos campos mistos; escape de conteúdo na serialização; ausência de fetch, XMLHttpRequest, backend e temporizador de atualização.

Não realizados: inspeção visual e testes de interação em navegador, acessibilidade com leitor de tela, confirmação do download real, incorporação e políticas do portal. Conferir no navegador antes da publicação: três visualizações, busca, filtro, ordenação, abertura/cancelamento/aplicação do editor, inclusão/exclusão, download e reabertura da cópia.

O projeto utiliza somente arquivos estáticos. A publicação depende da configuração de GitHub Pages do repositório.

## Repositório e publicação

Repositório: https://github.com/aagsf1/projetos

Endereço convencional previsto, sujeito à ativação e confirmação do GitHub Pages:
https://aagsf1.github.io/projetos/

### Ativar GitHub Pages

1. Abra Settings → Pages: https://github.com/aagsf1/projetos/settings/pages
2. Em Build and deployment, escolha Source: Deploy from a branch.
3. Escolha a branch main e a pasta / (root), e salve.
4. Aguarde a publicação e abra o endereço exibido pelo GitHub. Confirme que é a página de projetos.

Não há build ou dependência a instalar. O arquivo .nojekyll desativa o processamento Jekyll para a publicação estática. A disponibilidade pública somente deve ser considerada confirmada após a publicação.

### Atualizar o site após editar

1. Abra index.html localmente ou a página publicada e utilize o editor.
2. Baixe o index.html atualizado e abra a cópia para conferir.
3. Acesse o repositório; use Add file → Upload files e envie o novo index.html à raiz.
4. Revise a alteração e faça o commit na main, ou abra pull request conforme as regras do repositório.
5. Aguarde a publicação e confira o site; recarregue o navegador se necessário.

Não é necessário alterar o iframe a cada edição. Não renomeie o arquivo para index (1).html: o arquivo publicado deve permanecer index.html.

Referência oficial: https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site
