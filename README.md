# Namada. Гайд по установке и синхронизации.
## Установка Namada:

### 1. Воспользуемся скриптом для быстрой установки:
```shell 
wget -q -O namada.sh https://api.nodes.guru/namada.sh && chmod +x namada.sh && sudo /bin/bash namada.sh
```

### 2. Укажите имя для своей ноды и ждите завершения установки, после полной синхронизации перейдите к следующему шагу:
```shell
source $HOME/.bash_profile
```

### 3. Сгенерируйте ключи для своего аккаунта  и сохарните их:
```shell
namada wallet address gen --alias my-account
```

### 4. Инициализируем аккаунт валидатора:
```shell 
namada client init-validator \
  --alias $VALIDATOR_ALIAS \
  --source my-account \
  --commission-rate 0.1 \
  --max-commission-rate-change 0.1
```

### 5. Запрашиваем токены: 
```shell
namadac transfer \
    --token NAM \
    --amount 1000 \
    --source faucet \
    --target $VALIDATOR_ALIAS \
    --signer $VALIDATOR_ALIAS
```

### 6. Проверяем баланс, если всё хорошо переходим к следующему шагу:
```shell
namada client balance --token NAM --owner $VALIDATOR_ALIAS
```

### 7. Выдаем токены своему валидатору 
```shell
namada client bond \
  --validator $VALIDATOR_ALIAS \
  --amount 1000
```
_____________
# ВАЖНО !
### Если вы получите ошибку `` The address doesn’t belong to any known validator account `` попробуйте снова через несколько часов. `` (~1 час.) ``
