# Создание файла с защищенными переменными
ansible-vault create group_vars/elk_servers/vault.yml

# Пример содержимого vault.yml
# ---
# kibana_elasticsearch_password: "очень_сложный_пароль"
# elastic_password: "другой_сложный_пароль"
# logstash_system_password: "еще_один_пароль"

# Редактирование существующего зашифрованного файла
ansible-vault edit group_vars/elk_servers/vault.yml

# Запуск плейбука с запросом пароля для расшифровки vault
ansible-playbook -i inventory.ini playbook.yml --ask-vault-pass

# Запуск плейбука с файлом пароля
# (сначала создаем файл с паролем)
echo "мой_секретный_пароль_для_vault" > ~/.vault_pass
chmod 600 ~/.vault_pass
ansible-playbook -i inventory.ini playbook.yml --vault-password-file ~/.vault_pass