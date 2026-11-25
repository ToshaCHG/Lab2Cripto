# StegoCrypto - Лабораторная работа №2

## Описание
В данной лабораторной работе реализованы и исследованы три метода стеганографии (LSB-встраивания) с использованием шифрования AES для защиты скрываемого сообщения.

## Зависимости
- numpy
- pillow
- pycryptodome
- scikit-image
- matplotlib

## Установка зависимостей
Выполните в терминале (или в ячейке Colab):
pip install numpy pillow pycryptodome scikit-image matplotlib

## Запуск
1. Загрузите файл `src/lab2.ipynb` в Google Colab.
2. Загрузите исходные изображения в формате PNG (`gradient.png`, `checkerboard.png`) в рабочую директорию Colab.
3. Запустите все ячейки кода по порядку.

## Параметры по умолчанию
- `MESSAGE` = "Hello, this is a secret message for the lab!"
- `PASSWORD` = "SuperSecretPassword123"
- Уровни заполнения (Payload): 1% и 5%.

## Пример обычного LSB (Встраивание)
```python
stego_plain = embed_lsb_sequential(cover, message_bytes)
```

## Пример гибридного режима (Шифрование + LSB)
```python
# 1. Шифрование сообщения
encrypted_data = encrypt_message(message, PASSWORD)

# 2. Встраивание зашифрованных данных (последовательно)
stego_enc = embed_lsb_sequential(cover, encrypted_data)
save_image(stego_enc, 'stego_encrypted.png')

# 3. Встраивание зашифрованных данных (псевдослучайно)
stego_rand = embed_lsb_random(cover, encrypted_data, PASSWORD)
save_image(stego_rand, 'stego_random.png')
```

## Пример извлечения и расшифрования
```python
# 1. Извлечение байтов из LSB (последовательный метод)
extracted_bytes = extract_lsb_sequential(stego_enc)

# 2. Расшифрование
decrypted_text = decrypt_message(extracted_bytes, PASSWORD)
print(f"Извлеченный текст: {decrypted_text}")

# 4. Извлечение из случайного метода
extracted_rand_bytes = extract_lsb_random(stego_rand, PASSWORD)
decrypted_rand_text = decrypt_message(extracted_rand_bytes, PASSWORD)
print(f"Извлеченный текст (Random): {decrypted_rand_text}")
```
