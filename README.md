
# README: MediaPipe Tracking Script

## Descrição Geral
Este script utiliza o MediaPipe para rastrear marcadores corporais e salvar dados de posição em um arquivo Excel. Ele também gera um vídeo anotado com os pontos rastreados. As principais funcionalidades incluem:

1. Processamento de vídeo para identificar pontos corporais.
2. Cálculo de proporção pixels/cm para conversão de medidas.
3. Salvar dados no Excel.

---

## Variáveis e Parâmetros do Código

### 1. **Parâmetros do MediaPipe**

#### `min_detection_confidence=0.7`
- **Descrição**: Confiabilidade mínima necessária para detectar um marcador.
- **Por que 0.7?**: Um valor moderado que equilibra precisão e detecção confiável em cenários com variação de iluminação ou ruído.

#### `min_tracking_confidence=0.7`
- **Descrição**: Confiabilidade mínima necessária para rastrear um marcador já detectado.
- **Por que 0.7?**: Melhora a continuidade do rastreamento em quadros consecutivos, especialmente em movimentos rápidos.

#### `model_complexity=2`
- **Descrição**: Complexidade do modelo de pose do MediaPipe.
  - `0`: Modelo leve, mais rápido, menos preciso.
  - `1`: Modelo intermediário.
  - `2`: Modelo completo, maior precisão.
- **Por que 2?**: Para garantir maior precisão no rastreamento em análises biomecânicas detalhadas.

---

### 2. **Parâmetros Gerais**

#### `Name = 'Ana'`
- **Descrição**: Nome do arquivo de saída para diferenciar múltiplas análises.

#### `VIDEO_INPUT_PATH`
- **Descrição**: Caminho do vídeo de entrada.
- **Exemplo**: `"/Users/borba/Desktop/anna.mp4"`

#### `VIDEO_OUTPUT_PATH`
- **Descrição**: Caminho para salvar o vídeo com pontos anotados.
- **Formato**:
  ```python
  f"/Users/borba/Desktop/video_tracked_{Name}.mp4"
  ```

#### `EXCEL_OUTPUT_PATH`
- **Descrição**: Caminho para salvar o arquivo Excel com os dados.
- **Formato**:
  ```python
  f"/Users/borba/Desktop/hand_tracking_data_{Name}.xlsx"
  ```

---

## Estrutura do Excel

1. **Aba POS (Posição)**:
   - **Coluna 0**: Frame.
   - **Coluna 1**: Tempo (segundos).
   - **Colunas 2-19**: Coordenadas X e Y de marcadores corporais (ex.: `MCP_R_X`, `MCP_R_Y`, etc.).

---

## Funções e Operações Importantes

### `get_pixel_to_cm_ratio(frame)`
- **Descrição**: Permite ao usuário clicar em dois pontos na tela para definir uma referência de 33 cm.
- **Como funciona**:
  1. O usuário seleciona dois pontos clicando com o mouse.
  2. O script calcula a distância entre os pontos em pixels.
  3. Converte a distância para cm com base na proporção fornecida.

- **Por que 33 cm?**: Escolhido como uma distância de referência conhecida.

---

## Mensagens de Saída

1. **Vídeo processado**:
   - Salvo no caminho especificado por `VIDEO_OUTPUT_PATH`.
2. **Dados salvos**:
   - Arquivo Excel com uma aba

---

# Análise de Rastreamento de Mãos

## Descrição
Este script realiza a análise de rastreamento de mãos a partir de dados extraídos de um arquivo Excel processado anteriormente. O processamento inclui:
- Aplicação de um filtro passa-baixa Butterworth para suavizar os dados de posição.
- Cálculo das velocidades lineares dos marcadores.
- Determinação do deslocamento total de cada marcador.
- Geração de gráficos de trajetória com a área convexa utilizada pelos segmentos.
- Cálculo da área e densidade de pontos para cada marcador.
- Análise de assimetria entre os segmentos direito e esquerdo.
- Exportação dos resultados para arquivos Excel e imagem.

## Requisitos
O código requer as seguintes bibliotecas Python:
- `pandas`
- `numpy`
- `matplotlib`
- `scipy`

Você pode instalá-las usando o comando:
```bash
pip install pandas numpy matplotlib scipy
```

## Estrutura do Código
1. **Carregamento dos dados**: O script lê os dados de um arquivo Excel.
2. **Filtragem dos dados**: Aplicação de um filtro Butterworth para suavizar as séries temporais de posição.
3. **Cálculo de variáveis biomecânicas**:
   - Velocidades lineares
   - Deslocamento total
   - Área convexa utilizada
   - Densidade de pontos
   - Assimetria entre lados direito e esquerdo
4. **Geração de gráficos**: Um gráfico de trajetória é gerado e salvo.
5. **Exportação de resultados**: Os dados processados e métricas calculadas são salvos em arquivos Excel.

## Como Usar
1. **Coloque o arquivo de entrada** (`hand_tracking_data_Bruna.xlsx`) na mesma pasta do script.
2. **Execute o script Python**:
   ```bash
   python hand_tracking_analysis.py
   ```
3. **Verifique os arquivos gerados**:
   - `hand_tracking_velocity_Bruna.xlsx`: Contém os dados filtrados e processados.
   - `hand_tracking_summary_Bruna.xlsx`: Contém um resumo das métricas calculadas.
   - `hand_tracking_trajectory_Bruna.png`: Gráfico da trajetória dos marcadores.

## Observações
- Certifique-se de que o arquivo Excel de entrada contém colunas nomeadas corretamente para cada marcador.
- O script automaticamente lida com valores ausentes utilizando `fillna`.
- Caso precise modificar os parâmetros do filtro Butterworth, edite a função `butter_lowpass_filter()`.

## Autor
Este código foi desenvolvido por Edilson Borba para análise de rastreamento de mãos usando Python e bibliotecas científicas.

## Licença
Este projeto é de uso acadêmico e livre para modificações conforme necessário.
