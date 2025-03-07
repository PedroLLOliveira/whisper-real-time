# 🗣️ Transcrição de Áudio em Tempo Real com Faster Whisper

## 📌 Visão Geral
Este projeto implementa um sistema de transcrição de áudio em tempo real utilizando o modelo Whisper da OpenAI por meio da biblioteca `faster-whisper`. O programa captura áudio do microfone em segmentos de 5 segundos, transcreve o conteúdo e exibe o texto em tempo real no terminal. Além disso, todas as transcrições são salvas automaticamente em um arquivo de log ao encerrar a execução.

---

## 🚀 Funcionalidades
- 🎤 **Transcrição de áudio em tempo real**
- ⚡ **Uso otimizado de GPU com CUDA** para melhor desempenho
- 📜 **Registro automático da transcrição completa**

---

## 🖥️ Requisitos

### 🔧 Hardware
- **GPU NVIDIA** (Recomendado para aceleração via CUDA)
- **Pelo menos 4GB de VRAM** (8GB+ recomendado para modelos maiores)
- **Microfone** para captura de áudio

### 📦 Software
- **PyTorch** (necessário para execução do Whisper)
  - Se utilizar GPU, instale a versão compatível com CUDA disponível em [PyTorch.org](https://pytorch.org/get-started/locally/)
- **Python 3.8+**
- **Toolkit CUDA** (se utilizar GPU)
- **ffmpeg** (para processamento de áudio)

---

## 📥 Instalação

### 1️⃣ Criar um ambiente virtual (opcional, mas recomendado)
```bash
python -m venv whisper_env
source whisper_env/bin/activate  # macOS/Linux
whisper_env\Scripts\activate  # Windows
```

### 2️⃣ Instalar dependências
```bash
pip install pyaudio faster-whisper numpy torch torchvision torchaudio
```

### 3️⃣ Instalar `ffmpeg`
- **Linux**:
  ```bash
  sudo apt install ffmpeg
  ```
- **Windows** (usando Chocolatey):
  ```powershell
  choco install ffmpeg
  ```

## ▶️ Execução
Para iniciar a transcrição em tempo real, execute o seguinte comando:
```bash
python main.py
```

### ⏹️ Para interromper o programa
Pressione `CTRL + C` para interromper a execução de maneira segura. Ao encerrar, um arquivo `log.txt` será gerado com o texto completo transcrito.

---

## 📜 Estrutura do Código
- **`transcribe_chunk(model, file_path)`**: Processa um segmento de áudio e retorna a transcrição.
- **`record_chunk(p, stream, file_path, chunk_length=5)`**: Grava um segmento de áudio de 5 segundos e o salva como um arquivo WAV.
- **`main2()`**:
  - Carrega o modelo Whisper (`small`) utilizando GPU via CUDA.
  - Captura e transcreve o áudio continuamente.
  - Exibe a transcrição em tempo real e salva o conteúdo completo ao encerrar a execução.

## ⚙️ Configuração
- Você pode modificar a variável `model_size` para utilizar diferentes modelos Whisper (e.g., `tiny`, `base`, `small`, `medium`, `large`).
- O parâmetro `chunk_length` define o tamanho de cada segmento de áudio gravado.
- A transcrição é exibida em **neon green** (`NEON_GREEN`) no terminal para melhor visibilidade.

---

## 🔍 Exemplo de Execução
### 🎙️ Entrada (Usuário falando):
> "Olá, este é um teste de transcrição em tempo real."

### 🖥️ Saída no Terminal:
```bash
🟢 Olá, este é um teste de transcrição em tempo real.
```

### 📜 Conteúdo do `log.txt` ao final da execução:
```
Olá, este é um teste de transcrição em tempo real. Essa ferramenta facilita a conversão de fala para texto.
```

## 📝 Notas
- Se não houver uma GPU compatível com CUDA, o modelo será executado na CPU, resultando em um desempenho mais lento.
- Para melhor precisão na transcrição, utilize um microfone de boa qualidade e reduza ruídos de fundo.

