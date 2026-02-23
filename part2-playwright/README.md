
### 3. part2-playwright/test_title.py (улучшенный код с комментариями)

```python
"""
Тест проверяет заголовок главной страницы Playwright.dev
Запускается на двух браузерах: chromium и firefox
Автор: Сергеев Александр (KUSO)
"""

import pytest
from playwright.sync_api import sync_playwright, expect


@pytest.mark.parametrize("browser_name", ["chromium", "firefox"])
def test_playwright_title(browser_name):
    """
    Проверка заголовка страницы https://playwright.dev/
    Ожидаемый заголовок: "Fast and reliable end-to-end testing for modern web apps | Playwright"
    """
    with sync_playwright() as p:
        # Запускаем браузер в headless-режиме (без окна)
        browser = p[browser_name].launch(headless=True)
        page = browser.new_page()

        # Переходим на главную страницу
        page.goto("https://playwright.dev/")

        # Проверяем заголовок страницы
        expected_title = "Fast and reliable end-to-end testing for modern web apps | Playwright"
        expect(page).to_have_title(expected_title)

        # Альтернативный способ проверки (через page.title())
        # assert page.title() == expected_title, f"Заголовок не совпадает: {page.title()}"

        # Закрываем браузер
        browser.close()


# Для запуска из командной строки:
# pytest test_title.py -v
# или по конкретному браузеру:
# pytest test_title.py --browser chromium -v

[Вернуться на главную](..)
