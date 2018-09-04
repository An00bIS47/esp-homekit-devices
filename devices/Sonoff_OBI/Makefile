PROGRAM = Sonoff_OBI

EXTRA_COMPONENTS = \
	extras/dht \
	extras/http-parser \
	extras/dhcpserver \
	extras/rboot-ota \
    $(abspath ../../external_libs/wolfssl) \
    $(abspath ../../external_libs/cJSON) \
    $(abspath ../../external_libs/homekit) \
    $(abspath ../../external_libs/wifi_config) \
	$(abspath ../../libs/led_codes)

FLASH_SIZE = 8
FLASH_MODE = dout
FLASH_SPEED = 40
HOMEKIT_SPI_FLASH_BASE_ADDR = 0x8c000
HOMEKIT_MAX_CLIENTS = 16
HOMEKIT_OVERCLOCK_PAIR_SETUP = 0

EXTRA_CFLAGS += -I../.. -DHOMEKIT_SHORT_APPLE_UUIDS -DWIFI_CONFIG_CONNECT_TIMEOUT=120000

## DEBUG
#EXTRA_CFLAGS += -DHOMEKIT_DEBUG=1
.PHONY: signature

include $(abspath ../../sdk/esp-open-rtos/common.mk)

monitor:
	$(FILTEROUTPUT) --port $(ESPPORT) --baud 115200 --elf $(PROGRAM_OUT)

signature:
	$(openssl sha384 -binary -out firmware/Sonoff_OBI.bin.sig firmware/Sonoff_OBI.bin)
	$(printf "%08x" `cat firmware/Sonoff_OBI.bin | wc -c` | xxd -r -p >> firmware/Sonoff_OBI.bin.sig)
	$(mv firmware/Sonoff_OBI.bin firmware/sonoff_obi.bin)
	$(mv firmware/Sonoff_OBI.bin.sig firmware/sonoff_obi.bin.sig)
