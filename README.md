**`ftm_ap/main/ftm_main.c`**

```c
// Wifi Credentials
const char* SSID = "AP SSID";
const char* PWD = "비밀번호"; 
uint8_t channel = 1;
uint8_t bw = 20; //20 or 40
int8_t power = 84;
```

`SSID` : 생성할 AP의 SSID

`PWD` : 8자리 이상 비밀번호

`bw` : bandwidth (20Mhz or 40Mhz)

`power` : 신호 세기 설정


### AP 파워 값
**[esp_err_t](https://docs.espressif.com/projects/esp-idf/en/stable/esp32/api-reference/system/esp_err.html#_CPPv49esp_err_t) esp_wifi_set_max_tx_power ( int8_t power)**

power 허용 값 범위: 8 ~ 84 (2 ~ 20 dBm)
1 power = 0.25 dBm

power 값 설정 시 실제 적용되는 값

{{[8, 19],8}, {[20, 27],20}, {[28, 33],28}, {[34, 43],34}, {[44, 51],44}, {[52, 55],52}, {[56, 59],56}, {[60, 65],60}, {[66, 71],66}, {[72, 79],72}, {[80, 84],80}}.

ex) power = 8 ~19 로 설정 시 실제 power는 8 즉, int8_t power 값이 [,] 범위 안이면 다 똑같음

**실제 RSSI 값 (주변 신호가 매우 많은 연구실 실내에서, 변동 있음)**

power = 8; → RSSI = -55 ~ -60 dBm

power = 84; → RSSI = -35 ~ -40 dBm

### AP 40MHz 설정
채널 설정 시, primary channel, second channel 설정

primary channel: 1~12

```c
second channel = {
WIFI_SECOND_CHAN_ABOVE; //primary channel 위로 설정
WIFI_SECOND_CHAN_BELOW; // primary channel 아래로 설정
}
```

ex) primary channel = 1,  second channel = WIFI_SECOND_CHAN_ABOVE

위와 같이 설정 시, 중심채널이 3이고 대역폭이 40MHz인 신호 생성
