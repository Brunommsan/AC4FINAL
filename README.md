# Explicação Do Código

O código começa incluindo as bibliotecas necessárias: WiFi.h para conexão Wi-Fi, PubSubClient.h para comunicação MQTT, OneWire.h para comunicação com o sensor de temperatura, e DallasTemperature.h para obter leituras de temperatura.

Depois, são declaradas várias constantes: ssid e password para armazenar o nome e a senha da rede Wi-Fi, mqtt_server para armazenar o endereço do servidor MQTT, token para o token de autenticação do Ubidots, device_label para o nome do dispositivo e variable_label para o nome da variável de temperatura.

Em seguida, é definido o pino de dados do sensor de temperatura como 4 (oneWireBus). Depois, é criado um objeto DallasTemperature (sensors) associado ao objeto OneWire.

O WiFiClient (espClient) é instanciado para gerenciar a conexão Wi-Fi, seguido pela criação de um objeto PubSubClient (client) associado ao WiFiClient para gerenciar a comunicação MQTT.

A função setup_wifi é definida para conectar o ESP32 à rede Wi-Fi especificada. Ela inicia a conexão Wi-Fi usando o ssid e password e, em um loop, espera até que a conexão seja estabelecida, imprimindo pontos na Serial durante o processo. Uma vez conectado, imprime "WiFi conectado".

Na função setup, a comunicação serial é iniciada com uma taxa de 115200 bps. A função setup_wifi é chamada para conectar à rede Wi-Fi. Depois, o servidor MQTT é configurado com client.setServer e a função callback é associada ao cliente MQTT com client.setCallback. Por fim, o sensor de temperatura é iniciado com sensors.begin.

A função reconnect tenta reconectar ao servidor MQTT caso a conexão seja perdida. Ela tenta conectar repetidamente, imprimindo mensagens na Serial até que a conexão seja estabelecida ou falhe, aguardando 5 segundos entre as tentativas.

Na função loop, se o cliente MQTT não estiver conectado, chama reconnect para tentar reconectar. Em seguida, client.loop é chamado para manter a conexão MQTT. O sensor de temperatura é solicitado a medir a temperatura com sensors.requestTemperatures. A temperatura é coletada com sensors.getTempCByIndex(0) e convertida para string. Esta string é impressa na Serial.
