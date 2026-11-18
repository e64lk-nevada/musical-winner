# BTC 5M AI PRO — v0.2

Український signal-only BTC 5m dashboard. Користувач приймає рішення вручну.

## Що змінено у v0.2
- Взято компактний мобільний dashboard та індикаторні ідеї з наданого `btc-5m-signals.zip`.
- Відсоток `confidence/probability` прибрано: `signal_strength` — лише нормалізована сила евристичного score, НЕ шанс успіху.
- Перед аналізом відкидається незакрита хвилинна свічка Binance.
- Додано версію API, час генерації, кількість використаних закритих свічок і явну ознаку `execution_enabled: false`.
- Додано базові unit tests для захисної логіки.

## Поточні можливості
- FastAPI backend + PWA frontend.
- Binance BTCUSDT 1m klines та spot price.
- Momentum, EMA, діапазон, обсяг, волатильність.
- UP / DOWN / NO TRADE.
- Опційне тестове Telegram-повідомлення.

## Ще НЕ реалізовано
- Polymarket market resolver / order book.
- Chainlink RTDS.
- Постійний серверний worker та автоматичне Telegram-сповіщення про нові сигнали.
- База історії сигналів, backtesting, walk-forward та калібрування.
- Production deployment, HTTPS, моніторинг.

Поки ці джерела й перевірки не підключені, це експериментальний індикаторний прототип, а не підтверджена система прогнозування результатів Polymarket.

## Запуск
Python 3.11+
```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
cp .env.example .env
uvicorn app.main:app --host 0.0.0.0 --port 8000
```
Відкрити `http://127.0.0.1:8000`.

## Тести
```bash
pip install pytest
pytest -q
```

## Безпека
- Немає wallet/private key.
- Немає створення або підписання ордерів.
- `execution_enabled` завжди false.
- Не надсилайте Telegram token у чат і не комітьте `.env`.

Для iPhone потрібен HTTPS-хостинг; Safari → Share → Add to Home Screen. iOS PWA не гарантує безперервної фонової роботи, тому майбутній моніторинг має працювати на сервері.
