esphome:
  name: cyd-photo-frame

esp32:
  board: esp32dev
  framework:
    type: arduino

wifi:
  ssid: "yt-netfree-2.4G"
  password: "9rrWceWcte"

http_request:

spi:
  clk_pin: GPIO14
  mosi_pin: GPIO13
  miso_pin: GPIO12

output:
  - platform: ledc
    pin: GPIO21
    id: backlight_pwm

light:
  - platform: monochromatic
    output: backlight_pwm
    name: "Backlight"
    restore_mode: ALWAYS_ON

online_image:
  - url: "https://example.com/photo.jpg"
    id: my_photo
    format: JPEG
    type: RGB565
    resize: 320x240
    update_interval: 60s

display:
  - platform: ili9xxx
    model: ILI9341
    cs_pin: GPIO15
    dc_pin: GPIO2
    rotation: 90
    invert_colors: false
    lambda: |-
      it.image(0, 0, id(my_photo));
