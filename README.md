# Achievement Service

## Описание

Микросервис достижений в веб-приложении **CorporationX**. Отвечает за отслеживание прогресса пользователей и выдачу достижений за различные виды активности в приложении: набор подписчиков, создание проектов, лайки под постами, комментарии, выполненные цели и другие метрики вовлечённости. Реализован по event-driven принципу — сервис слушает события из других сервисов (например, `follower_channel` из `user_service`) через Redis Pub/Sub, обновляет прогресс пользователя по соответствующему достижению и выдаёт его при достижении нужного порога. При выдаче любого достижения `achievement_service`, в свою очередь, публикует событие в собственный Redis-топик `achievement_channel`, чтобы другие сервисы (например, `notification_service`) могли узнать об этом и, в частности, отправить пользователю уведомление о полученном достижении.

## Стек

- Java 17
- Spring Boot 3
- Spring Data JPA
- PostgreSQL
- Redis (Pub/Sub)
- Liquibase
- Feign Client
- MapStruct
- JUnit 5

## Запуск

### Предварительные требования
- Docker и Docker Compose
- JDK 17

### Шаги

1. Поднять инфраструктуру (Postgres, Redis, MinIO, Kafka):
```bash
git clone https://github.com/Erik18999/infra.git
cd infra
./run.sh
```
2. Склонировать и запустить сам сервис (порт 8085):
```bash
git clone https://github.com/Erik18999/achievement_service.git
cd achievement_service
```
Открыть проект в IntelliJ IDEA и запустить [`AchievementServiceApp`](src/main/java/faang/school/achievement/AchievementServiceApp.java).
