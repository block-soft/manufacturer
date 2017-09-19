# Antifake - система противодействия подделкам товаров


## Схема функционирования

_Знаком + отмечена дополнительная настраиваемая функциональность под конкретную реализацию_


0. [Основной контракт](1.contracts/readme.md)

1. [Создание товара (на стороне производителя)](1.manufacturer/readme.md)
	
	1.1. запускаем скрипт генерации публичного код и скрытого [код](1.manufacturer/generator.js)
	
	1.2. печатаем скрытый на упаковке товара внутри (его можно увидеть только после покупки)
	
	1.3. печатаем публичный код - снаружи (его можно увидеть до покупки)
	
	1.4. проверяем что товар записан в блокчейн по публичному коду

2. Отгружаем товар на доставку - он уходит в розничную сеть

3. Покупатель видит товар и проверяет по публичному коду через специальную страницу на сайте производителя / мобильное приложение / напрямую в блокчейн (2.site/readme.md)
	
	3.1. проверяет что такой код вообще есть - то есть что товар такой был создан
	
	3.2. проверяет что такой код еще не был заявлен как "проданный" - то есть что товар не является "дубликатом"
	
	3.+ при необходимости - может быть добавлена проверка даже магазина отправки и тд (чтобы покупатель из страны Н видел именно официально отгруженное в страну Н)

4. Покупатель принимает решение о покупке

5. Покупатель покупает товар и открывает коробку, получая доступ к скрытому коду, и проверяет его через специальную страницу ...
	
	5.1. если код не подходит - покупатель получает 100% подтверждение что этот товар фальшивка и может сразу требовать деньги обратно (не отходя от кассы магазина)
	
	5.2. если код подходит - но уже был зарегистрирован другим покупателем 
	
	5.2.1. вероятность что это фальшивка 50%, а вот вероятность что поставщик где-то по пути сделал копию 100%, в любом случае покупателю следует затребовать возврата денег / другой товар
		
	5.2.+ при необходимости - может быть добавлено "отслеживание" таких случаев и разбор цепочки доставки для отслеживания "ненадежного" поставщика (предлагается для этого 
	в учетной записи товара ввести "цепочку" доставки, и при массиве "задвоений" товара вычислять узел, присутствующий в таких цепочках)
	
	5.3. если и код подходит, и регистрации не было - покупатель получает 100% подтверждение что этот товар настоящий и автоматически подтверждает свое право собственности
	на него
	
	5.3.+ при необходимости - может быть добавлена передача права собственности покупателем другому участнику и подобная рыночная динамика уже проданных товаров
	
### Замечание по "откуда взять эфир покупателю"

Так как мы не можем 100% знать что покупатель уже является пользователем криптовалют - то мы создаем веб интерфейс с деньгами на контракте, но посылает он только
после предварительной проверки что посетитель-покупатель ввел именно закрытый валидный ключ (т.е. бесплатно проверяем сами и только тогда отправляем за деньги)