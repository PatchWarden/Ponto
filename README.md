# Cartão de Ponto — EMAE

Registro pessoal de ponto para conferência da marcação facial. PWA offline, sem
backend e sem login: cada pessoa instala no próprio celular e os dados ficam no
navegador do aparelho.

## Publicar no GitHub Pages

```bash
git init
git add .
git commit -m "Cartao de ponto - versao inicial"
git branch -M main
git remote add origin https://github.com/SEU-USUARIO/ponto.git
git push -u origin main
```

Depois: **Settings → Pages → Source: Deploy from a branch → Branch `main` / `(root)` → Save**.
Em 1–2 minutos o app fica em `https://SEU-USUARIO.github.io/ponto/`.

O repositório precisa ser **público** (o Pages em repositório privado exige plano pago).
Nenhum dado de ponto vai para o repositório — só o código.

## Instalar no celular

- **Android / Chrome:** abrir o link → menu ⋮ → *Instalar app*
- **iPhone / Safari:** abrir o link → compartilhar → *Adicionar à Tela de Início*
  (precisa ser o Safari; no Chrome do iOS não aparece a opção)

## Regras de jornada

| Situação | Cálculo |
|---|---|
| Seg–sex, um par entrada/saída | `(saída − entrada) − 1h30`, comparado com 7h30 |
| Seg–sex, dois ou mais pares | não desconta o intervalo de novo |
| Sáb/dom | sem desconto e sem previsto — tudo entra como adicional |
| Home office | jornada fixa de 7h30, sem marcação e sem hora extra; fecha em 00:00 |
| Dia útil passado sem marcação | −7h30 (pode ser marcado como abonado no editor do dia) |
| Hoje / dias futuros | "Pendente", fora do saldo |
| Só entrada ou só saída | "Em aberto" / "Inconsistente", fora do saldo |

O saldo apresentado é sempre **do mês selecionado**, não acumulado do ano.

## Retenção

Na abertura, o app arquiva o que passou de 3 meses: apaga o detalhe dia a dia e
mantém congelado o resumo do mês (trabalhado, previsto, saldo, faltas), para o
histórico mês a mês continuar íntegro. O prazo é ajustável em **Ajustes**
(3 / 6 / 12 meses ou desligado).

## Exportação

Arquivo `.xlsx` com duas abas: **Detalhado** (dia a dia, com marcações, situação e
observação) e **Resumo** (fechamento de cada mês). Quando o navegador bloqueia o
download, o botão "Copiar tabela do mês" joga o conteúdo na área de transferência
para colar direto no Excel.

## Atenção

Os dados vivem apenas no `localStorage` do navegador. Limpar os dados do site,
trocar de aparelho ou usar aba anônima apaga tudo. Há backup e restauração em
JSON dentro de **Ajustes** — vale rodar uma vez por mês.

## Arquivos

| Arquivo | Função |
|---|---|
| `index.html` | app inteiro: HTML, CSS, JS e o logo embutido em base64 |
| `sw.js` | service worker (network-first, com cache de fallback offline) |
| `manifest.webmanifest` | metadados de instalação do PWA |
| `icon-192.png`, `icon-512.png` | ícones da tela de início |
| `logo-emae-transparente*.png` | logo recortado, avulso (não é usado pelo app) |
