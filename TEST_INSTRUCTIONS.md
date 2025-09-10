# Инструкции по тестированию MCP плагина

## Обновленные тесты

### 🧪 Unit-тесты
После внесения изменений в код были обновлены следующие тесты:

1. **`CoreBatchValidationTest.java`**
   - ➕ `addElementsToViewAcceptsStylesWithoutError()` - проверка поддержки стилей
   
2. **`ScriptRunHttpHandlerTest.java`**
   - ➕ `testScriptExecutionErrorIncludesDetailedMessage()` - проверка детальных ошибок скриптов
   
3. **`ScriptEnginesHttpHandlerTest.java`**
   - ➕ `testMultipleEnginesSupported()` - проверка поддержки нескольких движков

### 🔥 Smoke-тесты
Обновлен `test_smoke.py`:
- ➕ Тест стилей в `POST /views/{id}/add-element`
- ➕ Тесты скриптов: `GET /script/engines`, `POST /script/run`

## Запуск тестов

### Unit-тесты
```bash
# В Eclipse/Archi среде - правый клик на test папке → Run As → JUnit Test
```

### Smoke-тесты
```bash
cd archi-mcp-plugin/com.archimatetool.mcp/test/smoke
./run_smoke_py.sh
```

## Новая функциональность для тестирования

### 1. Поддержка стилей в addElementsToView
```json
{
  "elementId": "element-id",
  "bounds": {"x": 100, "y": 100, "width": 150, "height": 80},
  "style": {
    "fillColor": "#4CAF50",
    "fontColor": "#FFFFFF",
    "fontSize": "14",
    "opacity": "100"
  }
}
```

### 2. Улучшенная обработка ошибок скриптов
- Детальные сообщения об ошибках в stderr
- Правильное определение движков скриптов
- Поддержка движков: ajs, groovy, jruby

### 3. Выполнение скриптов через MCP
```json
{
  "code": "console.show(); console.log('Test'); visualObject.fillColor = '#FF0000';",
  "engine": "ajs",
  "timeoutMs": 5000
}
```

## Проверка после обновления плагина

1. ✅ Проверить `GET /script/engines` возвращает `{"installed": true, "engines": ["ajs"]}`
2. ✅ Протестировать создание элемента со стилями
3. ✅ Выполнить простой скрипт через `POST /script/run`
4. ✅ Проверить детальные ошибки при неправильном скрипте

## Ожидаемые результаты

- **Unit-тесты**: все должны проходить без ошибок
- **Smoke-тесты**: все шаги должны завершаться успешно
- **Стили**: элементы должны отображаться с заданными цветами
- **Скрипты**: должны выполняться с подробными ошибками при сбоях


