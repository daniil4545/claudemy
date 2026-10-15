# Состояние проекта

Форк `assafkip/claudemy` (`daniil4545/claudemy`, рабочая ветка `dev`, оригинал - remote `upstream`). Цель: инструмент обучения на русском - тема на входе, на выходе аудиолекции (бесплатная локальная озвучка) и HTML-лекции по нашим стандартам (`~/.claude/rules/theory.md`, `html-pages.md`).

## Сделано

- 2026-10-15. Форк и разведка (sdd-lite, подготовка, шаг 1). В `docs/research/`: `claudemy.md` (устройство оригинала, где зашит английский, пробный прогон), `tts.md` (сравнение русской озвучки), `platform.md` (источники, конфликты со стандартами, доставка, вопросы к спеке). Проверено: прогон оригинала на 4 урока прошёл `check_lessons.py`; Piper и Silero озвучивают тестовый диалог за 3-4 с на 45 с аудио; `mermaid-lint` по документам зелёный.

## В работе

- Подготовка, шаг 2 «Спека»: за пользователем. Код не пишем до согласованной спеки.

## Дальше

1. Пользователь слушает сэмплы: `claudemy-workspace/tts-bench/out/` и курс оригинала `claudemy-workspace/llm-inference-serving/deliver/`. Каталог `claudemy-workspace/` в `.gitignore`, лежит только локально.
2. Докачать и озвучить тест Chatterbox Multilingual v3 и Qwen3-TTS 1.7B VoiceDesign (mlx-audio). Стенд: `claudemy-workspace/tts-bench/bench.py`, окружение пересоздать: `uv venv --python 3.12`, `uv pip install mlx-audio piper-tts silero torch soundfile`. Образцы голоса для клонирования: `tts-bench/ref/*.wav` (LibriVox, общественное достояние).
3. Ответы на вопросы `platform.md` (тон, длина урока, один голос или диалог, где слушать, субагенты), затем `docs/spec.md` по `~/.claude/templates/global-spec.md`, затем `spec-review` и `spec`.

## Открытое

- CDN HuggingFace (`us.aws.cdn.hf.co`) из домашней сети рвёт закачку: Chatterbox встал на 1,6 ГБ из 2,7 ГБ. Нужен VPN или повтор. Частичная закачка лежит в `~/.cache/huggingface/hub/models--mlx-community--chatterbox-multilingual-v3`.
- Silero выбрасывает латиницу и цифры: в спеке нужен шаг «текст для чтения вслух».
- Баг оригинала: `render_audio.py`, `stamp_card` склеивает строку `Listen` со следующей. Чинить в рамках задачи про озвучку.
- Субагенты: оригинал читает и пишет уроки агентами, глобальные правила их по умолчанию запрещают. Решение - в спеке.
