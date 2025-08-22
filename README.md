Установка и настройка Git/GitHub на Ubuntu — straightforward процесс. Вот подробное руководство.

## 1. Установка Git

Откройте терминал (`Ctrl+Alt+T`) и выполните:

```bash
# Обновите список пакетов
sudo apt update

# Установите Git
sudo apt install git
```

**Проверьте установку:**
```bash
git --version
# Должна отобразиться версия, например: git version 2.34.1
```

## 2. Базовая настройка Git

Настройте ваше имя и email (они будут привязываться к вашим коммитам):

```bash
git config --global user.name "Ваше Имя"
git config --global user.email "ваш.email@example.com"
```

**Дополнительные полезные настройки:**
```bash
# Установите основной редактор по умолчанию (например, nano)
git config --global core.editor nano

# Включите цветной вывод в терминале
git config --global color.ui auto

# Просмотрите все текущие настройки
git config --list
```

## 3. Создание SSH-ключа для безопасного подключения к GitHub

SSH-ключ позволяет работать с GitHub без постоянного ввода логина/пароля.

**Сгенерируйте новый SSH-ключ:**
```bash
ssh-keygen -t ed25519 -C "ваш.email@example.com"
```

- Нажмите `Enter` для сохранения в стандартной папке (`/home/ваш_пользователь/.ssh`)
- При желании установите парольную фразу для дополнительной безопасности

**Добавьте SSH-ключ в ssh-agent:**
```bash
# Запустите ssh-agent в фоне
eval "$(ssh-agent -s)"

# Добавьте ваш приватный ключ
ssh-add ~/.ssh/id_ed25519
```

## 4. Добавление SSH-ключа в аккаунт GitHub

**Скопируйте ваш публичный ключ:**
```bash
cat ~/.ssh/id_ed25519.pub
```

Выделите и скопируйте весь вывод (начинается с `ssh-ed25519...`)

**Добавьте ключ в GitHub:**
1. Перейдите на [GitHub.com](https://github.com)
2. Нажмите на ваш аватар → **Settings**
3. В боковом меню выберите **SSH and GPG keys**
4. Нажмите **New SSH key**
5. Введите название (например, "My Ubuntu PC") и вставьте ключ в поле "Key"
6. Нажмите **Add SSH key**

**Проверьте подключение:**
```bash
ssh -T git@github.com
```

Вы должны увидеть: `Hi username! You've successfully authenticated...`

## 5. Основные команды для работы с Git

**Клонирование репозитория:**
```bash
git clone git@github.com:username/repository-name.git
```

**Создание нового репозитория:**
```bash
mkdir my-project
cd my-project
git init
```

**Основной workflow:**
```bash
# Добавить файлы в staging area
git add filename.txt
# или добавить все файлы
git add .

# Создать коммит
git commit -m "Ваше описание изменений"

# Отправить изменения на GitHub
git push origin main

# Получить изменения с GitHub
git pull origin main

# Проверить статус
git status
```

## 6. Установка GitHub CLI (опционально)

Для большего удобства можно установить официальный CLI от GitHub:

```bash
# Установите curl если еще не установлен
sudo apt install curl

# Добавьте ключ репозитория GitHub
curl -fsSL https://cli.github.com/packages/githubcli-archive-keyring.gpg | sudo dd of=/usr/share/keyrings/githubcli-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/githubcli-archive-keyring.gpg] https://cli.github.com/packages stable main" | sudo tee /etc/apt/sources.list.d/github-cli.list > /dev/null

# Установите GH CLI
sudo apt update
sudo apt install gh
```

**Аутентификация в GH CLI:**
```bash
gh auth login
```

## 7. Решение возможных проблем

**Если забыли настроить имя/email перед первым коммитом:**
```bash
# Исправьте информацию автора в последнем коммите
git commit --amend --reset-author
```

**Если нужно сменить репозиторий с HTTPS на SSH:**
```bash
git remote set-url origin git@github.com:username/repository.git
```

**Проверка подключения:**
```bash
# Проверить настройки Git
git config --list

# Проверить SSH подключение
ssh -T git@github.com
```

Теперь вы готовы эффективно работать с Git и GitHub на Ubuntu! Для начала создайте тестовый репозиторий на GitHub и попрактикуйтесь в основных командах.
