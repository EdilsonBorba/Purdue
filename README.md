
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

## Contato
Em caso de dúvidas ou sugestões, entre em contato:
- **Autor**: [Edilson Borba]
- **E-mail**: [edilson.borba@example.com]
