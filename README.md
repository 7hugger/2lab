import re

def is_valid_hex_number(token):
    """ Проверяет, является ли строка валидным шестнадцатеричным числом. """
    try:
        value = int(token, 16)
        return (
            value % 2 == 1 and                   # Нечетное
            value <= 409510 and                  # Не превышает 409510
            len(token) > 3                       # Содержит более 3 цифр
        )
    except ValueError:
        return False

def number_to_words(number):
    """ Преобразует число в строку, где каждая цифра представлена прописью. """
    digit_to_word = {
        '0': 'ноль', '1': 'один', '2': 'два', '3': 'три', '4': 'четыре',
        '5': 'пять', '6': 'шесть', '7': 'семь', '8': 'восемь', '9': 'девять'
    }
    return '-'.join(digit_to_word[digit] for digit in str(number))

def process_file(file_path):
    """ Читает файл, используя регулярные выражения для обработки данных. """
    pattern = re.compile(r'\b[0-9A-Fa-f]{4,}\b')  # Регулярное выражение для поиска шестнадцатеричных чисел из 4 или более символов
    valid_numbers = []

    with open(file_path, 'r') as f:
        content = f.read()
        tokens = pattern.findall(content)  # Находим все совпадения в файле

        for token in tokens:
            if is_valid_hex_number(token):
                valid_numbers.append(int(token, 16))

    if valid_numbers:
        valid_numbers.sort()
        print(f"Подходящие числа: {valid_numbers}")
        print(f"Количество чисел: {len(valid_numbers)}")
        print(f"Минимальное число прописью: {number_to_words(valid_numbers[0])}")
    else:
        print("Подходящих чисел не найдено.")

# Укажите путь к вашему файлу
file_path = 'D:\input.txt'
process_file(file_path)
