# GEODATA_MG

Repositório de dados geoespaciais dos municípios de Minas Gerais, mantido pelo Centro de Gerenciamento e Análise de Dados (CGA) da Polícia Militar de Minas Gerais (PMMG).

## 📌 Sobre

Este repositório disponibiliza arquivos vetoriais (shapefiles) dos municípios mineiros, organizados individualmente por pasta. Cada diretório contém os dados geográficos correspondentes a um município específico, facilitando o acesso e a integração em sistemas de informação geográfica (SIG), análises espaciais e outras aplicações.

## 📁 Estrutura do Repositório

A estrutura do repositório é organizada da seguinte forma:

```
geodata-mg/
├── AbadiaDourados/
│   └── municipio.geojson
├── Abaete/
│   └── municipio.geojson
├── AbreCampo/
│   └── municipio.geojson
├── ...
```

Cada pasta é nomeada com o nome do município correspondente, sem espaços, acentos ou conjunções (como "de", "do", "da"), seguindo um padrão que facilita a busca e o uso programático dos dados, mais abixo está um exemplo de como realizar a normalização dos nomes dos municípios.

## 🧰 Utilização

Para utilizar os dados geoespaciais em seu projeto:

1. Clone o repositório:

   ```bash
   git clone https://github.com/CGA-PMMG/geodata-mg.git
   ```

2. Acesse a pasta do município desejado:

   ```bash
   cd geodata-mg/NomeDoMunicipio
   ```

3. Utilize os arquivos shapefile (.shp) em seu software de SIG preferido.

## 🔄 Padronização de Nomes

Para facilitar a integração com sistemas que requerem nomes padronizados, recomenda-se a seguinte função para formatar os nomes dos municípios:

```typescript
function formatarNomeMunicipio(nome: string): string {
  return nome
    .normalize("NFD") //Converte caracteres com acentos em suas formas decompostas (Água -> Agua + diacrítico)
    .replace(/[\u0300-\u036f]/g, "") //Remove os diacríticos gerados pela decomposição na linha anterior (Água -> Agua)
    .split(" ") //Divide o nome em um array de palavras, usando o espaço como delimitador (Juiz de Fora -> ["Juiz", "de", "Fora"]
    .filter((palavra) => /^[A-Z]/.test(palavra)) //Retira todas as palavras que não começam com letra maiúscula (["Juiz", "de", "Fora"] -> ["Juiz", "Fora"])
    .join(""); //une as palavras do array em uma única string, sem espaçamentos entre elas (["Juiz", "Fora"] -> ["JuizFora"])
}
```

## 🤝 Contribuições

Contribuições, correções e sugestões são sempre bem-vindas! Caso identifique melhorias ou tenha novas ideias, sinta-se à vontade para abrir uma *issue* ou enviar um *pull request*. Este repositório é um espaço colaborativo, e sua participação é fundamental para torná-lo ainda mais útil e eficiente para todos. 

## 📄 Licença

Este projeto está licenciado sob a Licença MIT. Consulte o arquivo [LICENSE](LICENSE) para mais detalhes.

---

Para mais informações ou contribuições, sinta-se à vontade para abrir uma issue ou pull request.
