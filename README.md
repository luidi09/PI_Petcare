
## Executar
```bash
npm install
npm run dev
```

## Gerar versão de produção
```bash
npm run build
npm run preview
```
A pasta `dist/` é criada pelo build. Para publicar com suporte a rotas diretas, configure o servidor para redirecionar as rotas ao `index.html`.

## Organização
- `src/main.jsx`: entrada React e BrowserRouter
- `src/App.jsx`: componentes React, telas, navegação e estados
- `src/styles.css`: CSS original, preservado com ajuste do diálogo
- `public/assets/`: imagens originais
- `index.html`: somente a página de montagem do React, não a implementação das telas


