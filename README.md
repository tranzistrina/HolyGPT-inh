# HolyGPT-inh

Экспериментальная русскоязычная базовая модель для продолжения текста на православную тематику.

- **Параметры:** 17 308 032.
- **Версия:** step23837.
- **Формат:** GGUF FP16.
- **Контекст:** 512 токенов.
- **Размер файла:** 35 143 264 байта.
- **Проверено:** macOS arm64, Ollama 0.40.11, CPU и Metal; генерация через CLI и API. На других версиях и устройствах результат может отличаться.

Это небольшая base completion model. Она может повторяться, ошибаться и придумывать цитаты; её ответы не являются надёжным богословским источником. Режимы CPU и Metal могут давать разные продолжения из-за округления вычислений.

## Скачать

[holygpt-inh-step23837-f16.gguf](https://media.githubusercontent.com/media/tranzistrina/HolyGPT-inh/main/model/holygpt-inh-step23837-f16.gguf)

SHA256:

```text
a1730ed35c369f0601ac39d5155c5840cdd80e309c92e6019c3e72bd7f20f649
```

## Запуск в Ollama

Установите [Ollama](https://ollama.com/download), затем в отдельном каталоге выполните:

```bash
curl -fL https://media.githubusercontent.com/media/tranzistrina/HolyGPT-inh/main/model/holygpt-inh-step23837-f16.gguf -o holygpt-inh-step23837-f16.gguf
echo 'a1730ed35c369f0601ac39d5155c5840cdd80e309c92e6019c3e72bd7f20f649  holygpt-inh-step23837-f16.gguf' | shasum -a 256 -c -
cat > Modelfile <<'EOF'
FROM ./holygpt-inh-step23837-f16.gguf
TEMPLATE "{{ .Prompt }}"
PARAMETER num_ctx 512
PARAMETER num_predict 128
PARAMETER temperature 0.8
PARAMETER top_k 40
PARAMETER top_p 1.0
PARAMETER repeat_penalty 1.1
EOF
ollama create holygpt-inh:step23837 -f Modelfile
ollama run holygpt-inh:step23837
```

Это продолжение текста без chat-ролей и системного промпта. Для воспроизводимых сравнений используйте temperature 0 и repeat penalty 1; prompt вместе с продолжением должен помещаться в контекст 512.

В репозитории публикуется только модель для инференса и минимальная сопроводительная информация. Код разработки, обучение, конвертер, исходные данные, отдельный тренировочный токенизатор и training checkpoint не публикуются.

Условия использования весов правообладатель определяет отдельно; новая лицензия здесь не предоставляется. Публичная доступность весов технически не предотвращает их копирование и дообучение.
