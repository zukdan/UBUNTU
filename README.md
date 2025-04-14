Откройте терминал. Вы можете найти терминал, выполнив поиск в меню приложений или нажав Ctrl+Alt+T.

Используйте cat для просмотра содержимого файла:

bash

sudo cat /etc/apt/apt.conf.d/50unattended-upgrades
sudo: Эта команда запускает команду cat с правами администратора (root), необходимыми для доступа к файлу. Вам будет предложено ввести свой пароль.
cat: Эта команда выводит содержимое файла в терминал.
/etc/apt/apt.conf.d/50unattended-upgrades: Это путь к конфигурационному файлу автоматических обновлений.
Проанализируйте вывод. Просмотрите содержимое файла в терминале. Обратите внимание на важные разделы, описанные в предыдущем ответе, особенно:

Unattended-Upgrade::Origins-Pattern: Убедитесь, что включены репозитории безопасности Ubuntu (и, возможно, другие репозитории, которые вы хотите обновлять автоматически). Должны быть строки, подобные:

"origin=Ubuntu,codename=${distro_codename},label=Ubuntu-Security";
"origin=Ubuntu,codename=${distro_codename},label=Ubuntu";
(или аналогичные)
Unattended-Upgrade::Package-Blacklist: Проверьте, есть ли в списке пакеты, которые вы не хотите обновлять автоматически.
Unattended-Upgrade::Auto-Reboot: Проверьте, включена ли автоматическая перезагрузка.
Unattended-Upgrade::Mail: Проверьте, настроен ли адрес электронной почты для уведомлений.
Unattended-Upgrade::MailOnlyOnError: Проверьте, будет ли отправляться письмо только при ошибках.
Пример вывода (примерный, он может немного отличаться в вашей системе):


// Automatically upgrade packages from these origins:
APT::Periodic::Unattended-Upgrade "1";

Unattended-Upgrade::Origins-Pattern {
        "origin=Ubuntu,codename=${distro_codename},label=Ubuntu-Security";
        "origin=Ubuntu,codename=${distro_codename},label=Ubuntu";
        "origin=Ubuntu,codename=${distro_codename}-updates,label=Ubuntu";
        //"origin=Ubuntu,codename=${distro_codename}-proposed,label=Ubuntu-Proposed";
        //"origin=Ubuntu,codename=${distro_codename}-backports,label=Ubuntu-Backports";
};

Unattended-Upgrade::Package-Blacklist {
//      "firefox";
//      "chromium-browser";
//      "kernel-*";
};

// Unattended-Upgrade::Mail "root";
// Unattended-Upgrade::MailOnlyOnError "true";
Unattended-Upgrade::Auto-Reboot "false";
Unattended-Upgrade::Auto-Reboot-Time "02:00";
Интерпретация примера:

APT::Periodic::Unattended-Upgrade "1";: Включены периодические автоматические обновления.
Unattended-Upgrade::Origins-Pattern: Обновления берутся из репозиториев Ubuntu-Security, Ubuntu и Ubuntu-updates.
Unattended-Upgrade::Package-Blacklist: Никакие пакеты не заблокированы (закомментировано).
Unattended-Upgrade::Auto-Reboot "false";: Автоматическая перезагрузка отключена.
Unattended-Upgrade::Auto-Reboot-Time "02:00";: Если перезагрузка была бы включена, она произошла бы в 2:00 утра (но это не имеет значения, т.к. перезагрузка отключена).
Unattended-Upgrade::Mail "root"; (закомментировано): По умолчанию почта отправляется пользователю root.
Unattended-Upgrade::MailOnlyOnError "true"; (закомментировано): Уведомления будут отправляться только при ошибках.
Если вы хотите поделиться содержимым файла (или его частью) для более конкретной помощи, используйте команды cat или less для просмотра содержимого, скопируйте текст из терминала и вставьте его сюда. Пожалуйста, удалите любые личные данные, такие как адрес электронной почты, если они есть.# UBUNTU
