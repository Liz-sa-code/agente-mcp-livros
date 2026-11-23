---
name: pesquisa-produtos
description: Pesquisa produtos em sites usando MCP Playwright e prepara um relatório Markdown com resultados verificados.
---

# Pesquisa de produtos

## Objetivo

Pesquisar produtos em sites e gerar um resumo em Markdown baseado somente em informações observadas nas páginas.

## Entradas

- **Site/URL:** endereço inicial do site ou da página de produtos.
- **Termos:** um ou mais nomes ou expressões a pesquisar.
- **Filtros opcionais:** critérios como faixa de preço, marca, categoria ou disponibilidade.
- **Quantidade de resultados:** máximo de resultados a registrar por termo.

Se uma entrada não for informada, prossiga sem esse critério e deixe explícita qualquer limitação relevante.

## Estratégia de busca

1. Verifique se há um campo de busca visível e utilizável. Se houver, pesquise cada termo e aplique apenas os filtros solicitados.
2. Se não houver campo de busca, não tente submeter formulários inexistentes. Para cada termo, escolha a categoria mais provável com base no conteúdo e na navegação visíveis.
3. Se ainda não houver resultados, percorra as páginas de listagem disponíveis, sem ultrapassar **5 páginas por termo**. Conte todas as páginas de resultados consultadas, inclusive as da categoria, nesse limite. Pare ao atingir o limite.

Não acesse páginas ou áreas que não sejam necessárias para responder à solicitação. Se o limite impedir uma busca abrangente, informe isso no relatório.

## Procedimento

1. Use as ferramentas MCP Playwright para abrir o site, observar a página e navegar. Não substitua a navegação por chamadas diretas ao site ou por outras ferramentas de navegador.
2. Verifique a presença de busca, as categorias e os controles de paginação visíveis. Pesquise um termo por vez conforme a estratégia acima.
3. Compare os títulos e demais dados exibidos com o termo e os filtros solicitados. Registre até a quantidade pedida, sem repetir o mesmo produto.
4. Colete, quando disponíveis, título original, preço, disponibilidade, avaliação, categoria e URL individual do produto. Se algum dado não estiver exposto, marque-o como **Não informado na página**.
5. Abra a página individual somente quando necessário para confirmar dados ou quando o usuário solicitar resumo. Escreva o resumo no idioma pedido, fiel à descrição visível e sem acrescentar fatos.
6. Gere um relatório Markdown organizado por termo. Registre também a estratégia, as categorias e as páginas consultadas e os termos sem resultados.
7. Se for solicitado criar um arquivo, salve-o no caminho indicado e leia-o novamente para conferir conteúdo e consistência com os dados observados.

## Regras

- Não invente, estime ou complete informações ausentes.
- Se não houver resultado após a busca realizada, registre **Não encontrado** e indique as categorias e páginas consultadas.
- Respeite os filtros, a quantidade solicitada e o limite máximo de 5 páginas por termo. Não sugira que a busca foi exaustiva se ela foi interrompida pelo limite.
- Não registre dados pessoais de vendedores. Inclua somente informações de produto necessárias à solicitação.
- Não contorne CAPTCHA, autenticação, bloqueios ou outras restrições do site. Interrompa a navegação afetada e informe a limitação.
- Não compre, reserve, adicione ao carrinho nem altere dados no site.

## Formato de saída

Organize os resultados por termo. Use uma tabela por termo:

```markdown
## <Termo de busca>

| Título original | Preço | Disponibilidade | Avaliação | Categoria | Link |
|---|---|---|---|---|---|
| <Título> | <Preço ou Não informado na página> | <Disponibilidade ou Não informado na página> | <Avaliação ou Não informado na página> | <Categoria ou Não informado na página> | [Ver produto](<URL>) |

**Resumo do primeiro resultado:** <Resumo em português, somente quando solicitado e quando houver resultado.>
**Busca realizada:** <Campo de busca ou categorias e páginas consultadas.>
```

Se não houver resultados, substitua a tabela por:

```markdown
**Não encontrado.** Consultei <categorias e páginas>. <Limitações, se houver.>
```
