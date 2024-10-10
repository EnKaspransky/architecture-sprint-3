# AsIs

## Текущая функциональтность:
- удалённое включение/отключение отопления
- установка желаемой температуры
- просмотр текущей температуры
- просмотр текущего состояние

## Архитектура монолитного приложения:
  Язык программирования: Java
  База данных: PostgreSQL
  Архитектура: Монолитная, все компоненты системы (обработка запросов, бизнес-логика, работа с данными) находятся в рамках одного приложения.
  Взаимодействие: Синхронное, запросы обрабатываются последовательно.
  Масштабируемость: Ограничена, так как монолит сложно масштабировать по частям.
  Развертывание: Требует остановки всего приложения.

## Структура:

    /docs
      /AsIs                                             // каталог с описанием текущего состояния
        c4_container.puml                               // c4 диаграмма контейнеров
        c4_context.puml                                 // c4 диаграмма конекста

# ToBe

## Структура:

    /docs
      /ToBe                                             // каталог с планируемым состоянием
        /component                                      // каталог с c4 диаграммами компонентов
          c4_component_api_gateway.puml
          c4_component_auth_service.puml
          c4_component_command_service.puml
          c4_component_device_manager_service.puml
          c4_component_telemetry_service.puml
          c4_component_telemetry_shovel_service.puml
        api.yaml                                        // описание API
        c4_container.puml                               // c4 диаграмма контейнеров
        c4_context.puml                                 // c4 диаграмма конекста
        ER.puml                                         // ER-диаграмма

# Smart Home Monolith

## Описание

Проект "Smart Home Monolith" представляет собой монолитное приложение для управления отоплением и мониторинга температуры в умном доме. Пользователи
могут удаленно включать/выключать отопление, устанавливать желаемую температуру и просматривать текущую температуру через веб-интерфейс.

## Структура проекта

Проект организован в соответствии со стандартной структурой Maven/Gradle проекта:

- **Основной класс приложения** аннотирован `@SpringBootApplication`.
- **Пакеты**:
    - `controller` - контроллеры для обработки HTTP-запросов.
    - `service` - сервисы для бизнес-логики.
    - `repository` - репозитории для доступа к базе данных.
    - `entity` - сущности JPA.
    - `dto` - объекты передачи данных (DTO).

## Зависимости

Проект использует следующие зависимости:

- Java 17
- Maven >=3.8.1 && <4.0.0
- `spring-boot-starter-web` - для создания веб-приложений.
- `spring-boot-starter-data-jpa` - для работы с JPA и базой данных.
- `postgresql` - драйвер для работы с PostgreSQL.
- `springfox-boot-starter` - для интеграции Swagger.
- `lombok` - для упрощения написания кода.
- `spring-boot-starter-test`, `spring-boot-testcontainers`, `junit-jupiter`, `testcontainers` - для тестирования.

## Запуск

1.

``` shell
docker run --name postgres-db -e POSTGRES_DB=smart_home -e POSTGRES_USER=your_username -e POSTGRES_PASSWORD=your_password -p 5432:5432 -d postgres:13-alpine
```

2.

``` shell
mvn spring-boot:run
```

## Тесты

``` shell
mvn test
```

## Конфигурация

### Подключение к базе данных

Конфигурация подключения к PostgreSQL находится в файле `application.yml`:

```yaml
spring:
  datasource:
    url: jdbc:postgresql://localhost:5432/smart_home
    username: user
    password: password
  jpa:
    hibernate:
      ddl-auto: update
    show-sql: true
```

## Логирование

В проекте используется SLF4J для логирования.

## Тестирование

В проекте написаны модульные тесты для сервисов и контроллеров.
