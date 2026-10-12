# Firmware and logger (Phase 4)

- Microcontroller firmware: reads every sensor at 1 Hz, prints one CSV line per reading, enforces the safety interlocks
- `logger.py`: writes the CSV to disk, shows a live plot, flags steady state
- A short note on how to flash the board and which pins go where
